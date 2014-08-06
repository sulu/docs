# DET 311 ContentMapper

The ContentMapper provides a interface to load (from phpcr) data and save (to phpcr). It uses Template Structures to detect Structure of Content ([Link to Documentation](https://github.com/sulu-cmf/docs/blob/master/detail-specification/300-webspaces/DET-301-template-architecture.md)). Therefor he iterates over the properties of the structure.

## Overview

![Template architecture](https://raw.github.com/massiveart/sulu-docs/master/detail-specification/images/diagrams/structure_architecture.png)


## PHPCR-Structure

[Link to Documentation](https://github.com/sulu-cmf/docs/blob/master/detail-specification/300-webspaces/DET-308-PHPCR-Structure.md)

## Load Process

For loading process the content mapper uses template key from phpcr node (template). With this key it gets the structure from StructureManager. This structure is the blueprint of the content node.

### Read Data

To read the data it iterrates over properties of structure. This properties will be translated over prefix `sulu_locale:<localization>-<property-name>` Example: `sulu_locale:de_at-title`. To load ghost pages it uses the LocalizationFinder (for example ParentChildAnyFinder -> section Ghost Pages).

### Interface

* __loadByParent__: returns a list of node, starting at the children of given parent node
	* $uuid: UUID from parent node
	* $depth: depth to load (default 1 -> only one layer)
	* $flat: True returns a list of nodes, false returns a tree of nodes
	* $excludeGhosts: True if ghost nodes should be hidden (default false -> ghost pages will be displayed)
* __load__: returns a specific node
	* $uuid: UUID of content node
	* $loadGhostContent: True to load Data from ghost node (default false -> no ghost content will be loaded)
* __loadStartPage__: returns the index node of given webspace
* __loadByResourceLocator__: return content node for given resource locator
* __loadBySql2__: returns a list of nodes specified with sql statement
	* $sql2: sql statement
	* $limit: limit of result

## Save Process

The save process takes an assozitive object and maps it with given structure (template key) to a phpcr structure.

### Save Data

To read the data it iterrates over properties of structure. This properties will be translated over prefix `sulu_locale:<localization>-<property-name>` Example: `sulu_locale:de_at-title`.

### Interface

* __save__: Saves data to phpcr database
	* $partialUpdate: True to ignore missing properties
	* $uuid: UUID of updated content node
	* $parentUuid: UUID of parent node (if node is new)
	* $state: value of state
	* $showInNavigation: True if this node should be shown in navigation
* __saveStartPage__: Saves data to a indexpage of given webspace
	* $partialUpdate: True to ignore missing properties

## Copy / Move

The copy / move relocating data in phpcr.

### Move / Copy Data

PHPCR interface provides a move / copy functionality so the process only calls this methods with the correct source and destination path. The destination path is generated from the parent path and the `sulu.node.name` cleaned up and make this name unique under the parent path.

If the node has a resource locator it would be adopted automatically like:

* copy: create a new resourcelocator with a generated (Strategy) url
* move: move the resourcelocator to a new generated RL (history is build autmatically)

To generate a new RL the last part of the old RL (or the `sulu.node.name`) will be used.

### Interface

* __move__: move node
* __copy__: copy node


## Navigation Contexts

`navContexts` in data used to describe in which navigatio the content appears.

## ContentTypes

ContentTypes are implemented as service to keep the coupling as minimum as possible. The IDS are prefixed with: `sulu.content.type.<<name>>`. To control the flow of save there are two types of ContentTypes POST_SAVE (executed after save), PRE_SAVE (executed before save).

* The __read__ method reads data from node (phpcr) and save it to property (structure)
* The __write__ method reads data from property (structure) and save it to node (phpcr)

### Interface

* __getType__: PRE_SAVE / POST_SAVE
* __read__: reads the value for given property from the node + sets the value of the property
* __readForPreview__: sets the value of the property with the data given
* __write__: save the value from given property
* __remove__: remove property from given node
* __getTemplate__: returns a template path to render a form

## Ghost Pages

To detect ghost pages, the content mapper uses the LocalizationFinder Service. Esecially the ParentChildAnyFinder. it uses a predifined property (like title or created).

1. check if __node__ (phpcr) has property in this language
1. check if a __parent__ localization exists
1. check if a __child__ localization exists
1. check if a __any__ localization exists

To avoid misunderstandings the GhostPageContent will not be displayed in the admin for now -> only the title will be displayed in column navigation.

