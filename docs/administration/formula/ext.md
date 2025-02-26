# Formula > Functions > Ext

* [ext\account\findByEmailAddressDomain](#extaccountfindbyemailaddressdomain)
* [ext\email\send](#extemailsend)
* [ext\email\applyTemplate](#extemailapplytemplate)
* [ext\sms\send](#extsmssend)
* [ext\pdf\generate](#extpdfgenerate)
* [ext\user\sendAccessInfo](#extusersendaccessinfo)

## ext\account\findByEmailAddressDomain

`ext\account\findByEmailAddressDomain(EMAIL_ADDRESS)`

Finds an account by an email address. If no full match found, then tries to find by domain name. Free email provider domains are ignored. 
Returns ID or null.

## ext\email\send

`ext\email\send(EMAIL_ID)`

Sends an email. EMAIL_ID is an ID of an email record. Returns TRUE if sent, false if not sent.

If *from* address is not set in the email, then the system email address will be used. If there's match between *from* address and 
the address of some group email account, then SMTP setting of the group email account will be used.

Example:

```
$id = record\create(
    'Email',
    'from', 'from-address@test.com',
    'to', 'to-address@test.com',
    'subject', 'Test from formula',
    'body', 'Hi,\n\nThis is a test.',
    'isHtml', false,
    'status', 'Sending'
);
ext\email\send($id);
```

## ext\email\applyTemplate

`ext\email\applyTemplate(EMAIL_ID, EMAIL_TEMPLATE_ID, [PARENT_TYPE, PARENT_ID])`

Applies an email template to an existng email record. Parent record can be passed optionally.

Example:

```
$emailId = record\create(
    'Email',
    'to', 'to-address@test.com',
    'status', 'Draft',
    'parentId', entity\attribute('id'),
    'parentType', 'Case'
);
ext\email\applyTemplate($emailId, 'some-email-template-id');
ext\email\send($emailId);
```

## ext\sms\send

`ext\sms\send(SMS_ID)`

Sends an SMD. SMS_ID is an ID of an SMS record. Returns TRUE if sent, false if not sent. (Available as of v7.0)

Example:

```
$smsId = record\create(
    'Sms',
    'to', '+1 000 111 222',
    'body', 'This is a test.'
);

ext\sms\send($smsId);
```

If *from* address is not set in the SMS, then the system SMS from number will be used.

The extension with SMS providers can be downloaded [here](https://github.com/espocrm/ext-sms-providers/releases).

## ext\pdf\generate

`ext\pdf\generate(ENTITY_TYPE, ENTITY_ID, TEMPLATE_ID, [FILENAME])`

Generates PDF file and returns attachment ID. If failed, then returns NULL. TEMPLATE_ID is an ID of PDF template.

Example:

```
$attachmentId = ext\pdf\generate(
    'Lead',
    entity\attribute('id'),
    'pdf-template-id',
    'test.pdf'
);

$emailId = record\create('Email',
    'subject', 'Test PDF',
    'body', 'PDF is attached',
    'to', entity\attribute('emailAddress'),
    'attachmentsIds', list($attachmentId)
);

ext\email\send($emailId);
```

Note, that this won't work for new records in before-create script because a record is not yet created. It will work in Workfows.

## ext\user\sendAccessInfo

`ext\user\sendAccessInfo(USER_ID)`

Send an email with access info to a specific user (via email). A user password will be reset. The user will be promted to specify their 
new password. This function is useful when creating a new user via formula. (as of v7.1)

Example:

```
$userId = record\create(
    'User',
    'userName', $userName,
    'firstName', $firstName,
    'lastName', $lastName,
    'type', 'portal',
    'portalsIds', list($portalId)
);

ext\user\sendAccessInfo($userId);
```
