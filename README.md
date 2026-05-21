# Python Chat Server

A multithreaded TCP chat server and command-line client built in Python for CSC138. The project demonstrates socket programming, concurrent client handling, and a small text-based protocol for joining a chat room, listing users, broadcasting messages, sending private messages, and disconnecting cleanly.

## Features

- Supports multiple clients through Python threads
- Uses TCP sockets for client-server communication
- Tracks active users and their connected sockets
- Handles chat-room commands:
  - `JOIN <username>`: register a client with the chat server
  - `LIST`: show currently connected users
  - `BCST <message>`: broadcast a message to all registered users
  - `MESG <username> <message>`: send a private message to one user
  - `QUIT`: leave the chat room and close the client connection
- Limits the chat room to 10 registered users
- Requires only the Python standard library

## Architecture

The server opens a TCP socket on the requested port and waits for incoming client connections. Each accepted client connection is handled in its own thread, allowing multiple users to interact with the chat room at the same time.

The server maintains two shared dictionaries:

- `currentUsers`: maps client addresses to usernames for display and routing
- `registered_clients`: maps client addresses to sockets so the server can send messages to specific users or broadcast to the room

The client connects to the server, sends user-entered commands, and starts a background thread to receive server messages while the user continues typing.

## Requirements

- Python 3
- No external dependencies

## Running the Project

Start the server with a port number:

```bash
python server.py 5000
```

In a separate terminal, start a client and connect to the server:

```bash
python client.py localhost 5000
```

To test multiple users, open additional terminals and run the client command again.

## Example Commands

```text
JOIN alex
LIST
BCST hello everyone
MESG username private message
QUIT
```

## Notes

This was built as a class project to practice network programming fundamentals with Python sockets. It is intended as a learning-focused implementation rather than a production chat system.
