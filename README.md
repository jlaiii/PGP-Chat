# PGP Chat+: Truly Private, End-to-End Encrypted Chat

## Live Website

You can use the live version of PGP Chat+ directly here:
**[Live Website URL Here]** (Remember to replace this with your actual GitHub Pages URL!)

---

## The Genesis: A Quest for Uncompromised Privacy

In a world where digital privacy is increasingly scrutinized, I sought a communication platform that offered a **true end-to-end encrypted (E2EE) chat experience**. Many existing solutions, while claiming strong encryption, often rely on centralized servers that could potentially log metadata, or worse, have backdoors. My primary concern was simple: if I'm having a private conversation, I want absolute assurance that **only the intended recipients can read it**, and that no third party, not even the service provider, can access its content.

This led me to build **PGP Chat+**. I didn't want to trust anyone else with my privacy, so I built it myself. This project is a straightforward, browser-based chat application leveraging **Gun.js for decentralized data storage** and **OpenPGP.js for robust cryptographic operations**. It's designed for those who demand the highest level of privacy in their casual conversations.

## How It Works: Simple, Secure, Decentralized

PGP Chat+ creates **private, ephemeral chat rooms** where every message is encrypted using PGP (Pretty Good Privacy) standards.

* **PGP End-to-End Encryption:** When you join or create a room, your browser generates a unique PGP key pair. Messages are then encrypted using the public keys of all participants in the room, ensuring that only those with the corresponding private keys can decrypt and read them.
* **Decentralized Data Storage (Gun.js):** Instead of relying on a single, vulnerable central server, messages are stored and synchronized across a decentralized network using Gun.js. This means your conversations aren't held in one place, making them resilient to single points of failure.
* **Browser-Based:** Everything runs directly in your web browser. No complex installations, no accounts, just pure PGP encryption at your fingertips.

## Message & Server Hosting Explained

PGP Chat+ uses a decentralized database called **Gun.js**. This means:

* **No Central Message Server:** Unlike traditional chat applications, there isn't one central server that permanently stores all your messages.
* **Peer-to-Peer Storage:** When you send a message, it's propagated across the Gun.js network to all connected peers (other browsers, dedicated Gun.js relay servers). Each peer that receives the data will store a local copy.
* **Relay Servers for Persistence:** To ensure wider availability and persistence even when participants are offline, this application connects to public Gun.js relay servers (like `https://gun-manhattan.herokuapp.com/gun`). These relays typically store data to disk and keep it available.
* **High Persistence:** Messages sent through this network are generally highly persistent. They will remain accessible for a very long time as long as there is at least one active Gun.js relay server or peer holding that data. There is no automatic "time-to-live" or deletion mechanism built into Gun.js itself for this data.
* **Your Privacy Shield: PGP Encryption:** Because messages are highly persistent on the decentralized network, your privacy is **solely dependent on the strength of the PGP end-to-end encryption**. Even if someone accesses the raw data on a Gun.js relay, they cannot read your messages without the corresponding private PGP keys.

## Features

* **True End-to-End Encryption:** Messages are encrypted in your browser and can only be decrypted by the intended recipients using their private PGP keys.
* **Private Rooms:** Each room is uniquely identified by a Room ID, acting as a shared secret to enter.
* **Decentralized:** Built on Gun.js, providing robust, peer-to-peer data synchronization without a central server.
* **Automatic PGP Key Generation:** Your PGP keys are generated instantly in your browser when you enter a room.
* **Simple Participant Management:** Easily see who's in the room and select who to encrypt your messages for.
* **"Show Raw Chat" Toggle:** For advanced users, view the encrypted data as it exists on the decentralized network, confirming the encryption.
* **Ephemeral Nature (from a user's perspective if Room ID is lost):** While Gun.js data persists, the *privacy* is tied to the room ID and shared keys. If you lose the room ID or the participants leave, the conversation effectively vanishes *for you*, as you can no longer access that specific data stream.

## Disclaimers & Important Considerations

**While PGP Chat+ offers strong cryptographic protection, it's crucial to understand its limitations and your responsibilities:**

* **Your Device's Security is Paramount:** The strength of PGP Chat+ hinges on the security of your device. If your computer or phone is infected with malware, spyware, or a virus, your PGP keys could be compromised *before* encryption or *after* decryption, rendering the encryption useless. **Always ensure your device is clean and secure.**
* **Room ID is the Shared Secret:** The **Room ID acts as the primary key to access a conversation's data stream.** Share it **only with trusted individuals.** If someone gets hold of your Room ID, they can see the encrypted messages.
* **Key Exchange is Crucial:** For secure communication, all participants must correctly exchange their public PGP keys. While the application attempts to automate this, if a participant's key is not correctly received or used, encryption for that recipient may fail.
* **No Message History Persistence (for new joiners):** Due to the E2EE design, users who join a room *after* messages have been sent will *not* be able to decrypt past messages, as they wouldn't have had the necessary public keys at the time of encryption.
* **No User Accounts:** There are no user accounts, passwords, or persistent identities. Your username is randomly generated each time, promoting anonymity but also meaning you must share your Room ID to re-enter a specific conversation.
* **Experimental Nature:** This project is for educational and experimental purposes. While it implements standard PGP encryption, it has not undergone formal security audits. Use at your own discretion for sensitive communications.

## Getting Started

1.  **Open the live website URL** in your web browser.
2.  Your browser will automatically generate a random username and PGP keys, and create a new private room.
3.  **Copy the Room ID** from the "Room ID" display.
4.  **Share the Room ID** with your friends. They simply paste it into their "Enter Room ID" field and click "Join Room."
5.  Once other participants join, their public keys will be exchanged, and you can begin sending encrypted messages!
