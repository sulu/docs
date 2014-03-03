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
* {String|Object} parentTemplate  
* {Function} changeStateCallback
* {Function} parentChangeStateCallback
* {String} instanceName
 
#### How to set a custom template?
Overwrite template parameter. See husky documentation for "edit-toolbar" component to get further information regarding the data-format.

#### How to extend an existing template?
Set "parentTemplate" to the template which should be extended. Then set "template" with the data on which the parent template should be extended. Do the same with "changeStateCallback" and "parentListener" if necessary

 * to insert new data: just pass the new item and define "position" to set its order in the edit-toolbar


###list-toolbar
Implementation of the husky toolbar component with most common templates:

option parameters:

* {String} heading
* {String|Object} template [default]
* {String|Object} parentTemplate 
* {Function} listener [default]  
* {Function} parentListener  
* {String} instanceName

#### How to set a custom template?
Overwrite template parameter. See husky documentation for "toolbar" component to get further information regarding the data-format.

#### How to extend an existing template?
Set "parentTemplate" to the template which should be extended. Then set "template" with the data on which the parent template should be extended. Do the same with "listener" and "parentListener" if necessary

 * to insert new data: just pass the new item and define "position" (and probably also "group") to set its order
 * to overwrite data: if you'd like to overwrite a main item just set the same id.



##Aura Extensions
The aura_extensions folder contains aura extensions with librarys of other manufacturers as well as own developments.
###sulu-content-tabs
Read [content-navigation-integration](https://github.com/sulu-cmf/docs/blob/master/developer-documentation/000-foundation/content-navigation-integration.md#-ii-content-tabs-integration-into-the-frontend) for further information on this extension.

###sulu-extension 
This extension contains multiple useful functions, making the developers live easier:

#### User Settings

* `sandbox.sulu.loadUrlAndMergeWithSetting (key, attributesArray, url, callback)`

	loads an url and matches it against user settings
	* {String} key Defines which setting to compare with
	* {String} attributesArray Defines which Attributes should NOT be taken from user-settings and from fields API instead
	* {String} url Where to fetch data from
	* {String} callback

* `sandbox.sulu.getUserSetting(key)`
	
	returns settings for a specified key
	* {String} key

* `sandbox.sulu.saveUserSetting(key, value, url)`

	saves data locally and to database
	* {String} key
	* {String} value
	* {String} url Defines where to save data to


#### Miscellaneous
* `sandbox.sulu.initListToolbarAndList(key, url, listToolbarOptions, datagridOptions)`

	initializes sulu list-toolbar with column options and datagrid. First, fields are loaded with the specified url and matched against settings of the specified key. Then a list-toolbar and the datagrid are initialized with the specified fields.
	
	* {String} key Settings key - will be stored in database with the specified key
	* {String} url Url to load and save fields
	* {Object} listToolbarOptions Options object of list-toolbar@suluadmin component
	* {Object} datagridOptions Options object of datagrid@husky component
