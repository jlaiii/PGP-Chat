# PGP Chat+: Truly Private, End-to-End Encrypted Chat

## Live Website

You can use the live version of PGP Chat+ directly here:
**https://jlaiii.github.io/PGP-Chat/**

---

## The Genesis: A Quest for Uncompromised Privacy 🕵️‍♀️

In a world where digital privacy is increasingly scrutinized, I sought a communication platform that offered a **true end-to-end encrypted (E2EE) chat experience**. Many existing solutions, while claiming strong encryption, often rely on centralized servers that could potentially log metadata, or worse, have backdoors. My primary concern was simple: if I'm having a private conversation, I want absolute assurance that **only the intended recipients can read it**, and that no third party, not even the service provider, can access its content.

This led me to build **PGP Chat+**. I didn't want to trust anyone else with my privacy, so I built it myself. This project is a straightforward, browser-based chat application leveraging **Gun.js for decentralized data storage** and **OpenPGP.js for robust cryptographic operations**. It's designed for those who demand the highest level of privacy in their casual conversations.

---

## Why PGP? The Power Behind Your Privacy 🔐

PGP (Pretty Good Privacy) isn't just a buzzword; it's a robust cryptographic standard that has stood the test of time for decades. It's the reason your messages in PGP Chat+ are truly private.

### How PGP Works (The Simple Version)

Imagine you want to send a secret message to a friend, Alice.

1.  **Keys, Not Locks:** Both you and Alice have two unique "keys":
    * **Public Key:** Think of this as an open padlock. You give this padlock to anyone you want to receive a secret message *from*. It can only lock messages, not unlock them.
    * **Private Key:** This is the *only* key that can open your specific public padlock. You keep this key absolutely secret and never share it.

2.  **Sending a Secret:**
    * You get Alice's public key (her open padlock).
    * You write your message and "lock" it using Alice's public key.
    * Now, only Alice's *private* key can open this message.

3.  **Alice Reads:**
    * Alice receives the locked message.
    * She uses her secret private key to "unlock" and read it.

Even if someone intercepts the locked message, without Alice's private key, it's just scrambled nonsense.

**In PGP Chat+:** When you send a message, it's locked using the public keys of *all selected participants* (including your own, so you can read your sent messages). This ensures that only those with the corresponding private keys can decrypt and understand the conversation.

### Real-World Security: The Strength of PGP

PGP encryption, especially with 2048-bit or 4096-bit RSA keys (which PGP Chat+ uses 2048-bit), is **exceptionally strong**.

* **Computational Impossibility:** Cracking a strong PGP encryption without the private key isn't just difficult; it's currently considered **computationally impossible** with existing technology. It would take quadrillions of years for even the most powerful supercomputers or vast networks of computers to guess the correct key.
* **Government Agencies & Law Enforcement:** There are numerous anecdotal and documented cases where law enforcement agencies, including the FBI and other intelligence services, have been unable to crack PGP-encrypted data. This isn't due to a lack of resources or expertise, but simply because the math behind the encryption makes it practically unbreakable. They often resort to other methods (like compromising the endpoint device with malware) rather than trying to brute-force the encryption itself.
* **The "Rubber Hose Cryptanalysis":** As famously quipped by Phil Zimmermann, the creator of PGP, the easiest way to get a PGP key is "with a rubber hose" – meaning, physical coercion. This grim humor highlights that the encryption itself is so robust that human vulnerabilities (like a compromised device or a user coerced into revealing their key) are typically the only practical weaknesses, not the cryptographic algorithm itself.

PGP provides a digital fortress for your communications, designed to protect your privacy even from determined adversaries.

---

## How It Works: Simple, Secure, Decentralized Magic ✨

PGP Chat+ creates **private, ephemeral chat rooms** where every message is encrypted using PGP (Pretty Good Privacy) standards. Here's a deeper dive into the magic behind the privacy:

1.  **Your Personal Crypto-Identity (PGP Keys) 🔑:**
    * The moment you open PGP Chat+ or join/create a room, your browser instantly generates a unique PGP key pair *right on your device*. This pair consists of a `public key` (which you share with others) and a `private key` (which you keep absolutely secret).
    * **Crucially, your private key never leaves your browser.** It's the digital "unlock code" for messages encrypted specifically for you.

2.  **Joining the Conversation (Key Exchange) 🤝:**
    * When you enter a room, your browser broadcasts your public key to the other participants in that room via the decentralized Gun.js network.
    * Simultaneously, you receive the public keys of everyone else in the room. This behind-the-scenes handshake ensures everyone has the necessary "locks" to encrypt messages for each other.
    * There are no intrusive "Public key received from..." messages cluttering your chat; it all happens silently in the background!

3.  **Sending a Secret Message (Encryption) 🔒:**
    * When you type a message and hit send, your browser takes your plaintext message (e.g., "Hello, privacy!").
    * It then encrypts this message using *all* the public keys it has for the selected recipients in the room (including your own public key, so you can always read your sent messages!).
    * This multi-recipient encryption creates a single, scrambled, unreadable blob of data.

4.  **Decentralized Delivery (Gun.js) 🌐:**
    * Instead of sending this encrypted blob to a central server, your browser pushes it onto the Gun.js decentralized network, associated with your specific room ID.
    * This data then propagates across the network to all connected peers and relay servers. Think of it like shouting a highly-encrypted message into a public square – everyone hears it, but only those with the right keys can understand it.

5.  **Reading a Secret Message (Decryption) 🔓:**
    * When your browser receives an encrypted message from the Gun.js network, it immediately tries to decrypt it using your **private PGP key**.
    * If successful, the readable message appears in your chat. If decryption fails (e.g., the message wasn't intended for you, or your keys aren't aligned), the message remains unreadable and is not displayed, ensuring only relevant, decrypted content reaches your eyes.

In essence, PGP Chat+ provides a secure "digital envelope" for every message, sealed with multiple locks (one for each recipient's public key), and then sent across a public, decentralized messenger service. Only those with the matching "keys" (their private PGP keys) can open their specific lock and read the message.

---

## Message & Server Hosting Explained

PGP Chat+ uses a decentralized database called **Gun.js**. This means:

* **No Central Message Server:** Unlike traditional chat applications, there isn't one central server that permanently stores all your messages.
* **Peer-to-Peer Storage:** When you send a message, it's propagated across the Gun.js network to all connected peers (other browsers, dedicated Gun.js relay servers). Each peer that receives the data will store a local copy.
* **Relay Servers for Persistence:** To ensure wider availability and persistence even when participants are offline, this application connects to public Gun.js relay servers (like `https://gun-manhattan.herokuapp.com/gun`). These relays typically store data to disk and keep it available.
* **High Persistence:** Messages sent through this network are generally highly persistent. They will remain accessible for a very long time as long as there is at least one active Gun.js relay server or peer holding that data. There is no automatic "time-to-live" or deletion mechanism built into Gun.js itself for this data.
* **Your Privacy Shield: PGP Encryption:** Because messages are highly persistent on the decentralized network, your privacy is **solely dependent on the strength of the PGP end-to-end encryption**. Even if someone accesses the raw data on a Gun.js relay, they cannot read your messages without the corresponding private PGP keys.

---

## Features ✨

* **True End-to-End Encryption:** Messages are encrypted in your browser and can only be decrypted by the intended recipients using their private PGP keys. 🔒
* **Private Rooms:** Each room is uniquely identified by a **Room ID**, acting as a shared secret to enter. 🚪
* **Decentralized:** Built on Gun.js, providing robust, peer-to-peer data synchronization without a central server. 🌐
* **Automatic PGP Key Generation:** Your PGP keys are generated instantly in your browser when you enter a room – no setup required! 🚀
* **Random Room ID Length:** Room IDs are generated with a random length between 16 and 20 characters to enhance unpredictability. 🎲
* **Simple Participant Management:** Easily see who's in the room and select who to encrypt your messages for. 👋
* **"Show Raw Chat" Toggle:** For advanced users, view the encrypted data as it exists on the decentralized network, confirming the encryption. 🕵️‍♂️
* **Ephemeral Nature (from a user's perspective if Room ID is lost):** While Gun.js data persists, the *privacy* is tied to the room ID and shared keys. If you lose the room ID or the participants leave, the conversation effectively vanishes *for you*, as you can no longer access that specific data stream. 👻
* **Mobile-Friendly Design:** The application is designed to look and work great on both desktop and mobile browsers, adapting fluidly to different screen sizes. 📱💻

---

## Disclaimers & Important Considerations ⚠️

**While PGP Chat+ offers strong cryptographic protection, it's crucial to understand its limitations and your responsibilities:**

* **Your Device's Security is Paramount:** The strength of PGP Chat+ hinges on the security of your device. If your computer or phone is infected with malware, spyware, or a virus, your PGP keys could be compromised *before* encryption or *after* decryption, rendering the encryption useless. **Always ensure your device is clean and secure.** 🛡️
* **Room ID is the Shared Secret:** The **Room ID acts as the primary key to access a conversation's data stream.** Share it **only with trusted individuals.** If someone gets hold of your Room ID, they can see the encrypted messages. 🤫
* **Key Exchange is Crucial:** For secure communication, all participants must correctly exchange their public PGP keys. While the application attempts to automate this, if a participant's key is not correctly received or used, encryption for that recipient may fail. 🔑❌
* **No Message History Persistence (for new joiners):** Due to the E2EE design, users who join a room *after* messages have been sent will *not* be able to decrypt past messages, as they wouldn't have had the necessary public keys at the time of encryption. ⏳
* **No User Accounts:** There are no user accounts, passwords, or persistent identities. Your username is randomly generated each time, promoting anonymity but also meaning you must share your Room ID to re-enter a specific conversation. 👤
* **Experimental Nature:** This project is for educational and experimental purposes. While it implements standard PGP encryption, it has not undergone formal security audits. Use at your own discretion for sensitive communications. 🧪

---

## Getting Started 🚀

1.  **Open the live website URL** in your web browser.
2.  Your browser will automatically generate a random username and PGP keys, and create a new private room.
3.  **Copy the Room ID** from the "Room ID" display.
4.  **Share the Room ID** with your friends. They simply paste it into their "Enter Room ID" field and click "Join Room."
5.  Once other participants join, their public keys will be exchanged, and you can begin sending encrypted messages! 🎉
