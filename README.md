# UrgentCargus PHP API
The API is RESTful JSON over HTTP using [GuzzleHttp](http://docs.guzzlephp.org/en/latest/) as a HTTP client.

# Usage example
```php
$client = new \MNIB\UrgentCargus\Client($apiKey, $apiUri);
$client->createAccessToken('username', 'password');

$result = $client->get('PickupLocations');

$params = [
    'Sender' => [],
    'Recipient' => [],
    'Parcels' => 1,
    'TotalWeight' => 1,
    'DeclaredValue' => 1000,
    'CashRepayment' => 1000,
    'BankRepayment' => 0,
    'OpenPackage' => true,
    'SaturdayDelivery' => false,
    'PackageContent' => 'awb content',
    'CustomString' => $orderId,
];
$awbId = $client->post('Awbs', $params);
```

You can also pass additional [Guzzle client config](https://docs.guzzlephp.org/en/stable/request-options.html) to the constructor (except `base_uri`, which is always enforced from `$apiUri` or default API uri):
```php
$client = new \MNIB\UrgentCargus\Client($apiKey, $apiUri, [
    'timeout' => 30,
    'headers' => [
        'User-Agent' => 'MyApp/1.0',
    ],
]);
```

Per request, you can override or append headers and timeout:
```php
$client->get('PickupLocations', [], null, [
    'headers' => [
        'X-Correlation-ID' => '12345',
        'Content-Type' => 'application/json; charset=utf-8',
    ],
    'timeout' => 10,
]);
```

# Official UrgentCargus Documentation
https://urgentcargus.portal.azure-api.net
