####[400 CONTACTS](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts "400 CONTACTS")

* [4100 General](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts/general.md "4100 General")
* [4200 Data Structuring](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts/data-structuring.md "4200 Data Structuring")
* [4300 Contact Management](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts/contact-management.md "4300 Contact Management")
* [4400 Connections](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts/connections.md "4400 Connections")
* 4500 Interfaces
* [4600 Security](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts/security.md "4600 Security")
* [4700 Newsletter](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts/newsletter.md "4700 Newsletter")

##![Contacts](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/contacts.png)4500 Interfaces

####FR-4501 Import / Export

**Definition:**

The system shall provide comprehensive import and export facilities. 

**Specification:**

1. Data sets within the list view shall be exportable to a XML-file or CSV-file
1. The list view shall support single and multiple selection options for the data export
1. External contacts shall be importable via CSV-file or vCards
1. The system should provide facilities for mapping the fields of the import file to the fields of the system 

####FR-4502 LDAP / AD Integration

The shall provide a facility to integrate user out of external LDAP and Active Directory structures to be further managed in the system (see [1550 User Management](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/user-management.md "1550 User Management")).

####FR-4503 Salesforce Integration

The system should use the open REST API of Salesforce to integrate standardized CRM data (details see [developerforce](http://wiki.developerforce.com/page/REST_API "developerforce" )).