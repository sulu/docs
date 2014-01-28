# Abstract RestController
* extracts some common rest functionality into a base class
* heavy usage of callback functions
* Childclass overwrites `entityName`-property
* Childclass uses predefined functions from abstract RestController (response* for response-generating functions and process* for functions doing some work without returning response objects)
 * responseGetById
 * responseList
 * processPut
 * responseFields
 * responsePersistSettings

## Example Usage
```php
<?php
namespace Sulu\Bundle\ExampleBundle\Controller;

use FOS\RestBundle\Routing\ClassResourceInterface;
use Sulu\Bundle\CoreBundle\Controller\Exception\EntityNotFoundException;
use Sulu\Bundle\CoreBundle\Controller\Exception\RestException;
use Sulu\Bundle\CoreBundle\Controller\RestController;
use \DateTime;

class ExampleController extends RestController implements ClassResourceInterface
{
     protected $entityName = 'SuluExampleBundle:Example';
     
     protected $unsortable = array('lft','rgt','depth');
     
     protected $fieldsDefault = array('name');
     protected $fieldsExcluded = array();
     protected $fieldsHidden = array('created');
     protected $fieldsRelations = array();
     protected $fieldsSortOrder = array();
     protected $fieldsTranslationKeys = array();
     protected $bundlePrefix = 'contact.accounts.';
    
     /**
     * returns all fields that can be used by list
     * @Get("accounts/fields")
     * @return mixed
     */
    public function getFieldsAction() {
        return $this->responseFields();
    }

    /**
     * persists a setting
     * @Put("accounts/fields")
     */
    public function putFieldsAction() {
        return $this->responsePersistSettings();
    }

    public function getAction($id)
    {
        $view = $this->responseGetById(
            $id,
            function ($id) {
                // Load data (e.g. from database)
            }
        );

        return $this->handleView($view);
    }

    public function listAction()
    {
        $view = $this->responseList();
        return $this->handleView($view);
    }

    public function deleteAction($id)
    {
        $view = $this->responseDelete(
            $id,
            function ($id) {
                // Delete data from database, throw Exceptions if operation not successful
                // EntityNotFoundException, EntityIdAlreadySetException and
                // an abstract RestException are already delivered with this bundle
            }
        );
        return $this->handleView($view);
    }
}
```
## ResponseList
ResponseList is usually taken for returning a flat structure of data. Therefore no nested relations are returned. 
Also, a HAL conform Rest API with useful informations for building a list is returned. 



## Fields Actions
The fields API is designed to return all presentable arguments of an entity (e.g. to display it in a list). To include it into your controller, the following actions have to be set BEFORE the getAction():
```
/**
     * returns all fields that can be used by list
     * @Get("[route]/fields")
     * @return mixed
     */
    public function getFieldsAction() {
        return $this->responseFields();
    }
````
If you would also like make the fields persistable for a certain user, then insert the responsePersistSettings-Action:
```
    /**
     * persists a setting
     * @Put("[route]/fields")
     */
    public function putFieldsAction() {
        return $this->responsePersistSettings();
    }
```

To define which fields should be displayed overwrite the following protected parameters:
* **$fieldsExcluded**: defines which fields should be excluded from api
* **$fieldsHidden**: defines which fields should not be visible by default
* **$fieldsRelations**: here, relation to other entities can be defined: e.g.: user_account_name
* **$fieldsSortOrder**: define the sort order of one or more fields: 0=>'name', 3=>'lastName'
* **$fieldsTranslationKeys**: defines specificialy which translation should be taken for a field otherwise the translationKey will be generated automatically by using the bundles $bundlePrefix
* **$fieldsDefault**: the fields that are marked as default. 
* **$fieldsEditable**: defines which fields can be edited
* **$fieldsValidation**: here validation rules for certain fields can be defined

#### TranslationKey generation
To understand how the translationkey is generated, it is important to understand the priorization of the parameters:
1. $fieldsTranslationKey  (if defined, this key will be taken for a field)
2. $fieldsDefaultTranslationKeys - defined in RestController (contains a set of most common translation keys, like 'id','name',..)
3. automatic generation by taking $bundlePrefix + fields ID 

If you do not want the predefined keys of the $fieldsDefaultTranslationKeys to be taken, just override it, or define the translation in $fieldsTranslationKey.
