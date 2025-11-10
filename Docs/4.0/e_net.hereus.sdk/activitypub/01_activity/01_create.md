[Back](../README.md)

# Creating an Activity

### `net.hereus.sdk.activitypub.activity.create(string summary, string contentWarning, string inReplyTo, string to, list cc, list attachments, map properties, string url) -> string`

Creates a new object with arguments given and publishes a `Create` activity.

### Parameters:

**`summary` string:** Text that summarizes the activity. Microblogging software will use this text to visualize it on the feeds.

**`contentWarning` string:** If empty, gets ignored; otherwise, enables `sensitive` bool in the `Note` object and provides the warning text.

**`inReplyTo` string:** Marks the `Note` object as a reply to another.

**`to` string:** Used by both sender network and receiver instance to route the `Note` object to the target. If `"Followers"`, `Note` object will be sent to all followers. If `"Public"`, `Note` object will be sent to all followers and be publicly available.

**`cc` list:** List of other targets (as strings) to receive the `Note` object, e.g. mentions.

**`attachments` list:** URL list of attachments, preferably an attachment uploaded to network via TheProtocols or an IPFS URI.

**`properties` map:** key-value paired data for programmed consumption of the activity.

**`url` string:** URL that "Open in remote instance" will open. If empty, will default to network's social provider, e.g. HereUS Social for HereUS.

### Return Value:

Returns ID of the `Note` object created.