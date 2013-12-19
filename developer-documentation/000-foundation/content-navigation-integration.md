# Integrate Content Tabs into your application
To integrate Content Tabs into your application you first need to implement a content navigation for your bundle in the backend. After that the server is going to be able to send the necesseary navigation data to the frontend application. After that, 

#### Table of Contents
[I. Content Navigation Integration in the Backend](#backend)<br />
 [ 1. create a content navigation in your bundle](#backend-create)<br />
 [ 2. extend an existing content navigation of another bundle](#backend-extend)<br />
[II. Content Tabs Integration into the Frontend](#frontend)<br />

##<a name="backend"></a> I. Content Navigation Integration in the Backend

The admin bundle holds all abstract classes and interfaces needed for implementing a content navigation. 
There are two different use cases: 

1. create a content navigation in your bundle
2. extend an existing content navigation of another bundle

In the following it is assumed that a content-navigation should be implemented in AcmeContactBundle and extended in AcmePermissionsBundle. 


###<a name="backend-create"></a> 1. Create Content Navigation in a Bundle

#### Create ContentNavigation

Create a file called AcmeContentNavigation in /Admin
    
```    
namespace Acme\Bundle\ContactBundle\Admin;

use Sulu\Bundle\AdminBundle\Admin\ContentNavigation;
use Sulu\Bundle\AdminBundle\Navigation\NavigationItem;

class AcmeContactContentNavigation extends ContentNavigation
{

    public function __construct()
    {
        parent::__construct();

		// define content-tabs
        $details = new NavigationItem('Details');
        $details->setAction('details');
        $details->setContentType('contact');
        // define which component has to be called
        $details->setContentComponent('contacts@acmecontact');
        $details->setContentComponentOptions(array('display'=>'form'));
        $this->addNavigationItem($details);
    }
}

```

The following NavigationItem options are important for creating a content item:
* setAction - the url to be called (either relative or absolute by providing '/')
* setContentType - used to group content tabs
* setContentDisplay - array which defines when tabs are shown (either 'new' or 'edit')
* setContentComponent - defines which component is called when clicking tab
* setContentComponentOption - array of options

And add service to Resources/config/services.yml (or xml):

```
parameters:
    acme_contact.admin.content_navigation.class: Acme\Bundle\ContactBundle\Admin\AcmeContentContentNavigation

services:
    acme_contact.admin.content_navigation:
        class: %acme_contact.admin.content_navigation.class%
```
    	
#### Create Compiler Pass (optional)

This step has only to be done, if you'd like to extend your content navigation by another bundle (see 2.).

In \DependencyInjection\Compiler insert AddContentNavigationPass. Rename services and tag. 

```
namespace Acme\Bundle\ContactBundle\DependencyInjection\Compiler;

use Sulu\Bundle\AdminBundle\DependencyInjection\Compiler\ContentNavigationPass;

/**
 * Add all services with the tag "acme.contact.content_navigation" to the content navigation
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

Then add compilerpass to bundles build function (AcmeContactBundle.php):

```
…
class AcmeContactBundle extends Bundle
{
    public function build(ContainerBuilder $container)
    {
        parent::build($container);

        $container->addCompilerPass(new AddContentNavigationPass);
    }
}

```

#### Navigation Controller
In Controllers Directory create Navigation Controller, which returns Navigation object.
The toArray('contact') function will return all NavigationItems which have the contentType = 'contact'; (which were defined in AcmeContentContentNavigation).

```
namespace Acme\Bundle\ContactBundle\Controller;

use Sulu\Bundle\AdminBundle\Admin\ContentNavigation;
use Symfony\Bundle\FrameworkBundle\Controller\Controller;
use Symfony\Component\HttpFoundation\Response;

class NavigationController extends Controller
{
    // has to be the same as defined in service.yml
    const SERVICE_NAME = 'acme_contact.admin.content_navigation';    

    /**
     * Lists all the contacts or filters the contacts by parameters
     * Special function for lists
     * @return \Symfony\Component\HttpFoundation\Response
     */
    public function contactAction()
    {

        /** @var ContentNavigation $contentNavigation */
        if ($this->has(self::SERVICE_NAME)) {
            $contentNavigation = $this->get(self::SERVICE_NAME);
        }

        return new Response(json_encode($contentNavigation->toArray('contact')));
    }
}
```

Don't forget to define the specified route in routing.yml:
```
acme_contact.navigation:
    path: /navigation/contact
    defaults: { _controller: AcmeContentBundle:Navigation:contact }
```

###<a name="backend-extend"></a> 2. Extend Navigation in another Bundle

If the Navigation should be extended by another Bundle proceed by following steps

#### implement ContentNavigationInterface
create a file AcmeExtensionContentNavigation in /Admin which implements ContentNavigationInterface of SuluAdminBundle:

```
namespace Acme\Bundle\PermissionBundle\Admin;

use Sulu\Bundle\AdminBundle\Navigation\ContentNavigationInterface;
use Sulu\Bundle\AdminBundle\Navigation\NavigationItem;

class AcmePermissionContentNavigation implements ContentNavigationInterface
{

    private $navigation = array();

    public function __construct()
    {
        $permissions = new NavigationItem('Permissions');
        $permissions->setAction('permissions');
        $permissions->setContentType('contact');
        $permissions->setContentDisplay(array('edit'));
        $permissions->setContentComponent('permissions@acmepermission');
        $permissions->setContentComponentOptions(array('display'=>'permissions');
        
        $this->navigation[] = $permissions;
    }

    public function getNavigationItems()
    {
        return $this->navigation;
    }
}
```

Now go to the bundles services.xml and register a tagged service with the tagname you specified in AcmeContactBundle before:

```
<parameters>
        <parameter key="acme_permission.admin.content_navigation.class">Acme\Bundle\PermissionBundle\Admin\AcmePermissionContentNavigation</parameter>
</parameters>
<services>
        <service id="acme_permission.admin.content_navigation" class="%acme_permission.admin.content_navigation.class%">
            <tag name="acme.permission.admin.content_navigation"/>
        </service>
</services>
```
Now the content-navigation of AcmeContactBundle is going to be extended by the NavigationItems of AcmePermissionBundle.

##<a name="frontend"></a> II. Content Tabs Integration into the Frontend
After you have integrated the content navigation in the backend you will be able to integrate content tabs in the frontend part of your application. 

For the components that should contain the content tabs and the edit toolbar a new component must be created. We like to call it content component.
So in our example, we create the component *contacts/components/content/main.js*:

```
define(function() {

    'use strict';

    return {
        content: {
            url: '/admin/contact/navigation/account',
            title: 'contact.accounts.title'
        }
    };
});
```
This component is just an abstract version and will start the sulu-content-tabs extension of the admin bundle, which will load the navigation from the specified url and then initialize the edit-toolbar and the tabs. The tabs are then loading the component that was specified in the backend above.

But before we are done, you will need to open / create your bundles main.js file. There you have to create backbone routes for your application.
```
        // show form for editing a contact
        sandbox.mvc.routes.push({
            route: 'contacts/contacts/edit::id/:content',
            callback: function(id, content){
                this.html(
                    '<div data-aura-component="contacts/components/content@acmecontact" data-aura-content="'+content+'" data-aura-id="' +id + '"/>'
                );
            }
        });
```

For the components containing the tabs you will need to first start the content component as specified above.

And now we are done.
