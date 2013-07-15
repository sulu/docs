####[400 CONTACTS](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts "400 CONTACTS")

* [4100 General](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts/general.md "4100 General")
* [4200 Data Structuring](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts/data-structuring.md "4200 Data Structuring")
* 4300 Contact Management
* [4400 Connections](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts/connections.md "4400 Connections")
* [4500 Interfaces](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts/interfaces.md "4500 Interfaces")
* [4600 Security](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts/security.md "4600 Security")

##![Contacts](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/contacts.png)4300 Contact Management

####FR-4301 Navigation Types

**Definition:**
The system shall provide the following two navigation views for browsing the contacts:
* Thumb nail view
* List view with multiple select and sorting functions

Both navigation views may have a standard filter for "My contacts", "All contacts" and "Last viewing".

**Specification:**

1. The user should be provided with facitlites to regonize the type of external files
1. The list view should enable the user to filter by initial letter over an alphabetical listing of all letters. 
 
![List view](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/list-view.png)
Fig.: List view example

####FR-4302 Single and Multiple Editing

**Definition:**
The system shall provide the standard data management functions ("New", "Edit", Duplicate" and "Delete") supporting single and multiple edit mode. The user should be provided with a simple function to move a contact to another account or to refer an alias of the contact to another account (details see [4100 General](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts/general.md)).

**Specification:**

1. Each data manipulation shall log the date of change and the user and save the older version in the change history (versioning and historiography functions). Deleted data sets shall be archived according to the content life cycle workflow (see [Content Life Cycle Workflow] (https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/content-life-cycle-workflow.md)).

1. The user shall be able to add an new contact quickly only entering surname and email address (associated account can be entered optionally, details see [CRM Approach](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts/general.md "CRM Approach")).

1. Every contact entry in the thumb nail view or list view shall lead the user direct to the edit mask.

1. The system shall allocate a multiple selection option (eg. a check box) to access the multiple edit mode. 

1. When a user selects the delete function, the system shall show a message box which the user has to confirm before deleting the data set.