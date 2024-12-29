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

### Bootstrap 5 Migration

These rules are derived from the Bootstrap 5 migration guide and should be followed when updating Moodle's UI.

#### General Migration

*   **Gradual Migration:** The migration to Bootstrap 5 will be done in a gradual way, with steps executed in different phases.
*   **PopperJS Upgrade:** Upgrade PopperJS to version 2, while maintaining compatibility with version 1 for Bootstrap 4.
*   **SCSS Deprecation:** Follow the SCSS deprecation process for cleanup after the Bootstrap 5 upgrade.
*   **Refactor BS4 Features:** Refactor Bootstrap 4 features that are deprecated or dropped in Bootstrap 5.
*   **BS5 Bridge:** Use a BS5 "bridge" to address simple breaking changes in advance.
*   **BS5 Upgrade:** Upgrade the current Bootstrap 4 version to version 5.
*   **BS4 Backwards-Compatibility:** Create a backwards-compatibility layer to allow Bootstrap 4 syntax to still work until final deprecation.
*   **Final Deprecation:** Eventually, fully deprecate Bootstrap 4 syntax.

#### Refactoring BS4 Features

*   **Badge Colors:** Replace `.badge-*` color classes with background utilities like `.bg-primary` and corresponding text color classes (`.text-dark` or `.text-white`).
*   **Badge Pills:** Replace `.badge-pill` with `.rounded-pill`.
*   **Media Component:** Replace the `.media` component with utility classes like `d-flex`, `flex-shrink-0`, and `flex-grow-1`.
*   **Mixins:** Refactor deprecated mixins such as `hover`, `float-left`, `nav-divider`, `img-retina`, `text-hide`, `invisible`, `form-control-focus`, `text-emphasis-variant`, `size`, `make-container-max-widths`, `g-variant`, and `bg-gradient-variant`. Use the suggested replacements.
*   **Form Groups:** Replace `.form-group` with margin utilities.
*   **Form Inline:** Replace `.form-inline` with utility classes like `d-flex` and `flex-wrap`.
*   **Card Decks:** Replace `.card-deck` with utility classes like `row` and `col`.

#### BS5 Bridge

*   **SCSS Bridge File:** Use the `bs5-bridge.scss` file in `theme/boost/scss/moodle` for compatibility changes.
*   **No Gutters:** Replace `.no-gutters` with `.g-0`.
*   **Close Button:** Replace `.close` with `.btn-close`.
*   **Directional Utilities:**
    *   Replace `.float-left` and `.float-right` with `.float-start` and `.float-end`.
    *   Replace `.border-left` and `.border-right` with `.border-start` and `.border-end`.
    *   Replace `.rounded-left` and `.rounded-right` with `.rounded-start` and `.rounded-end`.
    *   Replace `.ml-*` and `.mr-*` with `.ms-*` and `.me-*`.
    *   Replace `.pl-*` and `.pr-*` with `.ps-*` and `.pe-*`.
    *   Replace `.text-left` and `.text-right` with `.text-start` and `.text-end`.
*   **Theme Color Level:** Replace `theme-color-level()` with `shift-color()`, using percentages instead of levels (e.g., level 1 becomes 10%).
*   **Rounded Classes:** Replace `.rounded-sm` and `.rounded-lg` with `.rounded-1` and `.rounded-3`.
*   **Screen Reader Utilities:**
    *   Replace `.sr-only` and `.sr-only-focusable` with `.visually-hidden` and `.visually-hidden-focusable`.
    *   Replace `sr-only()` and `sr-only-focusable()` mixins with `visually-hidden()` and `visually-hidden-focusable()`.
*   **Font Utility Classes:**
    *   Replace `.font-weight-*` with `.fw-*`.
    *   Replace `.font-italic` with `.fst-italic`.
