# PGP Chat+

PGP Chat+ is a web-based, end-to-end encrypted group chat application. It uses [OpenPGP.js](https://openpgpjs.org/) for encryption and [GUN](https://gun.eco/) for decentralized data synchronization. Messages are encrypted with PGP keys before being shared, and only participants with the correct keys can decrypt the content.

## Features

- End-to-end encrypted messaging
- Decentralized backend via GUN
- Automatic key generation per user
- Room-based chat with shareable Room ID
- Toggle to view raw encrypted messages
- Option to auto-add new users for encryption
- Responsive and clean UI design

## Technologies Used

- HTML/CSS/JavaScript
- [GUN.js](https://gun.eco/)
- [OpenPGP.js](https://github.com/openpgpjs/openpgpjs)
- Google Fonts (Inter)

## How to Use

1. Open the web app in your browser.
2. Enter a unique Room ID to join or create a private chat room.
3. Share the Room ID with others to invite them.
4. Start chatting securely.

## Security Notes

- All messages are encrypted using PGP before being sent.
- Only users with the proper keys can decrypt the messages.
- No server stores messages in plain text.

## Live Demo

You can try it here: [https://github.com/jlaiii/PGP-Chat](https://github.com/jlaiii/PGP-Chat)
