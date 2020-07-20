# Sending and Receiving Messages

Messages are the core foundation of your client - without them, you won't be able to communicate with anyone.

Luckily enough, this is quite simple on i386chat as communication is simply socketed.

## Regular Messages

### Sending

To send a message, you must have:
- Initialised a socket connection
- Initialised UserData
- Received local UserData from the server

Use the created socket, and emit a message event like this:
```js
socket.emit("chat_message", {
    content: "message in variable form",
    userData, // Must be the local UserData array.
    room: "room name in variable form"
});
```

### Receiving
To receive a message, you must have:
- Initialised a socket connection
- Initialised UserData
- Received local UserData from the server

Otherwise, your client will not be sent events.

The server will emit all messages from your room only. To get these messages, extract them like this:
```js
socket.on('chat_message', (data) => {
    console.log("User has color " + data.userData.colour + ", author name is " + data.userData.nickname + " and message content is: " + data.content)
});
```

## Private Messages

Private messages will only be seen by you, and nobody else other than the person who sent it. The server should NOT be broadcasting these packets to everyone.

### Sending
To send a private message, you must have:
- Initialised a socket connection
- Initialised UserData
- Received local UserData from the server

Use the created socket, and emit a message event like this:
```js
socket.emit("chat_private_message", {
    content: "message in variable form",
    userData, // Must be the local UserData array.
    receiverID: "USER_ID_IN_VARIABLE_FORM" // Must be a string, sending an integer will cause issues on the server.
});
```

### Receiving
To receive a message, you must have:
- Initialised a socket connection
- Initialised UserData
- Received local UserData from the server

Otherwise, your client will not be sent events.

The server will emit messages to your socket instance only, so communication is secured. To get these messages, extract them like this:
```js
socket.on('chat_private_message', (data) => {
    console.log("PRIVATE MESSAGE - User has color " + data.userData.colour + ", author name is " + data.userData.nickname + " and message content is: " + data.content)
});
```

*( You will find more information on how data is structured in the Data Structures portion of the documentation )*