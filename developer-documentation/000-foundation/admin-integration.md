# Admin integration

* create admin class and define navigation in constructor
* create main.js file in `Resources/public/js`
 * is called when bundle gets initialized
 * register routes for bundle (usually extracted into own bundle.js file)
 * add path for bundle to require.config
 * usually extracted to bundle.js file with initialize-function

## Resources/public/js/main.js
* adds path to require.config
* use bundle.js to initialize routes

```javascript
require.config({
    paths: {
        suluexample: '../../suluexample/js'
    }
});

define(['suluexample/bundle'], function (Bundle) {

    'use strict';

    Bundle.initialize();

});
```

## Resources/public/js/bundle.js
* initlializes routes

```javascript
define(['router'], function (Router) {

    'use strict';

    var initialize = function () {
        // list all contacts
        Router.route('example', 'example:list', function() {
            require(['suluexample/controller/contact/list'], function(List) {
                new List({
                    el: App.$content
                });
            });
        });
    };

    return {
        initialize: initialize
    }
});
```

## Admin/SuluExampleAdmin.php
* Initializes navigation entries for bundle
* Initializes commands for app/console

```php
<?php
namespace Sulu\Bundle\ExampleBundle\Admin;

use Sulu\Bundle\AdminBundle\Admin\Admin;
use Sulu\Bundle\AdminBundle\Navigation\Navigation;
use Sulu\Bundle\AdminBundle\Navigation\NavigationItem;

class SuluExampleAdmin extends Admin
{

    public function __construct()
    {
        $rootNavigationItem = new NavigationItem('Root');
        $example = new NavigationItem('Example');
        $example->setIcon('example');
        $rootNavigationItem->addChild($example);

        $this->setNavigation(new Navigation($rootNavigationItem));
    }

    /**
     * {@inheritdoc}
     */
    public function getCommands()
    {
        return array();
    }

}

```
