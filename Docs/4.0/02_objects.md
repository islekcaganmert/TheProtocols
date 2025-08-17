[**Current Version:** 4.0](README.md)

# Objects

### Contact

Extensible object to keep extra data about a person.

`links` are a collection of all URLs that are profiles for the contact.

Addition to the `relation` and `links`, the key-value pairs available in a standard user ID can be added.
Client may either overwrite user declarations or prefer value set on interface.

If the value for `display_name` is empty, clients must create user name from name.

```json
{
  "@context": "https://theprotocols.org/ns/Contact.jsonld",
  "@id": "theprotocols://{username}@{network}/contact/{contact_username}@{contact_network}",
  "display_name": "",
  "links": [
    "https://community.example.com/~username",
    "https://social.example.com/@username"
  ],
  ...
}
```

### Reminder

`last_update_status` is the most recent time the reminder toggled.

`subs` is a list of sub-reminder object.

`repeat` must be the repeat interval in minutes.

```json
{
  "@context": "https://theprotocols.org/ns/Reminder.jsonld",
  "@id": "theprotocols://{username}@{network}/reminder/{list}/{title}",
  "deadline": "YYYY-MM-DD HH:mm",
  "last_update_status": "YYYY-MM-DD HH:mm",
  "repeat": {"value": 0, "unit": "minutes"},
  "status": true,
  "subs": [],
  "title": "Demo Task"
}
```

### Sub-Reminder

```json
{
  "@context": "https://theprotocols.org/ns/SubReminder.jsonld",
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
  "@context": "https://theprotocols.org/ns/Mail.jsonld",
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

`travel_time` must be given in minutes.

`repeat` must be an interval object.

`participants` is a collection of user addresses.

`notes` must be a simple Markdown document.

```json
{
  "@context": "https://theprotocols.org/ns/Event.jsonld",
  "@id": "theprotocols://{username}@{network}/event/YYYY-MM-DD/HH:mm/{index}",
  "name": "",
  "starts": "YYYY-MM-DD HH:mm",
  "ends": "YYYY-MM-DD HH:mm",
  "location": {
    "name": "",
    "street": 0,
    "no": 0,
    "zipcode": "00000",
    "country": "XX"
  },
  "alerts": [
    {"value": 1, "unit": "minutes"},
    {"value": 1, "unit": "hours"},
    {"value": 1, "unit": "days"},
    {"value": 1, "unit": "weeks"},
    {"value": 1, "unit": "months"},
    {"value": 1, "unit": "years"}
  ],
  "repeat": {"value": 0, "unit": "minutes"},
  "travel_time": 0,
  "participants": [],
  "notes": "Markdown",
  "url": "https://example.com/about/event/index.html",
  "attachments": [
    "https://example.com/about/event/photo.png"
  ]
}
```