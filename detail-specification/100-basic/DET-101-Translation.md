##![basic](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/basic.png)DET-101 Translations

####Database Diagram

![Translations database diagram](https://raw.github.com/massiveart/sulu-docs/master/detail-specification/images/db/translate.png)

####Description

tr_codes contains all the translation keys, which are available in our system. A package is a collection of consolidated keys. These packages have multiple catalogues, one for each language. The catalogues hold all the translations from the package-codes in the tr_translations-table. The location is an optional field for each code, by which the codes can be grouped into seperate sections.

####Console commands

#####Import
Basic command: <strong>sulu:translate:import</strong> << locale >>

Description: The above command imports translation files from all bundles. In every bundle it looks for the Resources/translations/sulu folder and imports the translation files in it. Per bundle and locale a backend file (backend.<< locale >>.xlf) and a frontend file (frontend.<< locale >>.xlf) get imported. The translations from the backend file are then available in the backend, the translations from the frontend file in the frontend. For each bundle an own package gets created which gets the same name as its corresponding bundle (if not already exists).

Options:
- (--file|-f) The path to the file to import. This is to import a single file
- (--packageId|-p) The id of the package to import the translations into. This can be used when you import a single file.
- (--path) Only important if you don't import a single file. Relative path from the bundle root to the translation folder
- (--name) If no package id gets specified for a single-file-import a new package will be created. This is the name for it.
- (--frontend) Makes imported translations available for the frontend
- (--backend) Makes imported translations available for the backend
- (--backendDomain) The prefix of the backend files. Only important if you don't import a single file
- (--frontendDomain) The prefix of the frontend files. Only important if you don't import a single file
- (--defaultLocale) The locale for which newly created catalogues get set as default

Examples:
- sulu:translate:import en (Imports all translations from all bundles with the en locale)
- sulu:translate:import -f path/to/your/translation/file.xlf en (Imports a single file to a new package with the locale en)
