# Chromeminer

## Prompt
Discurd has filed a DMCA violation regarding a popular browser extension claiming to be conducting VIP giveaways on the company's product. The addon store has since taken down the extension to prevent any potential browser cryptomining malware from being distributed in the marketplace. Could you investigate what the 'Discurd Nitro Giveaway' addon does exactly?

## Files
- DiscurdNitru.crx

## Unzipping the .crx

For this challenge, we're given a single file (see above). As stated in the prmopt, it's a browser extension. Some quick googling reveals you can unzip them, just like a `.zip` file. Who knew?! (Not me, this is my first time messing with chrome extensions, but now I have a hankering to rip apart all of the extensions I use in Firefox). 

Unzipping the CRX (*you wouldn't unzip a car?!* (+1 points for you if you get the reference)) reveals its contents. There's some images and other stuff, but that .js file is sure to be the meat of it. 

![Unzip CRX](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/chromeminer_unzipping_crx.png)

## background.js - Contents

Checking out background.js reveals a *massive* one-line, obfuscated js script.

![background.js contents](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/chromeminer_backgroundjs_contents.png)

Let's take that ugly duck and make it a swan with an online js beautifier:

![Contents Beautified](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/chromeminer_js_beautified.png)

*Nice*.

## background.js - Getting to Work

Now that we have the obfuscated js in a tolerable-to-look at format (well, almost tolerable), we can start picking it apart. Here's some protips I picked up from my days as a SOC Analyst...

### Protip 1 - CTRL+SHIFT+M on Parentheticals

In Sublime Text (you are using Sublime, *aren't* you?) you can move the caret to any parenthetical character (`(, ), [, ], {, }`) and press `CTRL + SHIFT + M` to highlight everything within it.

![Protip 1](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/chromeminer_protip1.png)

Doing this is great, especially when we combine it with Protip 2:

### Protip 2 - Dedupe w/ CTRL+D 

With the contents of a parenthetical highlighted, you can go ahead and press `CTRL + D` a bunch of times, until new instances of the highlighted content aren't found. If nothing is found, then there's only one instance, but that's okay. This is still going to save us a lot of time while de-obfuscating this script.

![Protip 2](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/chromeminer_protip2.png)

### Protip 3 - Firefox JS Console

Now that we have a technique down, we need to put it all together. Go ahead and open up your browser, open the developer pane, and click on the Console tab. **Disclaimer**: be careful here, and don't willy-nilly paste stuff and hit enter. We're going to just paste in the arrays of characters from the javascript to put it in temp memory and work with it.

![Protip 3-1](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/chromeminer_protip3_1.png)

With the array stored, we can use the js console to ***only*** paste in highlighted segments of the obfuscated script and *not* pressing enter, because the console will let you preview the output. 

![Protip 3-2](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/chromeminer_protip3_2.png)

### De-obfuscated Payload

After we've done that a whole bunch of times, we've got ourselves a polished js script that's lightyears ahead of where we started. Looks like we're doing some encrypting/decrypting and everything is hard-coded so we have our entire encryption recipe ready to go: ` AES-CBC; IV = "_NOT_THE_SECRET_", KEY = "_NOT_THE_SECRET_"`. To top it all off, we have some ciphertext just waiting to be read!

![De-obfuscated Payload](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/chromeminer_deobfu_payload.png)

### AES Decode

Throw that into cyberchef and we get our flag!

![AES Decode](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/chromeminer_aes_decode.png)

- Flag = `HTB{__mY_vRy_owN_CHR0me_M1N3R__}`
