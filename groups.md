# Groups

<!-- tabs:start -->

#### ** Python **

There are several methods in Python SDK to access the group data (available in ``bot.groups`` subclass):

- **create_group** - create group, first parameter is ``title`` - title of group, second parameter is ``username``, third parameter ``users`` user's outpeer array;
- **find_group_by_shortname** - returns ``Group`` object of group by shortname;

Examples:

```python
bot.groups.create_group('title', 'shortname') # create group
bot.groups.find_group_by_shortname('shortname') # return Group object by shortname
```

#### ** Python (SDK version 3.0.0 +) **

There are several methods in Python SDK to access the group data (available in ``bot.groups`` subclass):

- **create_public_group** - Create new public group. First parameter is ``title`` - title of group, second parameter is ``short_name``, returns AsyncTask with Group
- **create_private_group** - Create new private group. Single parameter is ``title`` - title of group, returns AsyncTask with Group
- **create_public_channel** - Create new public channel. First parameter is ``title`` - title of channel, second parameter is ``short_name``, returns AsyncTask with Group
- **create_private_channel** - Create new private channel. Single parameter is ``title`` - title of channel, returns AsyncTask with Group
- **find_group_by_short_name** - Finds **public** group or channel by short_name. Returns AsyncTask with Group.
- **find_group_by_id** - Finds group or channel by id. Returns AsyncTask with Group by id (if the group is in the dialogs).
- **load_members** - Load members from group or channel. First parameter is ``group_peer``, second parameter is ``limit`` - count of users. Returns AsyncTask with list of users from current group or None
- **kick_user** - Kick user from group or channel by Peer. First parameter is ``group_peer``, second parameter is ``limit``.
- **invite_user** - Invite user to group or channel by Peer. First parameter is ``group_peer``, second parameter is ``limit``.
- **set_default_group_permissions** - Set default group or channel permissions by Peer. First parameter is ``group_peer``, second/third parameters is ``permissions`` - add/delete.
- **set_member_permissions** - Set user permissions from group or channel by Peer. First parameter is ``group_peer``, second parameter is ``user_peer``, third/fourth parameters is ``permissions`` - add/delete.
- **get_group_member_permissions** - Load group members permissions by peers. First parameter is ``group_peer``, second parameter ``user_peers`` - list of Peer or AsyncTask with User. Returns AsyncTask with Permissions.
- **edit_group_title** - Change group title. First parameter is ``group_peer``, second parameter ``title`` - new title for group.
- **edit_avatar** - Change group avatar. First parameter is ``group_peer``, second parameter ``avatar`` - new avatar (path to image: str) for group. Returns new Avatar.
- **remove_group_avatar** - Delete group avatar. Single parameter is ``group_peer``. Returns UUID.
- **edit_group_about** - Change group about. First parameter is ``group_peer``, second parameter ``about`` - new about for group.
- **leave_group** - Leave from group. Single parameter is ``group_peer`.
- **make_user_admin** - Get for user admin-permissions. First parameter is ``group_peer``, second parameter ``user_peer``, third parameter ``permissions`` - list of Permissions.
- **transfer_ownership** - Transfer ownership permissions to user. First parameter is ``group_peer``, second parameter ``user_peer``.
- **get_group_invite_url** - Get url for invite users to group. Single parameter is ``group_peer``. Return AsyncTask with string url.
- **get_group_invite_url_base** - Get base url for invite users to group. Return AsyncTask with string url.
- **revoke_invite_url** - Get url for invite users to group (only for private groups). Single parameter is ``group_peer``. Return AsyncTask with string url.
- **join_group** - Join to group by group token or invite url. Single parameter is ``token`` or ``invite_url`` (string). Return AsyncTask with Group.
- **join_group_by_peer** - Join to group by group Peer (only for public groups). Single parameter is ``group_peer``.

``group_peer`` - Peer or AsyncTask with Group
``user_peer`` - Peer or AsyncTask with User

**load_members** - **join_group_by_peer** may be used if bot have permissions to do this.

Examples:

```python
group = bot.groups.create_public_group('title', 'short_name') # create group
user = bot.users.get_user_by_nick("admin")
bot.groups.invite_user(group, user) # invite user
bot.messaging.send_message(group, "See how I can")
bot.groups.edit_group_title(group, "My favorite group!") # change title
bot.groups.edit_group_about(group, "This is best of the best group!") # change about
bot.groups.edit_avatar(group, "path/to/the/best/image")  # change avatar
bot.groups.transfer_ownership(group, user) # change owner
bot.messaging.send_message(group, "This is your group now! Bye!")
bot.groups.leave_group(group)  # leave from group
```

#### ** Java **

There are several methods in Java SDK to access the group data (available in ``bot.groupsApi()`` subclass):

- **createGroup** - create group, first parameter is ``title`` - title of group (String), second parameter is ``username`` (String), third parameter ``users`` User's array, return Group object;
- **searchGroupByShortname** - returns ``Group`` list object of group by shortname;

Examples:

```java
List<User> users = bot.users().searchUserByNick("admin").get();
Group group = bot.groupsApi().createGroup("title", "shortname", users).get();
System.out.println(group);
System.out.println(bot.groupsApi().searchGroupByShortname("shortname").get().get(0));
```

<!-- tabs:end -->

Result:

?> ![](group.png)
