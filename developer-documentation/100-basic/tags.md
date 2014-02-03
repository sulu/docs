# Tags

* provide a common `Tag`-Entity
* makes the tags manageable in Sulu
  * add
  * edit
  * delete
  * merge
* provides events to tell other bundles about deletes and merges

## Usage
### TagManager
* registered as a service (`sulu_tag.tag_manager`)
* responsible for centralized tag management
* throws events described below

### Events
* register event listeners (http://symfony.com/doc/current/cookbook/service_container/event_listener.html)
  * `tag.delete`-event for deleted tags and `tag.merge`-event for merged tags
  * TagDeleteEvent contains `tag`-property containg the deleted Tag-Entity
  * TagMergeEvent contains `srcTag`-property for deleted tag and `destTag`-property for the replacement
