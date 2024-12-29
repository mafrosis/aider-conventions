# Aider JavaScript Rules for Moodle AJAX

These rules are derived from the Moodle AJAX guidelines and are intended to guide Aider in generating Moodle-compliant JavaScript code for AJAX interactions.

## General

-   **`core/ajax` Module:** Use the `core/ajax` JavaScript module for all new AJAX interactions.
-   **Web Service API:** AJAX calls should directly call web service functions built using the Moodle Web Service API.
-   **Security:** Web service functions used for AJAX must be marked as available for AJAX in `db/services.php` by defining `'ajax' => true`.
-   **Single HTTP Request:** Multiple web service requests can be chained in a single HTTP request.
-   **Type Checking:** Ensure strict type checking for all parameters and return types in web service functions.

## Design Patterns

-   **Repository Module:** Place all code using the `core/ajax` module into a single `repository.js` file within the component's `amd/src` directory.
-   **Meaningful Responses:** Each web service call should have a meaningful response.
-   **Chained Calls:** Use `core/ajax` to make multiple web service calls from a single transaction.
-   **Import `call`:** Import the `call` function from `core/ajax` as `fetchMany`.
-   **Export Functions:** Export functions from the repository module that encapsulate specific web service calls.
-   **Call Web Services:** Call the exported functions from other modules to initiate AJAX requests.

## Key Considerations

-   **Templates:** Use Moodle templates to update parts of the UI in response to AJAX changes.
-   **Theme Context:** When calling `$PAGE->get_renderer()` in a web service, ensure the correct theme is set, potentially by passing the theme as a parameter to the web service.
-   **Text Filtering:** Filter text returned from a web service using `external_format_text` or `external_format_string` with the correct context.
-   **Context Specificity:** Use the most specific context relating to the output when filtering text.
-   **Filter Notification:** After adding dynamic content to a page, notify Moodle's filters via `M.core.event.FILTER_CONTENT_UPDATED`.
-   **Web Service Updates:** After adding or changing any web service definition in `db/services.php`, bump the plugin or Moodle version number and run the upgrade.
-   **Safe Web Services:** Mark web services as safe to call without a session only if they return 100% public information and do not consume many resources.
    -   Add `'loginrequired' => false` to the service definition in `db/services.php`.
    -   Pass `false` as the third argument to the `call` method when calling the web service.

## Code Examples

### Repository Module

```javascript
import {call as fetchMany} from 'core/ajax';

export const submitGradingForm = (
    assignmentid,
    userid,
    data,
) => fetchMany([{
    methodname: 'mod_assign_submit_grading_form',
    args: {
        assignmentid,
        userid,
        jsonform JSON.stringify(data),
    },
}])[0];
```

### Calling the Web Service

```javascript
import {submitGradingForm} from './repository';

export const doSomething = async() => {
    // ...
    const assignmentId = getAssigmentId();
    const getUserId = getUserId();
    const data = getData();

    const response = await submitGradingForm(assignmentId, userId, data);
    window.console.log(response);
}
```

### Chained Calls

```javascript
import {call as fetchMany} from 'core/ajax';

const getGradingFormRequest = (assignmentid, userid, data) => ({
    methodname: 'mod_assign_submit_grading_form',
    args: {
        assignmentid,
        userid,
        jsonform JSON.stringify(data),
    },
});

const getNextGraderRequest = (assignmentid, userid) => ({
    methodname: 'mod_assign_get_grading_form',
    args: {
        assignmentid,
        userid,
    },
});

export const submitGradingFormAndFetchNext = (
    assignmentId,
    currentUserId,
    currentUserData,
    nextUserId
) => {
    const responses = fetchMany([
        getGradingFormRequest(assignmentId, usecurrentUserIdrId, currentUserData),
        getNextGraderRequest(assignmentId, nextUserId),
    ]);

    return {
        submittedGradingForm: responses[0],
        nextGradingForm: responses[1],
    };
};
```

### Calling Chained Web Services

```javascript
import {submitGradingFormAndFetchNext} from './repository';

export const doSomething = async() => {
    // ...
    const assignmentId = getAssigmentId();
    const getUserId = getUserId();
    const data = getData();

    const {
        submittedGradingForm,
        nextGradingForm,
    } = submitGradingFormAndFetchNext(assignmentId, userId, data, getNextuserId);
    window.console.log(await submittedGradingForm);
    window.console.log(await nextGradingForm);
}
```
