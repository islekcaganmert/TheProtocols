[Back](../README.md)

# HereUS SDK ActivityPub

### `net.hereus.sdk.activitypub.*`

Provides ActivityPub functionality to serverless applications without requiring a separate account per service. Introduces extra keys over ActivityPub standards to ensure intended functionality met for apps that are not social networking systems.

### Procedures:

- `..activity.`
    - [`..create`](01_01_activity_create.md)
    - [`..announce` & `..undoAnnounce`](01_02_activity_announce.md)
    - [`..delete`](01_03_activity_delete.md)
    - [`..get`](01_04_activity_get.md)
    - [`..list`](01_05_activity_list.md)
    - [`..like` & `..unlike`](01_06_activity_like.md)
    - [`..edit`](01_07_activity_edit.md)
- `..actor.`
    - [`..follow` & `..unfollow`](02_01_actor_follow.md)
    - [`..get`](02_02_actor_get.md)
    - [`..listFollowers`](02_03_actor_listfollowers.md)
    - [`..listFollowing`](02_04_actor_listfollowing.md)