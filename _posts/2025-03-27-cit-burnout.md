---
layout: post
title: The Burnt Out Analyst
subtitle: CTI Analysts in the Intel Feed Trap
cover-img: assets/img/Burnout-IT-guy.jpg
thumbnail-img: assets/img/Too Many alerts.webp
share-img: assets/img/Octo.jpg
tags: [posts]
author: L.
---

# The 24/7 Threat Feed Trap: Why CTI Analysts Are Drowning in Data

## Introduction: The CTI Analyst’s Dilemma
I've been working in CTI for little over 2 years now. and in that time, I've learned that in **Cyber Threat Intelligence (CTI)**, information is power. But...what happens when there’s **too much information**?

CTI analysts face a **data avalanche**—hundreds of threat feeds, dark web alerts, vendor reports, open-sourced intelligence (OSINT) and social media intelligence updates flood in daily. The expectation? **Filter through it all and deliver actionable intelligence.** The reality? **An overwhelming amount of noise, false positives, and redundant information.**

This constant **data overload** creates **burnout, inefficiency, and missed critical threats**. How did we get here, and more importantly—how do we fix it?

---

## The Problem: Too Many Feeds, Too Little Actionable Intel

### 1️⃣ The "More Feeds = Better Intelligence" Myth
Many organizations believe that **the more intelligence feeds they subscribe to, the better their security posture**. But in reality:
- **80%+ of data is redundant**—Most feeds **rehash public reports** or duplicate vendor intelligence ([SANS, 2023](https://www.sans.org/white-papers/)).
- **False Positives Drain Time**—Analysts waste **hours triaging alerts that lead nowhere** ([Ponemon Institute, 2023](https://www.ponemon.org/)).
- **Volume Doesn’t Equal Value**—A flood of low-quality data **buries the truly critical threats** ([Gartner, 2023](https://www.gartner.com/en/newsroom/press-releases/)).

> *“More isn’t always better. More is just... more.”*

### 2️⃣ The Pressure to Be "Always On"
Although many of us may not be a 24/7 shop, we can probably all agree that CTI isn’t just a 9-to-5 job. **Threat actors don’t follow office hours**—so neither do analysts.
- Teams feel pressured to **monitor feeds 24/7**, fearing they’ll miss a **critical attack signal** ([(ISC)² Cybersecurity Workforce Study, 2023](https://www.isc2.org/Research)).
- Even during "off hours," analysts are **glued to alerts, OSINT chatter, and breaking threat intel**.
- This leads to **mental fatigue, stress, and eventual burnout** ([Cynet, 2023](https://www.cynet.com/resources/reports/)).

### 3️⃣ The Signal-to-Noise Ratio Problem
Another problem is, not all threat intelligence is created equal. Many feeds generate **high volumes of low-quality alerts**, drowning out what actually matters.
- **SOC teams ignore CTI alerts** because they’ve seen too many false positives ([Mandiant, 2023](https://www.mandiant.com/resources/reports)).
- **Redundant intelligence wastes time**—as mentioned above, analysts spend **hours re-verifying known information** ([NIST SP 800-150](https://csrc.nist.gov/publications/detail/sp/800-150/final)).
- **And critical threats get buried** in an ocean of low-risk indicators.

> *“You don’t need more data. You need the right data.”*

---
![ALERTS](/assets/images/Over-Alerted.png)

## How to Fix It: Smarter CTI, Not More CTI

### ✅ 1. Set Clear Intelligence Requirements (PIRs & SIRs)
Before subscribing to another feed, ask:
- **Does this intelligence align with our industry’s threats?** (A mentor of mine when I first entered CTI drilled into me, until I had it ingrained in my mind- *"Does this matter to us?"*)
- **Does it provide unique insights we don’t already have?**
- **Can we action this intelligence, or is it just noise?** That same mentor taught me- *"It may matter to you, it may matter to our team, but does it matter to our customers?"*

Use **Priority Intelligence Requirements (PIRs)** and **Specific Intelligence Requirements (SIRs)** to **focus on what actually matters** ([MITRE ATT&CK, 2023](https://attack.mitre.org/)).

> *“Define what’s relevant before drowning in what’s available.”*

### ✅ 2. Automate and Filter Out the Noise
- **Use AI/ML tools** to **rank and prioritize alerts.** Things like Recorded Future, Cortex XSOAR, and ThreatStream ([Palo Alto Networks, 2023](https://unit42.paloaltonetworks.com/)).
- **Leverage automation** to de-duplicate low-value intelligence ([Splunk, 2023](https://www.splunk.com/en_us/resources.html)).
- **Customize feed ingestion** to **filter out irrelevant data before analysts see it.** Again, tools like Recorded Future and XSOAR shine here. ([The Threat Intelligence Handbook, Recorded Future](https://www.recordedfuture.com/threat-intelligence-handbook)).
- **Don't just aggregate all the same data** in one place. Part of the filtering process should be to *filter out* what is **irrelevant** from the feeds you already have.

> *“Your job isn’t to collect intelligence. It’s to make intelligence useful.”*

### ✅ 3. Finally, and most importantly - Build a Culture That Supports Analyst Well-Being
- **Rotate responsibilities** to prevent burnout. This method is helpful because it prevents there from being a singular "Go-To" person.
- **Create clear "off-duty" policies**—no one should be glued to alerts 24/7. Because if I've learned anything in my 2 years doing this, Analysts will watch alerts like a hawk - even when **they're not supposed too.**
- **Give analysts better tools**—manual processes **increase stress** and **waste time**. Now - this can be a bit tricky. You might be limited by your companies funding - but do what you can!

> *“A burnt-out analyst is a blind spot in your security program.”*

---

## Conclusion: Shift from Data Collection to Decision Support
CTI isn’t about **collecting the most data**—it’s about **delivering the right intelligence, in a timely manner, to drive action**. By **prioritizing quality over quantity, leveraging automation, and setting clear intelligence requirements**, CTI teams can escape the **24/7 threat feed trap** and focus on what really matters: **protecting their organizations.** There are additional things that matter like timeliness vs. delivery speed vs. false positives, but that is likely a post for another time.
