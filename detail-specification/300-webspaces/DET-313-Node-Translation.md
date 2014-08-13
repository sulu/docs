# Node Translation

A single Sulu content node can be translated into multiple langauges.

In Sulu we talk about `language` (i.e. "de", "fr", "es") and `country` (e.g. "at", "gb", "us")
and the composite form is called the `localization`. A localization must have a language and may
have a country. e.g. "en", "en_us", "de_at", etc. are all valid localizations.

## Prefix

Currently there exists a single strategy for node translation. The node properties are stored within the
PHPCR repository with a prefix:

````
+---------------------+---------+--------------------------------------+
| ...                 | ...     | ...                                  |
| i18n:de-template    | STRING  | overview                             |
| i18n:de-changer     | LONG    | 1                                    |
| i18n:de-created     | DATE    | 2014-08-12T16:58:31+02:00            |
| i18n:de-creator     | LONG    | 1                                    |
| i18n:de-name        | STRING  | Testname                             |
| i18n:de-state       | LONG    | 1                                    |
| i18n:de-changed     | DATE    | 2014-08-12T16:58:31+02:00            |
+---------------------+---------+--------------------------------------+
````

The prefix is made up of a namespace follwed by the *localization*.


## Concrete and Shadow Translations

- **Shadow Translation**: A translation which acts as a proxy for a concrete translation.
- **Concrete Translation**: A translation which is not a shadow translation.

The shadow status of a node is determined by the `shadow-on` and `shadow-base` properties of
the node:

````
+---------------------+---------+--------------------------------------+
| ...                 | ...     | ...                                  |
| i18n:de-shadow-base | STRING  | fr                                   |
| i18n:de-shadow-on   | BOOLEAN | true                                 |
+---------------------+---------+--------------------------------------+
````

In this case the user accesses the `de` version of this node, the `fr` version will be displaed.

If the `shadow-on` property is set to `false`:

````
+---------------------+---------+--------------------------------------+
| ...                 | ...     | ...                                  |
| i18n:de-shadow-base | STRING  | fr                                   |
| i18n:de-shadow-on   | BOOLEAN | false                                |
+---------------------+---------+--------------------------------------+
````

Then the user will see the content in the actual content of the node in the `de` localization.
