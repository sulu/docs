# App-config

used for receiving global vars in javascipt

##provided functions:
	
* **getUser()**

 	returns user variables + settings
 	
* **getSection(identifier)**

	@param {String} identifier - bundle name
	
	returns bundle specific settings. 
	
	
##example

```
define(['app-config'], function(AppConfig) {

	var section = AppConfig.getSection('contact-bundle');
	var types = section['types'];

```
	
##How-to pass global javascript vars from your Bundle

Basically there are two ways of defining new global javascript variables for your bundle. 

###directly define variables as arguments in service. First parameter has to be the identifying string

	```
	parameters:
		sulu_contact.jsconfig.class: Sulu\Bundle\AdminBundle\Admin\JsConfig
	services:
 	    sulu_contact.jsconfig:
        class: %sulu_contact.jsconfig.class%
        arguments:
          - 'custom-bundle'
          - type : 'basic'
            test : bla
        tags:
        - { name: sulu.jsconfig }
	```
        
###define your own JsConfig file

	Create new File:   
	  
	```   
	namespace Sulu\Bundle\ContactBundle\Admin;

	use Sulu\Bundle\AdminBundle\Admin\JsConfig;
	use Sulu\Bundle\ContactBundle\Entity\Account;

	class SuluContactJsConfig extends JsConfig
	{

    	protected $bundleName = 'sulu-contact';

   		public function __construct($bundleName = '', $params = array())
    	{

        	$this->parameters = array(
            	'accountTypes' => array(1,2,3,4)
			);
        	$this->parameters = array_merge($this->parameters, $params);
    	}
	}
	```
	then define the service as described above, change class
