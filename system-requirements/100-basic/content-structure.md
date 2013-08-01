####[100 BASIC](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic "100 BASIC")

<!--* [1100 General](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/general.md "1100 General")
* [1150 Caching Mechanism](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/caching-mechanism.md "1150 Caching Mechanism")
* [1200 Ressource Locator Path Management](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/rlp-management.md "1200 Ressource Locator Path Management")
* [1350 Content Life Cycle Workflow](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/clc-workflow.md "1350 Content Life Cycle Workflow")
* [1400 Publication](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/clc-workflow.md "1400 Publication")
* [1450 Data Interfaces](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/clc-workflow.md "1450 Data Interfaces")
* [1500 Security](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/security.md "1500 Security")
* [1600 Settings](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/settings.md "1600 Settings")
* [1900 Non-functional Requirements]https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/nfr.md "1900 Non-functional Requirements")-->

* 1250 Content Structure
* [1300 Multi-lingual Capability](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/multi-lingual-capability.md "1300 Multi-lingual Capability")
* [1550 Access Rights](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/access-rights.md "1550 Access Rights")

##![basic](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/basic.png)1250 Content Structure

####FR-1251 Templates and Content Types

**Definition:**

Content shall be structured in templates with various content types to build up the layout of a site. A template shall consist of a core container and one or more content types arranged in content containers. Content types have specific formats. A plausibility validation shall be implemented for each format. Wrong formats shall be determined immediately while data entering. The user should get a meaningful example of the correct data format. 

**Specification:**

Template Composition:

* Core container (title, article title, URL)
* Content container (content page, overview page, external link, internal link, iFrame and sitemap)

Supported content containers with their standard content types:
* Content page
	* Title media (image, video)
	* Article text
	* Multiple content blocks (title, media [image, video], text)
	* Gallery (multiple images)
	* Video (multiple)
	* Document (multiple)
	* Internal link (multiple)
	* Excerpt (text, image)
	* Contact (multiple assignment, see [500 ASSETS]((https://github.com/massiveart/sulu-docs/tree/master/system-requirements/500-assets "500 ASSETS"))
	* Additional content areas (depending on project)
* Overview page
	* Title media (image, video)
	* Article text
	* Smart content (title, filter settings [visual styling, category, amount, value for sorting, order, target node, include/exclude sub-pages)
	* Excerpt (text, image)
	* Contact (multiple assignment, see [500 ASSETS]((https://github.com/massiveart/sulu-docs/tree/master/system-requirements/500-assets "500 ASSETS"))
* External link
	* External URL
	* Target
	* Excerpt (text, image)
* Internal link (destination page)
* iFrame
	* External URL
	* Format (width, height)
* Sitemap

####FR-1252 Content Sniplets

**Definition:**

The System shall support a multiple usage of global defined content fragments (content sniplets). 

**Specification:**

1. The user shall be able to manage content sniplets at one centralized place.
1. The system shall allow an easy assignment of content sniplets to one or more pages.

####FR-1252 Microdata format
The system shall suppport the microdata format (see schema.org and http://dev.w3.org/html5/md-LC/).