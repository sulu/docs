# Testing

## Running tests

You can run all the tests from `sulu/sulu` using the following command:

````
$ ./bin/runtests.sh
````

You can execute tests for a specific bundle:

````
$ ./bin/runtests.sh ContentBundle
````

You will also want to execute tests directly with PHPUnit:

````
$ cd src/Sulu/Bundle/SearchBundle
$ phpunit
````

Note that you will need to launch the `runtests` script before running
the phpunit tests if you have tests which depend on the database.

## Debugging


### Launching the test console

The easiest way to launch the Symfony console in the test envionment (when
you have functional tests with an AppKernel) is to install this script:

    https://gist.github.com/dantleech/406197bae17a63c2c58b

You can then run `testconsole` from the base directory of any Sulu component.

## Implementing


### Adding tests

The `SuluTestBundle` has to be installed in the current bundle or app. This is
done with the adding the following line to the `require-dev`-attribute of the
corresponding `composer.json`:

```
"sulu/test-bundle": "dev-develop"
```

Afterwards the `SuluTestBundle` can be installed with the command `composer
update`. The last step is to add an instance of the `SuluTestBundle` in the
AppKernel. In a standalone bundle it can be added to the `bundles`-array in
`Tests/Resources/app/AppKernel.php` and in a full application it should be
added only in the dev-environment.

It's also very important to be sure that the security and testing-bundle are
configured correctly, as both of them deliver the same services (although the
one responsible for testing does it in a much easier way).

The Sulu testing practices are roughly based on the practices used by the
Symfony CMF. Be sure to check out the
[documentation](http://symfony.com/doc/current/cmf/components/testing.html) for
the Symfony testing component.

## Test directory structure

See the CMF testing documentation above, but briefly:

````
/Tests
    Unit/         # Tests which use mocks and nothing else
    Functional/   # Tests which test services and extend SuluTestCase
    WebTest/      # Tests which use the BrowserKit web client
````

## SuluTestCase

The `SuluTestCase` allows you to run tests within the context of your application. It extends
[CMF Testing](http://symfony.com/doc/current/cmf/components/testing.html) components
[BaseTestCase](https://github.com/symfony-cmf/Testing/blob/master/src/Functional/BaseTestCase.php).

It should be used whenever you need to test something which **requires a database/phpcr**
or when you do BrowserClient tests. It **must not** be used for Unit Tests.

A typical test might look like the following

````php
/*
 * This file is part of the Sulu CMS.
 *
 * (c) MASSIVE ART WebServices GmbH
 *
 * This source file is subject to the MIT license that is bundled
 * with this source code in the file LICENSE.
 */

namespace Sulu\Bundle\SecurityBundle\Tests\Functional\Controller;

use Sulu\Bundle\TestBundle\Testing\SuluTestCase;

class GroupControllerTest extends SuluTestCase
{
    public function setUp()
    {
        // retreve the entity manager
        $this->em = $this->db('ORM')->getOm();

        // purge the database
        $this->purgeDatabase();


        // load some fixtures
        $role1 = new Role();
        $role1->setName('Sulu Administrator');
        $role1->setSystem('Sulu');
        $role1->setCreated($datetime);
        $role1->setChanged($datetime);
        $this->em->persist($role1);
        $this->role1 = $role1;

        // ...

        $this->em->flush();
    }

    public function testList()
    {
        $client = $this->createAuthenticatedClient();
        $client->request('GET', '/api/groups?flat=true');

        $response = json_decode($client->getResponse()->getContent());

        $this->assertEquals(2, $response->total);
        $this->assertEquals('Group1', $response->_embedded->groups[0]->name);
        $this->assertEquals('Group2', $response->_embedded->groups[1]->name);
    }
````

Note the following methods are available when you extend `SuluTestCase`:

- **getContainer**: Return the container for the test application.
- **db($type)**: Return the DB manager (either `ORM` or `PHPCR` - see the CMF testing documentation)
- **getAuthenticatedClient**: Return a Symfony BrowserKit client has been configured with authentication credentials (see below)
- **purgeDatabase**: Remove all the records from the database (you should call this before creating fixtures)
- **initPhpcr**: Remove all the records in the content repository and then reinitialize the Sulu environemnt.

### Initializing the environment

You may need to do things such as update the database schema or start services before your test suite runs.

The test runner will automatically execute scripts in the following locations before starting the test run:

````
/path/to/bundle/Tests/Resources/app/testinit.sh
/path/to/bundle/Tests/app/testinit.sh
````

The script will be passed the kernel directory and the variable representing the console command as
illustrated in the following example:

````bash
#!/bin/bash

echo $KERNEL_DIR
echo $CONSOLE_COMMAND

$CONSOLE_COMMAND doctrine:schema:update
````

### Security

The testing environment must be set up to grant access to everybody. For this
there are Test-Implementations of the Security-classes.  Use these classes and
the http_basic authentication methods in the test configuration. This can be
done with the following lines in `Tests/Resources/app/config/config.yml`:

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

When you need to access the secured back office, use the `SuluTestCase#createAuthenticatedClient` method.

If the user gets persisted in the system under test, it will be stored in the `co_testusers`-table, with the following data:

field | value
--- | ---
id | 1
username | test
password | test
