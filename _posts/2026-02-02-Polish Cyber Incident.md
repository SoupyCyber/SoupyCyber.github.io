---
layout: post 
title: A tired analysis of the Polish Cyber Incident
subtitle: The one that happened in December
tags: [posts]
author: Levi
---


## Welcome Back!
What’s up guys, Levi here! 

Man, I don’t know about y’all, but I’ve never drank so much coffee in a 30 day window in my entire life. I mean I for real felt like January lasted 10 years. And good grief it was cold in my little corner of the world. I *really* must be getting older, because I have never hated winter before, but this year? Bring on Summer man, cause I’m over Winter.  Anywho, you guys didn’t come here to here (see?) me blab about the weather and coffee - or maybe you did how the heck should I know - you (probably) came here cause of the title of the blog post! So without further delay, lets get into it.


## SUMMARY
On 29 December 2025, during a period of severe winter weather in Poland, coordinated cyber attacks targeted the country's distributed energy infrastructure, including numerous wind and solar farms, a combined heat and power (CHP) plant serving nearly half a million customers, and a private manufacturing facility. According the Threat Intelligence groups like DRAGOS and CERT.PL, these attacks represent a significant escalation in cyber-physical threats, as they impacted both information technology (IT) systems and operational technology (OT) equipment—a rare occurrence in publicly reported incidents. The purely destructive nature of the attacks, comparable to deliberate acts of arson in the physical world, resulted in key operational equipment being disabled beyond repair at affected sites.

This incident marks the first major cyber attack specifically targeting distributed energy resources (DERs), which are smaller, decentralized wind, solar, and CHP facilities increasingly critical to modern electrical grids worldwide. While the attacks did not cause power outages, which may lead some to underestimate their significance, the adversares(? More on that later) demonstrated the ability to gain access to operational technology systems critical to grid operations and cause permanent physical damage.

Unlike previous electric grid cyber attacks in Ukraine (2015, 2016) that targeted centralized systems, this incident exploited the inherent vulnerabilities of distributed infrastructure: DERs are more numerous, require extensive remote connectivity for management, and typically receive less cybersecurity investment than traditional power generation facilities. This attack demonstrates that distributed energy resources are now validated targets for sophisticated adversaries and should serve as an urgent warning, particularly for countries increasingly dependent on decentralized renewable energy systems.


## My thoughts
Okay, now that we got the BLUF, I want give you guys some thoughts. I’m not going to spend a lot of time going into he technical detail, because - lets be honest, ‘Levi predicts with high likelihood that many of you will utilize LLMs or personalized agents to summarize the contents of this report.’ CTI phrasing ftw!

Anyways, I kind of eluded to it earlier on LinkedIn, but where I really want to focus in, is on the *style* of the attack (for lack of better phrasing) vs. the Infrastructure and tradecraft. And here’s why I want to focus there. Some groups (Like the great folks at DRAGOS) are reporting that they believe the attack was carried out by Russian GRU (Main Intelligence Directorate) VooDoo Bear AKA: ELECTRUM, Seashell Blizzard, Sandworm (though not 100% related), whereas other groups (like the detailed researchers at CERT.PL) are reporting that this was the handiwork of Russian FSB (Federal Security Service), Berserk Bear AKA: DYMALLOY, Ghost Blizzard, Dragonfly. So what gives? Why are these two groups stating different things?

### DRAGOS side
DRAGOS is framing this attack as an evolution of VooDoo Bear’s (Specifically ELECTRUM) OT-Destruction playbook, just pointed at a new part of the grid. What we have here is coordinated effort against some roughly 30-odd distributed energy sites - Solar, Wind, CHP. You’ve got destructive tooling that wipes some systems, and leaves others bricked beyond repair, AND an operational focus on communication paths and control infrastructure, not just random IT equipment. You layer that with their historical pattern of going after utilities, where they know grid protocols, OT tooling and how to have maximum impact once access is gained, without having to rewrite CRASHOVERIDE every time. You add all that together with with ecosystem reporting tying the wiper behavior and timing back into the Sandworm orbit - and from DRAGOS vantage point, the cleanest version of this story is VooDoo Bear/ELECTRUM doing what they do best, in a different local (kinda).

### CERT.PL side
CERT.PL, by contrast, is looking at this same attack and attributing it to Berserk Bear, specifically because of this group is better known for their long-term access and espionage capabilities. (+/- 10 months of dwell time) They seek to make the argument that the intrusion chain (exposed/unpatched FortiGate devices, weak or default credentials, Tor and compromised infra, broad ICS/DER exposure) alongside infrastructure/TTP overlap match earlier Berserk Bear work. They also posit that this would represent that FSB lineage’s first publicly acknowledged shift from pre-positioning into full-blown destructive action against energy-sector IT/OT, including RTUs and Controllers.  Now - there are obviously tons of people researching this and that’s part of the beauty of Cyber Threat Intelligence and Intelligence research and Incident Response. You have tons of incredible minds working overtime to identify what the hell happened here, and who is responsible.


## BUT WAIT...
That said, I’d like to offer a third opinion or option...

I’m not sure if this has been publicly stated anywhere or offered up by any other individual analyst or group, but just…go with me for a second. What if, for the first time in a while the GRU and FSB finally started talking to each other, and started working together? On one side, the activity feels very “VooDoo Bear/Sandworm-esque — coordinated effects at +/-30 DER sites, destructive wiper activity (DynoWiper), and an OT impact pattern that reads like an evolution of their previous grid operations, just pushed out to distributed renewables instead of big, centralized nodes.  

However, On the other side, Polish authorities and CERT.PL tie the intrusion chain, infrastructure, and long‑running energy‑sector presence back to FSB’s Berserk Bear, a service with deep access and familiarity in exactly these environments but a historically more espionage‑heavy profile. I mean to put it simply, one realistic thought is: GRU brings the playbook and destructive tooling, FSB brings the access and local context, resulting in Sandworm‑style wiper and OT tradecraft riding on top of Berserk Bear’s long‑term positioning in Polish and European energy assets.

Most open‑source work on Russian services describes them as overlapping, competitive organizations that sometimes coordinate when the Kremlin pushes a bigger political or strategic objective, rather than as a single, well‑oiled joint machine. That’s why a third option here—a rare, combined effort *seems* plausible to me. The operation has that rushed or “opportunistic” character: exploiting exposed edge devices and weak credentials on one side, while still delivering a fairly sophisticated, destructive OT punch on the other.  

So now we get back into the fancy CTI speak! "This analyst assesses with low to moderate confidence (cause I need to do more research), that the attack on the Polish grid was possibly a combination of the GRU’s VooDoo Bear AND the FSB’s Berserk Bear. From a defender’s standpoint, the precise wiring of Russian bureaucratic responsibility matters less than the operational takeaway: multiple mature Russian services now *APPEAR* both willing and able to pivot from years of reconnaissance and pre‑positioning in European energy infrastructure to coordinated, destructive activity against distributed resources and OT equipment. That shift, whether driven by one service or several, should be treated as a strategic warning indicator and factored into how we prioritize hardening, monitoring, and exercising around DER, CHP, and other OT‑adjacent assets."


## So...There you have it folks.
My surface thoughts. Its late, I didn’t have any coffee while I wrote this, and I had a house full of sick people over the last 9 or 10 days, so…here’s hoping everything I wrote made sense! Anyways, thanks for reading everyone, and as always - 

### *Guard your grids, mind your mids.*
### *Stay Soupy, Stay Cyber!*

PEACE!
