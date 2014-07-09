# Abstract RestController
* extracts some common rest functionality into a base class
* heavy usage of callback functions
* Childclass overwrites `entityName`-property
* Childclass uses predefined functions from abstract RestController
 * responseGetById
 * responseDelete
 * responsePersistSettings

# ListBuilder
* Creates the query and result for the given data with field descriptors
* Field Descriptors are different for every ListBuilder Implementation
 * e.g. DoctrineFieldDescriptor also requires information about joins
* ListBuilder is created with a concrete factory implementation
 * e.g. DoctrineListBuilderFactory
* ListBuilder is passed to the `initializeListBuilder`-Method of the `RestHelper`-Service
 * This method creates sets some values based on the common request parameters
* afterwards data can be set by methods available by the `ListBuilderInterface`
* ListRepresentation is used to deliver a list-response

# API Wrapper
* The `ApiWrapper`-class wraps an entity (e.g. from doctrine)
* Acts as a kind of a proxy to this entity, but creates it's own getter-methods for the API
* Data will be serialized by JMSSerializer with the `VirtualProperty`-Annotation

# Example Usage
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
     
     /**
      * @var DoctrineFieldDescriptor[]
      */
     protected $fieldDescriptors = array();
     
     public function __construct()
     {
        $this->fieldDescriptors['id'] = new DoctrineFieldDescriptor('id', 'id', $this->entityName);
        $this->fieldDescriptors['code'] = new DoctrineFieldDescriptor('code', 'code', $this->entityName);
        $this->fieldDescriptors['number'] = new DoctrineFieldDescriptor('number', 'number', $this->entityName);
     }
     
     /**
     * returns all fields that can be used by list
     * @Get("accounts/fields")
     * @return mixed
     */
    public function getFieldsAction() {
        return $this->handleView($this->view(array_values($this->fieldDescriptors)));
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

    public function cgetAction(Request $request)
    {
        $filter = array();

        $status = $request->get('status');
        if ($status) {
            $filter['status'] = $status;
        }

        $type = $request->get('type');
        if ($type) {
            $filter['type'] = $type;
        }

        if ($request->get('flat') == 'true') {
            /** @var RestHelperInterface $restHelper */
            $restHelper = $this->get('sulu_core.rest_helper');

            /** @var DoctrineListBuilderFactory $factory */
            $factory = $this->get('sulu_core.doctrine_list_builder_factory');

            $listBuilder = $factory->create($this->entityName);

            $restHelper->initializeListBuilder($listBuilder, $this->fieldDescriptors);

            foreach ($filter as $key => $value) {
                $listBuilder->where($this->fieldDescriptors[$key], $value);
            }

            $list = new ListRepresentation(
                $listBuilder->execute(),
                'products',
                'get_products',
                $request->query->all(),
                $listBuilder->getCurrentPage(),
                $listBuilder->getLimit(),
                $listBuilder->count()
            );
        } else {
            $list = new CollectionRepresentation(
                $this->getManager()->findAllByLocale($this->getLocale($request), $filter),
                'products'
            );
        }

        $view = $this->view($list, 200);
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
