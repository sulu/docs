####[100 BASIC](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic "100 BASIC")

* [1100 General](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1100_general.md "1100 General")
* 1150 Caching Mechanism
* [1200 Ressource Locator Path Management](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1200_rlp.md "1200 Ressource Locator Path Management")
* [1250 Content Structure](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1250_content-structure.md "1250 Content Structure")
* [1300 Multi-lingual Capability](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1300_multi-lingual-capability.md "1300 Multi-lingual Capability")
* [1350 Content Life Cycle Workflow](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1350_clc.md "1350 Content Life Cycle Workflow")
* [1400 Publication](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1400_publication.md "1400 Publication")
* [1450 Data Interfaces](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1450_data-interfaces.md "1450 Data Interfaces")

<!--* [1500 Security](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1500_security.md "1500 Security")-->
* [1550 Access Rights](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1550_access-rights.md "1550 Access Rights")
* [1600 Settings](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/1600_settings.md "1600 Settings")



##![basic](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/basic.png)Caching Mechanism
####![Alpha](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/alpha.png)FR-1151 Page Cache

**Definition:**

The system shall provide user-driven page cache mechanisms to optimize the speed of the managed portal.

**Specification:**

1. The user shall be able to cache a whole page
1. The system should also provide a cache on request functionality
1. Within the portal settings the user shall be able to generate a cache on save (cache warming)


####![Alpha](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/alpha.png)FR-1152 Cache Expiring

**Definition:**

The system shall support different cache expiring settings.

**Specification:**

The following methods for cache expiring shall be implemented:
* whole portal expiring (manually)
* single page expiring (manually or automatic on save)
* intelligent cache lifetime calculation (cache considers publish and expiring dates of all effected components and pages)

####![Alpha](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/alpha.png)FR-1153 Partial Cache Disabling

The system shall provide partial cache disabling mechanisms according to the Edge Side Includes (ESI) standard proceeded by the system or by varnish. 

####![Alpha](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/alpha.png)FR-1154 Database independent page delivery  

The system shall provide facilities to deliver cached pages without database requests. The site should be reachable even if the database is down. 

####NFR-1155  Transparent Caching Mechanism

The system shall provide intelligent caching mechanisms to minimize manual interventions by the user.
