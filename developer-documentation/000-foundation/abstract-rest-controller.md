# Abstract RestController
* extracts some common rest functionality into a base class
* heavy usage of callback functions
* Childclass overwrites `entityName`-property
* Childclass uses predefined functions from abstract RestController (response* for response-generating functions and process* for functions doing some work without returning response objects)
 * responseGetById
 * responseList
 * processPut

## Usage
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
                // EntityNotFoundException, EntityIdAlreadySetException and a RestException are already delivered with this bundle
            }
        );
    }
}
```
