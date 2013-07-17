####![Portals](https://raw.github.com/massiveart/sulu-docs/master/system-specification/images/package-white.png)[350 Smart Content](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts "400 CONTACTS")

* [4100 General](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts/general.md "4100 General")
* [4200 Data Structuring](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts/data-structuring.md "4200 Data Structuring")
* [4300 Contact Management](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts/contact-management.md "4300 Contact Management")
* 4400 Connections
* [4500 Interfaces](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts/interfaces.md "4500 Interfaces")
* [4600 Security](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-contacts/security.md "4600 Security")

##![Portals](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/portals.png)UC351 Add Smart Content

**Primary Actor:** [Content Manager](https://github.com/massiveart/sulu-docs/tree/master/system-specification/actors.md "Actors") 

**Scope:** [P300 Portals](https://github.com/massiveart/sulu-docs/tree/master/system-specification/p300 "P300 Portals") 

**Level:** Activity_User

**Stakeholders and Interests:**





**Precondition:** User has the right to access…

**Minimal quarantee:** Sufficient logging information that the system can detect that something went wrong…

**Success quarantee:** The user´s account information is updated…

**Main success szenario:** 

	1. User selects...
	2. System gets name of...
	3. System opens...
	4. User browses and...

**Extensions:**

	2a. User wants a web site the system does not support (Join 3):
		2a1. System gets new suggestion form user...
	3a. Web failure of any sort during setup (Join 3):
		3a1. System report...
		3a2. User either backs out thies use case, or tries again.
