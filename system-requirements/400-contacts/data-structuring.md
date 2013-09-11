####[400 CONTACTS](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts "400 CONTACTS")

* [4100 General](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts/general.md "4100 General")
* 4200 Data Structuring
* [4300 Contact Management](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts/contact-management.md "4300 Contact Management")
* [4400 Connections](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts/connections.md "4400 Connections")
* [4500 Interfaces](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts/interfaces.md "4500 Interfaces")
* [4600 Security](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts/security.md "4600 Security")
* [4700 Newsletter](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts/newsletter.md "4700 Newsletter")

##![Contacts](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/contacts.png)4200 Data Structuring

####FR-4201 Filtering

**Definition:**

The system shall provide a facility for dynamic filtering based on all contact attributes. The user shall be able to define and save those individual dynamic filters. Automatic filters based on the standard contact user roles shall be displayed by default. In addition the user shall be able to create a manual filter by assigning contacts to a named folder.

**Specification:**

2. The user shall define a unique filter name.
1. The standard contact user roles (User, Client, Newsletter) shall be a mandatory criteria with "All Contacts" as default setting.
3. The system shall provide a user interface for defining multiple filter criteria according to the following scheme: field (drop down of all contact fields), operator (equal, starts with, etc.) and value (text field).
4. The user should be able to define the fields to be viewed on the contact list (columns) with the ability to specify the priorities of order.
5. The user should be able to define whether the filter is public (for all users) or private (visible only for the user).
3. The system shall show the defined dynamic filter in the navigation area. 
6. To set up a manual filter, the user has to define a filter name and select the desired contacts (multiple selection).


####![Alpha](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/alpha.png)FR-4202 Hierarchical Structuring

The system may provide a facility to built up a user-specific hierarchical structures with multiple layers to assign contacts (in addition to the assignment to an account).