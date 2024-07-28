# TheProtocols Docs

**Current Version:** 3.1

**Test Suite:** *Not available yet*

**Implementation report:** *Not available yet*

**Author:** Cagan Mert ISLEK

#### Contributors:
- Cagan Mert ISLEK

<br>

### Abstract

**TheProtocols** is a federated protocol for decentralizing super apps by letting people choose a network and a client they want.
TheProtocols is designed to provide most functionality a standard user needs in a daily life.

### State of This Document

This section describes the status of this document at the time of its publication.
Other documents may supersede this document.

All interested parties are invited to provide implementation and bug reports and other comments through email, TheProtocols, X, fediverse, or issue tracker.
These will be considered in any future versions of this specification.

### TheProtocols URL format

This format is used in Resource Pointer object from below.

| Name      | URL                                             |
|-----------|-------------------------------------------------|
| User      | `theprotocols://{username}@{network}`           |
| Mail      | `theprotocols://mail:{mailbox}/{id}`            |
| Chat      | `theprotocols://chat:{id}`                      |
| Note      | `theprotocols://note:{path}`                    |
| Reminder  | `theprotocols://reminder:{list}/{title}`        |
| IoT       | `theprotocols://iot:{house}/{room}/{device}`    |
| File      | `theprotocols://file:{path}`                    |
| Event     | `theprotocols://event:YYYY-MM-DD/HH:mm/{index}` |
| Feed Post | `theprotocols://feed:{id}`                      |

> `theprotocols://` part is not necessary but recommended to avoid TheProtocols cause conflicts with other protocols.

### Objects
<table>

<!--Resource Pointer-->
<tr>
<td>

**Resource Pointer**

Used for pointing to any resource on web.

</td>
<td>

```json
{
  "title": "Example",
  "url": "https://example.com/index.html",
  "description": "Lorem ipsum dolor sit amet"
}
```

</td>
</tr>

<!--Feed Post-->
<tr>
<td>

**Feed Post**

A post listed in feed.<br>
`content` is in HTML format and an optional key if this object is in list.<br>
`id` must follow FAT32 filename limitation except space is not allowed.<br>


</td>
<td>

```json
{
  "title": "Post Title",
  "datetime": "YYYY-MM-DD HH:mm",
  "id": "post01",
  "content": "HTML"
}
```

</td>
</tr>

<!--Contact-->
<tr>
<td>

**Contact**

Extensible object to keep extra data about a person.<br>
Addition to the `Relation` and `Socials`, the key-value pairs available in a standard user ID can be added to replace hidden ones.<br>
Value of `Relation` must be `"Self"` if the contact is the current user and empty string if relation is not unique.

</td>
<td>

```json
{
  "Relation": "",
  "Socials": [
    "https://example.com/@username"
  ]
}
```

</td>
</tr>

<!--Reminder-->
<tr>
<td>

**Reminder**

Standard reminder object.<br>
`deadline` and `last_update_status` must be in "YYYY-MM-DD HH:mm" format.<br>
`last_update_status` is the most recent time the reminder toggled.<br>
`subs` is a list of sub-reminder object.
`repeat` must be an interval object.


</td>
<td>

```json
{
  "deadline": "",
  "last_update_status": "2024-01-24 11:28",
  "repeat": "",
  "status": true,
  "subs": [],
  "title": "Demo Task"
}
```

</td>
</tr>

<!--Sub-Reminder-->
<tr>
<td>

**Sub-Reminder**

Sub-reminder object.<br>
`deadline` must be in "YYYY-MM-DD HH:mm" format.


</td>
<td>

```json
{
  "deadline": "",
  "status": true,
  "title": "Demo Task"
}
```

</td>
</tr>

<!--Chat-->
<tr>
<td>

**Chat**

Two form object to keep information about two party and multiple party chats.<br>
Two party chats only have `last_index` key, other keys are only for multiple party chats.<br>
`image` must be an URL.<br>
`participants` is a list of TheProtocols addresses of participants.


</td>
<td>

```json
{
    "last_index": 0,
    "image": "",
    "title": "",
    "participants": []
}
```

</td>
</tr>

<!--Message-->
<tr>
<td>

**Message**

An object to keep information about a message.<br>
`date_received` must be in `YYYY-MM-DD HH:mm` format.<br>
`body` must be in Markdown format.

</td>
<td>

```json
{
  "from": "",
  "body": "",
  "date_received": ""
}
```

</td>
</tr>

<!--Mail-->
<tr>
<td>

**Mail**

An object to keep information about a mail.<br>
`date_received` must be in `YYYY-MM-DD HH:mm` format.<br>
`body` must be in HTML format.<br>
`sender` must be the address of sender.<br>
`to` and `cc` must be lists of addresses stringified with `;` as deliminator.<br>
`hashtag` must only contain lowercase, uppercase, and numbers.

</td>
<td>

```json
{
  "subject": "",
  "date_received": "",
  "sender": "",
  "to": "",
  "cc": "",
  "hashtag": "",
  "body": ""
}
```

</td>
</tr>

<!--Deleted-->
<tr>
<td>

**Deleted**

Used to inform network to delete a remote object.

</td>
<td>

```html
</deleted>
```

</td>
</tr>

</table>

### Network Information

To learn about a network, an **HTTPS POST** request to `/protocols/version` is used.

Server must not expect any data to be in body for this request.

Example Response Client Must Expect:

<table>
<tr>
<td>

```json
{
  "help": "",
  "os": {
    "arch": "",
    "family": "",
    "name": "",
    "version": ""
  },
  "rules": {
    "new_accounts_allowed": true
  },
  "software": {
    "build": 1,
    "channel": "",
    "developer": "",
    "name": "",
    "source": "",
    "version": ""
  },
  "membership_plans": [
    {
      "name": "Free",
      "storage": 0,
    },
    {
      "name": "Plus",
      "storage": 0,
    },
    {
      "name": "Pro",
      "storage": 0,
    },
    {
      "name": "Ultra",
      "storage": 0,
    }
  ],
  "users": [],
  "version": "3.1"
}
```

</td>
<td style="font-size:0.8em;">

String: Username of the account users must contact for help<br>
Dictionary: Information about OS of the server of the network<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String: Architecture of OS *(look below)*<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String: OS Family<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String: OS Name<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String: OS Version<br><br>
Dictionary: Rule configuration of the network<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bool: If network accepts new users to create account using TheProtocols<br><br>
Dictionary: Information about the server software<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Integer: Build number of the server software<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String: Release channel of the server software *(look below)*<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String: TheProtocols address of the developer<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String: Name of the server software<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String: `"Closed"` or URL of the repository of the server software<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String: Version of the server software<br><br>
Dictionary: Membership Plans<br><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String: Name of free plan<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Integer: Storage for free plan in bytes<br><br><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String: Name of paid plan #1<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Integer: Storage for paid plan #1 in bytes<br><br><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String: Name of paid plan #2<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Integer: Storage for paid plan #2 in bytes<br><br><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String: Name of paid plan #3<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Integer: Storage for paid plan #3 in bytes<br><br><br>
List: List of usernames of the users<br>
String: TheProtocol version server configured

</td>
</tr>
</table>

> Architecture of OS must be in official format like: x86, x86_64, AArch64

### Account Creation & Terms of Service

To create an account on a network these steps must be followed in the order:

1. **HTTPS POST** request to `/protocols/terms_of_service` to view Terms of Service of the network in HTML format. Account creation will assume you accepted.
2. **HTTPS POST** request to `/protocols/signup` with a JSON with these keys:

<table>
<tr>
<td>

```json
{
    "birthday": "YYYY-MM-DD",
    "country": "US",
    "gender": "Male",
    "name": "Given Name",
    "password": "Raw Password",
    "phone_number": "+1 000 000 0000",
    "postcode": "54050",
    "timezone": -8,
    "surname": "FAMILY",
    "username": "username"
}
```

</td>
<td style="font-size:0.8em;">

String: Birthday in `YYYY-MM-DD` format<br>
String: 2-letter Country Code<br>
String: Gender *(look below)*<br>
String: Given Name<br>
String: Raw Password of User<br>
String: Phone Number, "+1 000 000 0000" format without spaces<br>
String: Postcode of the user<br>
Integer: Difference of Timezone of User to UTC (ex. -8 is "UTC-08:00")<br>
String: Surname in all uppercase<br>
String: Username with only using ASCII lowercase and `-` symbol<br>

</td>
</tr>
</table>

> Standard `gender` values are Male, Female, Lesbian, Gay, Bisexual, Transgender, Queer, Intersexual, Asexual, and Pansexual.
> Clients and servers must code to support others before reporting the problem to me via [email](mailto:islekcaganmert@hereus.net), [GitHub](https://github.com/islekcaganmert/TheProtocols), or [HereUS](https://www.hereus.net/user/islekcaganmert@hereus.net).
> Clients are designed to assume there is no other possible value and unsupported values can cause problems.

> `+` symbol can also be used in usernames as alternative accounts of the main account.
> For instance, user@example.com can use user+untrustedapp@example.com for privacy and prevent spam if the server software supports as TheProtocols specification highly recommends.

Client must not expect anything except a status code to learn about is the server was able to create the account.

### Using the Account

After creating an account, next step is logging into it. There is two option for that:

**Using Credentials to get a Token:**
To get a token using credentials, an **HTTPS POST** request to `/protocols/login` is used.

Example JSON to generate signature from:

```JSON
{
  "package": "",
  "permissions": [
    ...
  ]
}
```

> `permissions` must be sorted to alphabetical order.

> TheProtocols strongly recommends signature to be signed remotely or treated as an application token.
> It is not recommended to distribute RSA private key.

Example Body Server Must Expect:
```JSON
{
  "username": "Username",
  "password": "Password",
  "package": "com.example.app",
  "signature": "...",
  "permissions": [
    "RSA",  // view private RSA key and work with tokens
    "HiddenInformation",  // see information hidden from public
    "Search",  // search objects and index
    "Feed",  // view feed and read posts
    "Contacts",  // list and view contacts
    "ContactsWrite",  // add, modify, and delete contacts
    "Reminders",  // view reminders and lists
    "RemindersWrite",  // add, modify, and delete reminders and lists
    "Chat",  // send and receive messages
    "Mail",  // list, view, move, trash, delete mails
    "MailSend",  // send mails
    "Notes",  // view notes
    "NotesWrite",  // create, edit, and delete notes
    "IoT",  // view states of IoT devices
    "IoT-Full",  // full control on IoT connections
    "ReadFile",  // view filesystem, read files
    "WriteFile",  // write files, create folders, delete any
    "Calendar",  // view calendar
    "Events",  // create, edit, and delete events on calendar
    "ModifyID",  // make modifications on ID
    "InterApp"  // read data and preferences of all apps
  ]
}
```

> `current_user_username` must be the username of the user and `current_user_password` must be the password of the user.

> Clients using this method shouldn't expect server to respect all permissions.
> Server softwares can let users disable some of the permissions.

Example Response Client Must Expect:

```JSON
{
  "token": ""
}
```

**Using Credentials with Every Request:**
For compatibility reasons, old method to login (`current_user_username` and `current_user_password` with all requests) will stay until 4.0 release.

**Continue with no account:**
You can use some endpoints without account; however experience can be less personalized.
To use the Guest account, do not send "cred" argument which means for endpoints to send blank JSON.

### Identity of The Current User

To get identity (including personal information and hidden information) of the current user,
an **HTTPS POST** request to `/protocols/current_user_info` is used.

Example Body Server Must Expect:
```json
{
  "cred": "token"
}
```

Example Response Client Must Expect:

<table>
<tr>
<td>

```json
{
  "birthday": "",
  "rsa_private_key": "",
  "rsa_public_key": "",
  "country": "",
  "gender": "",
  "name": "",
  "phone_number": "",
  "plus": false,
  "postcode": "00000",
  "profile_photo": "",
  "settings": {
    "apps": [],
    "plus_until": 20321108,
    "theme_color": "blue"
  },
  "social": {
    "biography": "",
    "emoji": "",
    "story": {
      "content": "",
      "datetime": 202401011200
    }
  },
  "surname": "SURNAME",
  "timezone": -8
}
```

</td>
<td style="font-size:0.8em;">


String: Birthday in `YYYY-MM-DD` format<br>
String: RSA Private Key<br>
String: RSA Public Key<br>
String: 2-letter Country Code<br>
String: Gender *(look below)*<br>
String: Given Name<br>
String: Phone Number, "+1 000 000 0000" format without spaces<br>
Integer: `0` is free plan, `1` is plus, `2` is pro, and `3` is ultra<br>
String: Postcode of the user<br>
String: URL of the profile photo of the user<br>
Dictionary: Settings of user which not owned by an app<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;List: List of package names keeping data in library of user<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Integer: When membership of the user ends in YYYYMMDD format<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String: Theme color preference of user<br><br>
Dictionary: Required keys to create a complete social media profile<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String: Social media biography with `<newline>` as line breaker<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String: Emoji to show next to the username<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dictionary: Story data for social media<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String: HTML Content of Story<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Integer: When story updated in YYYYMMDDHHmm format<br><br><br>
String: Surname in all uppercase.<br>
Integer: Difference of Timezone of User to UTC (ex. -8 is "UTC-08:00")<br>


</td>
</tr>
</table>

> Standard `theme_color` values are red, orange, yellow, green, blue, pink, purple, and blank.
> blank value means for client to not color the UI.

> Standard `gender` values are Male, Female, Lesbian, Gay, Bisexual, Transgender, Queer, Intersexual, Asexual, and Pansexual.
> Clients and servers must code to support others before reporting the problem to me via [email](mailto:islekcaganmert@hereus.net), [GitHub](https://github.com/islekcaganmert/TheProtocols), or [HereUS](https://www.hereus.net/user/islekcaganmert@hereus.net).
> Clients are designed to assume there is no other possible value and unsupported values can cause problems.

> If a server software implementor wants to create a feature like email aliases with privacy feature, the server must hide the data while respecting the standards above.
> For instance, while user_info can hide timezone by replacing with `"**"` but current_user_info can only hide by replacing with `0` or other standard compatible placeholder.

> Servers can modify count of memberships (`plus key`) available up to 4.
> That means servers can disable 1, 2, 3, 1 & 2, 1 & 3, 2 & 3, or all.
> The reason why TheProtocols has standard of memberships is these memberships are considered as TheProtocols Network membership by clients and names must be generated from an integer.

> `social` key can be removed to disable social media integrations.
> But if server sends this key included, value must follow the standard.

### User ID Modifications

To modify a value in user id, **HTTPS POST** request to `/protocols/set_user_data` is used.

> Networks can be configured to set immutable some of the keys. Client must not expect success everytime.

Example Body Server Must Expect:

```json
{
  "cred": "token",
  "key": "",
  "data": ""
}
```

> `key` must be in file path format.
> If the value placed directly in the root, `key` must be the key directly.

Client must not expect anything except a status code to learn about is the server was able to save.

### Search

To search for an object or a website from index of server, an **HTTPS POST** request to `/protocols/search` is used.

Example Body Server Must Expect:

```json
{
  "cred": "token",
  "key": ""
}
```

> `key` is the query string. Network will return every object matching with the key.

Response will be a JSON with a single key value pair.
Key is `results` and contains a list of resource pointer objects matching with the query.

### Feed

TheProtocols allows networks to serve a feed. To get the feed, an **HTTPS POST** request to `/protocols/get_feed` is used.

Example Body Server Must Expect:

```json
{
  "cred": "token",
}
```

Response will be a JSON with a single key value pair.
Key is `feed` and contains a list of feed post objects matching with the query.

To get a feed post, an **HTTPS POST** request to `/protocols/get_feed_post` is used.

Example Body Server Must Expect:

```json
{
  "cred": "token",
  "id": ""
}
```

> `id` must be the id of the post.

Response will be a feed post object.

### Cloud Storage Status

To check status of cloud storage allocated for the user, an **HTTPS POST** request to `/protocols/storage_status` is used.

Example Body Server Must Expect:

```json
{
  "cred": "token"
}
```

Example Response Client Must Expect:

```json
{
  "total": 0,
  "used": {}
}
```

> `used` can contain unlimited number of key value pairs to address what uses how much space.
> Values must be size in byte as integer. Recommended keys to have in `used` dictionary are size of user id as `id`, size of folder contains application data as `library_data`, size of folder contains mails as `mails`, size of folder contains notes as `notes`, size of folder contains reminders as `reminders`, and size of folder contains cold wallet as `token`.

> `total` is total space allocated for the user in byte as integer.

### Notes

To pull all notes from the network, an **HTTPS POST** request to `/protocols/pull_notes` is used.

Example Body Server Must Expect:

```json
{
  "cred": "token"
}
```

Response client must expect is a plain JSON.
If the value of a key is dictionary, the pair is a folder.
If the value of a key is string, the pair is a note.
For instance, if there notes folder of a user is `/Users/user/Notes`, and user has a note in `/Users/user/Notes/path/to/note.html`, response should be

```json
{
  "path": {
    "to": {
      "note": "<p>Hello, World!</p>"
    }
  }
}
```

To edit a note, an **HTTPS POST** request to `/protocols/edit_note` is used.

Example Body Server Must Expect:

```json
{
  "cred": "token",
  "path": "",
  "value": ""
}
```

> `path` must be the path of the note to edit.

> `value` must be text in HTML format.

Client must not expect anything except a status code to learn about is the server was able to save.

To delete a note, send deleted object as the new value of the note.

### Reminders

To pull reminders from the network, an **HTTPS POST** request to `/protocols/get_reminders` is used.

Example Body Server Must Expect:

```json
{
  "cred": "token"
}
```

Response client must expect is JSON key value pairs, task list titles as keys and lists of reminder objects as values.

To toggle a reminder, reversing `status` value, an **HTTPS POST** request to `/protocols/toggle_reminder` is used.

Example Body Server Must Expect:

```json
{
  "cred": "token",
  "list": "",
  "id": 0
}
```

> `list` must be the name of the list.

> `id` must be the index of the reminder in the list.
> Note that `id` is not unique and can change, best to pull reminders before editing, toggling, deleting a reminder.

Client must not expect anything except a status code to learn about is the server was able to save.

To edit a reminder, an **HTTPS POST** request to `/protocols/edit_reminder` is used.

Example Body Server Must Expect:

```json
{
  "cred": "token",
  "list": "",
  "id": 0,
  "data": ""
}
```

> `data` must be a reminder object that dumped to JSON.

Client must not expect anything except a status code to learn about is the server was able to save.

To delete a reminder, an **HTTPS POST** request to `/protocols/delete_reminder` is used.

Example Body Server Must Expect:

```json
{
  "cred": "token",
  "list": "",
  "id": 0
}
```

Client must not expect anything except a status code to learn about is the server was able to delete.

To create a new list, an **HTTPS POST** request to `/protocols/create_reminder_list` is used.

Example Body Server Must Expect:

```json
{
  "cred": "token",
  "list": ""
}
```

> Value of `list` must follow FAT32 filename limitations.

Client must not expect anything except a status code to learn about is the server was able to create.

To create a new reminder, an **HTTPS POST** request to `/protocols/create_reminder` is used.

Example Body Server Must Expect:

```json
{
  "cred": "token",
  "list": "",
  "title": "",
  "deadline": "",
  "repeat": ""
}
```

> Value of `title` must be string.
> `deadline` must be in "YYYY-MM-DD HH:mm" format.
> 'repeat` must be an interval object.

Client must not expect anything except a status code to learn about is the server was able to create.

To create a new sub-reminder, an **HTTPS POST** request to `/protocols/create_sub_reminder` is used.

Example Body Server Must Expect:

```json
{
  "cred": "token",
  "list": "",
  "reminder": "",
  "title": "",
  "deadline": ""
}
```

> Value of `title` must be string.
> `deadline` must be in "YYYY-MM-DD HH:mm" format.

Client must not expect anything except a status code to learn about is the server was able to create.

### Tokens

> While interacting with tokens, requests must be done to a relay in the token's network which supports TheProtocols.

To learn about a token, an **HTTPS POST** request to `/protocols/token/about` is used.

Server must not expect any data to be in body for this request.

Example Response Client Must Except:

<table>
<tr>
<td>

```json
{
  "exchange": 1,
  "name": "",
  "network": "",
  "os": {
    "arch":"",
    "family":"",
    "name":"",
    "version":""
  },
  "software": {
    "build": 0,
    "channel": "",
    "developer": "",
    "name": "",
    "source": "",
    "version": ""
  },
  "version":"3.1"
}
```

</td>
<td style="font-size:0.8em">

Float: Exchange Rate Recommended by The Server Software<br>
String: Token Name<br>
String: Network of the token *(not all clients to support all networks)*<br>
Dictionary: Server OS Information<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String: Architecture of OS *(in official format)*<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String: OS Family<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String: OS Name<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String: OS Version<br><br>
Dictionary: Server Software Information<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Integer: Build number of the server software<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String: Release channel of the server software (look below)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String: TheProtocols address of the developer<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String: Name of the server software<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String: `"Closed"` or URL of the repository of the server software<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String: Version of the server software<br><br>
String: TheProtocols Version<br>

</td>
</tr>
</table>

To check balance of a public key, an **HTTPS POST** request to `/protocols/token/balance` is used.

Example Body Server Must Expect:

```json
{
  "address": ""
}
```

> Value of `address` must be compatible with the target network.

Client must expect a number as plain/text.

To transfer token, an **HTTPS POST** request to `/protocols/token/transfer` is used.

Example Body Server Must Expect:

```json
{
  "address": "address1",
  "signature": "",
  "transactions": [
    {"from": "address1", "to": "address2", "amount": 0.05},
    {"from": "address1", "to": "address3", "amount": 0.01}
  ]
}
```

> Value of `address`, `from`s, and `to`s must be compatible with the target network. `from`s must be same as `address`

> Value of `receiver` must be the ChamyChain Public Key of receiver.

> Value of `amount`s must be a positive float.

> To generate signature, stringify same JSON without `signature` key in this order of keys and generate signature using the algorithm target network uses.

Client must not expect anything except a status code to learn about is the server was able to transfer.

### Identity of Others in Federalized Web

To get identity (excluding personal information, hidden information is censored) of others in federalized web,
an **HTTPS POST** request to `/protocols/user_info` is used.

> For this time, unlikely to other requests, we must make the request to the network of the person we want to learn about.
> DO SEND NEITHER YOUR TOKEN NOR YOUR CREDENTIALS!

Example Body Server Must Expect:
```json
{
  "username": "Username"
}
```

> `username` must be the username of the person we want to learn about.

Example Response Client Must Expect:

<table>
<tr>
<td>

```json
{
  "birthday": "",
  "rsa_public_key": "",
  "country": "",
  "gender": "",
  "name": "",
  "phone_number": "",
  "plus": false,
  "postcode": "00000",
  "profile_photo": "",
  "social": {
    "biography": "",
    "emoji": "",
    "story": {
      "content": "",
      "datetime": 202401011200
    }
  },
  "surname": "SURNAME",
  "timezone": -8
}
```

</td>
<td style="font-size:0.8em;">


String: Birthday in `YYYY-MM-DD` format<br>
String: RSA Public Key<br>
String: 2-letter Country Code<br>
String: Gender *(look below)*<br>
String: Given Name<br>
String: Phone Number, "+1 000 000 0000" format without spaces<br>
Integer: `0` is free plan, `1` is plus, `2` is pro, and `3` is ultra<br>
String: Postcode of the user<br>
String: URL of the profile photo of the user<br>
Dictionary: Required keys to create a complete social media profile<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String: Social media biography with `<newline>` as line breaker<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String: Emoji to show next to the username<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dictionary: Story data for social media<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String: HTML Content of Story<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Integer: When story updated in YYYYMMDDHHmm format<br><br><br>
String: Surname in all uppercase.<br>
Integer: Difference of Timezone of User to UTC (ex. -8 is "UTC-08:00")<br>


</td>
</tr>
</table>

> If a user wants to hide information or a network configured to not collect the data, value must contain censored version of the data.
> To censor data, replace value with multiple `*` symbol to mimic length of the original value or any value following standard.

> Servers can modify count of memberships (`plus key`) available up to 4.
> That means servers can disable 1, 2, 3, 1 & 2, 1 & 3, 2 & 3, or all.
> The reason why TheProtocols has standard of memberships is these memberships are considered as TheProtocols Network membership by clients and names must be generated from an integer.
> Extraction of membership plan names from Network Info is planned.

> `social` key can be removed to disable social media integrations.
> But if server sends this key included, value must follow the standard.

### Contacts

Since some value can be hidden from public identity, this can block some functionality of clients.
To solve this problem TheProtocols has contacts feature enabling users to fill hidden information of the people they know, changes only visible to them.

To get contacts, an **HTTPS POST** request to `/protocols/list_contacts` is used.

Example Body Server Must Expect:

```json
{
  "cred": "token"
}
```

Response will be the JSON with TheProtocols address of the contact as key and contact object as value.

To add someone as contact, an **HTTPS POST** request to `/protocols/add_contact` is used.

Example Body Server Must Expect:

```json
{
  "cred": "token",
  "email": "username@example.com",
  "relation": "",
  "socials": []
}
```

> Value of `socials` must be list of links of social media accounts of the contact, see contact object for more.

Client must not expect anything except a status code to learn about is the server was able to add.

To edit information of a contact, an **HTTPS POST** request to `/protocols/edit_contact` is used.

Example Body Server Must Expect:

```json
{
  "cred": "token",
  "email": "username@example.com",
  "data": { ... }
}
```

> Value of `data` must be a contact object.

Client must not expect anything except a status code to learn about is the server was able to save.

To delete a contact, `deleted` object must be set to contact data using the same request configuration as editing contact.

### Messages (API)

To list chats and get information about chats, an **HTTPS POST** request to `/protocols/list_chats` is used.

Example Body Server Must Expect:

```json
{
  "cred": "token"
}
```

Response will be dictionaries, chat id as key and chat object as value.

`last_index` is the index of the last message in a chat.
That means a for loop from 0 to `last_index` can be used to get all messages.
To get a message, an **HTTPS POST** request to `/protocols/get_message` is used.

Example Body Server Must Expect:

```json
{
  "cred": "token",
  "chat": "",
  "id": 0
}
```

Response will be a message object.

To send message, an **HTTPS POST** to `/protocols/send_message` is used.

Example Body Server Must Expect:

```json
{
  "cred": "token",
  "chat": "",
  "body": ""
}
```

> `body` must be in Markdown format.

Client must not expect anything except a status code to learn about is the server was able to save.

To create a chat group, send message with `"/"` as `chat` and a new stringified chat object as `body`.

### Messages (Federation)

> This requests must be done between networks.

To send a message to a chat, message must be added to the chat in every user's data in the group because TheProtocols assumes messages people receive are in the disk space allocated to the user and there is not a single pool of messages.
This means if there is two person in a chat from a different network than the current user, even these two are from same network as each, message must be sent to them separately.
Just like sending emails.

To request from a network to add a message to a user's data, an **HTTPS POST** request to `/protocols/lowend/add_message_to_server` of remote network is used.

Example Body Server Must Expect:

```json
{
  "add_to": "",
  "encrypted_object": "",
  "signature": ""
}
```

> Value of `add_to` must be the username of the sender, not address.

> `encrypted_object` is stringified message object encrypted with RSA public key of receiver.
> Padding is MGF1 and with SHA512. Hash algorithm is also SHA512. Label is none.

> `signature` is generated using RSA private key of sender.
> To validate successfully, decrypted object must be tested before JSONified back without any change in sort.
> Padding is MGF1 and with SHA512. Hash algorithm is also SHA512.

> Value of `from` in encrypted object must be the address of sender.

> Value of `chat` in encrypted object must be the ID of the chat.
> If it is two party chat, it must be set same as `from`.

Sender network must only expect a status code to make sure remote received the message.

### Mail (API)

To list mailboxes, an **HTTPS POST** request to `/protocols/list_mailboxes` is used.

Example Body Server Must Expect:

```json
{
  "cred": "token"
}
```

Response will be a dictionary, mailbox name as key and index for most recent mail as value.

> Every network must have these mailboxes available for everyone as standard: Primary, Promotions, Social, Spam, Sent, Archive, Trash.
> Also if a server software has a special process on mails, it can provide more default mailboxes.
> Users can create new mailboxes by moving a mail to a mailbox not exist.
> *Continue reading to learn how to move a mail.*

To get a mail, an **HTTPS POST** request to `/protocols/get_mail` is used.

Example Body Server Must Expect:

```json
{
  "cred": "token",
  "mailbox": "",
  "id": 0
}
```

> `id` is index of mail in the mailbox.

Client must expect a mail object.

To move a mail, an **HTTPS POST** request to `/protocols/move_mail` is used.

Example Body Server Must Expect:

```json
{
  "cred": "token",
  "mailbox": "",
  "mail": 0,
  "move_to": ""
}
```

> `mail` is index of mail in the mailbox.

> This will move the mail from `mailbox` to `move_to`.

Client must not expect anything except a status code to learn about is the server was able to move.

To delete a mail permanently, move it to `-`.

To send a mail, an **HTTPS POST** request to `/protocols/send_mail` is used.

Example Body Server Must Expect:

```json
{
  "cred": "token",
  "body": "",
  "to": "",
  "cc": "",
  "bcc": "",
  "hashtag": "",
  "subject": ""
}
```

> Values must follow same standards as a mail object except values of to and cc must be stringified with ; as deliminator.

Client must only expect a status code to make sure mail sent successfully.

### Mail (Federation)

> This requests must be done between networks, clients have nothing to do.

A mail must be sent to everyone added in `to`, `cc`, and `bcc`.

To request from a network to add a mail to a user's inbox, an **HTTPS POST** request to `/protocols/lowend/add_mail_to_server` of remote network is used.

Example Body Remote Server Must Expect:

```json
{
  "add_to": "",
  "encrypted_object": "",
  "signature": ""
}
```

> Value of `add_to` must be the username of the sender, not address.

> `encrypted_object` is stringified mail object encrypted with RSA public key of receiver.
> Padding is MGF1 and with SHA512. Hash algorithm is also SHA512. Label is none.

> `signature` is generated using RSA private key of sender.
> To validate successfully, decrypted object must be tested before JSONified back without any change in sort.
> Padding is MGF1 and with SHA512. Hash algorithm is also SHA512.

> Value of `from` in encrypted object must be the address of sender.

> Values of `to` and `cc` in encrypted object must be list of receivers.

> Value of `body` in encrypted object must be in HTML format.

> Hashtag must only contain lowercase, uppercase, and numbers.

Sender network must only expect a status code to make sure remote received the mail.

### Application Information

To identify packages, an **HTTPS GET** request to `/.well-known/app_info.json` of domain which is the reverse of package name must be sent.

An example `app_info.json`

```JSON
{
  "name": "",
  "icon": "",
  "description": "",
  "latest_version": "",
  "latest_build_number": 0,
  "preferences": {
    "Switch": true,
    "Textbox": "",
    "Slider": 50,
    "Select": {"selected": "Default", "all": ["Default", "Light", "Dark"]}
  }
}
```

> `preferences` contains default preferences of the application.

### Application Data

To get application data associated with a package name, an **HTTPS POST** request to `/protocols/pull_library_data` is used.

Example Body Server Must Expect:

```json
{
  "cred": "token",
  "app": "com.example.app"
}
```

> Package name sent as the value of `app` key must be in reverse domain format.

Response will be the application data as JSON.
If there is no data associated with the package name, blank JSON (`{}`) will be returned.

To push new data, data must be sent as the value of `data` key accordingly with an **HTTPS POST** request to `/protocols/push_library_data`.

Example Body Server Must Expect:

```json
{
  "cred": "token",
  "app": "com.example.app",
  "data": {}
}
```

Client must not expect anything except a status code to learn about is the server was able to save.

### Application Preferences

To get preferences of an application, an **HTTPS POST** request to `/protocols/pull_app_preferences` is used.

Example Body Server Must Expect:

```json
{
  "cred": "token",
  "app": "com.example.app"
}
```

> Package name sent as the value of `app` key must be in reverse domain format.

Response will be the app preferences as JSON.
If there is no data associated with the package name, blank JSON (`{}`) will be returned.

To push new data, data must be sent as the value of `data` key accordingly with an **HTTPS POST** request to `/protocols/push_app_preferences`.

Example Body Server Must Expect:

```json
{
  "cred": "token",
  "app": "com.example.app",
  "data": {}
}
```

Client must not expect anything except a status code to learn about is the server was able to save.

### Calendar

### IoT

### Drive