# Testing

## Security
The testing environment must be set up to grant access to everybody. For this there are Test-Implementations of the Security-classes.
Use these classes and the http_basic authentication methods in the test configuration.

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
