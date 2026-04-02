---
layout: post
title: Axios npm Supply Chain Compromise
subtitle: "Open-source analysis of recent Axios npm Supply Chain Compromise"
tags: [posts]
author: Levi.
---
## Aaaand Welcome Back!
I honestly can't believe you came back here...*have you seen how this guys writes?!* In all seriousness welcome back yall. I hope the rest of Q1 has been less busy for you than it has been for me. Spring has sprung and I'm lovin the weather. My allergies...not so much. And the day job has been BUSY...I am an Iran desk (among other things) analyst by day, so the grind has been real during the entirety of Operation Epic Fury. But today, I wanted to post something that steps away from the Iran/US/Israel conflict, and focus on something different...Water-Hole attacks! So thanks for joining. Below is my analysis of the Axios npm Supply Chain attack based on fully open-sourced intelligence and reporting. Enjoy!


# OPEN-SOURCE THREAT INTELLIGENCE
*A Review of What Happened*

**Published:** April 2026 | **Classificaiton:** TLP:CLEAR

*Sources: Mandiant, Huntress, X, and additional OSINT*

*This analysis is based entirely on publicly available, open-sourced information. The author (thats me!) maintains that this analysis and intelligence is a result of their own work and effort, and represents their own thoughts and opinions only, not those of any private company or intelligence community.*

# Summary

This analyst states with a high degree of confidence, that the Axios npm compromise was a pre-staged, cross-platform supply chain attack that moved from 'malicious package publication' to 'first observed infection' in 89 seconds, demonstrating how quickly trusted open-source dependencies can be weaponized in automated environments. Cybersecurity company Huntress observed at least 135 endpoints across Windows, macOS, and Linux contacting the attacker
infrastructure during the exposure window, reinforcing that this was an active and operational intrusion and not just a package delivery risk.

The attacker compromised the *jasonsaayman* npm maintainer account and published malicious versions `axios@1.14.1` and `axios@0.30.4`, which introduced the phantom dependency `plain- crypto-js@4.2.1` solely to execute a postinstall dropper and deploy platform-specific RAT payloads. Any system that resolved these versions during the exposure window should be treated as fully compromised, with priority placed on credential rotation, endpoint rebuilds, and downstream artifact review rather than limited package cleanup.

# Analyst Comment
This incident is significant because it's a perfect example of a high quality watering-hole attack. The attacker used structural access rather than technical novelty: one compromised maintainer account provided trusted distribution into a package ecosystem with massive downstream reach. The Huntress reporting strengthens this viewpoint...this was a deliberate, pre-staged operation optimized for rapid detonation, anti-forensics, and cross-platform post-exploitation. It was not a short-lived smash-and-grab package defacement.

Additionally, there appear to be overlaps related to infrastructure and tooling linked by multiple research groups that point to DPRK activity.These factors raise the confidence that this intrusion may fit a broader North Korean tradecraft pattern, though the exact initial credential compromise remains unconfirmed.

## Incident Overview
On March 31, 2026, malicious versions of Axios were published
directly to npm without corresponding GitHub release tags, bypassing
the normal release workflow and signaling direct abuse of
maintainer publishing access.[3][2] The malicious packages added
plain-crypto-js@4.2.1, a trojanized dependency that executed setup.js
during installation and downloaded second-stage payloads from
sfrclak.com:8000.[1][3]
Huntress further documented that the attack was pre-staged roughly
18 hours earlier when plain-crypto-js@4.2.0 was published from an
attacker-created account to establish package history before the
malicious 4.2.1 release was used operationally.[1] That detail
materially changes the assessment from opportunistic package abuse
to a planned supply chain operation intended to reduce scanner
suspicion and accelerate trust abuse at detonation time.[1]

## Timeline
| Time (UTC) | Event |
| --- | --- |
| 2026-03-30 @ 23:59:12 | plain-crypto-js@4.2.1 published with malicious postinstall payload. | 
| 2026-03-31 @ 00:05:41 | Socket flagged plain-crypto-js@4.2.1 as malware, about six minutes after publication |
| 2026-03-31 @ 00:21:58 | axios@1.14.1 published and tagged latest; Huntress assessed this as the point the attack went live. |
| 2026-03-31 @ 00:23:27 | First Huntress-observed infection, a macOS host, occurred 89 seconds after Axios publication. |
| 2026-03-31 @ 00:58:05 | First Huntress-observed Windows infection via wt.exe execution chain. |
| 2026-03-31 @ 01:00:57 | axios@0.30.4 published and tagged legacy, extending the compromise to the 0.x branch |
| ~2026-03-31 @ 03:29 | plain-crypto-js removed from npm by the npm security team. | 
| ~2026-03-31 @ 03:30 | Malicious Axios versions removed from npm. |

# Technical Details
## Initial Access and Publishing Abuse
The attacker changed the maintainer email on the compromised account to ifstap@proton[.]me and published directly through npm CLI using a long-lived token, bypassing the expected GitHub Actions OIDC-based publishing path. Sources noted that even where OIDC trusted publishing was configured, the presence of `NPM_TOKEN` as an environment variable meant token-based authentication still took precedence, creating a durable weakness in the release process.

## Dropper Behavior
The `plain-crypto-js@4.2.1` dependency executed `node setup.js`, a JavaScript dropper using reversed-base64 decoding and an XOR routine keyed with OrDeR_7077 to reveal module names, file paths, commands, and the C2 URL. After delivery, the dropper deleted `setup.js`, removed the malicious `package.json`, and replaced it with a clean stub by renaming `package.md` to `package.json`, making the remaining dependency directory appear benign during superficial
review.

# Cross-Platform Observations
Across all three platforms (Windows, Linux and MacOS), the malware used the same command vocabulary, 60-second beaconing interval, HTTP POST C2 model, and Internet Explorer 8 on Windows XP-style user-agent string, which has been described as highly anomalous in 2026. The POST bodies were crafted to resemble npm-related traffic using strings like packages.npm.org/product0, product1, and product2, an evasion measure intended to look ordinary in log review while still routing payloads by platform. The C2 endpoint http://sfrclak[.]com:8000/6202033 acted as a shared campaign path for the platform-specific loaders and beacons. That uniformity gives threat hunters multiple correlation points
across endpoint, DNS, proxy, EDR, and NetFlow data even when individual file artifacts have been deleted by anti-forensic cleanup.

## Indicators of Compromise

### Packages and hashes

| Indicator | Value | Notes |
|---|---|---|
| SHA-1 | `2553649f2322049666871cea805d0d6adc700ca` | Malicious `axios@1.14.1` package. |
| SHA-1 | `d6f3f62fd3b9f5432f5782b62d8cfd5247d5ee71` | Malicious `axios@0.30.4` package. |
| SHA-1 | `07d889e2dadce6f3910dcbc253317d28ca61c766` | Malicious `plain-crypto-js@4.2.1` dependency. |
| Version | `1.14.0` | Safe rollback target. |
| Version | `0.30.3` | Safe rollback target. |

### Stage-2 hashes

| Platform | SHA-256 | Description |
|---|---|---|
| Windows | `f7d335205b8d7b20208fb3ef93eedc817905dc3ae0c10a0b164f4e7d07121cd` | PowerShell download cradle stage 1. |
| Windows | `617b67a8e1210e4fc87c92d1d1da45a2f311c08d26e89b12307cf583c900d101` | PowerShell RAT stage 2. |
| macOS | `92ff08773995ebc8d55ec4b8e1a225d0d1e51efa4ef88b8849d0071230c9645a` | Mach-O universal RAT. |
| Linux | `fcb81618bb15edfdedfb638b4c08a2af9cac9ecfa551af135a8402bf980375cf` | Python RAT script. |

### Network indicators

| Type | Value | Notes |
|---|---|---|
| Domain | `sfrclak[.]com` | Primary C2 domain. |
| IP | `142.11.206[.]73` | C2 IP address. |
| URL | `hxxp://sfrclak[.]com:8000/6202033` | Shared campaign endpoint. |
| Port | `8000` | C2 communications. |
| POST body | `packages.npm.org/product0` | macOS routing string. |
| POST body | `packages.npm.org/product1` | Windows routing string. |
| POST body | `packages.npm.org/product2` | Linux routing string. |
| User-Agent | `mozilla/4.0 (compatible; msie 8.0; windows nt 5.1; trident/4.0)` | Shared beacon artifact. |

### Host indicators

| Platform | Artifact | Notes |
|---|---|---|
| All | `node_modules/plain-crypto-js/` | Presence indicates compromise even if contents appear clean. |
| All | `setup.js` | Postinstall dropper, often deleted after execution. |
| Windows | `OrDeR_7077` | XOR key used in dropper logic. |
| Windows | `%PROGRAMDATA%\wt.exe` | Renamed `powershell.exe` masquerade. |
| Windows | `%PROGRAMDATA%\system.bat` | Hidden persistence file. |
| Windows | `%TEMP%\6202033.vbs` | Temporary launcher, usually self-deleted. |
| Windows | `%TEMP%\6202033.ps1` | Temporary PowerShell payload, usually self-deleted. |
| Windows | `HKCU\Software\Microsoft\Windows\CurrentVersion\Run\MicrosoftUpdate` | Run key persistence. |
| macOS | `/Library/Caches/com.apple.act.mond` | Stage-2 Mach-O RAT path. |
| Linux | `/tmp/ld.py` | Python RAT path. |

### Account and identity indicators

| Indicator | Value | Notes |
|---|---|---|
| Compromised maintainer | `jasonsaayam` | Axios maintainer account used in publication. |
| Attacker-set email | `ifstap@proton[.]me` | Replaced maintainer email during takeover. |
| Attacker account | `nrwise@proton[.]me` | Published `plain-crypto-js` pre-stage package. |

## Immediate Actions
Roll back Axios to 1.14.0 or 0.30.3 and remove any plain-crypto-js dependency from all projects and build systems. Treat any endpoint that executed the payload as fully
compromised and rebuild from a known-good baseline rather than cleaning in place. Rotate all credentials accessible from affected systems, including npm tokens, SSH keys, cloud credentials, CI/CD secrets, OAuth tokens, API keys, and .env secrets. Block sfrclak.com, 142.11.206.73, and related campaign infrastructure at DNS, proxy, firewall, and EDR network
controls. Review downstream artifacts, package caches, containers, and release outputs generated by affected systems during or after the exposure window.

## Hardening Recommendations
Organizations should commit and enforce lockfiles, prefer npm ci over ad hoc npm install in pipelines, and apply install-time controls such as --ignore-scripts wherever operationally feasible. Huntress also recommended removing long-lived npm tokens and ensuring trusted publishing is not silently undermined by residual environment token precedence, which is a critical lesson for package maintainers and internal registries alike. Additional improvements should include a minimum release age policy for newly published dependencies, internal package proxying, software composition analysis with malware detection, provenance verification between npm and GitHub tags, and alerting on unusual postinstall execution chains in developer and CI/CD environments. For threat hunting teams, this event should drive permanent detections for npm install child-process anomalies, unexpected network egress from build systems, and persistence artifacts associated with package-manager execution.

---

**TLP:CLEAR – This document may be shared freely without restriction.**

*Open‑source analysis. Not affiliated with any government agency, company, or intelligence organization.*

## So, there you have it folks!
Thank you for joining! Post a comment with your thoughts back on the LinkedIn post. Lets connect and discuss. Thats one thing I've noticed in the intelligence community, is we don't always share feedback! Like I said, thanks for reading, and as always - 

### *Guard your grids, mind your mids.*
### *Stay Soupy, Stay Cyber!*

## References
1. Mandiant
2. Huntress
3. Axios
4. X
