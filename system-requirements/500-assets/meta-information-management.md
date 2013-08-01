####[500 ASSETS](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/500-assets "500 ASSETS")

* [5100 General](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/500-assets/general.md "1100 General")
* 5200 Meta Information Management
* [5300 Asset Management](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/500-assets/asset-management.md "5300 Asset Management")
* [5400 Connections](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/500-assets/connections.md "5400 Connections")
* [5500 Interfaces](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/500-assets/interfaces.md "5500 Interfaces")
* [5600 Security](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/500-assets/security.md "5600 Security")

##![Contacts](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/assets.png)5200 Meta Information Management

####FR-5201 Extraction of File Meta Information

**Definition:**

The system shall provide a facility to extract meta data information out of the uploaded files automatically.

**Specification:**

To the extent permitted by the specific file format, following meta information shall be extracted and stored in the system:
* File size
* File type
* Dimensions (eg. height and width of PSD-files)
* Geo-location (geo-coordinates stored by global positioning systems)
* Full text indices of text based documents

####FR-5202 User Generated Meta Information

**Definition:**

The system shall enable the user to manage user-specific meta data.

**Specification:**

1. The system shall support mass data manipulation functionalities for efficient adaption of numerous files
2. The user shall be able to adapt following standard meta information:
	* Title
	* Description
	* Tags (tags on parent nodes affect all subsidiary files)
	* Language mutation (import functionality for multi-language asset assignment)
	* Regional filtering by country codes (may be automized when geo-location is available)
	
####FR-5203 Statistical Information

**Definition:**

The system shall provide statistical information.

**Specification:**

1. Quantity of views
1. Quantity of downloads