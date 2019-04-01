# [Sending email messages in Basic App](http://basic-app.com/core/sending-emails.md)

The [PHPMailer](https://github.com/PHPMailer/PHPMailer) library is responsible for sending messages to the Basic App. Basic App allows you to set basic settings for sending mail in the backend of the site through the web interface. You will need to specify the name and e-mail address of the sender, on behalf of whom your site will send letters to users. In addition, you can specify the SMTP server settings that will be used to send emails.

For each email that the site sends, you can enable the option to send a copy of the email to the administrator. When this option is enabled, the administrator is added to the BCC email header. E-mail and administrator's name as well as other settings can be specified in the mail settings in the backend.

#### In total, you can configure the following options:

  - From Name
  - From E-mail
  - Reply To
  - Admin Name
  - Admin E-mail
  - Charset
  - Encoding
  - Use SMTP
  - SMTP Host
  - SMTP Port
  - SMTP Username
  - SMTP Password
  - SMTP Encryption (None, TLS, SSL)
  
`Reply To` Dropdown is responsible for what address will be specified in the `Reply-To` technical header for the email to be sent. If `Reply to Sender` is selected, then the `Reply-To` header will contain the address of the sender of the email, and if you select `Reply to Admin`, then the recipient of the email will be asked to reply to the address of the site administrator. You can leave this field blank, in which case the Basic App will not add a `Reply-To` header to the email.
  
If the SMTP flag is enabled, the site sends emails via the SMTP protocol using the SMTP server settings you specified. If this flag is not set, then the emails are sent in the usual way, even if the settings for the SMTP server are specified.

#### Sending emails:

To send emails, there is a service function `create_mailer()`, which creates and returns a new `PHPMailer` object in which all the settings that you specified in the mail settings in the backend are filled.

```
function create_mailer(bool $sendToAdmin = false, array $attachments = [])
```

If The admin e-mail field was configured in the admin panel, and the `create_mailer()` function was passed true to the `$sendToAdmin` parameter, the administrator will receive a copy of the email.

In the `$attachments` parameter, you can specify an array of files that will be added to the email sent in the attachment. You can specify the full path to the file in the value of an array element, and if you want to change the name of the file being sent, you must specify the array element in the `key => value` format, where key is the path to the file being sent, and value is its new name. 

#### Using the `create_mailer()` function:

```
$mail = create_mailer(true, ['/path/to/file1.jpg', '/path/to/file2.jpg' => 'New File Name.jpg']);

$mail->addAddress('user@example.com');
$mail->Subject = 'Here is the subject';
$mail->Body = 'This is the HTML message body';

$mail->send();
```

#### Templates of sent emails:

Using the `create_mailer()` function, you get full control over the email you send, but in most cases you need to send the same email to different users of your site. In the Basic App backend there is a special section for managing templates for sending emails. For the template, you can specify the following parameters:

  - UID
  - Subject
  - Body
  - Body is HTML
  - Enabled
  - Send Copy to Admin
  
If the `Enabled` flag is not set, then emails of this type will not be sent by the site. 

The Body is HTML flag is responsible for the format of the email text. As HTML, if it is active, or as simple text, in case the flag is not selected.

If you have set up an administrator’s e-mail address in the mail settings, then the header of the sent email will be added to the BCC. 

The `send_message()` function is responsible for sending emails according to a template:

```
function send_message(
    string $uid, 
    array $to = [], 
    bool $create = false, 
    array $message_params = [], 
    array $params = [], 
    array $options = []
)
```

The `$uid` parameter specifies the letter template identifier. You can specify the `$create` parameter as true to automatically create a template with such an identifier if it does not exist. 

In the `$message_params` property, you can specify additional parameters for the template being created:

  - message_subject
  - message_body
  - message_is_html
  - message_send_copy_to_admin
  - message_enabled
  
In the `$to` parameter you specify the recipients of the email as an array. You can specify the e-mail address of the recipient of the email in the value of the array element, and if you want to specify its name, you must specify the array element in the `key => value` format, where key is the e-mail address and value is the name of the recipient of the email.

In the `$params` parameter, you specify an array of parameters that will be replaced in the header and body of the email via the `strtr()` PHP function.

The `$options` parameter specifies additional email options. At the moment, this is only one possible parameter with the attachments key to attach files to the email. See the format of the parameter of the key attachments in the description of the `create_mailer()` function.

#### Example of use:

```
try
{
    $is_send = send_message(
        'test', 
        ['user@example.com'],
        true,
        [
            'message_subject' => 'Test message {date}',
            'message_body' => 'Hello, {name}',
            'message_enabled' => 1
        ],
        [
            '{date}' => date('Y-m-d'),
            '{name}' => 'J.D.'
        ],
        [
            'attachments' => [
                '/path/to/file1.jpg', 
                '/path/to/file2.jpg' => 'New File Name.jpg'
            ]
        ]
    );
}
catch(Exception $ex)
{
    $error = $ex->getMessage(); // error
}
```

The `send_message()` function returns true or false, depending on whether the email was sent. This depends on whether the enabled flag of the sent email template is turned on. If the flag is not turned on, this is a normal situation in which the email will not be sent, and false will be returned, in all other cases an exception will be thrown, in case of any error when sending the email, or the function will return true if the email was sent successfully.