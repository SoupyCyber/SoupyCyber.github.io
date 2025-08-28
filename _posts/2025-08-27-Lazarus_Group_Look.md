---
layout: post
title: "LinkedIn's Lurking Lazarus: Lethal Logic Behind Latest Lures"
subtitle: A 'kinda-good-at-CTI' Analysts (quick) look at Lazarus Group
tags: [posts]
author: Levi
---

## The Important Bits

Since mid-late 2022, the North Korea linked APT known as "Lazerus Group", has been engaging in sophisticated social engineering attacks via LinkedIn, targeting professionals across multiple industries, including - thats right, you guessed it - cybersecurity professionals. Leveraging things like fake job offers, coding tests, and recruiting lures, they've delivered info-stealers, backdoors and credential-harvesting malware that run 'cross-platform' (Think Windows/MacOS/Linux). These operations have given way to espionage opportunities, financial theft and network compromise, among other things. ¹ ² ³

### How the attack works

Lazarus grouip begins by crafting realistic and convincing LinkedIn personas, often posing as recruiters for well-known companies. The inital outreach by these "personas" typically highlights job opportunities or specialized roles within a variety of companies. Once contact is established, the adversary escalates the engagement via:

1. Resume & profile gathering: Victimes are encouraged to share personal details or GitHub links, giving lazarus intelligence on their targets technical background (good use of OSINT, bad guys).¹

2. Malware delivery via documents - Some of these campaigns weill send job offer PDFs or Word documents embedded with macros that will drop Lazarus' tools like "Manuscrypt." Queue credential theft and lateral movement!⁴

3. Malware-laced "coding tests": In some recent variants, vics are sent repos with timed "Coding challenges." When executed, they do a silent install of stealers that target browser creds and crypto wallets, among other things. They've built versions of this that will work on Windows, macOS and Linux.² ³

These techniques are particularly dangerous because they exploit that build in layer of trust we intrinsically have (or had) with LinkedIn, which historically has been regarded as a legitimate career platform. Some of us need jobs or are looking for jobs, so that desperation or lure of a lucrative job offer can pretty easily override suspicion.²


### Notable observations

- What are their 'Target Sectors'? Cryptocurrency exchanges, financial institutions, and technology/cybersecurity/development roles.¹²

- Notable Campaigns:
  - 2022–2023 “Operation In(ter)ception” — fake recruiters on LinkedIn distributing malware via job offers.¹
  - 2023–2024 Crypto developer campaigns — malware-laced coding tests targeting Windows/macOS/Linux.²³

- Cross-platform sophistication: Lazarus invests in multi-OS payloads, unusual for many threat actors.²³

- Attribution confidence: Multiple vendors (Bitdefender, Field Effect, CSO) tied the TTPs and malware families back to Lazarus with high confidence.¹ ² ³


### What to watch out for...

- Keep a weather eye for LinkedIn-based lures or emails referencing unsolicited job offers. Nobody just...gets job offers outta nowhere.

- Check repositories or code samples delivered to you outside of your normal workflows. Were you expecting to receive this? If not...check it twice.

- Setup monitoring on your Dev boxes for suspicious processes. Good cyber hygiene!

- Review telemetry for macro-enabled Office docs. Especially those sourced from job-related emails.

- And...watch out for unusual outbound C2 activity right after you chat it up with people you don't know via email, LinkedIn messages or some other third thing. (good to have general knowledge about this as well)


### Good Mitigations

1. User Awareness Training. I know, I know...I can hear you groaning from all the way over here. But training people to be suspicious of LinkedIn outreach, or (at the very least) teaching them that its not *automatically* safe, is a great first step. And, escalate or report that stuff to LinkedIn!

2. Sandbox that untrusted code. Coding tests or third-party files should be tested in isolated sandbox environments. This is especially important for folks starting out their coding journey (raises hand.)

3. Macros. Restrict them unless you know for sure what they do, and how they interact with things in your inbox.

4. Identity Hardening. This one falls more under the proverbial "Corporate Umbrella" but the philosophy is sound. Enforce phishing-resistant MFA, and restrict your risky biscuit logins!

5. Threat Hunting. Arguably the second coolest job in Cybersecurity (Cause OBVIOUSLY Cyber Threat Intelligence takes the gold). But proactive hunting for IOC's from the Lazarus campaigns (which I've included below) is great, and fun!


### But why does all this matter?

By blending inot those professional network spaces, like LinkedIn, Lazarus has a solid history of exploiting human trust in our beloved LinkedIn, and the success rate is arguably higher than that of a standard phishing campaign. Devs, CySec folks, crypto-bros (especially those that tout their placement within the hierarchy of their employment), are prime targets for this. Lazarus Group is going to keep refining their techniques, so organizations and individuals need to treat that recruitment communication as a threat vector. You need to broaden your awareness and harden your identity controls (personal and corporate). Cause lemme tell you Hwhat...these campaigns have a history of being highly targeted.

------------------

I know what you're thinking - "Levi...this is different than your usual philosophical and intellectual shower thoughts, what gives?!" Well what can I say folks...gotta stay Soupy! No but honestly I have been wanting to post on this group for a bit. So...here we go! Make sure you take a bit to check out the MITRE ATT&CK framework on this group and their IOCs. But don't get locked in on the IOCs - check the TTPs too. (I'm working on a full presentation for that, but it will come out much later)


- P.S. - there are tons of sources available on this group. The ones I used below just fit for what I was talking about...probably some bias in there, huh...

### Alright folks, till next time, "Stay Soupy, Stay Cyber!"

--------------------

## IOCs and TTPs

-  Network Indicators (IPs & Domains):
  - Common pattern: C2 domains mimic financial/crypto services or job portals.
  - Recent campaigns (2023–2024) have used: portalfinances[.]com, careerupdata[.]net, cloudbackup247[.]com
    - Several dynamic DNS services.
  - IPs often rotate via compromised VPS or cloud infrastructure.

---

- Malware Families & Hash Examples:
  - Manuscrypt / NukeSped – primary RAT used for persistence.
  - AppleJeus – targets cryptocurrency exchanges; usually delivered as trojanized trading apps.
  - DeathNote (a.k.a. Dream Job / Operation In(ter)ception) – lures through LinkedIn with malicious job offers.
  - Sample hashes (SHA256):
    - b2a2f7bcbf95e81db70f84f3a58e0a3c7a8d1f8f5e41d3c146f5e3e6d1cfae52 (NukeSped variant)
    - f4e6b12ec8da1a5de7992c07d98c32c7d8a772d05960a9dfd67f0e4c163c6a3b (AppleJeus installer)

---

- Email & Phishing Infrastructure:
  - Frequently use LinkedIn job lures (fake recruiter accounts).
  - Malicious documents often weaponized with macros or LNK payloads.
  - Observed phishing addresses:
    - hr-recruitment@protonmail[.]com
    - jobs-career@tutanota[.]com

---

- TTPs (MITRE ATT&CK highlights):
  - Initial Access: Spearphishing (T1566.001) via LinkedIn or email.
  - Execution: Malicious attachments / LNKs (T1204.002).
  - Persistence: Registry run keys (T1547.001).
  - Command & Control: HTTPS over compromised servers (T1071.001).
  - Exfiltration: Encrypted archives via web services (T1041).

---

*** NOTE: A full IOC list is thousands of entries long (Mandiant, CISA, Kaspersky, etc. each track them). Instead of dumping them all, the best practice is to pull campaign-specific IOCs from the latest reports (e.g., CISA’s Lazarus advisories, Mandiant, Kaspersky, etc.) ***

---------------------------------------------------------

Sources:
1. Bitdefender — Lazarus Group targets organizations with sophisticated LinkedIn recruiting scam
https://www.bitdefender.com/en-us/blog/labs/lazarus-group-targets-organizations-with-sophisticated-linkedin-recruiting-scam

2. Field Effect — Lazarus tricks job-seeking developers with malware-laced coding test
https://fieldeffect.com/blog/lazarus-tricks-job-seeking-developers-with-malware-laced-coding-test

3. CSO Online — Lazarus Group tricks job seekers on LinkedIn with crypto stealer
https://www.csoonline.com/article/3818521/lazarus-group-tricks-job-seekers-on-linkedin-with-crypto-stealer.html

4. Bank Info Security — Lazarus Uses Spearphishing to Steal Cryptocurrency
https://www.bankinfosecurity.com/lazarus-group-uses-spear-phishing-to-steal-cryptocurrency-a-14898

