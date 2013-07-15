####[400 CONTACTS](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts "400 CONTACTS")

* [4100 General](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts/general.md "4100 General")
* [4200 Data Structuring](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts/data-structuring.md "4200 Data Structuring")
* [4300 Contact Management](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts/contact-management.md "4300 Contact Management")
* 4400 Connections
* [4500 Interfaces](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts/interfaces.md "4500 Interfaces")
* [4600 Security](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts/security.md "4600 Security")

##![Contacts](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/contacts.png)4400 Connections

####FR-4401 Asset Assignment

**Definition:**

The system shall provide a facility to assign assets from the asset repository (see [500 ASSETS](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/500-assets/ "500 ASSETS")) to a contact, an account or an opportunity.

**Specification:**

1. The user shall be able to assign multiple assets
1. Assigned Assets should be displayed with a preview icon

####FR-4402 Direct Upload

**Definition:**

Assets, especially the profile image, shall be assigned via direct upload to the contact or an account.

**Specification:**

1. The user shall be able to assign assets either out of asset repository or via direct upload
1. When a user uploads a profile image to a contact, the system automatically does the image croping for proper representation on the user´s display 

####FR-4403 Content Assignment

**Definition:**
In some cases the system shall provide facilities to assign content to a contact, an account.

**Specification:**

1. The system shall enable the user to assign a contact to a specific site (eg. for assigning the head of a division to its responible divison site) 
1. The user shall be able to assign multiple contents (sites) to a contact or an account
1. The preview of each assigned site may be called directly from the corresponding contact or account