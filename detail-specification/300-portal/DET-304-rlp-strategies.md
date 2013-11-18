## DET-304 RLP Strategies & Mapper

#### Description
There are 2 Sections to devide RL storage and generating:

* Strategy: generates a RL
* Mapper: Check RL for uniqueness and save the RL in the storage

##### Strategy

Generates a Resource Locator (string) form a given Structure.

* Short - as short as Possible:
	* try if title is a valid unique RL
	* if not add a counter to the RL
	* with configuration add one (or more) layer from left
	* Example:
		* Existing RLs: /test
		* /product/test
		* generated RL = /test-1
* Tree - Whole Tree:
	* take whole ContentTree
	* if last layer is not unique add a counter to the RL
	* Example:
		* Existing RLs: /products/machines, /products/machines/drill
		* /products/machines/better-drill
		* generated RL = /products/machines/better-drill
		* /products/machines/drill (over Textbox)
		* generated RL = /products/machines/drill-1

##### Mapper

Saves RL in a storage provider:

* MySQL for flat URLs
* PHPCR for tree structured URLs

It cares about URL History.

TODO documentation of URL History

#### Class diagram

![Form Generation component diagram](https://raw.github.com/sulu-cmf/docs/master/detail-specification/images/diagrams/RLPStrategies.png)

#### Flow

1. ResourceLocator call strategy->generate()
2. Strategy generates RL and check if RL is unique with call mapper->unique()
	a. repeat if not unique
3. 	Strategy returns valid RL
4. 	ResourceLocator save a new Route with ContentStructure as a reference

#### CleanUP

The cleanup of URL contains:

* lowercase
* replace signs (language depending)

Example:

| Before | After |
| ------ |:-----:|
| +      | -     |
| space  | -     |
| ä      | ae    |
| ü      | ue    |
| ö      | oe    |

* ??? delete problematic characters ???
* relace multiple minus with one
* remove trailing start/end - 


