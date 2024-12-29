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
