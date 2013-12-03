# DET 305 RLP History

History will be created in RlpMapper::move. the old resource locator will be copied to the new path. the old path will be changed to history.

## Activity Diagramm

![History Generation activity diagram](https://raw.github.com/sulu-cmf/docs/master/detail-specification/images/diagrams/rlp-history.jpg)

### In short:

* copy source resource locator (+plus nested tree)
* foreach resourcelocator in this tree (+source resourcelocator)
	* set history to true
	* set content to new resourcelocator
	* forearch history to this resourcelocator: change content to new resourcelocator