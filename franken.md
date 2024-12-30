# Frankenstyle Component Naming Rules

These rules define how to name components in Moodle, following the "Frankenstyle" convention.

## General Format

Frankenstyle component names are constructed with a prefix and a folder name, separated by an underscore: `prefix_foldername`.

1.  **Prefix:** Determined by the plugin type (e.g., `mod` for activity modules).
2.  **Folder Name:** The plugin's folder name, always in lowercase (e.g., `quiz`).

   Example: The frankenstyle name for the quiz module is `mod_quiz`.

## Plugin Type Prefixes

Refer to the [Plugin types](https://docs.moodle.org/dev/Plugin_types) page for a comprehensive list of plugin types and their corresponding prefixes.

## Core Subsystems

Core subsystems use the format `core_subsystemname`.

Here's a list of core subsystems and their frankenstyle names:

-   Access: `core_access`
-   Administration: `core_admin`
-   Antivirus: `core_antivirus`
-   Authentication: `core_auth`
-   Conditional availability: `core_availability`
-   Backup and restore: `core_backup`
-   Badges: `core_badges`
-   Blocks: `core_block`
-   Blogging: `core_blog`
-   Bulk users operations: `core_bulkusers`
-   Caching: `core_cache`
-   Calendar: `core_calendar`
-   Cohorts: `core_cohort`
-   Comment: `core_comment`
-   Competency based education: `core_competency`
-   Completion: `core_completion`
-   Countries: `core_countries`
-   Course: `core_course`
-   Currencies: `core_currencies`
-   Database transfer: `core_dbtransfer`
-   Debugging: `core_debug`
-   Text editors: `core_editor`
-   Education fields: `core_edufields`
-   Enrol: `core_enrol`
-   Error reporting: `core_error`
-   Favourites: `core_favourites`
-   File picker: `core_filepicker`
-   Files management: `core_files`
-   User filtering: `core_filters`
-   Forms: `core_form`
-   Grades: `core_grades`
-   Advanced grading: `core_grading`
-   Groups: `core_group`
-   Help: `core_help`
-   Hub: `core_hub`
-   IMS CC: `core_imscc`
-   Installer: `core_install`
-   ISO 6392: `core_iso6392`
-   Language pack configuration: `core_langconfig`
-   License: `core_license`
-   Maths library: `core_mathslib`
-   Media: `core_media`
-   Messaging: `core_message`
-   MIME types: `core_mimetypes`
-   MNet: `core_mnet`
-   Dashboard: `core_my`
-   User notes: `core_notes`
-   Page types: `core_pagetype`
-   Pictures and icons: `core_pix`
-   Plagiarism: `core_plagiarism`
-   Plugins management: `core_plugin`
-   Portfolio: `core_portfolio`
-   Privacy: `core_privacy`
-   Course publishing: `core_publish`
-   Question bank engine: `core_question`
-   Ratings: `core_rating`
-   Site registration: `core_register`
-   Repository: `core_repository`
-   RSS: `core_rss`
-   Roles: `core_role`
-   Global search: `core_search`
-   Tabular data display/download (deprecated): `core_table`
-   Tagging: `core_tag`
-   Timezones: `core_timezones`
-   User: `core_user`
-   User key: `core_userkey`
-   Web service: `core_webservice`

## Usage Rules

### Function Names

-   All plugin functions must start with the full frankenstyle prefix.
-   Activity modules may also use `modulename_` as a prefix for backward compatibility.
-   Avoid global functions; use autoloaded classes instead.

### Class Names

-   Place all component classes in the `classes` directory.
-   Use namespaces based on the frankenstyle component name.
    -   Example: A discussion class in the forum activity should be in the `mod_forum` namespace and may have a class name of `discussion` - `\mod_forum\discussion`.
-   Avoid non-namespaced classes using only the frankenstyle prefix.

### Constants

-   All plugin constants must start with an uppercase frankenstyle prefix (e.g., `MOD_FORUM_XXXX`).
-   Use class constants on autoloaded classes instead of global constants where possible.

### Table Names

-   All table names for a plugin must begin with its frankenstyle name (after the standard Moodle table prefix).
-   Exception: Moodle activities do not have the `mod_` prefix in table names (for historical reasons).
    -   Examples:
        -   `local_coolreport`
        -   `local_coolreport_users`
        -   `forum` (for the `mod_forum` component)

### Plugin Configuration Table

-   In the `config_plugins` table, the `plugin` column uses the frankenstyle name.

### Capabilities

-   All capabilities for a plugin use the frankenstyle name, with `/` instead of `_`.
    -   Examples:
        -   `mod/quiz:viewattempt`
        -   `block/library:readbook`

### Language Files

-   The main language file for each plugin (except activity modules) is named after the frankenstyle component name.
    -   Examples:
        -   `/blocks/participants/lang/en/block_participants.php`
        -   `/mod/quiz/lang/en/quiz.php`

### Other places

-   `@package` declarations in phpdocs
-   Web service function names
-   Moodle Plugins database
-   JS module names
-   Template names

## Theme Name Variants

-   When creating a theme that is a derivative of another theme, avoid including the parent theme's name in the new theme's name.

## See Also

-   [Plugins](https://docs.moodle.org/dev/Plugins)
-   [Subplugins](https://docs.moodle.org/dev/Subplugins)
-   [Core APIs](https://docs.moodle.org/dev/Core_APIs)
-   [Automatic class loading](https://docs.moodle.org/dev/Automatic_class_loading)
