LocalBitcoins.com PHP Client
============================

This is a (work-in-progress) client for the LocalBitcoins.com API:

https://localbitcoins.com/api-docs/

TODO
----

 * [x] Authentication
 * [x] AccountInfo
 * [x] Myself
 * [ ] Escrows
 * [ ] EscrowRelease
 * [ ] Ads
 * [ ] AdUpdate

Installing
----------

Install with composer:

```bash
git clone https://github.com/lox/localbtc-php.git
composer install
```

Authenticating
--------------

The API uses OAuth2, so it's somewhat annoying to authenticate to for console apps. First you need 
to register an application and generate a client ID and client secret in the API console:

https://localbitcoins.com/accounts/api/

Then use these commands to generate a access_token:

```
export LOCALBITCOINS_CLIENT_ID=1234567
export LOCALBITCOINS_CLIENT_SECRET=123456

php oauth.php --authorize
php -S localhost:9000 oauth.php
```

Click the link generated, grant the application access in your localbitcoins.com account.

Copy the access_token from the output for the below example.

Example
-------

```php
<?php

$client = \LocalBtc\Client::factory(array(
    'access_token' => 'generated access token goes here',
));

$command = $client->getCommand('Myself');
$data = $client->execute($command);

var_dump($data);
```
