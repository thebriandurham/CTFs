# Chromeminer

## Prompt
Discurd has filed a DMCA violation regarding a popular browser extension claiming to be conducting VIP giveaways on the company's product. The addon store has since taken down the extension to prevent any potential browser cryptomining malware from being distributed in the marketplace. Could you investigate what the 'Discurd Nitro Giveaway' addon does exactly?

## Files
- DiscurdNitru.crx

## Unzipping the crx

![Unzip CRX](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/chromeminer_unzipping_crx.png)

## background.js - contents beautified

![background.js contents](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/chromeminer_backgroundjs_contents.png)
![Contents Beautified](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/chromeminer_js_beautified.png)

## background.js - getting to work

### protip 1 - ctrl shift m on parentheticals

![Protip 1](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/chromeminer_protip1.png)

### protip 2 - dedupe w/ ctrl d 

![Protip 2](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/chromeminer_protip2.png)

### protip 3 - firefox js console

![Protip 3-1](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/chromeminer_protip3_1.png)
![Protip 3-2](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/chromeminer_protip3_2.png)

### deobfu payload

![De-obfuscated Payload](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/chromeminer_deobfu_payload.png)

### AES Decode

![AES Decode](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/chromeminer_aes_decode.png)

- Flag = `HTB{__mY_vRy_owN_CHR0me_M1N3R__}`
