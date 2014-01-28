# Testing

## Enable testing support
The `SuluTestBundle` has to be installed in the current bundle or app. This is done with the adding the following line to the `require-dev`-attribute of the corresponding `composer.json`:

```
"sulu/test-bundle": "dev-develop"
```
Afterwards the `SuluTestBundle` can be installed with the command `composer update`. The last step is to add an instance of the `SuluTestBundle` in the AppKernel. In a standalone bundle it can be added to the `bundles`-array in `Tests/Resources/app/AppKernel.php` and in a full application it should be added only in the dev-environment.

## DatabaseTestCase
The DatabaseTestCase is the abstract base class for functional tests. It provides a member variable to the entity manager from doctrine and creates an instance of the SchemaTool, for resetting the database after every test run.

The usual test methods can be used, and although you should consider following the here described schema:

```php
<?php

namespace Sulu\Bundle\ExampleBundle\Tests\Functional\Controller;

use Doctrine\ORM\Tools\SchemaTool;

class TagControllerTest extends DatabaseTestCase
{
    /**
     * @var array
     */
    protected static $entities;

    public function setUp()
    {
        $this->setUpSchema();

        // your setup code
    }

    public function setUpSchema()
    {
        self::$tool = new SchemaTool(self::$em);

        self::$entities = array(
            self::$em->getClassMetadata('Sulu\Bundle\ExampleBundle\Entity\Example'),
            // and probably more ClassMetaData loaded like the line above
        );

        self::$tool->dropSchema(self::$entities);
        self::$tool->createSchema(self::$entities);
    }

    public function tearDown()
    {
        parent::tearDown();
        self::$tool->dropSchema(self::$entities);
    }

    // test methods
}

```

## Security
The testing environment must be set up to grant access to everybody. For this there are Test-Implementations of the Security-classes.
Use these classes and the http_basic authentication methods in the test configuration. This can be done with the following lines in `Tests/Resources/app/config/config.yml`:

```yml
# Configuration file for security in the test environment
# Grants access to every User
# DO NOT USE IN PRODUCTION ENVIRONMENT

security:
    access_decision_manager:
        strategy: affirmative

    encoders:
        Sulu\Bundle\TestBundle\Entity\TestUser: plaintext

    providers:
        testprovider:
            id: test_user_provider

    firewalls:
        test:
            http_basic:
```

In the tests the client of the symfony framework can handle the http_basic authentication method. Just passt the username `test` and the password `test` as credentials:

```php
$client = $this->createClient(
    array(),
    array(
        'PHP_AUTH_USER' => 'test',
        'PHP_AUTH_PW' => 'test',
    )
);
```

If the user gets persisted in the system under test, it will be stored in the `co_testusers`-table, with the following data:

field | value
--- | ---
id | 1
username | test
password | test
