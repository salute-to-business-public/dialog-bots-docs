# Messaging

## Subscribing on updates

In all of SDK's there is only way to receive messages (and any other updates): subscription on messages via ``onMessage`` method:

<!-- tabs:start -->

#### ** Python **

```python
bot = DialogBot.get_insecure_bot(
    ...
)

bot.messaging.on_message(on_msg) # subscription on incoming messages with callback
```

``on_msg`` is a callback that accepts the ``params`` tuple with message updates. Fields of ``params`` object are:

* **peer** - Peer object of message sender
* **sender_uid** - sender's id
* **date** - message timestamp
* **message** - MessageContent object
* **mid** - message id

For example:

```python
def on_msg(*params):
    text = params[0].message.textMessage.text
    print(text)
```

Notice that `on_message` method is blocking. It means that bot will listen to messages, call callback in case of message and won't do anything else. Since version `1.2.0` of Python Bot SDK there is also
`on_message_async` method that performs subscription to updates in a separate thread. Let's see:

```python
bot.messaging.on_message(on_msg) # blocking version of subscription

print('Hey, I am here!') # this code is unreachable
```

```python
bot.messaging.on_message_async(on_msg) # non-blocking subscription

print('Hey, I am here!') # will be printed

```


#### ** Java **

```java
Bot bot = Bot.start("cbb4994cabfa8d2a5bce0b5f7a44c23da943f767").get();

bot.messaging().onMessage(message -> // subscribing on incoming messages with callback
            ...
)
```

#### ** JavaScript **

```javascript
bot.updateSubject.subscribe({ // subscribing on updates
  next(update) {
    console.log('update', update);
  }
});

bot
  .onMessage(async (message) => { // providing a callback
    ...
 })
```

<!-- tabs:end -->


## Sending messages

There are high-level functions for sending messages:

<!-- tabs:start -->

#### ** Python **

```python
bot.messaging.send_message(peer, message)
```

#### ** Java **

```java
bot.messaging().sendText(peer, message);
```

#### ** JavaScript **

```javascript
bot.sendText(peer, text)
```

<!-- tabs:end -->

## Update messages

There are high-level functions for updating messages:

<!-- tabs:start -->

#### ** Python **

```python
bot.messaging.update_message(message_id, text)
```

#### ** Java **

```java
bot.messaging().update(messageId, text);
```

<!-- tabs:end -->

## Delete messages

There are high-level functions for deleting messages:

<!-- tabs:start -->

#### ** Python **

```python
bot.messaging.delete(mids) # mids - array of message ids
```

#### ** Java **

```java
bot.messaging().sendText(mids); //  mids - array of message ids (List<UUID>)
```

<!-- tabs:end -->

## Reply messages

There are high-level functions for replying messages:

<!-- tabs:start -->

#### ** Python **

```python
bot.messaging.reply(peer, mids, text) # text may by None
```

#### ** Java **

```java
bot.messaging().reply(peer, messageId, text); # text is not null
```

<!-- tabs:end -->

Example result:

?> ![](reply.png)

## Sending files

For sending files:

<!-- tabs:start -->

#### ** Python **

```python
bot.messaging.send_file(peer, path_to_file)
```

#### ** Java **

```java
bot.messaging().onMessage(message ->
         ...
        ).thenCompose(aVoid ->
                bot.messaging().sendFile(message.getPeer(), new File(path_to_file))
        )
...
```

#### ** JavaScript **

```javascript
bot.sendDocument(message.peer, filename)
```

<!-- tabs:end -->

Result:

?> ![](files.png)

## Sending images with preview

You can also send images to chat with auto-generated preview (not like files):

<!-- tabs:start -->

#### ** Python **

```python
bot.messaging.send_image(peer, path_to_image)
```

#### ** Java **

```java
bot.messaging().onMessage(message ->
         ...
        ).thenCompose(aVoid ->
                bot.messaging().sendFile(message.getPeer(), new File(path_to_file))
        )
...
```

#### ** JavaScript **

```javascript
bot.sendImage(message.peer, path_to_image)
```

<!-- tabs:end -->

Result:

?> ![](images.png)

## Handling interactive elements

It's possible to send different controls (buttons, comboboxes) directly to the chat, for example:

<!-- tabs:start -->

#### ** Python **

For Python SDK, it's needed to add extra callback for handling actions:

```python
from dialog_bot_sdk import interactive_media


def on_msg(*params):
    print('on msg', params)
    bot.messaging.send_message(
        params[0].peer,
        "buttons",
        [interactive_media.InteractiveMediaGroup(
            [
                interactive_media.InteractiveMedia(
                    1,
                    interactive_media.InteractiveMediaButton("Test", "button_one")
                ),
                interactive_media.InteractiveMedia(
                    1,
                    interactive_media.InteractiveMediaButton("Test", "button_two")
                ),
            ]
        )]
    )

def on_click(*params):
    print('on click', params)


bot.messaging.on_message(on_msg, on_click)

```

``on_click`` is a callback that accepts the ``params`` tuple with interactive media updates. Fields of ``params`` object are:

* **uid** - id of user who performed interaction
* **value** - element value
* **id** - element local id (within message)
* **mid** - message id where interaction was performed

For example:

```python
def on_click(*params):
    uid = params[0].uid
    which_button = params[0].value
    print(uid, 'clicked on', which_button)
```

#### ** Java **

```java
List<InteractiveAction> actions = new ArrayList<>();

actions.add(new InteractiveAction("button_one", new InteractiveButton("button_one", "button_one")));
actions.add(new InteractiveAction("button_two", new InteractiveButton("button_two", "button_two")));

InteractiveGroup group = new InteractiveGroup(actions);

return bot.interactiveApi().send(peer, group);
```

#### ** JavaScript **

```javascript
bot
  .onMessage(async (message) => {
    await bot.sendText(
        message.peer,
        message.content.text,
        MessageAttachment.reply(message.id),
        ActionGroup.create({
            actions: [
                Action.create({
                    id: 'test',
                    widget: Button.create({ label: 'button_one' })
                }),
                Action.create({
                    id: 'test',
                    widget: Button.create({ label: 'button_two' })
                })
            ]
        })
    );
  }
)
```

<!-- tabs:end -->

Result:

?> ![](bots_simple_buttons.png)

To call confirmation alert before action:

<!-- tabs:start -->

#### ** Python **

```python
confirm = InteractiveMediaConfirm("Are you sure?", "Confirm", "ok", "dismiss")

button = interactive_media.InteractiveMediaButton("Button", "button")

bot.messaging.send_message(
    params[0].peer,
    'button',
    [
        InteractiveMediaGroup(
            [
                InteractiveMedia(1, button, 'default', confirm)
            ]
        )
    ]

)
```

#### ** Java **

```java
List<InteractiveAction> actions = new ArrayList<>();
actions.add(
        new InteractiveAction(
                "button_one",
                new InteractiveButton("button_one", "button_one"),
                new InteractiveConfirm("Are you sure?", "Confirm", "ok", "dismiss"))
        );

InteractiveGroup group = new InteractiveGroup(actions);

```

#### ** JavaScript **

```javascript
bot
  .onMessage(async (message) => {
    await bot.sendText(
        message.peer,
        message.content.text,
        MessageAttachment.reply(message.id),
        ActionGroup.create({
            actions: [
                Action.create({
                    id: 'test',
                    widget: Button.create({ label: 'button_one' }),
                    confirm: ActionConfirm.create({ title: 'Confirm', text: 'Are you sure?', ok: 'ok', dismiss: 'dismiss' })
                }),
            ]
        })
    );
  }
)
```
<!-- tabs:end -->

## Send media

Except the images can be to send audio and webpage content

<!-- tabs:start -->

#### ** Python **


```python
def on_msg(*params):
    image = get_media.get_image(bot, 'image_file') # MessageMedia with ImageMedia
    medias = [image] # send_media worked only with array of medias
    bot.messaging.send_media(params[0].peer, medias) # send message with media content for current peer

```

**get_image** function has several params:

* **bot** - DialogBot;
* **file** - path to image file;
* **width** - image's width (default 100);
* **height** - image's height (default 100).

**get_audio** function has several params:

* **bot** - DialogBot;
* **file** - path to audio file;
* **duration** - audio's duration.

**get_webpage** function has several params:

* **url** - url;
* **title** - webpage's title;
* **description** - webpage's description;
* **image_location** - ImageLocation object (can be obtained from get_media.get_image_location(bot, file, width, height));

#### ** Java **


```java
File imageFile = new File("imagePath");
MediaAndFilesOuterClass.FileLocation image = MediaAndFilesApi.upLoadFile(imageFile, null).get(); // second attribute is mimeType
FileLocation fileLocation = new FileLocation(image.getFileId(), image.getAccessHash());
ImageLocation imageLocation = new ImageLocation(fileLocation, width, height, image.getSerializedSize());
ImageMedia imageMedia = new ImageMedia(imageLocation);
MediaMessage mediaMessage = new MediaMessage(imageMedia, null, null, null);
ArrayList<MessagingOuterClass.MessageMedia> medias = new ArrayList<>();
medias.add(MediaMessage.buildMedia(mediaMessage));
bot.messaging().sendMedia(
        users.get(0).getPeer(),
        medias
)

```

**ImageLocation** has several params:

* **FileLocation fileLocation** - FileLocation class has params fileId (int) and accessHash (int)
* **int width** - image's width
* **int height** - image's height
* **int fileSize** - image's file size

**AudioLocation** has several params:

* **FileLocation fileLocation** - FileLocation class has params fileId (int) and accessHash (int)
* **int duration** - audio's duration
* **String mimeType** - mime type of audio
* **int fileSize** - audio's file size

**WebpageLocation** has several params:

* **String url** - web page's URL
* **String title** - web page's title
* **String description** - web page's description
* **ImageLocation image** - image which will be displayed with web page's content

<!-- tabs:end -->

## Message history

In Python SDK there's a feature of loading history of messages from conversations with particular peers:

<!-- tabs:start -->

#### ** Python **


```python
def on_msg(*params):
    history = bot.messaging.load_message_history(
        outpeer=bot.manager.get_outpeer(params[0].peer),
        limit=100
    )

    print(history)
```

This function has several params:

* **outpeer** - outpeer of user which history of messages we want to load
* **limit** - number of messages
* **date** - from which date we load history (in unix timestamp format)
* **direction** - direction of history (can be ``messaging_pb2.LISTLOADMODE_FORWARD`` or ``messaging_pb2.LISTLOADMODE_BACKWARD``)

#### ** Java **


```java
bot.messaging().onMessage(message ->{
        CompletableFuture<List<Message>> history = bot.messaging()
                .load(message.getPeer(), 0L, 100, MessagingApi.Direction.BACKWARD);
        System.out.println(history.get().toString());
        }
);
```

This function has several params:

* **Peer peer** - peer of user which history of messages we want to load
* **long date** - from which date we load history (in unix timestamp format)
* **int limit** - number of messages
* **Direction direction** - direction of history (can be ``MessagingApi.Direction.FORWARD``, ``MessagingApi.Direction.BACKWARD`` or ``MessagingApi.Direction.BOTH``)

<!-- tabs:end -->
