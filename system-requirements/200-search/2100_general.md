####[200 SEARCH](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/200-search "200 SEARCH")

* 2100 General
* [2200 Admin Search](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/200-search/2200_admin.md "2200 Admin Search")
* [2300 Front-end Search](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/200-search/2300_frontend.md "2300 Front-end Search")
* [2400 Statistics](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/200-search/2400_statistics.md "2400 Statistics")
* [2500 Interfaces](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/200-search/2500_interfaces.md "2500 Interfaces")
* [2600 Security](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/200-search/2600_security.md "2600 Security")

##![search](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/search.png)2100 General

####![Alpha](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/alpha.png)FR-2101 Search Index

**Definition:**

The system shall provide a search index for all relevant data to be found via search queries.

**Specification:**

1. The implementation of the search should be designed as an abstraction layer for Elastic Search and ZEND Lucene
1. The system shall support customizable priorities for search indices
1. Referenced content should also be indexed

####FR-2102 Advanced Search

The system shall provide a facility to prioritize and list search results in the order of frequency of clicked result links. When a user enters a search query the system shall display a recommendation of meaningful search terms.
