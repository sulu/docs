####[100 BASIC](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic "100 BASIC")

* 1100 General
* [1150 Caching Mechanism](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1150_caching.md "1150 Caching Mechanism")
* [1200 Ressource Locator Path Management](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1200_rlp.md "1200 Ressource Locator Path Management")
* [1250 Content Structure](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1250_content-structure.md "1250 Content Structure")
* [1300 Multi-lingual Capability](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1300_multi-lingual-capability.md "1300 Multi-lingual Capability")
* [1350 Content Life Cycle Workflow](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1350_clc.md "1350 Content Life Cycle Workflow")
* [1400 Publication](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1400_publication.md "1400 Publication")
* [1450 Data Interfaces](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1450_data-interfaces.md "1450 Data Interfaces")
* [1500 Security](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1500_security.md "1500 Security")
* [1550 Access Rights](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1550_access-rights.md "1550 Access Rights")
* [1600 Settings](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1600_settings.md "1600 Settings")

##![basic](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/basic.png)1100 General
####![Alpha](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/alpha.png)FR-1101 Basic User Interface Concept

**Definition:**

The basic user interface concept defines UI layout with the basic UI elements and its usage.

**Specification:**

1. All formulars, lists and views shall be consistent in design, interaction concept and functionalities
1. The interaction concept strictly differentiates between list and edit views with their own UI behavior rules and functionalities.
1. When deleting an item within the list view a message box appears ("…do you really want to delete…")
1. Deleted elements like input fields or complex content types within the edit view shall be marked as deleted before confirming the changes by saving the form (see states of save button in fig. buttons and functions)

######LISTS:

![General list](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/list_general.png)

Fig. General list view

![General list](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/list_contacts.png)

Fig. Contacts list view

######NAVIGATION:

![General list](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/navigation_node-treeview.png)

Fig. Node tree view navigation (portals)

![General list](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/navigation_contacts.png)

Fig. Contacts navigation

![General list](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/navigation_assets.png)

Fig. Assets navigation

######UI ELEMENTS:

![General list](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/buttons_functions.png)

Fig. Buttons and functions

![General list](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/forms.png)

Fig. Forms

![General list](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/typography.png)

Fig. Typography

####FR-1102 Import / Export Functions in Lists

**Definition:**

The user shall be able to export each list view in the system to different formats. The import feature shall be customizable and has to be defined for every section.

**Specification:**

1. The exported file shall contain all columns which are displayed by the corresponding view-
1. The following export file formats shall be provided: XML, JSON and CSV


####FR-1103 Separation of Staging and Live Environment

The system architecture shall support a physical and logical separation of the staging and live environment. Staging and live data repositories shall be synched according to the master - slave approach.

####FR-1104 Multiple Copy-Paste with Field Mapping

**Definition:**

The system must provide a means of copying specific sites or assets to a multiple entry scrapbook.

**Specification:**

1. The user shall be able to select one or more items in the scrapbook to paste them into the current context
1. All added items in the scrapbook can be selected or removed
1. The system shall provide a facility to automatically map copied data fields to the target dataset during the pasting process.
1. Pasted assets shall be linked do the corresponding content


