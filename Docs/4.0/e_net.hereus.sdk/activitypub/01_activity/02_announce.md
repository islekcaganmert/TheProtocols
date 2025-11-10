[Back](../README.md)

# Announcing an Activity

### `net.hereus.sdk.activitypub.activity.announce(string objectId, to string, cc list) -> null`

Announces an activity, aka. boosting or reposting.

### Parameters:

**`objectId` string:** ID of the object getting announced. Must be a full URL.

**`to` string:** Used by both sender network and receiver instance to route the `Announce` activity to the target. If `"Followers"`, `Announce` activity will be sent to all followers. If `"Public"`, `Announce` activity will be sent to all followers and be publicly available.

**`cc` list:** List of other targets (as strings) to receive the `Announce` activity, e.g. mentions.

### `net.hereus.sdk.activitypub.activity.undoAnnounce(string objectId) -> null`

Undoes the announce.