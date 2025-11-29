# Real-Time Chat Using WebSockets (Socket.IO)

## Steps to Implement

### 1. Build the Chat UI

- Create a chat window UI at route: `/chat/:targetUserId`

### 2. Set Up Socket.IO in Backend

- Install Socket.IO:

```
npm install socket.io
```

- Create a socket connection on the backend server.

### 3. Create Socket Connection on Frontend

- Install socket.io-client and establish a connection to the backend.
- Once connected, the client can send and receive events in real-time.

### 4. Create a Room for Two Users

- When a user opens the chat page, emit a `joinChat` event from the frontend.
- Backend receives it and:
  - Generates a roomId (based on userId + targetUserId)
  - Adds both users to that room

### 5. Sending Messages

- Frontend emits a `sendMessage` event along with:
  - sender info
  - message text
- Backend receives it and forwards the message to the specific room.

### 6. Receiving Messages

- Backend emits `messageReceived` to all users in the room.
- Frontend listens for this event and updates the UI by adding the new message.

## Workflow Summary

```
Frontend → emit("joinChat") → Backend
Backend → join room → confirm setup

Frontend → emit("sendMessage") → Backend
Backend → emit("messageReceived") to room → Frontend
Frontend → display message in chat window where developer can chat
```
