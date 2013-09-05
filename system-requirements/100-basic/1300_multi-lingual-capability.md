####[100 BASIC](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic "100 BASIC")

* [1100 General](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1100_general.md "1100 General")
* [1150 Caching Mechanism](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1150_caching.md "1150 Caching Mechanism")
* [1200 Ressource Locator Path Management](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1200_rlp.md "1200 Ressource Locator Path Management")
* [1250 Content Structure](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1250_content-structure.md "1250 Content Structure")
* 1300 Multi-lingual Capability
* [1350 Content Life Cycle Workflow](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1350_clc.md "1350 Content Life Cycle Workflow")
* [1400 Publication](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1400_publication.md "1400 Publication")
* [1450 Data Interfaces](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1450_data-interfaces.md "1450 Data Interfaces")
* [1500 Security](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1500_security.md "1500 Security")
* [1550 Access Rights](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1550_access-rights.md "1550 Access Rights")
* [1600 Settings](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1600_settings.md "1600 Settings")

##![basic](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/basic.png)1300 Multi-lingual Capability

####![Alpha](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/alpha.png)FR-1301 Translations

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

![translation-packages](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/translation-package-settings.png)

Fig. Translation package settings

![translation-packages](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/translating-table.png)

Fig. Translating table

####![Alpha](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/alpha.png)FR-1302 Language Fall Back
A user must be able to choose a different language for a page within the specific language version of a portal. All pages within a content node has to be viewable as list showing all available and assigned languages. The language fall back function has to be accessible also via the list view. 

####![Alpha](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/alpha.png)FR-1303 Copying a Language Version
An existing page in a certain language can be a valuable input for the translation into another language. Therefore the user copies a specific page and translates the content. Translated pages can be stored anywhere in the same or in a different portal. The list view allows to copy and save whole nodes or a selection of pages at once.

####![Alpha](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/alpha.png)FR-1304 Language Detection

**Definition:**

The standard language detection shall be based on the site URL. The system shall support different mapping combinations of top-level and sub domains configurable for each implemented portal.

**Specification:**

Following mapping options shall be implemented.
* http://www.example.de - Top-level domain
* http://www.example.com - Top-level domain 
* http://de.example.com - Sub domain
* http://www.example.com/de - URL-path-prefix
* http://www.example.com/de-ch - URL-path-prefix with localization
* http://de.example.ch - Combination of sub and top-level domain
* http://www.example.de /ch - Combination of top-level domain and URL-path-prefix


####FR-1305 IP to Location

**Definition:**

The IP-to-location function automatically forwards the user to the language version of his country of origin. Sulu shall support an IP-to-location service, implemented as a plugin. The mapping of the country-specific IP-address ranges to the different languages can be done by system engineers. 

**Specification:**

1. The system shall implement a service which updates new IP-Entries automatically.
2. Alternatively the user shall be able to select a standard language for a portal.
3. In later versions an user interface should enable the content manager to manage the IP to location mapping table manually.




