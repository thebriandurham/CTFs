# Chromeminer

## Prompt
Discurd has filed a DMCA violation regarding a popular browser extension claiming to be conducting VIP giveaways on the company's product. The addon store has since taken down the extension to prevent any potential browser cryptomining malware from being distributed in the marketplace. Could you investigate what the 'Discurd Nitro Giveaway' addon does exactly?

## Files
- DiscurdNitru.crx

## Unzipping the crx
![[Pasted image 20220718105552.png]]

## background.js - contents beautified
![[Pasted image 20220718105714.png]]
![[Pasted image 20220718105700.png]]

## background.js - getting to work

### protip 1 - ctrl shift m on parentheticals
![[Pasted image 20220718105842.png]]

### protip 2 - dedupe w/ ctrl d 
![[Pasted image 20220718105959.png]]

### protip 3 - firefox js console
![[Pasted image 20220718110117.png]]
![[Pasted image 20220718110213.png]]

### deobfu payload
![[Pasted image 20220718112014.png]]

### AES Decode
![[Pasted image 20220718112133.png]]

- Flag = `HTB{__mY_vRy_owN_CHR0me_M1N3R__}`