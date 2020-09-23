# Profile

<!-- tabs:start -->

#### ** Python **

There are several methods in Python SDK to access the profile of bot (available in ``bot.profile`` subclass):

- **edit_name** - Change bot name. Single parameter ``name`` (string).
- **edit_nickname** - Change bot nickname. Single parameter ``nick`` (string).
- **check_nickname** - Check bot nickname. Single parameter ``nick`` (string). Returns True if nickname is available.
- **edit_about** - Edit bot about. Single parameter ``about`` (string).
- **edit_avatar** - Edit bot about. Single parameter ``file`` (string of file path). Returns Avatar object if done or None if fail.
- **remove_avatar** - Remove bot avatar. Without parameters.
- **edit_time_zone** - Edit bot timezone. Single parameter ``tz`` (string).
- **edit_preferred_languages** - Edit bot preferred_languages. Single parameter ``preferred_languages`` (list of strings).
- **edit_sex** - Edit bot sex. Single parameter ``sex`` (string).
- **edit_custom_profile** - Edit bot custom_profile. Single parameter ``custom_profile`` (string).
- **edit_user_status** - Edit bot user_status. Single parameter ``user_status`` (string).

Examples:

```python
if bot.profile.check_nickname("the best bot"):
    bot.profile.edit_nickname("the best bot")
else:
    bot.profile.edit_avatar("path/to/the/best/avatar")
```

#### ** Java **

There are several methods in Java SDK to access the profile of bot (available in ``bot.botProfileApi()`` subclass):

- **editName** - Change bot name. Single parameter ``name`` (string).
- **editAbout** - Edit bot about. Single parameter ``about`` (string).

Examples:

```java
bot.botProfileApi().editName("the best bot");
```

<!-- tabs:end -->