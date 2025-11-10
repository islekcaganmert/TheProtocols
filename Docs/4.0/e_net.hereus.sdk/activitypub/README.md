[Back](../README.md)

# HereUS SDK ActivityPub

### `net.hereus.sdk.activitypub.*`

Provides ActivityPub functionality to serverless applications without requiring a separate account per service. Introduces extra keys over ActivityPub standards to ensure intended functionality met for apps that are not social networking systems.

### Procedures:

- `..activity.`
    - [`..create`](01_activity/01_create.md)
    - [`..announce` & `..undoAnnounce`](01_activity/02_announce.md)
    - [`..delete`](01_activity/03_delete.md)
    - [`..get`](01_activity/04_get.md)
    - [`..list`](01_activity/05_list.md)
    - [`..like` & `..unlike`](01_activity/06_like.md)
    - [`..edit`](01_activity/07_edit.md)
- `..actor.`
    - [`..follow` & `..unfollow`](02_actor/01_follow.md)
    - [`..get`](02_actor/02_actor_get.md)
    - [`..listFollowers`](02_actor/03_listfollowers.md)
    - [`..listFollowing`](02_actor/04_listfollowing.md)