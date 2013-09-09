####[500 ASSETS](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/500-assets "500 ASSETS")

* [5100 General](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/500-assets/5100_general.md "1100 General")
* [5200 Data Structuring](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/500-assets/5200_data-structuring.md "5200 Meta Information Management")
* 5300 Asset Management
* [5400 Connections](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/500-assets/5400_connections.md "5400 Connections")
* [5500 Interfaces](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/500-assets/5500_interfaces.md "5500 Interfaces")
* [5600 Security](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/500-assets/5600_security.md "5600 Security")

##![Contacts](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/assets.png)5300 Asset Management

####![Alpha](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/alpha.png)FR-5301 Visualization of Multiple File Types
**Definition:**

The system must provide a means of representing and accessing external files uploaded by the user. 

**Specification:**

1. The system shall be provided with facilities to automatically identify following file types:
	* .pdf
	* Images (.png, .bmp, .gif, .jpg, .tif, .pcx and Photoshop EPS)
	* Videos (.mov, .asf, .avi, .flv, .mp4, .mpg, .rm, .wmv and .mts)
	
1. Each file type as listed above shall be represented as a specific thumb nail icon
1. If supported by the type, the file shall have a preview image displayed on click
1. Facilities shall be provided for the preview image to be defined by the user

####![Alpha](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/alpha.png)FR-5302 Multiple Upload / Download

**Definition:**

The system shall provide a multiple upload and download of files.

**Specification:**

1. The user shall be enabled to select one or more external files to upload to the system
1. Within the multiple editing functionalities the user shall be able to select one or more files in the list view to download to the local disc
1. Uploaded ZIP-files shall be decompressed automatically

####![Alpha](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/alpha.png)FR-5303 Navigation Types

**Definition:**

The system shall provide two navigation views for browsing assets:
* Thumb nail view
* List view with multiple select and sorting functions

Both navigation views may have a standard filter for "My assets", "All assets" and "Last viewing". 

**Specification:**

1. The thumb nails of the files shall generated automatically (see FR-5301 above)
1. The thumb nail icon size shall be continuous ajustable 

####![Alpha](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/alpha.png)FR-5304 File Versioning

**Definition:**

The system must provide a version history of all managed files. 

**Specification:**

1. The user shall be able to reactivate previous file versions
1. The user shall be able to download previous file versions

####![Alpha](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/alpha.png)FR-5305 Single and Multiple Editing

**Definition:**

The system shall provide the standard asset management functions ("Upload", "Download", "Edit" and "Delete") supporting single and multiple edit mode.

**Specification:**

1. Each file manipulation shall log date of change, version and user to be saved in the change history (see FR-5304 above). Deleted files shall be archived according to the content life cycle workflow (see [Content Life Cycle Workflow] (https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/content-life-cycle-workflow.md)).

1. The user shall be able to add tags to a new asset quickly

1. Every asset in the thumb nail view or list view shall lead the user direct to the edit mask.

1. The system shall allocate a multiple selection option (eg. a check box) to access the multiple edit mode. 

1. When a user selects the delete function, the system shall show a message box which the user has to confirm before deleting the file.

####FR-5306 Video Support

**Definition:**

The system shall support streaming video services.

**Specification:**

1. The system shall be able to manage youtube and vimeo video services
1. The user shall be able to play these videos within the system
1. Referred videos shall be displayed with preview images

####![Alpha](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/alpha.png)FR-5307 Meta Data

**Definition:**

The system shall provide a facility to extract meta data information out of the uploaded files automatically and enable the user to manage user-specific meta data.

**Specification:**

1. To the extent permitted by the specific file format, following meta information shall be extracted and stored in the system:
	* File size
	* File type
	* Dimensions (eg. height and width of PSD-files)
	* Geo-location (geo-coordinates stored by global positioning systems)
	* Full text indices of text based documents
1. The system shall support mass data manipulation functionalities for efficient adaption of numerous files
2. The user shall be able to adapt following standard meta information:
	* Title
	* Description
	* Tags (tags on parent nodes affect all subsidiary files)
	* Language mutation (import functionality for multi-language asset assignment)
	* Regional filtering by country codes (may be automized when geo-location is available)


####![Alpha](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/alpha.png)FR-5308 Statistical Information

**Definition:**

The system shall provide statistical information.

**Specification:**

1. Quantity of views
1. Quantity of downloads
