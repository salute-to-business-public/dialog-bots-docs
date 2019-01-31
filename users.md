# Users

<!-- tabs:start -->

#### ** Python **

There are several methods in Python SDK to access the user data (available in ``bot.users`` subclass):

- **find_user_outpeer_by_nick** - returns ``OutPeer`` object of user, which is used to message him (first parameter in ``send_message`` method). If a user didn't write to bot earlier, it's only way to obtain approprite ``OutPeer`` object to write him first;
- **get_user_by_nick** - returns ``User`` object by nickname (contain some useful info);
- **get_user_full_profile_by_nick** - returns ``FullUser`` object by nickname, which contains some additional info about user (such as ``custom_profile`` field);
- **get_user_custom_profile_by_nick** - returns ``custom_profile`` field of ``FullUser`` object by nickname of user;
- **get_user_custom_profile_by_peer** - same but by ``Peer`` object of user.

Examples:

```python
bot.users.get_user_by_nick('admin') # returns User object of 'admin' user

```

```python
outpeer = bot.users.find_user_outpeer_by_nick('alice') # obtain OutPeer from nickname

# now we can write to person first
bot.messaging.send_message(
    outpeer,
    'I found you anyway!'
)
```

<!-- tabs:end -->
