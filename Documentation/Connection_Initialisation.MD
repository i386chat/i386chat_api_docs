# Connection Initialisation

Client connection initialisation (on the web client) is handled according to this flowchart:
![Client Connection Flowchart](https://github.com/i386chat/i386chat_api_docs/raw/master/Documentation/client_connect_flow.png)

Bear in mind that this can vary on your client, and a socket connection may be dropped if your user is banned (try to catch this, so a user isn't left confused).