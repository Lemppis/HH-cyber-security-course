# h3 Cyber lab[^4]



## x) Read and summarize

  * Heinonen 2026: How to Install Linux to Virtualbox?[^1]
    *	Preparations and installation: Ensuring hardware virtualization (VT-x/similar) is enabled in your BIOS/UEFI and downloading Oracle VirtualBox.
    *	Downloading the image: Acquiring the Debian live ISO image and understanding basic concepts like ISOs and Linux distributions.
    *	VM creation: Configuring the virtual machine's settings in VirtualBox (allocating RAM, CPUs etc., and setting up the virtual hard disk).
    *	OS Installation: Booting into the live environment, running the Calamares installer to complete the real installation, rebooting, and performing initial system updates (apt-get update and upgrade).

  * Karvinen 2020: Command Line Basics Revisited[^2]
    * Navigation: Moving around the filesystem (pwd, ls, cd, less).
    * File Handling: Creating, editing, moving, copying, and deleting files and folders (nano, mkdir, mv, cp).
    * Remote Access: Managing remote machines and transferring files securely (ssh, scp).
    * Help & Efficiency: Using manual pages (man) and autocomplete features (Tab key, command history).
    * System: Understanding key Linux directories (/home, /etc, /var/log).
    * Package Management: Installing, searching for, and removing software safely using administrator privileges (sudo apt-get).

  * Karvinen 2022: Cracking Passwords with Hashcat[^3]
    * Setting up: Installing hashcat, hashid, and downloading a standard wordlist (rockyou.txt).
    * Hash Identification: Using hashid to figure out the type of cryptographic hash and its corresponding Hashcat mode (e.g., -m 0 for MD5).
    * Cracking the Hash: Running Hashcat against the hash using the dictionary file to brute-force a match (hashcat -m 0 [hash] rockyou.txt -o solved).
    * Making it better: Checking the results, viewing output status, and understanding how to leverage hardware for faster cracking speeds.
    * Next steps: Try writing your own dictionaries, e.g. CFT (capture the Flag -game). 


 ## a) Reserve your presentation
 
 I have reserved a presentation title in [Laksu](https://app.terokarvinen.com/). Presentation title is: _Evaluating Multi-Factor Authentication: How it works and how it might break_. Presentation will be held on Wednesday 18th of November.


## b) Installing Linux (Debian 13-Trixie)[^1]


After downloading the Oracle VirtualBox and following the instructions[^1] on how to set up a new virtual machine, I did run into a problem when trying to boot up the system for the first time.

Screenshot 1: [Error pop-up when booting up the system for the first time]
<img width="1022" height="901" alt="Screenshot 2026-11-07 225825" src="https://github.com/user-attachments/assets/100607ce-ba32-424e-9526-1c776e41d8de" />

At first I had no idea what the problem could have been. After checking the instructions again I realized that I should have set up the operating system as a 64-bit system (since that is what the given ISO was also). By default the VirtualBox wanted to make a 32-bit version and that is what I had made initially. I then just changed this from the settings-menu and I was good to go.


Screenshot 2: [Debian installer (Calamares)]
<img width="1280" height="800" alt="Installation of Debian 13" src="https://github.com/user-attachments/assets/97149623-457d-4e9f-8dec-7eab96a92dd7" />

Screenshot 3: [Completed installation of Debian 13-Trixie]
<img width="1280" height="800" alt="Intallation of Debian complete" src="https://github.com/user-attachments/assets/ed6a97ce-2345-4b9c-a0ce-cfc24f1a9e95" />

Screenshot 4: [Using command line to install necessary updates and upgrades on a fresh Linux distribution]
<img width="1280" height="800" alt="Running update and upgrade commands" src="https://github.com/user-attachments/assets/f5771a5b-6bc6-4cb8-9597-39670357b7ac" />

## c) Crack the hash 6b1628b016dff46e6fa35684be6acc96[^3]

I used the command line to install the hashcat application and make a new directory for the solve using the instructions provided[^3]. After that I downloaded the required wordlists and analyzed the hash, as seen in the below screenshots.

Screenshot 1: [Retrieving wordlists]
<img width="1280" height="800" alt="Retrieving wordlists" src="https://github.com/user-attachments/assets/c1e7251c-9455-4ef1-97a6-3cac7e775fea" />

Screenshot 2: [Analyzing the hash]
<img width="1280" height="800" alt="Analyzing the hash" src="https://github.com/user-attachments/assets/5384ed22-fcb0-4984-81d7-8241374cab8b" />

Lastly, I ran the command to try to solve the hash with MD5 hash type. It worked and the hash was solved, as seen below.

Screenshot 3: [Hash solved, see the status as "cracked"]
<img width="1280" height="800" alt="Hash solved" src="https://github.com/user-attachments/assets/e2223c17-095b-4b61-be0a-1c6f79203335" />

Screenshot 4: [Locating the solved file]
<img width="1280" height="800" alt="Location of the document" src="https://github.com/user-attachments/assets/e6bd9050-e86b-4922-bfd7-0bd9274ec6f6" />







## References

[^1]:Heinonen, J. n.d. Module 1.md. GitHub. Available at: https://github.com/johannaheinonen/johanna-test-repo/blob/main/module_1.md. Accessed: 9 November 2026.
[^2]:Karvinen, T. 2020. Command line basics revisited. Available at: https://terokarvinen.com/2020/command-line-basics-revisited/. Accessed: 9 November 2026.
[^3]:Karvinen, T. 2022. Cracking passwords with Hashcat. Available at: https://terokarvinen.com/2022/cracking-passwords-with-hashcat/. Accessed: 9 November 2026.
[^4]:Karvinen, T. 2026. Cyber Security - 2026 late autumn. Available at: https://terokarvinen.com/cyber-security/. Accessed: 9 November 2026.
