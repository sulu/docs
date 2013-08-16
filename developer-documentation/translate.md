# Translate Bundle
## Editing
* define relational backbone models
* define list and form backbone view
* set Callbacks to bundle's rest api

## List
* use husky data-grid
* set listeners for editing/adding items

## Import
* Use XliffFileLoader of Symfony/Translate
* build Package
* Insert to database
* addional flushes because of combined primary key with foreign identities
* Implement separate command class and register it in app/console

## Export
* Use XliffFileDumper of Symfony/Translate and own implementation of FileDumper-Interface for JSON
* Written own Repository for filtering desired Translations
* Implement separte command class and register it in app/console
