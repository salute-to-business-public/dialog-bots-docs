# Users

<!-- tabs:start -->

#### ** Python **

There are several methods in Python SDK to access the user data (available in ``bot.users`` subclass):

- **find_user_outpeer_by_nick** - returns ``OutPeer`` object of user, which is used to message him (first parameter in ``send_message`` method). If a user didn't write to bot earlier, it's only way to obtain approprite ``OutPeer`` object to write him first;
- **get_user_outpeer_by_id** - returns ``OutPeer`` object of user by user id;
- **get_user_peer_by_id** - returns ``Peer`` object of user by user id;
- **get_user_by_nick** - returns ``User`` object by nickname (contain some useful info);
- **get_user_full_profile_by_nick** - returns ``FullUser`` object by nickname, which contains some additional info about user (such as ``custom_profile`` field);
- **get_user_custom_profile_by_nick** - returns ``custom_profile`` field of ``FullUser`` object by nickname of user;
- **get_user_custom_profile_by_peer** - same but by ``Peer`` object of user;
- **search_users_by_nick_substring** - find users list by substring of nickname (not complete coincidence!), returns list of ``User``'s objects or None if could not find.

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

#### ** Python (SDK version 3.0.0 +) **

Class User have attributes:

- **peer** - main parameter for working with messages and groups
- **data** - class UserData witch have parameters **name**, **avatar**, **about**, **nick**

Class FullUser have attributes:

- **id** - user id
- **about** - about the user info
- **preferred_languages** - list of user's languages
- **time_zone** - user's timezone
- **custom_profile** - user's custom profile

There are several methods in Python SDK to access the user data (available in ``bot.users`` subclass):

- **get_user_by_nick** - returns ``AsyncTask`` object with ``User`` object of user, which is used to message him (first parameter in ``send_message`` method). If a user didn't write to bot earlier, it's only way to write him first;
- **get_user_by_id** - returns ``AsyncTask`` object with ``User`` object of user. Find user from dialogs, if user wrote earlier.
- **get_full_profile_by_nick** - returns ``AsyncTask`` object with ``FullUser`` object by nickname;
- **get_full_profile_by_id** - returns ``AsyncTask`` object with ``FullUser`` object by id;
- **search_users_by_nick_substring** - find users list by substring of nickname (not complete coincidence!), returns ``AsyncTask`` with list of ``User``'s objects.

Examples:

```python
bot.users.get_user_by_nick('admin')         # returns AsyncTask object

```
```python
bot.users.get_user_by_nick('admin').wait()  # returns User object (blocked main thread)

```

```python
user = bot.users.get_user_by_nick('admin')

# now we can write to person first
bot.messaging.send_message(
    user,
    'I found you anyway!'
)
```

#### ** Java **

There are several methods in Java SDK to access the user data (available in ``bot.users()`` subclass):

- **findUserOutPeerByNick** - returns ``CompletableFuture<Optional<Peers.OutPeer>>`` object of user, which is used to message him (first parameter in ``send_message`` method). If a user didn't write to bot earlier, it's only way to obtain approprite ``OutPeer`` object to write him first;
- **findUserPeer** - returns ``CompletableFuture<Optional<Peer>>`` object of user by user id;
- **searchUserByNick** - returns ``CompletableFuture<List<User>>`` object by nickname (contain some useful info);
- **getUserFullProfileByNick** - returns ``CompletableFuture<UsersOuterClass.FullUser>`` object by nickname, which contains some additional info about user (such as ``custom_profile`` field) or null;
- **getUserCustomProfileByNick** - returns ``String custom_profile`` field of ``CompletableFuture<UsersOuterClass.FullUser>`` object by nickname of user;
- **getUserCustomProfileByPeer** - same but by ``Peer`` object of user;
- **searchUsersByNickSubstring** - find users list by substring of nickname (not complete coincidence!), returns ``CompletableFuture<List<User>>``'s objects or nill if could not find.


Examples:

```java
List<User> users = bot.users().searchUserByNick("admin").get(); // returns list of User objects of 'admin' user
```

```java
# now we can write to person first
if (!users.isEmpty()) {
    bot.messaging().sendText(
            users.get(0).getPeer(),
            "I found you anyway!"
    );
} else System.out.println("No user with this nickname")
```

<!-- tabs:end -->
