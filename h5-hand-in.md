# h5 Alice and Bob[^7]

## x) Read and summarize
* € Schneier 2015: Applied Cryptography[^10]. Summary of Chapters 1.1 and 2.5
  * Explains how encryption (E) and decryption (D) work to secure messages (M: plaintext/cleartext)
  * Cryptography is also used to provide authentication, integrity and nonrepudiation
  * Cipher is a cryptographic algorithm that is used in encryption and decryption, and there are a lot of different algorithms and implementations
  * Keys are an essential part of cryptography that can be used in key-based algorithms in two main ways: symmetric and public-key (asymmetric)
  * Symmetric algorithms are much faster than asymmetric ones, which is why hybrid cryptosystems are useful – the session key is encrypted and decrypted using asymmetric algorithms (public/private keys), and the actual message is encrypted and decrypted with a symmetric algorithm using that session key
  * Describes Merkle's Puzzles: a key-exchange method where an eavesdropper has to do quadratically more work (n2) to find the shared key than the legitimate parties (n)

* Karvinen 2023: PGP - Send Encrypted and Signed Message - gpg[^6]
  * Explains how to use PGP with the Linux command-line tool GNU Privacy Guard (gpg) to send encrypted (confidential) and signed (verified, tamper-proof) messages over an untrusted network like the Internet
  * Demonstrates the workflow by simulating two users (Tero and Alice) on a single machine, using a separate restricted directory and --homedir . to give Alice an isolated keyring
  * Each user generates a keypair (gpg --gen-key) consisting of a secret key (kept private) and a public key (freely shared and exported as copy-pasteable ASCII text using --export --armor)
  * Both parties import each other's public keys (--import), verify the key fingerprints over a separate trusted channel (e.g., a phone call), and sign the keys (--sign-key) to mark them as fully trusted
  * To send a secret message, Alice encrypts the file with Tero's public key (--encrypt --recipient) so only Tero can decrypt it, and signs it with her own secret key (--sign) to prove her identity
  * Tero decrypts the received file with gpg --decrypt, which uses his secret key to reveal the plaintext and Alice's public key to verify the signature (Good signature)
  * Includes basic troubleshooting for gpg, such as resetting a stuck gpg-agent with killall gpg-agent and using gpg --fingerprint to verify imported keys and confirm which keyring is active

## a) Pubkey today

I use a smart card for work daily. It is a normal part of our work environment. It can be used to digitally sign documents and even logging into my work computer. The card is granted by Digi- ja väestötietovirasto (DVV). DVV uses the International Telecommunications Union’s (ITU) standard X.509 that is described in RFC 3647.[^12][^2][^1]

### How I have used it recently:
When I log in to my work Windows computer with a smart card, I am using Windows Smart Card Logon, which relies on Kerberos with PKINIT (Public Key Cryptography for Initial Authentication in Kerberos). Instead of using a password, Windows uses asymmetric (public-key) cryptography to prove your identity to your organization's network and then hands off to symmetric cryptography for the rest of my session.[^11]

### How the process works[^8][^9]:
* (User + Smart Card / Windows PC): The smart card holds the private key (permanently locked inside the chip and protected by PIN) and the public key (stored in an X.509 digital certificate).
* The Domain Controller / KDC (Key Distribution Center): My organization's authentication server (Active Directory). It has its own KDC private key and KDC public key (in its own server certificate)
* The Certificate Authority (CA): The trusted authority, in this case DVV has signed both, my certificate and the KDC's certificate using the CA's private key. My PC and the KDC have the CA's public key pre-installed.


## b) Encrypt and decrypt a message
I chose to install the gpg-software for Windows (gpg4win) from their website (https://www.gpg4win.org/download.html). I chose to skip the use of Linux VM for more simplified approach (for me). In general, I followed the same process as described by Karvinen in his Linux guide[^6], but without the need for command prompt. I chose to use Kleopatra, which acts as a graphical interface for the process. It is installed during the gpg4win installation (checked by default).

[Screenshot of gpg4win installation with Kleopatra]
<img width="868" height="675" alt="gpg4win installation" src="https://github.com/user-attachments/assets/aa21b1a2-6769-4be2-bae4-f0f484efc792" />

I used this guide[^3] to help with the Kleopatra software. I remembered that I used this software in my previous studies, but with time I had seemingly forgotten everything – time to learn again!

### In this example I used the classic Alice and Bob -pair. 
1. I opened Kleopatra and clicked File → New OpenPGP Key Pair. I did this for Alice and Bob. I used generic a “[firstname]@example.com” as the email address. I also protected the keys with a passphrase.

    [Screenshot of key-pair creation window]
    <img width="2091" height="1398" alt="Create key-pairs" src="https://github.com/user-attachments/assets/c1b39a3d-0319-41a4-84a7-b35b144ecf87" />

    [Screenshot of created key-pairs]
    <img width="1930" height="700" alt="Key pairs created" src="https://github.com/user-attachments/assets/2d2d9a6f-3ac7-4eeb-88f2-3bdbdc5ea39e" />


2. Then I clicked the Notepad button in the top toolbar and typed my secret message.

3. I typed in my very secret message and chose the appropriate sender and receiver on the right-hand side panel. I chose Alice as the sender (Sign as) and receiver as Bob (Encrypt for others). I unchecked the “Encrypt for others” because I want that only Bob can read the message. I also unchecked the “Encrypt with password” as this would negate the whole point, since this would give anyone with the right password access to the message content.

    [Screenshot of encryption process using Kleopatra]
    <img width="2308" height="1487" alt="Encrypting secret message" src="https://github.com/user-attachments/assets/bb3b8dbc-fc92-4a63-8971-61cf62a9629b" />

4. Immediately after I pressed the bottom right-hand corner “Sign / Encrypt”, the message became an unreadable PGP-message block. Actually, first I had to type in the passphrase that I had created earlier. After that the message became unreadable.

    [Screenshot of encrypted message]
    <img width="2318" height="1496" alt="Encrypted secret message" src="https://github.com/user-attachments/assets/bdf6cc27-3490-45e9-90e9-e2d89049e0ba" />


5. Right form this screen (with the PGP message block) I can also decrypt the message and verify Alice’s signature. In the bottom left-hand corner, there is a “Decrypt / Verify” option.
6. Pressing the “Decrypt/Verify” button reveals the original message again and the program shows a banner verifying that it is a valid signature from Alice.

    [Screenshot of decryption and verification]
    <img width="2322" height="1499" alt="Decryption and verification" src="https://github.com/user-attachments/assets/39aca812-aeca-4b10-abd8-ea3e30245ead" />

### How different parties use different keys at different stages of operation[^5]

1.	Key Generation (Alice & Bob): Each generates a Public Key + Private (Secret) Key. Creates each user's cryptographic identity. Private keys stay secret (protected by a passphrase, because I chose to make one); public keys are shared.
2.	Key Exchange & Trust (Alice & Bob): Alice's Private Key signs Bob's Public Key (and vice versa). After verifying fingerprints (40-character hex code) out-of-band (i.e. phone call, meeting in-person, other secure messaging platform), signing each other's public keys establishes trust that the key belongs to the right person.
3.	Encryption & Signing (Alice (Sender)): One-time Symmetric Session Key, Bob's Public Key, and Alice's Private Key. Under the hood, GPG encrypts the message with a fast random symmetric session key, encrypts that session key with Bob's public key (confidentiality), and signs the message with Alice's private key (authenticity & integrity).
4.	Decryption & Verification (Bob (Recipient)) Bob's Private Key, the Symmetric Session Key, and Alice's Public Key. GPG uses Bob's private key to unlock the symmetric session key and decrypt the message, then uses Alice's public key to verify her signature.

### Evaluating PGP and the tool chosen[^4]

OpenPGP (usually via GnuPG/gpg) is still widely used for signing software packages, Linux kernel releases (e.g., Debian, Ubuntu), as well as some encrypted email setups (like Thunderbird and Proton Mail). However, for everyday private messaging, almost nobody uses PGP anymore. Simple file encryption, many security engineers now prefer other methods, and for signing Git commits, SSH keys are increasingly used instead.

The biggest advantage of PGP seems to be that the algorithm for encryption is still unbreakable. In general use, that by itself is not enough to secure packages or messages. The program or processes of using PGP need to be understood, otherwise mistakes may happen. It may be too complicated for everyday users and people that are not that tech savvy. Even someone with a basic understanding of computers and software might struggle, even if presented with a graphical interface for PGP. It is no wonder then, that there are publicly available guides on how to use PGP/Kleopatra and others.

It is also worth noting that only the message content that is encrypted is “anonymous”. The services used to send the encrypted messages are still traceable and the subject line isn’t encrypted either. Also worth pointing out is that both the sender and receiver need to be using the same version of the software. Otherwise, the communication will not work.

## c) Password management

I have been using NordPass (nordpass.com) password manager for multiple years. It is available for most systems: Windows, MacOS, Linux, Android, iOS. I’ll be honest: I didn’t do a lot of research before choosing this password manager. I was already familiar with Nord Security’s software solutions and kind of accepted it as is.

It is also available for free, which begs the question – how do they make money? Usually, you are the product. Of course, paying for a service doesn’t guarantee that you aren’t treated the same way. However, I chose a plan that does cost a bit but also gives access to all the features. Below you can se a screenshot straight from their website (https://nordpass.com/plans/. taken on 23.11.2026). They are clearly quite aggressive with sales as well. That’s not necessarily a good thing either...

[Screenshot of Nordpass deals / 23.11.2026]
<img width="1911" height="1207" alt="Nordpass versions" src="https://github.com/user-attachments/assets/ca278639-cb32-4f21-bbca-b88641d2fb63" />


### Using Nordpass

Nordpass is available as a standalone software or as a browser extension. I use both solutions. I have the desktop application on my computer and the Firefox extension in browser. Obviously, I have the application installed on my phone as well. It recognizes most login screens that you might come across. There might be some setting up beforehand though. At least on Android, you must go into the settings and choose it as the main password manager. Otherwise, most logins will try to find the passwords from Google’s own password manager.

On firefox, you can type "about:addons" in the address bar and it takes you directly to the page where you can search for addons. Just type "nordpass" in the search and select the one shown below:

[Screenshot Nordpass browser extension installation]
<img width="1914" height="1653" alt="Firefox extension" src="https://github.com/user-attachments/assets/61802a5d-a782-47e7-b799-f02aafb4f21d" />


The different desktop versions of the app work in similar fashion, no matter what system you are running or what browser extension you have chosen. You can add new entries manually from the app (upper right-hand corner).

[Screenshot of Nordpass browser extension]
<img width="1914" height="591" alt="browser extension interface" src="https://github.com/user-attachments/assets/f8be90d8-6e6c-4d12-8100-54097fcb8336" />

If you are using the browser extension or the app on your phone, Nordpass automatically suggests adding login-info to the vault, so you don’t need to add them separately. If you just use the desktop app, you have to manually copy login info from the app.

### What kind of attacks take advantage of people not using password managers?

A few come to mind regarding the protection a password manager provides.

* Brute-force attacks: People usually have short and easily solvable (for computers) passwords.
* Phishing-attempts: Password managers usually have built-in features to prevent automatic fill on fake websites.
* Repeating passwords: If attacker gets a hold of one password, they usually have access to multiple services at once. Password managers make it easy to have unique passwords on every website.
* Nordpass also checks online for any leaked credentials and data breaches to services and compares them to your saved websites; if there is a match, it will let you know and provides steps to secure your account.


## References
[^1]: Chokhani, S., Ford, W., Sabett, R., Merrill, C. & Wu, S. November 2003. RFC 3647: Internet X.509 Public Key Infrastructure Certificate Policy and Certification Practices Framework. RFC Editor. URL: https://www.rfc-editor.org/info/rfc3647/. Accessed: 23 November 2026.
[^2]: Digi- ja väestötietovirasto (DVV) 17.6.2026. Varmennepolitiikka: Organisaatiovarmenne eIDAS v.1.7. URL: https://dvv.fi/documents/16079645/220291443/Varmennepolitiikka+Organisaatiovarmenne+eIDAS+v.1.7.pdf/989c84c1-69bc-fa18-c698-cf2fb3fe1da7?version=1.0&t=1789649026869. Accessed: 23 November 2026.
[^3]: Equifax 25 February 2021. Kleopatra - A PGP Tutorial. URL: https://assets.equifax.com/pgp/mft/external_Equifax_DXS_Kleopatra_PGP_Tutorial_v02252021.pdf. Accessed: 23 November 2026.
[^4]: Fortinet s.a. What is PGP Encryption? Pretty Good Privacy Explained. Fortinet Cyber Glossary. URL: https://www.fortinet.com/uk/resources/cyberglossary/pgp-encryption. Accessed: 23 November 2026.
[^5]: Free Software Foundation 1999. The GNU Privacy Handbook. GnuPG. URL: https://www.gnupg.org/gph/en/manual.html. Accessed: 23 November 2026.
[^6]: Karvinen, T. 2023. PGP - Send Encrypted and Signed Message - gpg. Tero Karvinen. URL: https://terokarvinen.com/2023/pgp-encrypt-sign-verify/. Accessed: 23 November 2026.
[^7]: Karvinen, T. 2026. Cyber Security - 2026 late autumn - ICB705AS3YE-2 +cy2. Tero Karvinen. URL: https://terokarvinen.com/cyber-security/. Accessed: 23 November 2026.
[^8]: Microsoft 3 June 2025. [MS-PKCA]: Interactive Logon Using Smart Cards. Microsoft Learn. URL: https://learn.microsoft.com/en-us/openspecs/windows_protocols/ms-pkca/53dd48a1-8325-4c0f-971f-d8c538d07f96. Accessed: 23 November 2026.
[^9]: Microsoft s.a. Smart Card Architecture. Microsoft Learn. URL: https://learn.microsoft.com/en-us/windows/security/identity-protection/smart-cards/smart-card-architecture?source=recommendations. Accessed: 23 November 2026.
[^10]: Schneier, B. 2015. Applied Cryptography: Protocols, Algorithms, and Source Code in C. 20th anniversary ed. John Wiley & Sons. URL: https://learning.oreilly.com/library/view/applied-cryptography-protocols/9781119096726/. Accessed: 23 November 2026.
[^11]: Rublon Authors 11 June 2026. Smart Card Authentication: What It Is And How It Works. Rublon Blog. URL: https://rublon.com/blog/smart-card-authentication/. Accessed: 23 November 2026.
[^12]: Sectigo Team 22 July 2026. What is an X.509 certificate? The X.509 standard explained. Sectigo Blog. URL: https://www.sectigo.com/blog/what-is-x509-certificate. Accessed: 23 November 2026.
[^13]: Townsend, K. 28 May 2025. How is PKI Used in Authentication? Securing Digital Identities in the Modern World. Intercede. URL: https://www.intercede.com/how-is-pki-used-in-authentication-securing-digital-identities-in-the-modern-world/. Accessed: 23 November 2026.
