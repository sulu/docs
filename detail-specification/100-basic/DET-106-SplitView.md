# SplitView

The Splitview Component enables the developer to develop a widget based overview for example a contact.

__Parts:__

* Backend:
  * Controller to handle request
  * Service for rendering SplitView content
  * Private Service for each Widget with a special Tag
  * CompilerPass to compile tags for a service ID
* Frontend:
  * Aura Component get a url and a parameter to request the content
  
## Backend

### Controller

__/Controller/ContactSplitViewController.php__

```php
class ContactSplitViewController extends Controller
{
    public function renderAction($id)
    {
        /** @var SplitViewInterface $view */
        $view = $this->get('sulu_contact.contact.split_view');

        return new Response($view->render($id));
    }
}
```

### Widgets

__/SplitView/ContactExampleWidget1.php__

```php
/**
 * example widget for contact controller
 * @package Sulu\Bundle\ContactBundle\SplitView
 */
class ContactExampleWidget1 implements SplitViewWidgetInterface
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
        return 'SuluContactBundle:SplitView:example1.html.twig';
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

__/Resources/views/SplitView/example1.html.twig__

```html
<p>Widget: {{ name }} with priority: {{ priority }}</p>

<p>{{ data.test }}</p>
```

### Service Configuration

__/Resources/config/services.yml__

```yml
parameters:
    sulu_contact.contact.split_view.class: Sulu\Bundle\AdminBundle\SplitView\SplitView
    sulu_contact.contact.split_view.widget1.class: Sulu\Bundle\ContactBundle\SplitView\ContactExampleWidget1
    sulu_contact.contact.split_view.widget2.class: Sulu\Bundle\ContactBundle\SplitView\ContactExampleWidget2
    
services:
    sulu_contact.contact.split_view:
        class: %sulu_contact.contact.split_view.class%
        arguments: [@templating, "Contact Split View"]
    sulu_contact.contact.split_view.widget1:
        class: %sulu_contact.contact.split_view.widget1.class%
        tags:
            - {name: sulu.contact.split_view, priority: 5}
            - {name: sulu.contact.split_view, priority: 10}
    sulu_contact.contact.split_view.widget2:
        class: %sulu_contact.contact.split_view.widget2.class%
        tags:
            - {name: sulu.contact.split_view, priority: 20}
            - {name: sulu.contact.split_view, priority: 1}
```

### CompilerPass

__/SuluContactBundle.php__

```php
class SuluContactBundle extends Bundle
{
    public function build(ContainerBuilder $container)
    {
        parent::build($container);

        $container->addCompilerPass(
            new Sulu\Bundle\AdminBundle\SplitView\SplitViewCompilerPass('sulu_contact.contact.split_view', 'sulu.contact.split_view')
        );
    }
}
```

### Result

```html
<div id="split-view">
    <div class="header">
        <h1>Contact Split View</h1>
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

## Frontend

TODO