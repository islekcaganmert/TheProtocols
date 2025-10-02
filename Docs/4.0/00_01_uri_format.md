[**Current Version:** 4.0](README.md)

# TheProtocols URI format

| Name         | URL                                                                                |
|--------------|------------------------------------------------------------------------------------|
| User         | `theprotocols://{username}@{network}`                                              |
| User         | `theprotocols://{username}@{network}/contact/{contact_username}@{contact_network}` |
| Mailbox      | `theprotocols://{username}@{network}/mail/{mailbox}`                               |
| Mail         | `theprotocols://{username}@{network}/mail/{mailbox}/{id}`                          |
| Chat         | `theprotocols://{username}@{network}/chat/{id}`                                    |
| Note         | `theprotocols://{username}@{network}/note/{path}`                                  |
| Reminder     | `theprotocols://{username}@{network}/reminder/{list}/{title}`                      |
| Sub-Reminder | `theprotocols://{username}@{network}/reminder/{list}/{title}/{sub_reminder_title}` |
| IoT House    | `theprotocols://{username}@{network}/iot/{house}`                                  |
| IoT Room     | `theprotocols://{username}@{network}/iot/{house}/{room}`                           |
| IoT Device   | `theprotocols://{username}@{network}/iot/{house}/{room}/{device}`                  |
| File         | `theprotocols://{username}@{network}/file/{path}`                                  |
| Event        | `theprotocols://{username}@{network}/event/YYYY-MM-DD/HH:mm/{index}`               |
| Event        | `theprotocols://{network}/network/about`                                           |

Networks are encouraged to support HTTPS URL formats below but clients must not rely on existence of this paths.

| Name         | URL                                                                              |
|--------------|----------------------------------------------------------------------------------|
| User         | `https://{network}/~{username}`                                                  |
| Note         | `https://{network}/~{username}/note/{path}.html`                                 |
| Reminder     | `https://{network}/~{username}/reminder/{list}/{title}.ics`                      |
| Sub-Reminder | `https://{network}/~{username}/reminder/{list}/{title}/{sub_reminder_title}.ics` |
| File         | `https://{network}/~{username}/file/{path}`                                      |
| Event        | `https://{network}/~{username}/event/YYYY-MM-DD/HH:mm/{index}.ics`               |
