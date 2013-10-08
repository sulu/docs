# Content Navigation Integration

The admin bundle holds all abstract classes and interfaces needed for implementing a content navigation. 
In the following it is assumed that a content-navigation should be implemented in AcmeContentBundle and extended in AcmeExtensionBundle.


## Insert Content Navigation into a Bundle

### Extend ContentNavigation

Create a file called AcmeContentNavigation in /Admin
    
```    
namespace Acme\Bundle\ContentBundle\Admin;

use Sulu\Bundle\AdminBundle\Admin\ContentNavigation;
use Sulu\Bundle\AdminBundle\Navigation\NavigationItem;

class AcmeContentContentNavigation extends ContentNavigation
{

    public function __construct()
    {
        parent::__construct();

		// define navigation 
        $this->setName('Content');
        $this->setHeader(array(
            'title'         => 'back to content',
            'displayOption' => 'link',
            'action'        => 'content'
        ));
		// define content-tabs
        $details = new NavigationItem('Details');
        $details->setContentType('contact');
        $details->setAction('details');
        $details->setType('content');

        $this->addNavigationItem($details);
    }
}

```
And add service to Resources/config/services.yml (or xml):

```
parameters:
    acme_content.admin.content_navigation.class: Acme\Bundle\ContentBundle\Admin\AcmeContentContentNavigation

services:
    acme_content.admin.content_navigation:
        class: %acme_content.admin.content_navigation.class%
```
    	
### Extend Compiler Pass

In \DependencyInjection\Compiler insert AddContentNavigationPass. Rename services and tag. 

```
namespace Acme\Bundle\ContentBundle\DependencyInjection\Compiler;

use Sulu\Bundle\AdminBundle\DependencyInjection\Compiler\ContentNavigationPass;

/**
 * Add all services with the tag "acme.content.content_navigation" to the content navigation
 *
 * @package Sulu\Bundle\AdminBundle\DependencyInjection\Compiler
 */
class AddContentNavigationPass extends ContentNavigationPass
{

    public function __construct()
    {
        self::$tag = 'acme.content.admin.content_navigation';
        self::$serviceName = 'acme_content.admin.content_navigation';
    }

}
```

Then add compilerpass to bundles build function (AcmeContentBundle.php):

```
…
class AcmeContentBundle extends Bundle
{
    public function build(ContainerBuilder $container)
    {
        parent::build($container);

        $container->addCompilerPass(new AddContentNavigationPass);
    }
}

```

### Navigation Controller
In Controllers Directory create Navigation Controller, which returns Navigation object.
The toArray('contact') function will return all NavigationItems which have the contentType = 'contact'; (which were defined in AcmeContentContentNavigation).

```
namespace Sulu\Bundle\ContactBundle\Controller;

use Sulu\Bundle\AdminBundle\Admin\ContentNavigation;
use Symfony\Bundle\FrameworkBundle\Controller\Controller;
use Symfony\Component\HttpFoundation\Response;

class NavigationController extends Controller
{

    const SERVICE_NAME = 'acme_content.admin.content_navigation';    

    /**
     * Lists all the contacts or filters the contacts by parameters
     * Special function for lists
     * @return \Symfony\Component\HttpFoundation\Response
     */
    public function contactAction()
    {

        // TODO: get type of content (contact / account ...)

        /** @var ContentNavigation $contentNavigation */
        if ($this->has(self::SERVICE_NAME)) {
            $contentNavigation = $this->get(self::SERVICE_NAME);
        }

        return new Response(json_encode($contentNavigation->toArray('contact')));
    }
}
```

Don't forget to define the specified route in routes.yml!

### Javascript - get navigation  object
When you want to load the contentnavigation put following code into your javascript:
```

		initialize: function() {
	      	// show navigation submenu
           	this.getTabs(this.options.id, function(navigation) {
                this.sandbox.emit('navigation.item.column.show', {
                    data: navigation
                });
           	}.bind(this))
		},
 	     
       	
		getTabs: function(id, callback) {
            var navigation = JSON.parse(ContentNavigation),
                hasNew, hasEdit;

            // get url from backbone
            this.sandbox.emit('navigation.url', function(url) {
                var items = [];
                // check action
                this.sandbox.util.foreach(navigation.sub.items, function(content) {
                    // check DisplayMode (new or edit) and show menu item or don't
                    hasNew = content.displayOptions.indexOf('new') >= 0;
                    hasEdit = content.displayOptions.indexOf('edit') >= 0;
                    if ((!id && hasNew) || (id && hasEdit)) {
                        content.action = this.parseActionUrl(content.action, url, id);
                        items.push(content);
                    }
                }.bind(this));
                navigation.sub.items = items;
                callback(navigation);
            }.bind(this));
        },

        parseActionUrl: function(actionString, url, id) {
            // if first char is '/' use absolute url
            if (actionString.substr(0, 1) === '/') {
                return actionString.substr(1, actionString.length);
            }
            if (id) {
                var strSearch = 'edit:' + id;
                url = url.substr(0, url.indexOf(strSearch) + strSearch.length);
            }
            return  url + '/' + actionString;
        }
    };
            
```


## Extend Navigation in another Bundle

If the Navigation should be extended by another Bundle proceed by following steps

### implement ContentNavigationInterface
create a file AcmeExtensionContentNavigation in /Admin which implements ContentNavigationInterface of SuluAdminBundle:

```
namespace Acme\Bundle\ExtensionBundle\Admin;

use Sulu\Bundle\AdminBundle\Navigation\ContentNavigationInterface;
use Sulu\Bundle\AdminBundle\Navigation\NavigationItem;

class AcmeExtensionContentNavigation implements ContentNavigationInterface
{

    private $navigation = array();

    public function __construct()
    {
        $permissions = new NavigationItem('Permissions');
        $permissions->setContentType('contact');
        $permissions->setAction('permissions');
        $permissions->setDisplayOptions(array('edit'));
        $permissions->setType('content');

        $this->navigation[] = $permissions;
    }

    public function getNavigationItems()
    {
        return $this->navigation;
    }
}
```

Now go to the bundles services.xml and register a tagged service with the tagname you specified in AcmeContentBundle before:

```
<parameters>
        <parameter key="acme_extension.admin.content_navigation.class">Acme\Bundle\ExtensionBundle\Admin\AcmeExtensionContentNavigation</parameter>
</parameters>
<services>
        <service id="acme_extension.admin.content_navigation" class="%acme_extension.admin.content_navigation.class%">
            <tag name="acme.extension.admin.content_navigation"/>
        </service>
</services>
```
Now the content-navigation of AcmeContentBundle is going to be extended by the NavigationItems of AcmeExtensionBundle.
