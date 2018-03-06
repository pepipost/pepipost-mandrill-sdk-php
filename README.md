# pepipost-mandrill-sdk-php
Modified Mandrill SDK working via Pepipost API

# Install
```
curl -s http://getcomposer.org/installer | php
```
```
php composer.phar require pepipost/pepipost-mandrill-sdk-php:dev-master
```

# Usage:
```php
<?php
require 'vendor/autoload.php';
$mandrill = new Mandrill('yourPepipostsecretkey'); // PEPIPOST API KEY HERE
$message = array(
        'subject' => "This is your subject",
        'from_name' => 'sender name',
        'from_email' => 'from@example.com',
        'html' => '<p>hi [% NAME %], Pepipost Mandrill Migration API Testing Test</p>',//file_get_contents($template_files[$j]),
        'recipients_cc' => 'recipient1@domain.com',
        'bcc' => 'bcc@domain.com',
        'to' => array(
            array(
                "email" => 'recipient@example.com',
                "name" => ''
            )
        ),
        'important' => true,
        'track_opens' => true,
        'track_clicks' => true,
        'tags' => array("Tag1"),
        'merge_vars' => array(
            array(
                    "rcpt" => 'recipient@example.com',
                    "vars" => array(
                        array(
                            "name" => "NameOfRecipient1",
                            "age" => "11"
                        )
                    )
            )
        )
);
//$result = $mandrill->messages->send($message, $async, $ip_pool, $send_at);
try{
    $result = $mandrill->messages->send($message);
}
catch(Mandrill_Error $e) {
    // Mandrill errors are thrown as exceptions
    echo 'A mandrill(via Pepipost) error occurred: ' . get_class($e) . ' - ' . $e->getMessage();
    // A mandrill error occurred: Mandrill_Unknown_Subaccount - No subaccount exists with the id 'customer-123'
    throw $e;
}

print_r($result);
