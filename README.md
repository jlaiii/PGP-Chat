# PGP Chat+

PGP Chat+ is a web-based, end-to-end encrypted group chat app built with privacy and decentralization in mind. It uses [OpenPGP.js](https://openpgpjs.org/) for strong encryption and [GUN](https://gun.eco/) for decentralized, peer-to-peer data synchronization.

## Features

- End-to-end encrypted messaging
- Decentralized backend with no central server
- Automatic per-user PGP key generation in the browser
- Keys stored in RAM only (wiped on refresh or close)
- Room-based chats with copy/share Room ID
- Optional "Raw View" to see encrypted messages
- Mobile-friendly and responsive design

## How It Works

### PGP Key Handling

- Each time a user opens the app, a new PGP keypair is generated in the browser using `openpgp.js`.
- **Private keys are never saved to disk or cloud.**
- All keys are stored **only in RAM**, meaning they are automatically deleted when the browser is refreshed or closed.
- This ensures that no sensitive cryptographic data is left behind—similar to how **Mullvad VPN uses RAM-only servers** for privacy.

### Message Storage

- Messages are encrypted using OpenPGP before being sent.
- The encrypted messages are stored in a decentralized GUN database.
- Messages are **never readable** by the server or any third-party, only by recipients with the correct private key.
- The raw encrypted data can optionally be viewed for transparency/debugging.

## Technologies Used

- HTML, CSS, JavaScript
- [GUN.js](https://gun.eco/) for decentralized data sync
- [OpenPGP.js](https://github.com/openpgpjs/openpgpjs) for encryption
- Google Fonts (Inter)

## Usage Instructions

1. Open the app in your browser.
2. Enter or share a unique Room ID to create or join a private room.
3. Begin chatting. Messages will be encrypted and sent securely.
4. Share the Room ID with others to invite them to the conversation.

## Live Demo

Try it here: [https://github.com/jlaiii/PGP-Chat](https://github.com/jlaiii/PGP-Chat)
