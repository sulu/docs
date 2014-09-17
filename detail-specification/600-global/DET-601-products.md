##![global](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/global.png)DET-601 Products

###Database Diagram

![Products database diagram](https://raw.github.com/massiveart/sulu-docs/master/detail-specification/images/db/products.png)

###Description
The bundle contains the abstract products entity and a concrete implementation of it as well. There the most common information is hold, like a key, serial numbers, a manufacturer and so on. Additionally it stores the type of the product (`pr_types`). It is also linked to a language dependent table containing the products name and description (`pr_product_translations`).

##### Product attributes
The `pr_attributes`-table contains all the available attributes in the system together with a unit and a type (enumeration, text, integer, double, ...). The relation to the product is established by the `pr_product_attributes`-table containing the value as well. The `pr_attribute_sets`-table combines some of these attributes, to offer some preconfigured attribute sets to the user for convenience.

##### Product types
All products are categorized in the following types:
* `Products` are the most used type, which represents products with no different variants. They are also used for the variants in the master product.
* `ProductVariants` define a product, which is available in different variants. Variants are stored as seperate products, and differ only in some specified attributes. The master product's price can be overruled by its assigned variants.
* `ProductAddons` are not visible in the standard overview, and are for products which are only available in combination with another one.
* `ProductSets` are a combination of products, which can be bought all together. There is also the possibility to specify an own price for the set.

##### Product links
Products can also be linked to other products, which is described in the tables `pr_crosssells`, `pr_upsells`, `pr_relations` and `pr_extras`. These connections are classified as follows:
* `pr_relations` define related products, which can add some additionally value to the original product.
* `pr_upsells` define products which can be bought instead of the original one, and is usually used for more expensive alternatives.
* `pr_crosssells` define other possibly interesting products, which not necessarily have a connection to the original product, and are usually shown in the basket.
* `pr_extras` show other products, which only can be bought in addition to the original product and usually have the product type `extra`. It also contains a price, which can be used to override the extra products original price.

Additionaly there is the table `pr_sets`, which is used only for ProductSets, and defines the products which the set consists of.

##### Configureable options
There are tables lik `pr_delivery_type` or `pr_delivery_status`, which can hold additional information base on the configurations of the bundle.

