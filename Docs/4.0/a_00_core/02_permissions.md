[**Current Version:** 4.0](../README.md)

> ### Security Warnings:
> 
> `***`: High risk, must only granted to high trust apps
> 
> `**`: Medium risk, must be granted with care
> 
> `*`: Low risk, most required for user experience

# Permissions

`org.theprotocols.session.permission.*`

### Security

**`.security.accessHiddenInformation`** *

Lets apps to view personal information of the user, including the information hidden from the public. *Limited to self `User` fetch.*

**`.security.generateSessions`** ***

Allows app to generate new sessions without requiring direct user authorization. Can be used to impersonate other apps or escalate permissions. Recommended to keep the permission exclusive to the network default authorization mechanism.