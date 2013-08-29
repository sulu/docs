# Abstract RestController
* extracts some common rest functionality into a base class
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
        return $this->responseGetById(
            $id,
            function ($id) {
                // Load data (e.g. from database)
            }
        );
    }

    public function listAction()
    {
        return $this->responseList();
    }
}
```
