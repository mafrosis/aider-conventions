## Moodle Plugin Development Conventions

These conventions are used to guide the development of Moodle plugins.

### General

*   **HTTP Requests:** Prefer `httpx` over `requests` for making HTTP requests.
*   **Type Hints:** Use type hints wherever possible to improve code clarity and maintainability.

### Moodle Specific

*   Follow the Moodle coding standards and API documentation:
    *   [Moodle Architecture](https://docs.moodle.org/dev/Moodle_architecture)
    *   [Moodle Development Policies](https://moodledev.io/general/development/policies)
    *   [Moodle Web Service API](https://docs.moodle.org/dev/Web_service_API_functions)

*   Use Moodle's recommended development tools:
    *   [Node.js](https://moodledev.io/general/development/tools/nodejs)

### Moodle Architecture

*   **Modular System:** Moodle is a modular system. Always extend functionality through plugins, not by modifying core files.
*   **Plugin Types:** Understand the different plugin types (activities, resources, blocks, themes, etc.) and use the appropriate APIs for each.
*   **Core Concepts:** Be aware of core Moodle concepts like courses, activities, users, roles, and permissions.
*   **Course Structure:** Courses are sequences of activities and resources grouped into sections.
*   **User Roles:** Users have roles (e.g., student, teacher) that define their capabilities within a course or the site.
*   **Contexts:** Understand that Moodle uses contexts (e.g., courses, modules, blocks) to manage permissions.
*   **Permissions:** Permissions control what users can do in a given context.
*   **Database:** Moodle's database is composed of core tables and plugin-specific tables.
*   **Database Definitions:** Database structure is defined in `install.xml` files within each plugin's `db` folder.
*   **Transaction Script:** Moodle primarily uses a transaction script approach, with core functionality refactored into libraries.
*   **Presentation Layer:** Separate presentation from business logic using themes and renderer classes.
*   **Upgrade Process:** Moodle can be upgraded in four steps:
    1.  Ensure server compatibility.
    2.  Create backups and test installations.
    3.  Replace Moodle code.
    4.  Trigger the upgrade from the admin page.
*   **Activity and Resource Plugins:** Activities and resources are the main tools for teaching and learning.
*   **Block Plugins:** Blocks provide interface functionality on pages.
*   **Theme Plugins:** Themes control the visual style of the Moodle site.
*   **Language Packs:** Moodle is internationalized, use language packs for different languages.
*   **Course Format Plugins:** Course formats control how the course structure is presented.
*   **Authentication Plugins:** Authentication plugins control how users log in.
*   **Enrolment Plugins:** Enrolment plugins control which users are enrolled in which courses.
*   **Repository Plugins:** Repository plugins provide ways for users to get content into Moodle.

### Moodle Development Policies (from https://moodledev.io/general/development/policies)

These rules are derived from the Moodle development policies and should be followed when developing Moodle plugins.

#### General Architecture

*   **Platform Compatibility:** Moodle aims to run on a wide range of platforms. Ensure your code is compatible and portable.
*   **Modularity:** Moodle is modular. Extend functionality through plugins, not by modifying core files.
*   **Plugin Types:** Understand and use the appropriate plugin types (activities, resources, blocks, themes, etc.) and their APIs.

#### Coding Style

*   **Consistent Style:** Follow Moodle's coding style to ensure code readability and maintainability.
*   **Community Acceptance:** Adhering to the coding style is important for code to be accepted by the Moodle community.

#### Security

*   **Security Guidelines:** Strictly follow Moodle's security guidelines to protect user data and prevent vulnerabilities.
*   **Responsible Internet Citizen:** Ensure your code does not introduce vulnerabilities that could compromise the server.

#### Standards

*   **HTML5 Compliance:** Produce strict, well-formed HTML5 code, preferably backwards compatible with XHTML 1.1.
*   **Accessibility:** Comply with common accessibility guidelines (W3C WCAG 2.0, ARIA).
*   **CSS for Layout:** Use CSS for layout and separate presentation from business logic.
*   **Theme Extension:** If creating a custom theme, extend the Moodle 'Boost' theme.

#### JavaScript

*   **Vanilla JavaScript:** Write new JavaScript in Vanilla JavaScript using ES6 style.
*   **Discourage Frameworks:** Avoid using jQuery, YUI, and other frameworks except for legacy interfaces.
*   **Avoid Interface Manipulation:** Write code to avoid removing or adding interfaces as the page loads.
*   **Accessibility:** Ensure all JavaScript is accessible.

#### Internationalisation

*   **Language Packs:** Keep language strings and locale information separate from the code, using language packs.
*   **Default Language:** Use English (AU) as the default language for all code, comments, and documentation.

#### Accessibility

*   **Wide Range of Users:** Ensure Moodle works well for the widest possible range of people.

#### Component Library

*   **Component Reuse:** Utilize the component library to identify and reuse frequently-used user interface components.

#### Performance

*   **Scalability:** Ensure your code scales well with an increasing number of users, courses, and activities.
*   **Discourage Performance Issues:** Avoid features that are discouraged on production sites for performance reasons.

#### Database

*   **XMLDB:** Use Moodle's database abstraction layer (XMLDB) for database interactions.
*   **Database APIs:** Use the provided tools and APIs for defining, modifying, retrieving, and storing data.

#### Events

*   **Event Observers:** Use event observers to be notified when events happen and act on the data.
*   **Observer Limitations:** Observers cannot modify event data or prevent actions from occurring.
*   **Naming Convention:** Follow the events naming convention.

#### Web Services

*   **Web Service API:** Implement web services according to the Web Service API functions.
*   **Naming Convention:** Follow the naming convention for web service functions.

#### Testing

*   **Manual Testing:** Write clear testing instructions for manual testing.
*   **Unit Testing:** Create automated unit tests for each bit of functionality using PHPUnit.
*   **Acceptance Testing:** Automate user interaction testing using the Behat framework.

#### Third Party Libraries

*   **Standard Inclusion:** Use the standard way to include third-party libraries in your code.

#### Other Standards

*   **Unique Style:** Moodle coding style is unique and not compatible with PEAR or other common PHP standards.

#### Translations

*   **Internationalization:** Pay attention to keeping the language strings and locale information separate from the code, in language packs.
