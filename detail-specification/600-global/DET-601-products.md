##![global](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/global.png)DET-601 Products

###Database Diagram

![Products database diagram](https://raw.github.com/massiveart/sulu-docs/master/detail-specification/images/db/products.png)

###Description
The data for the products region is split into multiple bundles. The `SuluProductBaseBundle` contains the most common stuff, which is shared among all the other bundles. This bundle can be considered abstract, as it contains a mapped super class.

The shown `SuluProductAdvancedBundle` introduces suppliers, which is not always required, thus it is in an own bundle.

Later there will also be a `SuluProductSimpleBundle`, which adds some missing fields to the product required for a simple shop without suppliers.

####SuluProductBaseBundle
This bundle contains the abstract products entity (for the `pr_products`-table shown in the diagram, which is never generated due to its abstractness), holding the most common information like a key, serial numbers, a manufacturer and so on. Additionally it stores the type of the product (`pr_product_types`). It is also linked to a language dependent table containing the products name and description (`pr_product_translations`).

##### Product attributes
The `pr_attributes`-table contains all the available attributes in the system together with a unit and a type (enumeration, text, integer, double, ...). The relation to the product is established by the `pr_product_attributes`-table containing the value as well. The `pr_templates`-table combines some of these attributes, to offer some preconfigured templates to the user for convenience.

##### Product types
All products are categorized in the following types:
* Masterproducts consist of different variants. These variants are stored as seperate products, and differ only in some specified attributes. The master product's price can be overruled by its variants.
* Simple products are the most used type, which represents products with no different variants. They are also used for the variants in the master product.
* Extra products are not visible in the standard overview, and are for products which are only available in combination with another one.

##### Product links
Products can also be linked to other products, which is described in the tables `pr_crosssells`, `pr_upsells`, `pr_relations` and `pr_extras`. These connections are classified as follows:
* `pr_relations` define related products, which can add some additionally value to the original product.
* `pr_upsells` define products which can be bought instead of the original one, and is usually used for more expensive alternatives.
* `pr_crosssells` define other possibly interesting products, which not necessarily have a connection to the original product, and are usually shown in the basket.
* `pr_extras` show other products, which only can be bought in addition to the original product and usually have the product type `extra`. It also contains a price, which can be used to override the extra products original price.

##### Product sets
The `pr_sets`-table can group some products and offer the entire set for a special price. The price is defined by a percental discount, as set can also contain master products being available in different variants and prices, which make the handling quite hard.

#### SuluProductAdvancedBundle
The advanced version of the products introduces suppliers. The suppliers are represented by the `co_accounts`-table from our ContactBundle.

The advanced product bundle also defines it's own version of the product in `ap_products`, but does not add any additional fields. The `ap_supplier_products`-table adds the link to the suppliers or accounts, and adds some additional informations and/or overrides the information from the original product by the information from the concrete supplier. The additional information contains the delivery status of the supplier's product (`ap_product_delivery_status`), the product's status (`ap_product_status_translations`) and some attributes which are only defined by the supplier (`ap_supplier_product_attribues`), whereby the same attributes as in the SuluProductBaseBundle are available. 

The pricing is done in the `ap_supplier_product_prices`, where also a minimum quantity for the price is written, which enables the possibility to model different price ranges.
