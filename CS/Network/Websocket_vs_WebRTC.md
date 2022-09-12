# 💙 Websocket vs WebRTC

[ref 1](https://www.youtube.com/watch?v=H2SlMSWPfm0) , [ref2](https://www.youtube.com/watch?v=5EhsjtBE7I4)

---

## 1. Websocket :

- uses TCP protocol.
- it is a bidirectional protocol that is used in the client server communication.
- it is written as the followings : `ws://` or `wss://`
- it is a stateful protocol, meaning the connection between client and server is kept alive until terminated by either side.

<br>

## 2. WebRTC

- uses UDP protocol, thus the data transfer is faster, but relatively unstable.
- it is designed for high-performance & quality communication of video, audio, and arbitrary data.
- it is browser to browser communication (P2P), thus faster than the websocket.
- however, webRTC also utilize similar mechanism to that of websocket called `signaling mechanism` to connect peer to peer.

<br>

## 3. Conclusion

- In most cases, WebRTC is faster than Web socket.
- Both websocket and webRTC can be utilized, former being signal channel and the latter being a video & audio & text channel, to maximize advantages.
- Websocket alone isn't an ideal choice for streaming services.