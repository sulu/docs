##![basic](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/basic.png)DET-103 Tags
#### Description
##### Storage
The tags are stored in our relational database, and consist of an `id`, a `name`, `created`- and `changed`-dates and users. The `name` has an unique index, because there are no double tag names allowed in our system.

##### Functionality
Tags can be added, edited, deleted and merged in the Settings-section of Sulu. There is some additional work to do because the tags can be used in many different contexts.

Adding is no problem at all, as long as the desired tag name is not already taken.

Editing should have an effect on all the objects, which already have a reference on this tag. That's not a big task, because the objects only save the ID to the tag, so no additional work has to be done when a tag gets renamed. Of course the new tag name has not to be taken.

Deleting is already a bit more special, as the `SuluTagBundle` cannot remove the deleted tag from all the objects from other bundles. In theory this can be done with a constraint in a RDBMS, but not all of our data is stored in a RDBMS. That's why an `tag.delete`-event with the deleted tag is thrown, and the other bundles have to react on this event on their own.

Merging is not much more complicated than deleting, due to the usage of the same procedure. However, this procedure includes more tags: many tags will be deleted, and another tag will be used instead of these ones. Again, because of the missing knowledge of the other bundles objects, an event is thrown, and every bundle is responsible on his own to replace the tags.
