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
