# Widgets

The Widgets feature enables the developer to develop a widget-based overview which can be used, for example, to display further information for a contact.

__Parts:__

* Backend:
  * Controller to handle request
  * Service for rendering the content of the widgets
  * Private Service for each Widget with a special Tag
  * CompilerPass to compile tags for a service ID
* Frontend:
  * Aura Component get a url and a parameter to request the content
  
## Backend

### Controller

__/Controller/ContactWidgetsController.php__

```php
class ContactWidgetsController extends Controller
{
    public function renderAction($id)
    {
        /** @var WidgetsInterface $view */
        $view = $this->get('sulu_contact.contact.widgets');

        return new Response($view->render($id));
    }
}
```

### The widgets themselve

__/Widgets/ContactExampleWidget1.php__

```php
/**
 * example widget for contact controller
 * @package Sulu\Bundle\ContactBundle\Widgets
 */
class ContactExampleWidget1 implements WidgetInterface
{
    /**
     * return name of widget
     * @return string
     */
    public function getName()
    {
        return 'Example1';
    }

    /**
     * returns template name of widget
     * @return string
     */
    public function getTemplate()
    {
        return 'SuluContactBundle:Widgets:example1.html.twig';
    }

    /**
     * returns data to render template
     * @param mixed $id
     * @return array
     */
    public function getData($id)
    {
        return array(
            'test' => 1
        );
    }
}
```

__/Resources/views/Widgets/example1.html.twig__

```html
<p>Widget: {{ name }} with priority: {{ priority }}</p>

<p>{{ data.test }}</p>
```

### Service Configuration

__/Resources/config/services.yml__

```yml
parameters:
    sulu_contact.contact.widgets.widget1.class: Sulu\Bundle\ContactBundle\Widgets\ContactExampleWidget1
    sulu_contact.contact.widgets.widget2.class: Sulu\Bundle\ContactBundle\Widgets\ContactExampleWidget2
    
services:
    sulu_contact.contact.widgets.widget1:
        class: %sulu_contact.contact.widgets.widget1.class%
        tags:
            - {name: sulu.widget, alias: sulu-contact-account-info}
    sulu_contact.contact.widgets.widget2:
        class: %sulu_contact.contact.widgets.widget2.class%
        tags:
            - {name: sulu.widget, alias: sulu-contact-contact-info}
```

### CompilerPass

__/SuluAdminBundle.php__

```php
class SuluAdminBundle extends Bundle
{
    public function build(ContainerBuilder $container)
    {
        parent::build($container);

        $container->addCompilerPass(
            new Sulu\Bundle\AdminBundle\Widgets\WidgetsCompilerPass('sulu_contact.contact.widgets', 'sulu.contact.widgets')
        );
    }
}
```

### Result

```html
<div id="widgets">
    <div class="header">
        <h1>Contact Widgets</h1>
    </div>

    <div class="content">
        <div class="widget widget-Example2 widget-priority-20">
            <p>Widget: Example2 with priority: 20</p>

            <p>2</p>
        </div>
        <div class="widget widget-Example1 widget-priority-10">
            <p>Widget: Example1 with priority: 10</p>

            <p>1</p>
        </div>
        <div class="widget widget-Example1 widget-priority-5">
            <p>Widget: Example1 with priority: 5</p>

            <p>1</p>
        </div>
        <div class="widget widget-Example2 widget-priority-1">
            <p>Widget: Example2 with priority: 1</p>

            <p>2</p>
        </div>
    </div>
</div>
```

##Frontend

TODO


##Widget Toolbar

Basic idea behind the handling of the toolbar items:

###WidgetToolbarItemService
A WidgetToolbarItemService should implement the WidgetToolbarItemServiceInterface and provides WidgetToolbarItems for the toolbar in the sidebar. Each WidgetToolbaritemPass will be collected by the WidgetToolbarItemPass when it has the `sulu.widget.toolbar_items` tag.

###WidgetToolbarItemPass
The WidgetToolbarItemPass will collect the tagged WidgetToolbarItemServices and add them to the WidgetToolbarItemManager.

###WidgetToolbarItemManager
The WidgetToolbarItemManager holds a set of WidgetToolbarItemServices and will delegate the getWidgetToolbarItems method call to each service.

```
sulu_admin.widgets_toolbar_item_manager:
	class: %sulu_admin.widgets_toolbar_item_manager.class%
```

###WidgetToolbarContext
This object is just a container for the current context.

###WidgetToolbarItem
This object is just a container which holds all information needed for the toolbar to render a icon.

![image](https://raw.githubusercontent.com/sulu-cmf/docs/master/detail-specification/images/diagrams/WidgetToolbarItem.png)
