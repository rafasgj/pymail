pymail
======

This is a mass email sender with nearly no features, designed for fast and easy
use, mainly tested agaist Google's GMail SMTP.

## Usage

```
usage: pymail [-h] [-v] [--dump] [-C CONFIGURATION] [--subject SUBJECT] [-d]
              [-c NUM] [-t MINS]
              [emails] [message]
```

> Note: Although email can be sent in daemon mode, it is not yet fully
implemented. Use it at your own risk.

pymail can be executing by providing the path of twe files. The first one is a
CSV file with contacts, where the first column is the contact name, and the
second column the contact email. The other file is a template message body.

To configure the message *Subject*, the argument `--subject` must be used. If
no subject is set, the messages are sent without this header (and is prone to
be identified as **spam**).

## Configuration

Configuration is read from the file *.config*, but another file can be provided
using the `--configuration` option.

To create the default configuration files (the config file, the contact list,
and the message file), run pymail with the `--dump` option, and three example
files will be created in the current directory. The configuration file created
has the default setting applied if no configuration is found.

The configuration file uses a JSON format.

```json
{
    "server": "smtp.example.com",
    "port": 465,
    "magic_number": 20,
    "sleep": 60,
    "sender": "No One <noone@example.com",
    "username": "A Gmail User Name",
    "password": "The username plain text password.",
    "template": "From: {sender}\nTo: {recipient}>\nSubject: {subject}\n\n{body}"
}
```

The available configuration options are:

* server: The SMTP server address.
* port: The (optional) SMTP server port (defaults to 465).
* magic_number: is te number of contacts to use as recipients for each message.
* sleep: The time to sleep between each message.
* sender: The email of the sender.
* username: The SMTP server username.
* password: The SMTP server password, in plain text.
* template: A message template.

## Message Template

The Message Template can use some special fields enclosed in brackets "{}",
which will be replaced by some text.

* {recipient}: The list of emails that will receive the message.
* {subject}: The email subject as defined by `--subject`
* {body}: The message body defined by the provided file.
* {*Any configuration item*}: The value of the item. It means, you can create
items in the configuration that can be used in the message template.
