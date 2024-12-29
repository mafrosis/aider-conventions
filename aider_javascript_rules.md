# Aider JavaScript Rules for Moodle Plugin Development

These rules are derived from the Moodle JavaScript guidelines and are intended to guide Aider in generating Moodle-compliant JavaScript code.

## General

-   **ES2015+ Modules:** All new JavaScript code must use ES2015+ module format, which is transpiled into CommonJS format.
-   **RequireJS Loader:** Modules are loaded in the browser using the RequireJS loader.
-   **Moodle Features:** Use Moodle's Mustache templates, translated strings, and web service framework.
-   **Vanilla JavaScript:** Use vanilla JavaScript with Moodle helpers, avoiding jQuery, YUI, and other frameworks except for legacy interfaces.
-   **Accessibility:** Ensure all JavaScript is accessible.

## Module Structure

-   **Naming Convention:** JavaScript modules must follow the naming convention: `[component_name]/[optional/sub/namespace/][modulename]`.
-   **Component Directory:** The first directory in any subfolder must be either a Moodle API or `local`.
-   **Examples:**
    -   `mod_forum/discussion`
    -   `mod_assign/grades/grader`
    -   `block_newsitems/local/modal/confirmation`
    -   `core_user/local/participants/selectors`
-   **Subdirectories:** Create a main entry-point module with related modules in a subdirectory.
    -   Example: `core_user/participants` with submodules in `local/participants`.
    -   `local/participants/repository.js` (module name: `core_user/local/participants/repository`)
    -   `local/participants/selectors.js` (module name: `core_user/local/participants/selectors`)
    -   `participants.js` (module name: `core_user/participants`)

## Module Content

-   **Entry Point:** Each module should have an entry point, usually a function called `init`, which is exported.
-   **Dependencies:** Import dependencies using the `import` keyword.
-   **Exports:** Export functions, objects, classes, and other data structures as needed.

## DOM Event Handling

-   **Event Listeners:** Use `document.addEventListener()` to listen for DOM events.
-   **CSS Selectors:** Store CSS selectors in a separate `Selectors` object within the module.
-   **Data Attributes:** Use `data-*` attributes to identify elements for event listeners.
-   **Namespaces:** Use namespaces for `data-action` attributes to identify the purpose of the button.
-   **Event Delegation:** Use event delegation to handle events on multiple elements with a single listener.
-   **`e.target.closest()`:** Use `e.target.closest()` to check if the clicked element or its parent matches a CSS selector.

## Including JavaScript

-   **From Templates:** Use `{{#js}}` tags in Mustache templates to include JavaScript.
    -   Example:
        ```html
        {{#js}}
        require(['mod_forum/discussion'], function(Discussion) {
            Discussion.init();
        });
        {{/js}}
        ```
    -   Use `{{uniqid}}` to generate unique IDs for DOM elements and pass them to the module.
-   **From PHP:** Use `$PAGE->requires->js_call_amd()` to include JavaScript from PHP.
    -   Example: `$PAGE->requires->js_call_amd('mod_forum/discussion', 'init');`
    -   Pass arguments to the function as an array: `$PAGE->requires->js_call_amd('mod_forum/discussion', 'init', [$course->id]);`
    -   Use array destructuring in JavaScript to get named values from multi-dimensional arrays.

## Data Handling

-   **Data Attributes:** Use `data-*` attributes to pass data to JavaScript modules.
-   **Web Services:** Use Moodle Web Services to fetch complex data structures dynamically.

## Promises

-   **`then` and `catch`:** Use `then` and `catch` consistently for promise handling.
-   **Return Promises:** Return a Promise from a function if the function is primarily tasked with creating that Promise.
-   **Avoid `done`, `fail`, `always`:** Do not use `done`, `fail`, or `always` functions on Promises.

## Strings

-   **`core/str` Module:** Use the `core/str` module to fetch and render language strings.
-   **`getString`:** Use `getString` to fetch a single string (returns a native Promise).
-   **`getStrings`:** Use `getStrings` to fetch a set of strings (returns an array of native Promises).
-   **`get_string`:** Use `get_string` to fetch a single string (returns a jQuery Promise, for legacy support).
-   **`get_strings`:** Use `get_strings` to fetch a set of strings (returns an array of jQuery Promises, for legacy support).
-   **Caching:** Strings are cached in LocalStorage.
-   **Native Promises:** Prefer `getString` and `getStrings` from Moodle 4.3 onwards.

## Prefetching

-   **`core/prefetch` Module:** Use the `core/prefetch` module to prefetch assets.
-   **`prefetchString`:** Prefetch a single string.
-   **`prefetchStrings`:** Prefetch multiple strings.
-   **`prefetchTemplate`:** Prefetch a single template.
-   **`prefetchTemplates`:** Prefetch multiple templates.

## Dropzone

-   **`core/dropzone` Module:** Use the `core/dropzone` module to create drop zones.
-   **Accessibility:** The module ensures accessibility requirements are met.
-   **Callbacks:** Drop zones trigger callbacks for common actions.

## Reactive State

-   **Framework Independence:** Core developments are framework independent.
-   **Ad-hoc Library:** Moodle implements a basic reactive state pattern using an ad-hoc library.

## Tools

-   **NodeJS:** Most Moodle JavaScript tooling requires NodeJS.
-   **Grunt:** Use Grunt to compile JavaScript and CSS, and to lint JavaScript, CSS, and Behat tests.
    -   `npm -g install grunt-cli`
    -   `npx grunt` or `grunt`
-   **ESLint:** Use ESLint for JavaScript linting.
