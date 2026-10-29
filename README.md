# Multicast Chat

A small command-line group chat written in Java. Participants join the same IP multicast group and UDP port to exchange messages directly; there is no central chat server.

## How It Works

Each participant runs the application, enters a display name, and sends messages to the configured multicast group. A background thread listens for incoming datagrams and prints messages from other participants. Messages sent by the local participant are filtered out. Type `Exit` to leave the group and close the application.

The project contains two Java source files:

- `MulticastChat.java` starts the chat, joins the multicast group, reads user input, and sends messages.
- `ReadThread.java` receives and displays messages in a separate thread.

## Requirements

- Java Development Kit (JDK)
- A network interface and network that support IP multicast

## Build and Run

From the project directory, compile both source files:

```bash
javac -d out MulticastChat.java ReadThread.java
```

Run the application with a multicast group address and UDP port:

```bash
java -cp out multicastchat.MulticastChat <multicast-group> <port>
```

For example:

```bash
java -cp out multicastchat.MulticastChat 239.1.2.3 5000
```

Start another instance using the same group address and port to join the same chat. The group address must be in the IPv4 multicast range (`224.0.0.0`–`239.255.255.255`), and the chosen UDP port must be available. Network configuration and firewalls must allow multicast traffic.

## Network Scope

The current implementation sets the multicast time-to-live (TTL) to `0`. As a result, packets are limited to the local host and will not be forwarded to other machines. To chat across computers, the TTL and network multicast configuration need to be adjusted.

## Author

[Ana Athayde](https://github.com/ana-athayde)
