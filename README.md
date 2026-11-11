# TCP Chat Server

## Setup

Requires GCC, make, cJSON, pthreads, and tmux.

Build:

```sh
make
```

Start the server:

```sh
./tcpserver
```

The server listens on port 8181.

## Same Wi-Fi

On the server PC, find its local IP address:

```sh
hostname -I
```

Allow TCP port 8181 through the server PC's firewall if needed:

```sh
sudo firewall-cmd --permanent --add-port=8181/tcp
sudo firewall-cmd --reload
```

Start `./tcpserver` on the server PC. On another PC connected to the same Wi-Fi, build or copy `chat-client`, then connect using the server PC's IP:

```sh
./chat-client <IP> 8181 taran
```

Replace `<IP>` with the IP shown by `hostname -I`. Usernames must be registered by the server, and both PCs must be able to reach each other on the network.

## Local Testing

In another terminal, start the client with a registered username:

```sh
./chat-client 127.0.0.1 8181 taran
```

Client commands:

```text
/chat <username>  Open a chat in a new tmux pane
/quit             Close the current chat pane
/ls               List users
/exit             Exit the client
```

Type normal text to send it to the selected chat. Messages are stored when the recipient is offline and shown when the chat is opened.

To attach to the tmux session later:

```sh
tmux attach -t tcp-chat-taran
```

Clean build files:

```sh
make clean
```

## References
https://mecha-mind.medium.com/

https://mecha-mind.medium.com/a-non-threaded-chat-server-in-c-53dadab8e8f3

https://craftinginterpreters.com/hash-tables.html

https://github.com/sheredom/hashmap.h
