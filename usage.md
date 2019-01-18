# Usage

## Test endpoint

For test purposes you can use our test environment with a credentials above:

||
| -------------------------------------- | -----------------------------------|
| **Web URL**                            | https://grps-test.transmit.im      |
| **Endpoint for browser/desktop app**   | https://grps-test.transmit.im:8443 |
| **Endpoint for bot (insecure)**        | grps-test.transmit.im:8080         |
| **Login**                              | alice                              |
| **Password**                           | password                           |

Web URL is needed to access messenger via browser. Endpoints for browser or desktop app and
for bot used for connect to Dialog GUI and Dialog API correspondingly. Insecure means that we establish
connections to test environment without SSL.  

## Obtaining a token

Dialog bots use token-based authorization. For obtaining a token for your bot,
you have to go to Dialog url (for example ``https://grps-test.transmit.im``),
type ``Security Bot`` in search bar of your Dialog and start conversation with them.
To create new bot just send him this command:
```
/bot new <bot_nickname> <bot_name>
```
?> Notice that `nickname` is unique system name while `name` is displayed in dialog
list and can be non-unique.

## Configuring

For establishing connection in Java SDK, it's needed to configure endpoint explicitly in ``dialog.conf`` file like this:

```
dialog.botsdk {
  host = grpc-test.transmit.im
  port = 8080
  fork-join-pool.parallelism = 16
}
```

## Simple echobot example
Endpoint address and token are all you need to create your bot. So the full example of simple echobot looks like this:

<!-- tabs:start -->

#### ** Python **

```python
from dialog_bot_sdk.bot import DialogBot
import grpc
import os


def on_msg(*params):
    print('on msg', params)
    d.messaging.send_message(
        params[0].peer, str(params[0].message.textMessage.text)
    )


if __name__ == '__main__':
    d = DialogBot.get_insecure_bot(
        'grpc-test.transmit.im:8080',  # bot endpoint
        os.environ.get('BOT_TOKEN')  # bot token
    )

    d.messaging.on_message(on_msg)

```

#### ** Java **

```java
import java.util.concurrent.ExecutionException;

import im.dlg.botsdk.Bot;
import im.dlg.botsdk.domain.content.DocumentContent;
import im.dlg.botsdk.domain.content.TextContent;
import im.dlg.botsdk.domain.interactive.InteractiveGroup;

public class Main {

    public static void main(String[] args) throws InterruptedException, ExecutionException {

        Bot bot = Bot.start("cbb4994cabfa8d2a5bce0b5f7a44c23da943f767").get();

        bot.messaging().onMessage(message ->
                bot.users().get(message.getSender()).thenAccept(userOpt -> userOpt.ifPresent(user -> {
                            System.out.println("Got a message: " + message.getText() + " from user: " + user.getName());
                        })
                ).thenAccept(uuid ->
                        System.out.println("Sent a message with UUID: " + uuid)));

        bot.await();
    }
}
```

#### ** JavaScript **

```javascript
import path from 'path';
import dotenv from 'dotenv';
import Bot, { MessageAttachment, ActionGroup, Action, Button } from '../src';

dotenv.config();

const token = process.env.BOT_TOKEN;
if (typeof token !== 'string') {
  throw new Error('BOT_TOKEN env variable not configured');
}

const bot = new Bot({
  token,
  endpoints: ['https://grpc-test.transmit.im:9443']
});

bot.updateSubject.subscribe({
  next(update) {
    console.log('update', update);
  }
});

bot
  .onMessage(async (message) => {
    if (message.content.type === 'text') {
      const mid = await bot.sendText(
        message.peer,
        message.content.text,
        MessageAttachment.reply(message.id),
        ActionGroup.create({
          actions: [
            Action.create({
              id: 'test',
              widget: Button.create({ label: 'Test' })
            })
          ]
        })
      );
    }
  })
  .toPromise()
  .catch((error) => {
    console.error(error);
    process.exit(1);
  });

bot
  .onAction(async (event) => {
    console.log(event);
  })
  .toPromise()
  .catch((error) => {
    console.error(error);
    process.exit(1);
  });
```

<!-- tabs:end -->
