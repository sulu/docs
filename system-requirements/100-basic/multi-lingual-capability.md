####[100 BASIC](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic "100 BASIC")

<!--* [1100 General](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/general.md "1100 General")
* [1150 Caching Mechanism](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/caching-mechanism.md "1150 Caching Mechanism")
* [1200 Ressource Locator Path Management](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/rlp-management.md "1200 Ressource Locator Path Management")
* [1350 Content Life Cycle Workflow](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/clc-workflow-management.md "1350 Content Life Cycle Workflow")
* [1400 Publication](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/publication.md "1400 Publication")
* [1450 Data Interfaces](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/data-interfaces.md "1450 Data Interfaces")
* [1500 Security](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/security.md "1500 Security")
* [1600 Settings](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/settings.md "1600 Settings")
* [1900 Non-functional Requirements](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/nfr.md "1900 Non-functional Requirements")-->

* [1250 Content Structure](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/content-structure.md "1250 Content Structure")
* 1300 Multi-lingual Capability
* [1550 Access Rights](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/access-rights.md "1550 Access Rights")

##![basic](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/basic.png)1300 Multi-lingual Capability

####FR-1301 Translations

**Definition:**

The system shall provide a user interface for a centralized translation of all static content.

**Specification:**

1. The system shall support higher-level translation packages (see Fig. Translation packages)
1. Each translation package shall consist of one or more language catalogues and sections (see Fig. Translation package settings)
1. Each language catalogue shall be defined by one dedicated language 
1. Sections shall be used to categorize the translation codes in meaningful headlines
1. Each translation code (language key) shall have an editable field for the translation to the target language and a suggestion to support the translation work (see Fig. Translating table)

![translation-packages](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/translation-packages.png)

Fig. Translation packages

![translation-packages](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/translation-packages-settings.png)

Fig. Translation package settings

![translation-packages](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/translating-table.png)

Fig. Translating table

####FR-1302 Language Fall Back
A user must be able to choose a different language for a page within the specific language version of a portal. All pages within a content node has to be viewable as list showing all available and assigned languages. The language fall back function has to be accessible also via the list view. 

####FR-1303 Copying a Language Version
An existing page in a certain language can be a valuable input for the translation into another language. Therefore the user copies a specific page and translates the content. Translated pages can be stored anywhere in the same or in a different portal. The list view allows to copy and save whole nodes or a selection of pages at once.

####FR-1304 Language Detection


####FR-1305 IP to Location

**Definition:**

The IP-to-location function automatically forwards the user to the language version of his country of origin. Sulu shall support an IP-to-location service, implemented as a plugin. The mapping of the country-specific IP-address ranges to the different languages can be done by system engineers. 

**Specification:**

1. The system shall implement a service which updates new IP-Entries automatically.
2. Alternatively the user shall be able to select a standard language for a portal.
3. In later versions an user interface should enable the content manager to manage the IP to location mapping table manually.




