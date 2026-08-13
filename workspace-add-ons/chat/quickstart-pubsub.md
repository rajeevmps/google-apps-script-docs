# Build a Google Chat app that uses Pub/Sub

## Overview

This page explains how to create a Chat app that receives events from Chat using Cloud Pub/Sub. This architecture is useful if your Chat app is behind a firewall or if you want to send or receive events about a Chat space or user with the Google Workspace Events API.

In this architecture, a user interacting with a Pub/Sub Chat app has the following flow of information:

1. A user interacts with the Chat app by, for example, sending it a message, issuing a command, or adding or removing it from a Chat space.
2. Chat sends the message to a Pub/Sub topic.
3. An application server, that is either a cloud or on-premises system that contains the Chat app logic, subscribes to the Pub/Sub topic in order to receive the message through the firewall.
4. Optionally, the Chat app can call the Chat API to asynchronously post messages or perform other operations.

## Prerequisites

### Node.js
- A Business or Enterprise Google Workspace account with access to Google Chat
- A Google Cloud project with billing enabled
- Node.js 14 or greater
- The npm package management tool
- An initialized Node.js project (created via `npm init`)

### Python
- A Business or Enterprise Google Workspace account with access to Google Chat
- A Google Cloud project with billing enabled
- Python 3.6 or greater
- The pip package management tool

### Java
- A Business or Enterprise Google Workspace account with access to Google Chat
- A Google Cloud project with billing enabled
- Java 11 or greater
- The Maven package management tool

## Enable the APIs

Before using Google APIs, you need to turn them on in a Google Cloud project. You can turn on one or more APIs in a single Google Cloud project.

In the Google Cloud console, enable the Google Chat API and the Pub/Sub API.

## Set up Pub/Sub

1. Create a Pub/Sub topic that the Chat API can send messages to. We recommend that you use a single topic per Chat app.
2. Create a service account for the Chat app to authorize with Pub/Sub and Chat and save the private key file to your working directory.
3. Create a pull subscription to the topic.
4. Assign the **Pub/Sub Subscriber Role** on the subscription for the service account that you previously created.

**Note:** If you use VPC Service Controls, you may need to configure an ingress rule in your service perimeter to allow the service account to access Pub/Sub.

## Write the Script

In this section, you define the application logic for your Chat app. You write a script that authenticates with Google Cloud and subscribes to the Pub/Sub topic to receive events from Chat, such as when a user sends a message to your Chat app.

When the script receives a message, it processes the event data and uses the Google Chat API to post a response back to the user or space. This setup allows your Chat app to function behind a firewall while still interacting with Chat users.

### Node.js

1. In a CLI, provide service account credentials:
```
export GOOGLE_APPLICATION_CREDENTIALS=SERVICE_ACCOUNT_FILE_PATH
```

2. In a CLI, provide the Google Cloud project ID:
```
export PROJECT_ID=PROJECT_ID
```

3. In a CLI, provide the subscription ID for the Pub/Sub subscription that you previously created:
```
export SUBSCRIPTION_ID=SUBSCRIPTION_ID
```

4. In your working directory, create a file named `package.json`.

5. In the `package.json` file, paste the following code:

```json
{
  "name": "pub-sub-app",
  "version": "1.0.0",
  "description": "Google Chat App that listens for messages via Cloud Pub/Sub",
  "main": "index.js",
  "scripts": {
    "start": "node index.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "dependencies": {
    "@google-apps/chat": "^0.4.0",
    "@google-cloud/pubsub": "^4.5.0"
  },
  "license": "Apache-2.0"
}
```

6. In your working directory, create a file named `index.js`.

7. In `index.js`, paste the following code:

```javascript
const {ChatServiceClient} = require('@google-apps/chat');
const {MessageReplyOption} = require('@google-apps/chat').protos.google.chat.v1.CreateMessageRequest;
const {PubSub} = require('@google-cloud/pubsub');
const {SubscriberClient} = require('@google-cloud/pubsub/build/src/v1');

// Receives messages from a pull subscription.
function receiveMessages() {
  const chat = new ChatServiceClient({
    keyFile: process.env.GOOGLE_APPLICATION_CREDENTIALS,
    scopes: ['https://www.googleapis.com/auth/chat.bot'],
  });

  const subscriptionPath = new SubscriberClient()
    .subscriptionPath(process.env.PROJECT_ID, process.env.SUBSCRIPTION_ID)
  const subscription = new PubSub()
    .subscription(subscriptionPath);

  // Handle incoming message, then acknowledge the received message
  const messageHandler = message => {
    console.log(`Id : ${message.id}`);
    const event = JSON.parse(message.data);
    console.log(`Data : ${JSON.stringify(event)}`);

    // Post the response to Google Chat.
    const request = formatRequest(event);
    if (request != null) {
      chat.createMessage(request);
    }

    // Acknowledge the message.
    message.ack();
  }

  subscription.on('message', messageHandler);
  console.log(`Listening for messages on ${subscriptionPath}`);

  // Keep main thread from exiting while waiting for messages
  setTimeout(() => {
    subscription.removeListener('message', messageHandler);
    console.log(`Stopped listening for messages.`);
  }, 60 * 1000);
}

// Send message to Google Chat based on the type of event
function formatRequest(event) {
  const chatEvent = event.chat || {};

  // If the app was removed, we don't respond.
  if (chatEvent.removedFromSpacePayload) {
    console.log(`App removed from space.`);
    return null;
  }

  const payload = chatEvent.messagePayload || chatEvent.addedToSpacePayload;
  const spaceName = payload?.space?.name;

  if (!spaceName) {
    console.log('No space name in event.');
    return null;
  }

  if (chatEvent.addedToSpacePayload) {
    // An app can also be added to a space by @mentioning it in a
    // message. In that case, we fall through to the message case
    // and let the app respond. If the app was added using the
    // invite flow, we just post a thank you message in the space.
    return {
      parent: spaceName,
      message: { text: 'Thank you for adding me!' },
    };
  } else if (chatEvent.messagePayload) {
    // In case of message, post the response in the same thread.
    const message = chatEvent.messagePayload.message;
    return {
      parent: spaceName,
      messageReplyOption: MessageReplyOption.REPLY_MESSAGE_FALLBACK_TO_NEW_THREAD,
      message: {
        text: 'You said: `' + message.text + '`',
        thread: { name: message.thread.name },
      },
    };
  }
}

if (!process.env.PROJECT_ID) {
  console.log('Missing PROJECT_ID env var.');
  process.exit(1);
}
if (!process.env.SUBSCRIPTION_ID) {
  console.log('Missing SUBSCRIPTION_ID env var.');
  process.exit(1);
}
if (!process.env.GOOGLE_APPLICATION_CREDENTIALS) {
  console.log('Missing GOOGLE_APPLICATION_CREDENTIALS env var.');
  process.exit(1);
}

receiveMessages();
```

### Python

1. In a CLI, provide service account credentials:
```
export GOOGLE_APPLICATION_CREDENTIALS=SERVICE_ACCOUNT_FILE_PATH
```

2. In a CLI, provide the Google Cloud project ID:
```
export PROJECT_ID=PROJECT_ID
```

3. In a CLI, provide the subscription ID for the Pub/Sub subscription that you previously created:
```
export SUBSCRIPTION_ID=SUBSCRIPTION_ID
```

4. In your working directory, create a file named `requirements.txt`.

5. In the `requirements.txt` file, paste the following code:

```
google-cloud-pubsub>=2.23.0
google-apps-chat==0.1.9
```

6. In your working directory, create a file named `app.py`.

7. In `app.py`, paste the following code:

```python
import json
import logging
import os
import sys
import time
from google.apps import chat_v1 as google_chat
from google.cloud import pubsub_v1
from google.oauth2.service_account import Credentials

def receive_messages():
  """Receives messages from a pull subscription."""

  scopes = ['https://www.googleapis.com/auth/chat.bot']
  service_account_key_path = os.environ.get('GOOGLE_APPLICATION_CREDENTIALS')
  creds = Credentials.from_service_account_file(service_account_key_path)
  chat = google_chat.ChatServiceClient(
      credentials=creds, client_options={'scopes': scopes}
  )

  project_id = os.environ.get('PROJECT_ID')
  subscription_id = os.environ.get('SUBSCRIPTION_ID')
  subscriber = pubsub_v1.SubscriberClient()
  subscription_path = subscriber.subscription_path(project_id, subscription_id)

  # Handle incoming message, then acknowledge the received message
  def callback(message):
    event = json.loads(message.data)
    logging.info('Data : %s', event)

    # Post the response to Google Chat.
    request = format_request(event)
    if request is not None:
      chat.create_message(request)

    # Acknowledge the message.
    message.ack()

  subscriber.subscribe(subscription_path, callback = callback)
  logging.info('Listening for messages on %s', subscription_path)

  # Keep main thread from exiting while waiting for messages
  while True:
    time.sleep(60)

def format_request(event):
  """Send message to Google Chat based on the type of event.
  Args:
    event: A dictionary with the event data.
  """
  chat_event = event.get('chat', {})

  # If the app was removed, we don't respond.
  if 'removedFromSpacePayload' in chat_event:
    logging.info('App removed from space.')
    return

  payload = chat_event.get('messagePayload') or chat_event.get(
      'addedToSpacePayload'
  )
  space_name = payload.get('space', {}).get('name') if payload else None

  if not space_name:
    logging.warning('No space name in event.')
    return

  if 'addedToSpacePayload' in chat_event:
    # An app can also be added to a space by @mentioning it in a
    # message. In that case, we fall through to the message case
    # and let the app respond. If the app was added using the
    # invite flow, we just post a thank you message in the space.
    return google_chat.CreateMessageRequest(
        parent = space_name,
        message = {
          'text': 'Thank you for adding me!'
        }
    )
  elif 'messagePayload' in chat_event:
    # In case of message, post the response in the same thread.
    message = chat_event['messagePayload']['message']
    return google_chat.CreateMessageRequest(
        parent = space_name,
        message_reply_option = google_chat.CreateMessageRequest.MessageReplyOption.REPLY_MESSAGE_FALLBACK_TO_NEW_THREAD,
        message = {
          'text': 'You said: `' + message['text'] + '`',
          'thread': {
            'name': message['thread']['name']
          }
        }
    )

if __name__ == '__main__':
  if 'PROJECT_ID' not in os.environ:
    logging.error('Missing PROJECT_ID env var.')
    sys.exit(1)

  if 'SUBSCRIPTION_ID' not in os.environ:
    logging.error('Missing SUBSCRIPTION_ID env var.')
    sys.exit(1)

  if 'GOOGLE_APPLICATION_CREDENTIALS' not in os.environ:
    logging.error('Missing GOOGLE_APPLICATION_CREDENTIALS env var.')
    sys.exit(1)

  logging.basicConfig(
      level=logging.INFO,
      style='{',
      format='{levelname:.1}{asctime} {filename}:{lineno}] {message}')
  receive_messages()
```

### Java

1. In a CLI, provide service account credentials:
```
export GOOGLE_APPLICATION_CREDENTIALS=SERVICE_ACCOUNT_FILE_PATH
```

2. In a CLI, provide the Google Cloud project ID:
```
export PROJECT_ID=PROJECT_ID
```

3. In a CLI, provide the subscription ID for the Pub/Sub subscription that you previously created:
```
export SUBSCRIPTION_ID=SUBSCRIPTION_ID
```

4. In your working directory, create a file named `pom.xml`.

5. In the `pom.xml` file, paste the following code:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
     xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
     <modelVersion>4.0.0</modelVersion>

     <groupId>com.google.chat.addon</groupId>
     <artifactId>pubsub-addon-chat-app</artifactId>
     <version>0.1.0</version>

     <name>pubsub-addon-chat-app-java</name>

     <properties>
       <maven.compiler.release>11</maven.compiler.release>
       <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
     </properties>

     <dependencyManagement>
       <dependencies>
         <dependency>
           <groupId>com.google.cloud</groupId>
           <artifactId>libraries-bom</artifactId>
           <version>26.41.0</version> <!-- Use a recent BOM version -->
           <type>pom</type>
           <scope>import</scope>
         </dependency>
       </dependencies>
     </dependencyManagement>

     <dependencies>
       <!-- Google Chat GAPIC library -->
       <dependency>
         <groupId>com.google.cloud</groupId>
         <artifactId>google-cloud-chat</artifactId>
       </dependency>
       <!-- Google Cloud Pub/Sub library -->
       <dependency>
         <groupId>com.google.cloud</groupId>
         <artifactId>google-cloud-pubsub</artifactId>
       </dependency>
       <!-- Google Apps Add-ons Event Object -->
       <dependency>
         <groupId>com.google.apps.addons.v1</groupId>
         <artifactId>google-apps-addons-v1-java</artifactId>
         <version>0.2.0</version> <!-- Check for latest version -->
       </dependency>
       <!-- Protobuf JSON utility -->
       <dependency>
         <groupId>com.google.protobuf</groupId>
         <artifactId>protobuf-java-util</artifactId>
       </dependency>
       <!-- Google Auth Library -->
       <dependency>
         <groupId>com.google.auth</groupId>
         <artifactId>google-auth-library-oauth2-http</artifactId>
       </dependency>
       <dependency>
         <groupId>com.google.api</groupId>
         <artifactId>gax</artifactId>
       </dependency>
       <!-- JSON utilities for PubSub message (if needed, though protobuf-java-util is primary for EventObject) -->
       <dependency>
         <groupId>com.fasterxml.jackson.core</groupId>
         <artifactId>jackson-databind</artifactId>
         <version>2.14.2</version>
       </dependency>
       <dependency>
         <groupId>org.slf4j</groupId>
         <artifactId>slf4j-jdk14</artifactId>
         <version>1.7.36</version>
         <scope>runtime</scope>
       </dependency>
     </dependencies>

     <build>
       <plugins>
         <plugin>
           <groupId>org.apache.maven.plugins</groupId>
           <artifactId>maven-compiler-plugin</artifactId>
           <version>3.13.0</version>
           <configuration>
             <source>11</source>
             <target>11</target>
           </configuration>
         </plugin>
         <plugin>
           <groupId>org.codehaus.mojo</groupId>
           <artifactId>exec-maven-plugin</artifactId>
           <version>3.3.0</version>
           <configuration>
             <mainClass>Main</mainClass>
           </configuration>
         </plugin>
       </plugins>
     </build>
</project>
```

6. In your working directory, create the directory structure `src/main/java`.

7. In the `src/main/java` directory, create a file named `Main.java`.

8. In `Main.java`, paste the following code:

```java
import com.fasterxml.jackson.databind.JsonNode;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.google.api.gax.core.FixedCredentialsProvider;
import com.google.auth.oauth2.GoogleCredentials;
import com.google.chat.v1.ChatServiceClient;
import com.google.chat.v1.ChatServiceSettings;
import com.google.chat.v1.CreateMessageRequest;
import com.google.chat.v1.CreateMessageRequest.MessageReplyOption;
import com.google.chat.v1.Message;
import com.google.chat.v1.Thread;
import com.google.cloud.pubsub.v1.AckReplyConsumer;
import com.google.cloud.pubsub.v1.MessageReceiver;
import com.google.cloud.pubsub.v1.Subscriber;
import com.google.pubsub.v1.ProjectSubscriptionName;
import com.google.pubsub.v1.PubsubMessage;
import java.io.FileInputStream;
import java.util.Collections;

public class Main {

  public static final String PROJECT_ID_ENV_PROPERTY = "PROJECT_ID";
  public static final String SUBSCRIPTION_ID_ENV_PROPERTY = "SUBSCRIPTION_ID";
  public static final String CREDENTIALS_PATH_ENV_PROPERTY = "GOOGLE_APPLICATION_CREDENTIALS";

  public static void main(String[] args) throws Exception {
    ProjectSubscriptionName subscriptionName =
        ProjectSubscriptionName.of(
            System.getenv(Main.PROJECT_ID_ENV_PROPERTY),
            System.getenv(Main.SUBSCRIPTION_ID_ENV_PROPERTY));

    // Instantiate app, which implements an asynchronous message receiver.
    EchoApp echoApp = new EchoApp();

    // Create a subscriber for <var>SUBSCRIPTION_ID</var> bound to the message receiver
    final Subscriber subscriber = Subscriber.newBuilder(subscriptionName, echoApp).build();
    System.out.println("Subscriber is listening to events...");
    subscriber.startAsync();

    // Wait for termination
    subscriber.awaitTerminated();
  }
}

/**
 * A demo app which implements {@link MessageReceiver} to receive messages.
 * It echoes incoming messages.
 */
class EchoApp implements MessageReceiver {

  // Path to the private key JSON file of the service account to be used for posting response
  // messages to Google Chat.
  // In this demo, we are using the same service account for authorizing with Cloud Pub/Sub to
  // receive messages and authorizing with Google Chat to post messages. If you are using
  // different service accounts, set the path to the private key JSON file of the service
  // account used to post messages to Google Chat here.
  private static final String SERVICE_ACCOUNT_KEY_PATH =
    System.getenv(Main.CREDENTIALS_PATH_ENV_PROPERTY);

  // Developer code for Google Chat API scope.
  private static final String GOOGLE_CHAT_API_SCOPE = "https://www.googleapis.com/auth/chat.bot";

  private static final String ADDED_RESPONSE = "Thank you for adding me!";

  ChatServiceClient chatServiceClient;

  EchoApp() throws Exception {
    GoogleCredentials credential =
        GoogleCredentials.fromStream(new FileInputStream(SERVICE_ACCOUNT_KEY_PATH))
            .createScoped(Collections.singleton(GOOGLE_CHAT_API_SCOPE));

    // Create the ChatServiceSettings with the app credentials
    ChatServiceSettings chatServiceSettings =
        ChatServiceSettings.newBuilder()
            .setCredentialsProvider(FixedCredentialsProvider.create(credential))
            .build();

    // Set the Chat service client
    chatServiceClient = ChatServiceClient.create(chatServiceSettings);
  }

  // Called when a message is received by the subscriber.
  @Override
  public void receiveMessage(PubsubMessage pubsubMessage, AckReplyConsumer consumer) {
    System.out.println("Id : " + pubsubMessage.getMessageId());
    // Handle incoming message, then acknowledge the received message
    try {
      ObjectMapper mapper = new ObjectMapper();
      JsonNode dataJson = mapper.readTree(pubsubMessage.getData().toStringUtf8());
      System.out.println("Data : " + dataJson.toString());
      handle(dataJson);
      consumer.ack();
    } catch (Exception e) {
      System.out.println(e);
      // Negative acknowledgement makes Pub/Sub redeliver the message.
      consumer.nack();
    }
  }

  // Send message to Google Chat based on the type of event.
  public void handle(JsonNode eventJson) throws Exception {
    // Google Chat events for add-ons are wrapped in a 'chat' object.
    if (!eventJson.has("chat")) {
      System.out.println("Ignored: Not a Chat event (missing 'chat' field).");
      return;
    }

    JsonNode chatNode = eventJson.get("chat");
    CreateMessageRequest createMessageRequest = null;

    if (chatNode.has("messagePayload")) {
      // HANDLE MESSAGE
      JsonNode messagePayload = chatNode.get("messagePayload");
      JsonNode message = messagePayload.get("message");
      JsonNode space = messagePayload.get("space");

      String spaceName = space.get("name").asText();
      String userText = message.has("text") ? message.get("text").asText() : "";
      String threadName = message.has("thread") ? message.get("thread").get("name").asText() : "";

      System.out.println("Received message in " + spaceName + ": " + userText);

      createMessageRequest =
          CreateMessageRequest.newBuilder()
              .setParent(spaceName)
              .setMessageReplyOption(MessageReplyOption.REPLY_MESSAGE_FALLBACK_TO_NEW_THREAD)
              .setMessage(
                  Message.newBuilder()
                      .setText("You said: `" + userText + "`")
                      .setThread(Thread.newBuilder().setName(threadName).build())
                      .build())
              .build();

    } else if (chatNode.has("addedToSpacePayload")) {
      // HANDLE ADDED TO SPACE
      JsonNode addedPayload = chatNode.get("addedToSpacePayload");
      JsonNode space = addedPayload.get("space");
      String spaceName = space.get("name").asText();

      System.out.println("Added to space: " + spaceName);

      createMessageRequest =
          CreateMessageRequest.newBuilder()
              .setParent(spaceName)
              .setMessage(Message.newBuilder().setText(ADDED_RESPONSE).build())
              .build();

    } else if (chatNode.has("removedFromSpacePayload")) {
      System.out.println("Removed from space.");
      return;
    } else {
      System.out.println("Ignored: Unhandled Chat event type.");
      return;
    }

    if (createMessageRequest != null) {
      // Post the response to Google Chat.
      chatServiceClient.createMessage(createMessageRequest);
      System.out.println("Sent reply.");
    }
  }
}
```

## Configure the Chat app

Configure the Chat app in the Google Cloud console to provide details like its name and avatar, and to set up the connection to the Pub/Sub topic.

By connecting to the Pub/Sub topic, you enable Chat to send events to your app. Your script, which subscribes to the topic, can then receive these events and respond to users.

1. In the Google Cloud console, go to **Menu menu > APIs & Services > Enabled APIs & Services > Google Chat API > Configuration**.

2. Configure the Chat app for Pub/Sub:

   1. In **App name**, enter `Add-on Chat App`.
   2. In **Avatar URL**, enter `https://developers.google.com/workspace/add-ons/images/quickstart-app-avatar.png`.
   3. In **Description**, enter `Quickstart app`.
   4. Under **Functionality**, select **Join spaces and group conversations**.
   5. Under **Connection settings**, select **Cloud Pub/Sub** and paste the name of the Pub/Sub topic that you previously created.
   6. Under **Visibility**, select **Make this Google Chat app available to specific people and groups** in your domain and enter your email address.
   7. Under **Logs**, select **Log errors to Logging**.

3. Click **Save**.

Now that you've configured the Chat app, you must update a Pub/Sub configuration.

1. On the Chat API configuration page, under **Connection settings** copy the **Service account email**, which is a unique email generated for your Google Cloud project.
2. Grant Chat permission to publish to the topic by assigning the **Pub/Sub Publisher** role to the service account email you previously copied.

**Note:** If you use VPC Service Controls, you may need to configure an ingress rule in your service perimeter to allow the service account to access Pub/Sub.

The app is ready to receive and respond to messages on Chat.

## Run the Script

In a CLI, switch into your working directory and run the script:

### Node.js

```
npm install
npm start
```

### Python

```
python -m venv env
source env/bin/activate
pip install -r requirements.txt -U
python app.py
```

### Java

```
mvn compile exec:java -Dexec.mainClass=Main
```

When you run the code, the application starts listening to messages published to the Pub/Sub topic.

## Test your Chat app

To test your Chat app, open a direct message space with the Chat app and send a message:

1. Open Google Chat using the Google Workspace account that you provided when you added yourself as a trusted tester.

2. Click add **New chat**.
3. In the **Add 1 or more people** field, type the name of your Chat app.
4. Select your Chat app from the results. A direct message opens.

**Note:** If you don't see your Chat app in the list of results, ensure that you've included your Google Workspace account in the **Visibility** settings of the **Chat API Configuration** page in the Google Cloud console.

5. In the new direct message with the app, type `Hello` and press `enter`.

To add trusted testers and learn more about testing interactive features, see [Test interactive features for Google Chat apps](/workspace/chat/test-interactive-features).

## Troubleshoot

When a Google Chat app or card returns an error, the Chat interface surfaces a message saying "Something went wrong." or "Unable to process your request." Sometimes the Chat UI doesn't display any error message, but the Chat app or card produces an unexpected result; for example, a card message might not appear.

Although an error message might not display in the Chat UI, descriptive error messages and log data are available to help you fix errors when error logging for Chat apps is turned on. For help viewing, debugging, and fixing errors, see [Troubleshoot and fix Google Chat errors](/workspace/chat/troubleshoot).

## Clean up

To avoid incurring charges to your Google Cloud account for the resources used in this tutorial, we recommend that you delete the Cloud project.

**Caution:** Deleting a project has the following effects:

- **Everything in the project is deleted.** If you used an existing project for this tutorial, when you delete it, you also delete any other work you've done in the project.
- **Custom project IDs are lost.** When you created this project, you might have created a custom project ID that you want to use in the future. To preserve the URLs that use the project ID, such as a URL on appspot.com, delete the selected resources inside the project instead of deleting the whole project.

If you plan to explore multiple tutorials and quickstarts, reusing projects can help you avoid exceeding project quota limits.

1. In the Google Cloud console, go to the **Manage resources** page. Click **Menu** menu **> IAM & Admin > Manage Resources**.

2. In the project list, select the project you want to delete and then click **Delete** delete.
3. In the dialog, type the project ID and then click **Shut down** to delete the project.

## Related topics

- To add more features to your Chat app, see the following:
  - [Send Google Chat messages](/workspace/add-ons/chat/send-messages)
  - [Respond to commands](/workspace/add-ons/chat/commands)
- [Build Google Chat interfaces](/workspace/add-ons/chat/build)
