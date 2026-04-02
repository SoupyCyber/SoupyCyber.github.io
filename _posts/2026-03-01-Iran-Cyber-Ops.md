---
layout: post
title: Iranian State-Sponsored Cyber Operations
subtitle: "Open-source conflict-scenario assessment of Iranian APT groups potential retaliatory response"
tags: [posts]
author: Levi.
---

# OPEN-SOURCE THREAT ANALYSIS

## Iranian State-Sponsored Cyber Operations

*A Conflict-Scenario Assessment of Iranian APT Groups Targeting Critical Infrastructure*

**Published:** February 2026 | **Classification:** TLP:WHITE – Freely Shareable

*Sources: CISA, Microsoft, Mandiant, ODNI, NSA, and peer‑reviewed threat research.*

*This analysis is based entirely on publicly available, open‑source information. The author maintains no affiliation with any government agency, private company, or intelligence community organization. All assertions are supported by cited sources in the references section.*\[4\]\[10\]

## Summary

This report synthesizes publicly available threat intelligence to assess the Iranian cyber threat landscape within the context of potential or active kinetic conflict with the United States.\[4\]\[10\] It serves as an educational resource for security practitioners, policy researchers, IT administrators, and informed members of the public seeking to understand Iranian state‑sponsored hacking operations—their methodologies, target profiles, and actionable defensive countermeasures.\[4\]\[10\]

All information derives from open‑source publications: U.S. government advisories, published threat research from established cybersecurity firms, and declassified intelligence assessments.\[1\]\[2\]\[3\]\[16\] No proprietary, classified, or organizationally sensitive material is included.\[1\]\[2\]\[3\]\[16\]

> **ANALYST NOTE:**  
> Iranian cyber actors almost certainly pre‑position network access weeks to months before kinetic conflict begins. The current period of heightened geopolitical tension should be treated by defenders as an active preparatory phase, not a future hypothetical.

---

## Strategic Context: Iran’s Asymmetric Cyber Doctrine

### The Rationale for Cyber Operations

Iran’s conventional military capabilities are substantially outmatched by the United States across multiple domains, including air power, naval projection, precision strike, and logistics.\[4\] Cyber operations provide Iran a mechanism to impose tangible costs on an adversary without triggering direct conventional military response.\[4\]\[10\] This constitutes the foundation of Iran’s asymmetric strategy—leveraging cyberspace to generate friction, instill fear, and inflict economic disruption that compensates for conventional inferiority.\[4\]\[10\]

Iran’s cyber capabilities have evolved significantly since early operations during the 2012–2014 period.\[2\]\[4\]\[31\] Today, the Islamic Revolutionary Guard Corps (IRGC) and the Ministry of Intelligence and Security (MOIS) each maintain distinct cyber units with specialized missions, ranging from destructive attacks on infrastructure to long‑term human intelligence collection through social engineering campaigns.\[2\]\[4\]\[31\]

### Doctrinal Principles in Practice

Iranian cyber operations adhere to a deliberate doctrine rather than opportunistic disruption.\[1\]\[2\]\[4\] Public reporting and declassified government advisories consistently identify the following characteristics:\[1\]\[2\]\[4\]

- **Graduated escalation:** Operations commence with reconnaissance and pre‑positioning, sometimes months before overt action, then escalate in intensity as conflict develops.\[4\] Sudden “zero‑day” attacks without observable precursor activity are rare.\[4\]
- **Proportional ambiguity:** Attacks are calibrated to remain below the threshold the U.S. would likely characterize as an act of war, preserving diplomatic space for de‑escalation while still imposing costs.\[4\]\[10\]
- **Plausible deniability through proxies:** The IRGC routinely deploys “hacktivist” front organizations (Handala, Moses Staff, Cyber Av3ngers) to claim responsibility for attacks, providing the Iranian state operational distance.\[19\]\[22\]\[3\]
- **Psychological amplification:** The perceived impact of an operation is deliberately magnified through coordinated social media and Telegram campaigns. Public fear is treated as a mission objective in itself.\[19\]\[23\]
- **Multi‑domain synchronization:** Cyber attacks are often timed to coincide with kinetic strikes, diplomatic pressure, and information operations to compound effects and overwhelm defenders.\[2\]\[4\]

> **Historical Precedent:**  
> Following the January 2020 killing of IRGC Quds Force commander Qasem Soleimani, U.S. federal agencies observed a measurable surge in Iranian cyber reconnaissance against U.S. critical infrastructure within days.\[4\] This pattern of rapid operational escalation following kinetic events is well‑documented in public reporting.\[4\]

---

## Four Iranian APT Groups of Note

Iran fields multiple Advanced Persistent Threat (APT) groups, each with distinct missions, techniques, and target profiles.\[4\]\[31\] The four groups below are assessed as presenting the most significant threat to U.S. critical infrastructure in a conflict scenario.\[4\]\[31\]

### Table 1 – Iranian APT Groups: Mission Profiles and Threat Assessment

| Group (Alias)                  | Mission                | Primary Vector                                                                                     | Key Targets                                                                                 | Threat Level |
|--------------------------------|------------------------|----------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|-------------|
| Refined Kitten (APT33/Peach Sandstorm) | Strategic Sabotage      | Password spray → cloud identity compromise → OT pivot; SHAPESHIFT wiper; Tickler backdoor          | Energy and power generation, grid SCADA, aviation                                          | **CRITICAL** |
| Charming Kitten (APT42/35)     | Espionage & HUMINT    | GenAI‑fabricated personas; long‑tail encrypted app engagement; TAMECAT / PowerLess backdoors      | Policy staff, defense‑adjacent personnel, researchers, executives                          | **HIGH**    |
| Static Kitten (MuddyWater)     | Recon & ISP Hijack    | Trusted inbox compromise → internal phishing; Phoenix / BugSleep loaders; ISP traffic interception | Telecom providers, ISPs, IT supply chain, managed service providers                        | **HIGH**    |
| Banished Kitten (Void Manticore) | Chaos & PsyOps        | Destructive ransomware (Handala / Moses Staff); Telegram amplification; data wipe without ransom   | Public utilities, water systems, transport, ports—high media‑visibility targets           | **MED‑HIGH** |

Detailed profiles of each group follow.\[1\]\[2\]\[16\]\[19\]

---

## Refined Kitten (APT33) — The Strategic Saboteur

**Threat Level:** CRITICAL | **Sponsor:** IRGC‑IO | **Mission:** Infrastructure Sabotage

Refined Kitten (APT33, Peach Sandstorm, Holmium) is assessed by multiple research organizations as the most operationally dangerous Iranian cyber actor targeting U.S. infrastructure.\[11\]\[31\] Active since at least 2013, the group has evolved from targeted spear‑phishing campaigns into one of the most industrialized cloud‑credential‑harvesting operations on record.\[11\]\[31\]

The group’s defining innovation, documented by Microsoft Threat Intelligence in 2024, is the “Cloud‑to‑OT Pivot.”\[1\] Rather than directly targeting operational‑technology networks, Refined Kitten compromises enterprise cloud accounts and then uses those trusted identities to move laterally into OT‑connected systems defenders assumed were protected by network separation.\[1\]\[40\]

### Attack Chain Methodology

The typical attack chain follows four observed stages:\[11\]\[1\]

1. **Stage 1 — Password spraying at scale**  
   Thousands of login attempts per hour target Microsoft 365 and Azure tenants, using one common password across many accounts to evade lockout policies.\[11\]\[1\]\[40\] Legacy service accounts, shared mailboxes, and dormant employee logins lacking MFA are primary targets.\[11\]\[1\]\[40\]

2. **Stage 2 — Cloud identity compromise**  
   Once valid credentials are obtained, the group establishes persistence via legitimate administrative tooling, enrolling new authentication methods and creating service principals that survive password resets.\[29\]\[2\] The Tickler backdoor is often deployed during this phase for reliable command‑and‑control.\[29\]\[2\]

3. **Stage 3 — Lateral movement to OT**  
   Using compromised cloud identities that appear as legitimate users, the group enumerates internal resources, discovers paths to OT systems, and pivots across the IT/OT boundary-transforming an email compromise into a potential physical impact.\[1\]\[2\]

4. **Stage 4 — SHAPESHIFT deployment**  
   At a time of Iran’s choosing—potentially aligned with kinetic action-SHAPESHIFT, a destructive disk‑wiping malware comparable in impact to the 2012 Shamoon attack on Saudi Aramco, is deployed against targeted systems.\[11\]\[2\]

> **ANALYST NOTE:**  
> A cluster of “impossible travel” alerts across multiple cloud accounts within a 48‑hour window is a high‑fidelity early‑warning signal of an active Peach Sandstorm intrusion.\[11\]\[1\] This warrants immediate incident‑response escalation, not routine tuning.

### Implications Across Sectors

Refined Kitten’s cloud‑focused approach means any organization running Microsoft 365: law firms, hospitals, universities, municipal governments, defense contractors, etc, can serve as a primary target or a pivot point.\[1\]\[7\] Any entity whose network touches the supply chain or IT systems of critical infrastructure is a legitimate target for credential harvesting, even if it is not the ultimate objective.\[2\]\[31\]

---

## Charming Kitten (APT42) — The Social Engineering Architect

**Threat Level:** HIGH | **Sponsor:** IRGC‑IO | **Mission:** Human Intelligence & Credential Theft

Charming Kitten (APT42/APT35) functions as Iran’s premier human‑intelligence collection apparatus in cyberspace.\[16\]\[32\] Where Refined Kitten targets cloud infrastructure with automated campaigns, Charming Kitten invests weeks or months cultivating relationships with carefully selected human targets.\[16\]\[17\]

Mandiant’s 2022 report “Crooked Charms, Cons and Compromises” documents systematic use of fabricated personas-journalists, academics, think‑tank researchers, NGO workers-to gain the trust of policy analysts, defense researchers, diplomats, and government officials.\[16\]\[24\] Since 2024, generative AI has significantly amplified this tradecraft.\[13\]\[42\]

### The AI‑Powered Persona Problem

Open‑source reporting from Microsoft, Google’s Threat Analysis Group, and Mandiant shows Iranian operators using AI‑generated content to fabricate personas at scale.\[13\]\[42\] Operators can now generate photorealistic profile photos, plausible publication histories, and weeks of coherent email exchanges with minimal effort.\[13\]\[25\] Traditional red flags—poor grammar, stock photos, thin social‑media history—are increasingly unreliable.\[13\]\[25\]

### The Long‑Tail Engagement Cycle

Charming Kitten’s signature method is extended relationship‑building before any malicious request.\[24\]\[25\] Targets often receive weeks of professional, substantive, and benign correspondence; only once trust is established do operators introduce a malicious element such as:

- A document link
- A request for a sensitive file
- An invitation to a video call where malware is delivered\[16\]\[24\]\[17\]

This approach bypasses most awareness training, which emphasizes “do not click links from strangers.” By the time a malicious link is sent, the operator is no longer perceived as a stranger.\[16\]\[24\]\[17\]

**Signature tools:** TAMECAT (PowerShell backdoor delivered via cloud file‑sharing links)\[13\] and PowerLess (memory‑resident backdoor designed to evade file‑based detection).\[9\]

> **Target Profile:**  
> Priority targets include defense and national‑security researchers, journalists covering Iran, government officials and their staff, academics studying the Middle East, and employees of defense contractors, anyone whose knowledge has intelligence value to Tehran.\[16\]\[32\]

---

## Static Kitten (MuddyWater) — The Infrastructure Infiltrator

**Threat Level:** HIGH | **Sponsor:** MOIS | **Mission:** Reconnaissance, ISP Compromise, Espionage

Static Kitten (MuddyWater, Seedworm, MERCURY) operates under Iran’s Ministry of Intelligence and Security, reflecting a distinct intelligence mandate.\[29\]\[2\] While IRGC units like Refined Kitten emphasize disruption and Charming Kitten focuses on human intelligence, Static Kitten specializes in long‑term, methodical network infiltration for persistent access and collection.\[20\]\[29\]

Recent reporting (Deep Instinct 2023-2024, Check Point Research 2024) highlights a pronounced TTP shift toward targeting telecommunications companies and ISPs.\[20\]\[21\]\[28\] This shift has strategic implications far beyond any single victim organization.\[28\]

### The Trusted Inbox Technique

Static Kitten’s distinctive method weaponizes existing trust relationships between organizations.\[20\]\[29\] Instead of sending obviously suspicious emails from unknown domains, the group:

1. Compromises a legitimate employee account at a partner, contractor, or vendor.\[20\]\[21\]
2. Uses that inbox to send malware‑laden emails to contacts in the victim’s address book.\[20\]\[21\]

Recipients see messages from genuine colleagues at organizations they already work with, arriving from verified domains that pass spam filters and bearing plausible filenames.\[29\]\[2\] This dramatically increases compromise likelihood because defensive training has been neutralized by authenticity signals.\[29\]\[2\]

### Strategic Implications of ISP Targeting

The surge in Static Kitten activity against ISPs warrants specific attention.\[27\]\[28\] An ISP is not merely another endpoint; it is the transit layer for all customer traffic.\[27\]\[29\] A compromised regional ISP can enable:

- Interception and analysis of customer communications
- Selective manipulation or blocking of traffic at scale
- Real‑time insight into defensive postures and operational timelines\[27\]\[28\]

This capability is valuable for both pre‑conflict intelligence and conflict‑phase disruption at a time of Iran’s choosing.\[27\]\[28\]

**Signature tools:** Phoenix loader (modular, persistent remote‑access tool)\[26\] and BugSleep (defense‑evasion backdoor mimicking legitimate scheduled tasks).\[20\]\[21\]\[26\]

---

## Banished Kitten (Void Manticore) — The Chaos Engine

**Threat Level:** MEDIUM‑HIGH | **Sponsor:** IRGC (via hacktivist proxies) | **Mission:** Public Chaos, Psychological Impact, Deniability

Banished Kitten, operating under brands such as Handala, Moses Staff, and Karma, plays a distinct role in Iran’s cyber arsenal.\[19\]\[22\] Its primary mission is perception management, not technical disruption.\[19\]\[23\]

Where other Iranian APTs prioritize stealth, Banished Kitten seeks visibility.\[19\]\[23\] The group routinely deploys ransomware that:

- Does not seek ransom payment
- Often lacks any decryption capability\[19\]\[22\]\[3\]

Data is wiped; the “ransomware” is a facade for a wiper.\[19\]\[23\] The true payload is the Telegram post publicizing the incident minutes or hours later.\[19\]\[23\]

### Ransomware as 'Theater'

Open‑source analyses describe a recurring pattern:\[19\]\[22\]\[23\]

1. Compromise of an internet‑facing system via known vulnerabilities or purchased access.\[22\]\[3\]
2. Data exfiltration for public posting as “proof” of breach.\[19\]\[23\]
3. Wiper deployment to destroy data and disrupt operations.\[15\]\[16\]
4. Rapid publication of screenshots and internal documents on Telegram, framed in geopolitical terms.\[19\]\[23\]
5. Public, media, and policy‑maker perception of a devastating cyberattack—regardless of the actual operational effect.\[17\]

This reflects sophisticated understanding of modern information ecosystems.\[19\]\[23\] Even an unaffected organization can suffer reputational, regulatory, and financial damage if a false breach claim goes viral before it can respond.\[19\]\[23\]

> **Critical Context:**  
> Banished Kitten frequently exaggerates impact and sometimes claims attacks that did not occur.\[19\]\[23\] The existence of a Telegram claim is not evidence of a breach or of the claimed impact. Verification through direct assessment is essential before any public statement is made.\[19\]\[23\]

---

## Early Warning Indicators

The following indicators have been publicly documented as precursors or concurrent signals of Iranian APT activity.\[1\]\[2\]\[36\] A single indicator may be coincidental; clustering across identity, network, and social‑engineering dimensions within a short timeframe significantly raises the probability of an active operation.\[1\]\[4\]

### Table 2 – Iranian APT Early Warning Indicators and Response Actions

| Indicator                | Observable Signal                                                                                                                                                 | Likely Actor                 | Recommended Response                                                                                                                                                           |
|--------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Identity Noise           | Spike in failed or “impossible travel” logins on cloud accounts—especially legacy or dormant accounts without MFA                                                | Refined Kitten               | Enforce MFA on all affected accounts; disable legacy authentication; escalate to incident response if alerts cluster across multiple accounts within 48 hours                 |
| Edge Device Scanning     | Inbound reconnaissance from Iranian‑attributed IP space targeting unpatched VPN/remote‑access appliances (Ivanti, Citrix, Fortinet)                              | Multiple actors (pre‑staging) | Verify patch posture on all internet‑facing appliances; deploy deception assets; coordinate upstream blocking with ISPs                                                        |
| Trusted Inbox Lure       | Email from a known partner or contractor address with unusual attachments (.zip, .iso, .lnk) or unexpected cloud‑sharing links; SPF/DKIM irregularities         | Static Kitten                | Quarantine and sandbox; notify the apparent sending organization; audit the sender’s recent outbound communications                                                           |
| Social Engineering Contact | Unsolicited outreach via LinkedIn, Signal, or Telegram from personas posing as journalists, academics, or recruiters requesting calls, documents, or opinions | Charming Kitten              | Do not engage further; capture screenshots of conversation; report immediately to security or counterintelligence points of contact                                           |
| OT Lateral Movement      | Cloud or IT‑side credentials authenticating to OT systems (historians, engineering workstations, DCS jump hosts)                                                 | Refined Kitten (active)      | Isolate affected OT segments immediately; invoke ICS incident‑response playbooks; notify CISA ICS‑CERT                                                                         |
| Hacktivist Claim         | Iranian‑linked Telegram channels (Handala, Moses Staff, Cyber Av3ngers) posting screenshots or statements claiming compromise of infrastructure                  | Banished Kitten (PsyOps)     | Do not confirm or deny publicly until verified; conduct rapid internal triage; coordinate external communications through legal and communications leadership                 |

---

## Conflict Escalation Phase Model

Historical precedent, including Iranian activity surrounding the 2019–2020 escalation period and the 2019 Aramco attacks, supports a phased model of Iranian APT activity across conflict stages.\[4\]\[10\]\[37\] The critical insight is that Phase 1 (pre‑conflict pre‑positioning) typically unfolds during periods of elevated tension, well before formal conflict declarations.\[4\]\[10\]

### Table 3 – Iranian APT Activity SCENARIOS Across Conflict Phases

| Phase                       | Timeline   | Primary Actors                       | Expected Activity                                                                                                                                                                                                 | Recommended Actions                                                                                                                                                                 |
|-----------------------------|-----------|--------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Phase 1 – Pre‑Conflict      | T‑30 to T‑0 | All groups (pre‑positioning)         | Potential intensified password spraying against cloud infrastructure; increased social‑engineering targeting defense‑adjacent personnel; ISP reconnaissance and edge‑device scanning; pre‑staging of backdoors             | Move to 24/7 monitoring; enforce MFA across all accounts; accelerate patching of internet‑facing systems; brief key personnel on elevated risk                                     |
| Phase 2 – Conflict Onset    | T+0 to T+14 | Refined Kitten + Banished Kitten     | SHAPESHIFT wiper attempts against OT targets; ransomware‑theater and public‑facing disruption operations; aggressive Telegram and social‑media amplification of every incident                                  | Activate ICS incident‑response playbooks; aggressively segment or isolate OT from IT; block known Iranian IP ranges; engage CISA and sector ISACs                                  |
| Phase 3 – Sustained Conflict | T+14 to T+45 | All groups (synchronized operations) | Multi‑vector coordinated attacks; Charming Kitten activates cultivated human assets for insider‑assisted access; Static Kitten leverages ISP footholds to manipulate regional traffic                           | Assume persistent adversary presence; conduct full‑scope threat hunts; reassess third‑party and vendor connectivity; implement enhanced segmentation and monitoring where feasible |
| Phase 4 – Post‑Conflict     | T+45+     | Charming Kitten + Static Kitten      | Long‑term espionage persistence; exfiltration of sensitive data and personnel information; preservation of backdoors for future campaigns; repurposing compromised infrastructure                               | Execute comprehensive credential rotation; perform forensic audits across critical systems; harden third‑party integrations; update threat‑intelligence requirements and subscriptions |

> **On Post‑Conflict Persistence:**  
> Charming Kitten and Static Kitten frequently maintain access to compromised networks long after the triggering event.\[16\]\[20\]\[29\] Organizations breached during a conflict period should assume continued presence until a thorough forensic review—not just a malware scan—has cleared the environment.\[16\]\[20\]\[29\]

---

## Defensive Guidance for Practitioners

These recommendations are mere suggestion. Individual contributers and leadership personnel should ALWAYS analyze reporting from closed and open sources to assess validity and relevance to individual scenarios and situations. (Just because you saw it here, doesn't mean you SHOULD do it. The recommendations draw from CISA advisories, NSA guidance, and cross‑sector best practices.\[1\]\[8\]\[7\] They are provided as reference for security practitioners, IT administrators, and other defenders seeking to operationalize lessons from this threat landscape.\[1\]\[8\]\[7\]

### Identity and Cloud Security (Refined Kitten / Peach Sandstorm)

1. Audit and disable legacy authentication protocols (SMTP AUTH, IMAP, POP3) wherever modern alternatives exist.\[1\]\[6\]
2. Enforce phishing‑resistant MFA (hardware keys, passkeys) for all accounts accessing sensitive systems; treat SMS‑based MFA as significantly weaker.\[1\]\[8\]
3. Review and remove dormant accounts; every unused service or mailbox presents a potential entry point for password spraying.\[11\]\[8\]
4. Implement conditional‑access policies that flag or block logins from anomalous locations, ISPs, or devices.\[1\]\[8\]
5. Monitor closely for “impossible travel” alerts; clusters across multiple accounts are strong intrusion indicators.\[11\]\[1\]

### Social Engineering Defense (Charming Kitten / APT42)

1. Apply heightened scrutiny to unsolicited professional contact, regardless of how polished the persona appears; AI‑generated profiles increasingly bypass basic checks.\[13\]\[42\]
2. Verify identities out‑of‑band using independently sourced contact details before sharing documents or joining calls.\[16\]\[24\]
3. Treat cloud file‑sharing links from first‑contact senders as high‑risk, particularly where content is “urgent” or “sensitive.”\[13\]\[9\]
4. Provide specialized training on APT42’s long‑tail engagement patterns to personnel who interact frequently with media, academia, policy communities, or defense contractors.\[16\]\[24\]\[25\]

### Supply Chain and Network Hygiene (Static Kitten / MuddyWater)

1. Implement and enforce DMARC, DKIM, and SPF for all organizational domains and validate equivalent controls for key partners.\[29\]\[2\]
2. Restrict and monitor all third‑party remote access; treat every vendor, consultant, and MSP as a potential lateral‑movement vector.\[1\]\[8\]
3. Periodically review threat intelligence related to primary telecommunications and ISP providers; compromise at that layer can impact you even with strong internal controls.\[27\]\[28\]

### Operational Technology Environments

1. Audit all pathways between IT and OT networks, including “indirect” paths via shared file systems, historians, or dual‑homed engineering workstations.\[2\]\[4\]
2. Ensure boundary controls between IT and OT can be isolated within minutes using documented procedures that non‑specialists can execute under pressure.\[8\]\[2\]
3. Review all remote‑access pathways into OT; each legitimate pathway can serve as a lateral‑movement route for Refined Kitten and similar actors.\[1\]\[8\]

### Preparing for the PsyOps Dimension (Banished Kitten / Void Manticore)

1. Establish monitoring for major Iranian hacktivist Telegram channels; early notification enables proactive communication planning.\[19\]\[23\]
2. Pre‑draft holding statements for confirmed breaches, unconfirmed claims, and demonstrably false claims, recognizing each scenario requires a different posture.\[3\]\[39\]
3. Define and rehearse an internal verification protocol for rapidly assessing the validity and scope of publicly claimed breaches.\[40\]

---

## Reporting Channels and Public Resources

The following public channels support reporting suspected Iranian APT activity and obtaining authoritative guidance.\[2\]\[1\]

**CISA (Cybersecurity and Infrastructure Security Agency)**  
24/7 reporting: (888) 282‑0870  
Email: <ics-cert@cisa.dhs.gov>  
Web: <https://www.cisa.gov/report>

**FBI Internet Crime Complaint Center (IC3)**  
<https://www.ic3.gov> – accepts reports from individuals and organizations regarding suspected nation‑state cyber activity.

**NSA Cybersecurity Collaboration Center**  
Email: <cybersecurity@nsa.gov> – engages directly with critical‑infrastructure operators.

**CISA Free Cybersecurity Services and Tools**  
<https://www.cisa.gov/free-cybersecurity-services-and-tools> – catalog of no‑cost services and tools for organizations of all sizes.\[8\]

**CISA Known Exploited Vulnerabilities Catalog**  
<https://www.cisa.gov/known-exploited-vulnerabilities-catalog> – definitive public list of actively exploited CVEs for patch‑prioritization.\[7\]

Sector‑specific Information Sharing and Analysis Centers (ISACs)—including E‑ISAC (energy), WaterISAC (water), FS‑ISAC (financial services), and H‑ISAC (healthcare)—provide sector‑tailored threat intelligence and incident information.\[8\]

---

## Methodological Note on Attribution

All threat‑actor descriptions in this report rely on publicly attributed analysis from established cybersecurity research organizations and U.S. government advisories.\[4\]\[16\]\[31\] Cyber attribution is inherently probabilistic; the underlying sources explicitly caveat their own findings.\[4\]\[16\]\[31\] This document synthesizes that open‑source record and does not represent original intelligence collection.\[4\]\[16\]\[31\]

Readers requiring authoritative, current, and potentially non‑public threat intelligence should work directly with CISA, relevant sector ISACs, or licensed commercial threat‑intelligence providers.\[1\]\[8\]

---

**TLP:WHITE – This document may be shared freely without restriction.**

*Open‑source analysis. Not affiliated with any government agency, company, or intelligence organization.*

---

## References

1. CISA. “Iranian Cyber Actors’ Brute Force and Credential Access Activity Compromises Critical Infrastructure Organizations.” Joint Advisory AA24‑290A (FBI / CISA / NSA / CSE / AFP / ASD ACSC). October 16, 2024. <https://www.cisa.gov/news-events/cybersecurity-advisories/aa24-290a>  
2. CISA / NSA / FBI. “Iranian Government‑Sponsored APT Actors Compromising U.S. Organizations.” Alert AA21‑321A. November 17, 2021. <https://www.cisa.gov/news-events/cybersecurity-advisories/aa21-321a>  
3. CISA / FBI. “StopRansomware: Iran Government‑Sponsored APT Actors Conducting Ransomware Operations.” Alert AA22‑257A. September 14, 2022. <https://www.cisa.gov/news-events/cybersecurity-advisories/aa22-257a>  
4. ODNI. “Annual Threat Assessment of the U.S. Intelligence Community.” February 5, 2024. Iran section, pp. 14–17. <https://www.dni.gov/files/ODNI/documents/assessments/ATA-2024-Unclassified-Report.pdf> 

```
