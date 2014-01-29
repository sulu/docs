# Admin Components
The Admin Bundle contains multiple useful/mandatory AuraJS front-end components, which are used to accomplish the desired functionality and look and feel. 


##Components
(located under Resources/publich/js/components)
###dialog
To use the predefined dialog templates, sandbox events have to be triggered:

* `sulu.dialog.confirmation.show`: full configurable dialog
	
	parameters:
	* {Object} data 
		* {Object} content
			* {String} title
			* {String} content
		* {Object} footer
            * {String} buttonCancelText
            * {String} buttonSubmitText
		* {Object} callback:
			* {Function} cancel (optional)
			* {Function} submit
 	* {String} templateType


* `sulu.dialog.error.show`: displays an error dialog
	
	parameters:
	* {String} message

* `sulu.dialog.ok.show`: display an ok dialog (normal message with ok button)
	
	parameters:
	* {String} message		


###edit-toolbar
Implementation of the husky edit-toolbar component with most common templates:

	option parameters:
		* {String} heading
		* {String|Object} template [default]
		* {String} instanceName


###list-toolbar
Implementation of the husky toolbar component with most common templates:

	option parameters:
		* {String} heading
		* {String|Object} template [default]
		* {String} instanceName


##Aura Extensions
The aura_extensions folder contains aura extensions with librarys of other manufacturers as well as own developments.
###sulu-content-tabs
Read [content-navigation-integration](https://github.com/sulu-cmf/docs/blob/master/developer-documentation/000-foundation/content-navigation-integration.md#-ii-content-tabs-integration-into-the-frontend) for further information on this extension.

###sulu-extension 
This extension contains multiple useful functions, making the developers live easier:

#### User Settings
* `sandbox.sulu.loadUserSetting ( key, url, callback )` : DEPPRECATED
* `sandbox.sulu.loadUrlAndMergeWithSetting` (key, attributesArray, url, callback) 
```
             loads an url and matches it against user settings
             @param key Defines which setting to compare with
             @param attributesArray Defines which Attributes should NOT be taken from user-settings and from fields API instead
             @param url Where
             @param callback
```
* `sandbox.sulu.getUserSetting(key)`
```
			 returns settings for a specified key
             @param key
             @returns mixed
```
* `sandbox.sulu.saveUserSetting(key, value, url)`
```
			 saves data locally and to database
             @param key
             @param value
             @param url Defines where to save data to
```

#### Miscellaneous
* `sandbox.sulu.initListToolbarAndList(key, url, listToolbarOptions, datagridOptions)`
```
			initializes sulu list-toolbar with column options and datagrid
             @param key Settings key
             @param url Url to load fields from
             @param mixed Toolbar-options
             @param listToolbarOptions
             @param datagridOptions
```