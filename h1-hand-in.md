# h1 CyberScience homework

## a) Science hunt

I chose to review an article titled: The Evolution of Phishing and Future Directions: A Review[^1]. The publication that it has been released in has a JUFO ID 86562 and is rated at level 1. The article already has 27 citations as of the date that I reviewed it (25th of October 2026). I think phishing emails, phone calls etc. are things that we all know about, either through personal experiences or have heard through friends and family. That is what motivated me to look up review articles on the topic.

## b) Review of the review[^1]

  * _What are the key areas being researched?_
    
    It discusses and analyzes the past and current landscape of phishing attacks, especially focusing on the rise of AI and machine learning tactics used for these phishing scams.      The advancement of AI has enabled many new and sophisticated ways of setting up different kinds of phishing attacks. Nowadays it is also possible to buy these services,             described as "Phishing-as-a-service". The review aims to evaluate the impcat of technological advancements and how they might aid in the defence against theses new threats.

  * _What's widely agreed upon?_

    Phishing solutions are becoming increasingly more sophisticated. The only way for organizations and individuals to fight against these new methods is to use the same kind of        countermeasurements and defences that aid the attackers in crafting the phishing attacks. At the organization level, these include AI-powered detection-systems and more             advanced email-authentication mechanisms. At the individual level this means using multifactor authentication methods and overall vigilance when using services and opening          links. The human element cannot be overstated. More user education and training has to be a part of the organization's strategy, on top of using multifactorial countermeasure       tools as part of the defence infrastructure.
    
  * _What are the open questions?_

    The review didn't directly propose any open questions about the current phishing climate. Still, I think it is uncertain what kind of advancements might be around the corner        and what countermeasurements we are able to deploy. It really feels like a game of cat and mouse.

## c) Threat modeling quickrun

  * _Company_

    A major local bank
     
  * _Crown jewels_

    * Customers' money and personal data (income etc.)
    * Reputation and liquidity
    * Shareholders and stock price (if public company as most of them are)
   
  * _Bad guys - What do they want?_
    
    * Access to customers' money
      * Most likely through social engineering using different phishing solutions
    * To disrupt the normal operations of an organization
      * Through DDoS attacks or similar

  * _Two major risks_

    * Likelihood for a banking customer to fall victim to a phishing attack is quite small, but if every single banking customer has at some point received a phishing email, the          odds do stack up. Lets imagine a major bank with 20 million customers. If the likelihood of a successful attempt is only a mere 0,0001%, but every single customer has been          targeted at least once, it becomes purely a numbers' game. The likelihood is a mere cenrtainty and with that calculation becomes 2000, meaning it will happen to at least 2000       people. We can multiply the likelihood with the impact per customer. Let's say each customer is worth 5000$ on average. That gives us the estimated value of 2000 * 5000$ = 10       000 000$.
    * Another major risk for a bank is DDoS attacks or other incidents affecting operations that limit the bank's ability to serve its customers. This also impacts the wellbeing of       its workers (especially the once dealing with customers). This can have major financial impacts on the bank if it happens often and these circumtances last for a long time.         This one is harder to put into numbers but the likelihood is almost certainly 100% and impact can range from low to critical. We are probably talking about an estimated value       of tens of millions of dollars yearly.

  * _What shall we do with that one biggest risk?_

    * Better DDoS protections and firewalls (mitigate)
    * Modernize the core architecture and try to find and eliminate zero-point failures (eliminate)
    * Make sure service level agreements with vendors are up to date and regularly checked (transfer)
    * If possible, purchase separate cyber insurance that covers major outages (transfer)
    * Regularly perform recovery drills with critical personnel and with staff (accept)


## References
[^1]: Osamor, J., Ashawa, M., Shahrabi, A., Phillip, A. and Iwend, C., 2025, March. The evolution of phishing and future directions: A review. In International Conference on Cyber Warfare and Security (pp. 361-368). Academic Conferences International Limited. Available at: https://doi.org/10.34190/iccws.20.1.3366 (Accessed: 25 October 2026).

