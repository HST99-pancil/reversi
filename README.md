# Big Cat Reversi

Reversi (Othello) for the browser. A panther and a snow leopard take the two
sides: whoever's turn it is sits up alert, the other one dozes, and taking a
corner gets a roar.

Play it at **https://hst99-pancil.github.io/reversi/**

## Three ways to play

**Computer** — you are the Panther against a snow leopard that searches ahead
with alpha-beta. The difficulty setting is simply how far it looks: two, three,
or four moves. There is a coach that explains what each move did, an undo, and a
hint that highlights a square and says why.

**Online** — one player creates a table and gets a five-character code. The other
enters that code. The two browsers then talk directly over a WebRTC data channel,
so moves appear on both screens as they are played. There is no server holding the
game and nothing is stored anywhere; the game lives only in the two open tabs.

**By code** — for when a network blocks the direct connection, or when you would
rather play slowly. Each move produces a 24-character code carrying the whole
position. Send it however you like, your opponent pastes it in, and plays back.

## How it is put together

A single `index.html` with no build step and no dependencies of its own. PeerJS is
loaded from a CDN and used only to find the other browser and open the data channel.

In online play the player who created the table owns the game state. The joiner
sends move intents and renders whatever comes back, and the host validates every
incoming move against the rules before applying it, so the two screens cannot
drift apart or be desynchronised by a malformed message.

## Running it locally

Open `index.html` in a browser. **Computer** and **By code** both work from a
`file://` page. **Online** needs an `https://` origin, which is why it is served
from GitHub Pages rather than opened as a file.
