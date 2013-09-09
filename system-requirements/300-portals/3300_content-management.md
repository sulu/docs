####[300 PORTALS](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/300-portals "300 PORTALS")

* [3100 General](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/300-portals/3100_general.md "3100 General")
* [3200 Data Structuring](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/300-portals/3200_data-structuring.md "3200 Data Structuring")
* 3300 Content Management]
* [3400 Connections](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/300-portals/3400_connections.md "3400 Connections")
* [3500 Interfaces](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/300-portals/3500_interfaces.md "3500 Interfaces")
* [3600 Security](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/300-portals/3600_security.md "3600 Security")

##![portals](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/portals.png)3300 Content Management

####![Alpha](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/alpha.png)FR-3301 Text Editor

**Definition:**

The system shall provide basic text formatting functionalities through CKEditor.

![CKEditor](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/ckeditor.png)

Fig. UI CKEditor

**Specification:**

1. The editor shall provide most common text formatting functions, especially 
 * Bold, italic and underlined text
 * Ordered and unordered lists
 * Excerpt
 * Defined headlines (CSS) accessible over pull down menue
1. Following features are recommended:
 * Asset assignment (pictures and documents)
 * Internal links
 * Word import with plain text (no formatting)

####![Alpha](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/alpha.png)FR-3302 Navigation Types

**Definition:**

The system shall provide two navigation views:
* List view with multiple select and sorting functions
* Node tree view 

**Specification:**

![Node tree view navigation](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/navigation_node-treeview.png)

Fig. Node tree view navigation (portals)

####![Alpha](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/alpha.png)FR-3303 Single and Multiple Edit

**Definition:**

The system shall provide the standard functions "Edit", "Delete", "Move" and "Alias" supporting single and multiple edit mode.

**Specification:**

1. The user shall be able to delete a page

1. Deleted pages shall be removed to a trash archive (see [Content Life Cycle Workflow] (https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/content-life-cycle-workflow.md))

1. When a user selects the delete function, the system shall show a message box which the user has to confirm before deleting a page

1. The system shall allocate a multiple selection option (eg. a check box) to access the multiple edit mode

1. One or more selected pages can be moved to another place (cut and paste)

1. The user shall be able to create an alias of one or more selected pages and move dem to another place (copy and paste) 

1. Each data manipulation shall log date of change and user to be saved in the change history

####![Alpha](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/alpha.png)FR-3304 Front End Editing

**Definition:**

The user should be provided with facilities to make textual amendments in the front end.

**Specification:**

1. Text blocks enabled for front end editing shall be marked by an icon on mouse over
1. When a user selects such an icon, the specific text block can be edited
1. After editing the icon changes to a save button for confirming the amendments
1. Front end editing is limited to textual amendments, which means that no new content blocks or asset assingment features are available

####![Alpha](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/alpha.png)FR-3306 Preview

**Definition:**

The system shall display a preview of the edited content.

**Specification:**

1. The system shall display the preview in a new window
1. The system should display the preview in place within the edit area
