# h4 Feed me[^1]

## x) Why would you want to use a feed reader (and RSS/Atom)? 
  *	It is systematic and stabile way to organize news feeds from various sources
  * It is free of personalised content algorithms and post filtering that most media platforms utilize in their services
  * It is standardized and mature platform that renders all information in a similar format for easy reading
  * It can be moved between a variety of platforms without an issue and its compatibility makes is future-proof
  
    Info gathered from RSS app guides[^4]

## y) Supreme court of Finland, case Osuuspankkikeskus [^2]
  * In November 1998, a 17-year-old (named A) used a scanning program to systematically scan all IP addresses on the internet-facing network of Osuuspankkikeskus-OPK
  * A argued that port scanning was just to check for open services and does not forcibly "break" a security mechanism. The Supreme Court rejected this, ruling that systematic vulnerability/port scanning is designed to map weaknesses that enable unauthorized entry. 
  * Using such port-scanning tools against third-party networks without authorization crosses the threshold into an attempted data break-in even before an exploit is launched or a firewall is penetrated.
  * For security practitioners, explicit scope and written authorization are mandatory before conducting any external reconnaissance or penetration testing.
  * He was convicted of attempted data break-in and ordered A to pay a total of 75 000 mk.

## a) Install a feed reader
  * Installed Feedbro Firefox-extension (available at: https://addons.mozilla.org/en-US/firefox/addon/feedbroreader/). It seemed like a popular option amongst Firefox users. It is also available in Chrome.
    
    [Screenshot of Feedbro installation]
    <img width="1387" height="383" alt="Feedbro install" src="https://github.com/user-attachments/assets/1f6d00e2-78c6-4d44-ae01-02930f8a9db7" />

    [Screenshot of Feedbro RSS feed on full screen]
    <img width="1713" height="909" alt="Fullview of Feedbro RSS feed" src="https://github.com/user-attachments/assets/dcc437b8-d338-4128-b1f2-bc6e63b49f8d" />

    There are a couple of different view modes in the extension. One is the above screenshot, other is straight from the browser-extension button. This shouws the latest news from selected sources based on upload time.

## b) Add the feed for Krebs. https://krebsonsecurity.com/feed/
  * Krebs added

    [Screenshot of the Krebs RSS feed in Feedbro]
    <img width="1489" height="447" alt="Krebs in Feedbro" src="https://github.com/user-attachments/assets/0cdb911d-560d-4269-b218-251aafd07b23" />

## c) Add a feed for Schneier on Security

  Found the Schneier on Security by googling. It was easy to add the feed from the website. Just copy the link from the RSS-icon on a website to add it easily to a feed reader.

  [Screenshot of the Schneier on Secuirty page with the RSS feed-icon]
  <img width="1055" height="437" alt="Schneier on security RSS feed" src="https://github.com/user-attachments/assets/e95a1846-1e0a-489e-83a2-907451809120" />

  It is very simple to use Feedbro and add RSS feed. Simply navigate to the top left corner with the RSS feed-icon. Click it and then put the URL of the RSS feed. You need to add a name for the feed before it can be set up. 

  [Screenshot of the Feedbro extension view]
  <img width="1324" height="731" alt="adding RSS feed in Feedbro" src="https://github.com/user-attachments/assets/750daa8e-8433-4ba9-8d52-5977cd512d97" />

## d) Find and add two more security related feeds
  * Found two more RSS feed on a blog post from FeedSpot: Top 100 Cyber Security RSS Feeds in 2026.[^5] They had the Krebs for security listed as number one so at least seems like a somewhat reliable top-list. I googled security related RSS feeds.
    * At first added Wired-RSS feed (https://www.wired.com/feed/rss), because it is already familiar to me from other news-topics (technology etc.) Unfortunately, the feed contained ads(!) and overall, just a lot of fluff that I found unnecessary.
      * Not a great look for Wired or the blog post!
      * It also filled the extension window completely, with no other feeds on it. Maybe this could be customized a bit but it was already game over at this point and I removed the feed. 
    * In the end I added The Hacker news RSS feed (https://feeds.feedburner.com/TheHackersNews?format=xml) and Dark Reading RSS Feed (https://www.darkreading.com/rss.xml), because they seemed interesting.

## e) Follow security feeds for a while
  * When feeds are selected carefully and based on actual interests, it really takes the fluff out (for the most part).
  * My normal methods of following the scenes include personalized feed from social media apps and manual browsing between different technology related websites. Compared to that, RSS feed is vastly superior in regards to actually getting the info that is relevant.
  * My selected RSS feed-reader was also quite good. However, the preview window in Feedbro is quite unuseful since it organizes the feed based on publication time. Some feeds simply do not put out that much info to be visible on the preview all the time.
    * You really need to browse the specified RSS feed separately or go to the full view of the extension for a better experience.

## f) Port scan

I installed nmap and apache2 with the following commands:

```bash
sudo apt-get update
sudo apt-get -y install nmap apache2
```

I deviated a bit from the provided intructions with help from Gemini 4 Argon AI-model. It made the setup a bit simpler and easier to follow.

I installed both right away so I didn't need to disconnect the VM from the internet twice. Since Debian usually starts the daemon automatically, next stop was to stop the Apache2 with a command:
```bash
sudo systemctl stop apache2
```

I then proceeded to check that the service was down with this command:
```bash
sudo systemctl status apache2
```
[Screenshot of inactive Apache2]
<img width="1280" height="800" alt="Apache2 inactive (dead)" src="https://github.com/user-attachments/assets/96b68e7e-dbb7-4b17-b0b9-9427094ee548" />

The above screenshot proves that Apache2 was indeed “dead”. I then pressed “q” to get back to the normal command prompt. I did all of this to avoid needing to disconnect from the internet twice i.e. first for the port scan without a daemon and then with it active.

After this I disconnect from the internet (the VM only) to do the ping-test using command:
```bash
ping -c 4 8.8.8.8 
```
The -c 4 -command specifies to send for ping packets before stopping automatically. 

[Screenshot of failed ping-command]
<img width="1280" height="800" alt="Ping 8 8 8 8 failed proof" src="https://github.com/user-attachments/assets/88e94739-8227-47ff-a1e2-e8e986a404cd" />

The above screenshot also shows that the internet is indeed disconnected on the VM (upper-right corner).

Next, I ran the command:
```bash
sudo nmap -A -v localhost
```

[Screenshot of port scan without Apache2 active]
<img width="1280" height="800" alt="Portscanning localhost without Apache2 and no internet" src="https://github.com/user-attachments/assets/cadaf54a-bfcf-45be-bc65-2bd983cb5ca3" />

And got the following info. It can be seen from the screenshot that the internet is disconnected (upper right corner) and the only open port out of the 1000 scanned TCP ports was port 631 (CUPS), which is Debian’s default local printing daemon. Port 80, which is used by Apache, was not open.

I restarted the Apache2 with the following command:
```bash
sudo systemctl start apache2
```
I then ran the port scan again and got the following result.

[Screenshot of port scan with Apache2 active]
<img width="1280" height="800" alt="Portscanning localhost with Apache2 on but still no internet connection" src="https://github.com/user-attachments/assets/c792705c-1ced-489f-be4f-051828e9012c" />

Now, instead of only one open port, there are two: 631 (the same) and a new one (80). Comparing the two scans shows that starting a background daemon (apache2) immediately opens a listening network port (80/tcp). 

Criminals can use port scanners like nmap against a company's public IP addresses to discover not only which ports are open, but also the exact software product, version number (Apache 2.4.71), and operating system (Debian) running on the server. With that exact version number, an attacker can search vulnerability databases (CVEs) for known exploits targeting that specific version

On top of using the provided tips from Tero Karvinen's website[^1], this section was done with help of Gemini 4 Argon AI-model and Manish Shivanandhan's article[^3].

## References
[^1]: Karvinen, T. 2026. Cyber Security - 2026 late autumn - ICB705AS3YE-2 +cy2. Available: https://terokarvinen.com/cyber-security/. Accessed: 15 November 2026.
[^2]: Korkein oikeus 2003. Ennakkopäätös KKO:2003:36. Finlex. Available: https://www.finlex.fi/fi/oikeuskaytanto/korkein-oikeus/ennakkopaatokset/2003/36. Accessed: 15 November 2026.
[^3]: Shivanandhan, M. 2020. What is Nmap and How to Use it – A Tutorial for the Greatest Scanning Tool of All Time. freeCodeCamp. Available: https://www.freecodecamp.org/news/what-is-nmap-and-how-to-use-it-a-tutorial-for-the-greatest-scanning-tool-of-all-time/. Accessed: 15 November 2026.
[^4]: RSS.app 2026. Why Use RSS in 2026? Available: https://rss.app/guides/what-is-rss/why-use-rss. Accessed: 15 November 2026.
[^5]: FeedSpot 2026. Top 100 Cyber Security RSS Feeds in 2026. Available: https://rss.feedspot.com/cyber_security_rss_feeds/. Accessed: 15 November 2026.
