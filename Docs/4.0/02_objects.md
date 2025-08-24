[**Current Version:** 4.0](README.md)

# Objects

### Contact

Extensible object to keep extra data about a person.

Addition to the `relation` and `links`, the key-value pairs available in a standard user ID can be added.
Client may either prefer remote user or what set on contact.

```json
{
  "@context": "https://theprotocols.org/ns/4.0/Contact.jsonld",
  "@id": "theprotocols://{username}@{network}/contact/{contact_username}@{contact_network}",
  "displayName": "", // If empty, clients must create user name from name
  "links": [ // collection of all URLs that are profiles
    "https://community.example.com/~username",
    "https://social.example.com/@username"
  ],
  ...
}
```

### Reminder

```json
{
  "@context": "https://theprotocols.org/ns/4.0/Reminder.jsonld",
  "@id": "theprotocols://{username}@{network}/reminder/{list}/{title}",
  "deadline": "YYYY-MM-DD HH:mm",
  "lastUpdateStatus": "YYYY-MM-DD HH:mm", // the most recent time the reminder toggled.
  "repeat": {"value": 0, "unit": "minutes"}, // repeat interval
  "status": true,
  "subs": [], // sub-reminder collection
  "title": "Demo Task"
}
```

### Sub-Reminder

```json
{
  "@context": "https://theprotocols.org/ns/4.0/SubReminder.jsonld",
  "@id": "theprotocols://{username}@{network}/reminder/{list}/{title}/{sub_reminder_title}",
  "deadline": "YYYY-MM-DD HH:mm",
  "last_update_status": "YYYY-MM-DD HH:mm",
  "status": true,
  "title": "Demo Task"
}
```

### Mail

`body` must be an HTML document.

`sender` must be the address of sender.

`to` and `cc` are collection of related addresses.

```json
{
  "@context": "https://theprotocols.org/ns/4.0/Mail.jsonld",
  "@id": "theprotocols://{username}@{network}/mail/{mailbox}/{id}",
  "subject": "",
  "date_received": "YYYY-MM-DD HH:mm",
  "sender": "",
  "to": [],
  "cc": [],
  "body": ""
}
```

### Event

`country` must be two letter country code.

```json
{
  "@context": "https://theprotocols.org/ns/4.0/Event.jsonld",
  "@id": "theprotocols://{username}@{network}/event/YYYY-MM-DD/HH:mm/{index}",
  "name": "",
  "starts": "YYYY-MM-DD HH:mm",
  "ends": "YYYY-MM-DD HH:mm",
  "location": {
    "name": "",
    "line1": "",
    "line2": "",
    "city": "",
    "state": "", // ... or province
    "country": "" // two-letter country code
  }
  "alerts": [
    {"value": 1, "unit": "minutes"},
    {"value": 1, "unit": "hours"},
    {"value": 1, "unit": "days"},
    {"value": 1, "unit": "weeks"},
    {"value": 1, "unit": "months"},
    {"value": 1, "unit": "years"}
  ],
  "repeat": {"value": 0, "unit": "minutes"},
  "travel_time": 0, // in minutes
  "participants": [], // Collection of user addresses
  "notes": "Markdown", // Simple Markdown document
  "url": "https://example.com/about/event/index.html",
  "attachments": [
    "https://example.com/about/event/photo.png"
  ]
}
```

### User

```json
{
  "@context": "https://theprotocols.org/ns/4.0/User.jsonld",
  "@id": "theprotocols://{username}@{network}",
  "profilePhoto": "", // URL for profile photo
  "firstName": "", // First Name (Given Name)
  "middleName": "", // Middle Name
  "lastName": "", // Last Name (Family Name, Surname)
  "nameSuffix": "", // Name Suffix, only legal (e.g. Sr., Jr., I, II, III, ...)
  "birthdate": "", // Birth date in `YYYY-MM-DD` format
  "country": "", // 2-letter Country Code
  "gender": "", // Gender ("Male" or "Female")
  "phoneNumber": "", // Phone Number, `"+00000000000"` format
  "timezone": "", // IANA Timezone String, e.g. America/Los_Angeles
  "description": "", // for public profile, like bio on social media
  "rsaPublicKey": "", // RSA Public Key (Compatibility & ActivityPub only!)
  "signatureId": "", // PQC Dilithium Mode 2 Public Key, base64 encoding
  "encryptionId": "", // PQC Kyber512 Public Key, base64 encoding
}
```

### App

```JSON
{
  "@context": "https://theprotocols.org/ns/4.0/App.jsonld",
  "@id": "https://app.example.com/.well-known/app-info.json",
  "name": "",
  "icon": "",
  "description": "",
  "latestVersion": "",
  "latestBuildNumber": 0,
  "defaultPreferences": {
    "Sub1.Switch": true,
    "Sub1.Textbox": "",
    "Sub2.Slider": 50,
    "Sub2.Select": {"selected": "Default", "all": ["Default", "Light", "Dark"]}
  },
  "initialPermissions": []
}
```

> `preferences` contains default preferences of the application.

> `initialPermissions` include all permissions that must be granted initially to the apps during authorization. Check [list of permissions](02_01_permissions.md).
