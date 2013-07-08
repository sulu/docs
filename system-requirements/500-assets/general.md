####[400 CONTACTS](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts "400 CONTACTS")

##![Contacts](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/contacts.png)4100 General

####FR-4101 Role-based Storage

**Definition:**

The system shall store all contacts with its role in a centralized data repository. By default the following standard contact roles shall be implemented:

* User (registered sulu user)
* Client (registered shop client)
* Newsletter (newsletter subscriber)

**Specification:**

1. The system shall provide an automatic assignment of the standard user roles to each added contact depending on its origin (eg. a new registered shop user shall be assigned to the role "Client")
2. Each standard role may have be represented as a specific folder in the navigation area
3. Each standard role shall be accessible through the user management (see [1550 User Management] (https://raw.github.com/massiveart/sulu-docs/master/system-requirements/100-basic/user-management-md "1550 User Management"))


####FR-4102 CRM Approach

**Definition:**

The contacts shall follow the customer relationship systems approach (CRM-approach) in a simplified form. The system shall consider following business objects:

* Contacts
* Accounts
* Activities

Further the system should provide following CRM-extensions:

* Opportunities
* Notes
* Attachments (see [4400 Connections] (https://raw.github.com/massiveart/sulu-docs/master/system-requirements/400-contacts/connections.md "4400 Connections"))

**Specification:**

1. A contact shall be assigned to an account
1. An account shall have a name and an address
1. Each account may have a parent account
1. The system shall support contacts without account assignment
1. A contact shall contain profile image, surname, name, email, standard roles and an optional address (copy of account address or own address if no account assigned)
1. Accounts and contact should support additional customizable fields
1. Contacts with the standard role "Sulu User" shall be accessible through the user management (see [1550 User Management] (https://raw.github.com/massiveart/sulu-docs/master/system-requirements/100-basic/user-management-md "1550 User Management"))
1. The system shall provide a facility to built up a user-specific hierarchical structures with multiple layers to assign contacts (in addition to the assignment to an account)
1. The system shall enable the user to create activities and assign them to an account and / or a contact
1. User depended activities triggered by system events like "newsletter subscribed", "order raised", "for course registered" etc. shall automatically stored to the corresponding contact as a tracking history
1. The system should support opportunities revering to an account and / or a contact 
1. An opportunity should have a name, a phase, a probability and an amount and should optionally refer to an activity
1. The system should enable the user to create notes and add attachments referring to an account or a contact
1. Added attachments and the profile image should be stored in a reserved folder within the asset repository (see [500 ASSETS](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/500-assets/ "500 ASSETS"))
