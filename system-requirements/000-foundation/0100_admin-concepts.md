####[000 FOUNDATION](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/000-foundation "000 FOUNDATION")

* 0100 Admin Concepts
* [0200 Content Delivery](https://github.com/massiveart/sulu-docs/tree/master/system-requirements/000-foundation/0200_content-delivery.md "0200 Content Delivery")

####FR-0101 Non Destructive Delete

The system shall support a non destructive delete by transferring deleted entities into a trash repository. The user shall be able to restore deleted data out of the trash.

####![Alpha](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/alpha.png)FR-0102 Validation

**Definition:**

The system shall validate data entries to support the user to enter the correct data formats. 

**Specification:**

* An entered number or date shall be validated in dependency of the defined system language respectively the corresponding country (localization)
* The system shall support different validation types
* Number and date formats shall be setable per language
* The user should be informed by the system while entering wrong data formats
