# Breakout

# TOC
- [Prompt](#prompt)
- [Target](#target)
- [Running Strings](#running-strings)
- [Check Flag Presence](#check-presence-of-flag)
- [Carving the Clutter](#carving-the-clutter)
- [Getting There](#getting-there)
- [Flag](#flag)
- [TLDR](#tldr)

## Prompt 
The CCSS suffered a ransomware attack that compromised the Unique Digital Medical File (EDUS) and the National Prescriptions System for the public pharmacies. They've reported that their infrastructure has been compromised, and they cannot regain access. The APT left their implant interface exposed, though, and you'll need to break into it and find out how it works. NOTE: This challenge is intended to be solved before 'Breakin'.

# Target

Looking at the target's web server we get a listing of `/` on the compromised host. Looking over all of these directories, it would be easy to get lost poking around for clues. I did for a good few minutes, before I noticed the non-standard, not-even-a-directory file at the top level: `bkd` (a real 'doh' moment for me).

![Target Host](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/breakout_host.png)

Grab a copy of the file. Run `file` on it if you like. Spoiler: it's an ELF, but it doesn't run! 

## Running Strings

When I get any kind of larger, pre-compiled file in a CTF, I like to visit good 'ol `strings` first.

![Running Strings](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/breakout_running_strings.png)

### Check Presence of Flag

Running `strings bkd` results in a *massive* amount of strings, so let's see if it has anything immediately obvious, such as, say, the string 'HTB?' 

![Flag Check](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/breakout_flag_check.png)

Yup! Sure does! 

### Carving the clutter

**Before**

Let's remove some of the clutter we see before scrolling thru the massive output. I saw a lot of lines starting with `_ZN` so I targeted that.

![Before Carving](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/breakout_carving_the_clutter.png)

**After**

Look at how clean it is now! Oh, and the flag's still there, which is good.

![After Carving](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/breakout_flag_check_2.png)

## Getting there

Now, simply scroll thru the output until we find the flag split over multiple lines.

![Getting There](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/breakout_getting_there.png)

## Flag

Put it all together and we get the flag:

- flag = `HTB{th3_pr0c_f5_15_4_p53ud0_f1l35y5t3m_wh1ch_pr0v1d35_4n_1nt3rf4c3.....}`

# TLDR
1. navigate to host & download `bkd` file
2. `strings bkd | grep -nv '^_ZN*' 
3. scroll to find 'HTB'
4. put the lines together

[Back to Top](#toc)
