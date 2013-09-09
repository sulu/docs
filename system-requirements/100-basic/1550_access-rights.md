####[100 BASIC](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic "100 BASIC")

* [1100 General](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1100_general.md "1100 General")
* [1150 Caching Mechanism](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1150_caching.md "1150 Caching Mechanism")
* [1200 Ressource Locator Path Management](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1200_rlp.md "1200 Ressource Locator Path Management")
* [1250 Content Structure](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1250_content-structure.md "1250 Content Structure")
* [1300 Multi-lingual Capability](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1300_multi-lingual-capability.md "1300 Multi-lingual Capability")
* [1350 Content Life Cycle Workflow](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1350_clc.md "1350 Content Life Cycle Workflow")
* [1400 Publication](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1400_publication.md "1400 Publication")
* [1450 Data Interfaces](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1450_data-interfaces.md "1450 Data Interfaces")

<!--* [1500 Security](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1500_security.md "1500 Security")-->
* 1550 Access Rights
* [1600 Settings](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1600_settings.md "1600 Settings")

##![basic](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/basic.png)1550 Access Rights
####FR-1551 Support of LDAP Principles

**Definition:**

The security for the user access rights shall be based on LPDAP-principles.

**Specification:**

1. LDAP (Lightweight Directory Access Protocol) is a directory service for storing data (details see [The Principles Behind LDAP](http://linuxandwindows.uw.hu/linuxwinworld-chp-8-sect-1.html)).
2. The system shall provide a facility to match a LDAP-structured permission tree to the systems access right structure.
3. Every LDAP directory layer shall be allocated to an unique user group layer. Therefore the system shall support nested user groups (more see FR-1202).

####![Alpha](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/alpha.png)FR-1552 User, Groups, Roles and Permissions

**Definition:**

The access right management shall cover the complex requirements arising from the multi-portal and multi-language capabilities of the system. Therefore the language settings should be assignable on user as well as on user group level.

**Specification:**

1. The system shall enable the user to define system users and system user groups.
1. A user group shall consist of one or more dedicated users.
1. Each system user or user group shall have one or more associated content languages.
1. Each user group shall be assignable to parent user group(s).
1. A role shall be assignable to a system user or a user group.
1. The system shall provide a facility to define the permission settings for each security context of the system bundles (ACL´s).
1. A role shall be implemented as a security context with assigned user permissions.
1. Within the contact management the system shall provide a facility to change the assigned user groups and / or roles (see [4600 Security](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts/securtiy.md "4600 Securty")) and to show all user generated security contexts in an non-editable overview.

![Access rights model](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/access-rights-model.png)

Fig. Access rights model

![Access rights model](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/contact-permissions.png)

Fig. Contact permission settings
