##![basic](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/basic.png)DET-101 Translations

####Database Diagram

![Translations database diagram](https://raw.github.com/massiveart/sulu-docs/master/detail-specification/images/db/translate.png)

####Description

tr_codes contains all the translation keys, which are available in our system. A package is a collection of consolidated keys. These packages have multiple catalogues, one for each language. The catalogues hold all the translations from the package-codes in the tr_translations-table. The location is an optional field for each code, by which the codes can be grouped into seperate sections.
