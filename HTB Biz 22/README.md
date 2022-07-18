# HTB Business CTF 2022

## Completed Challenges

- ![Breakout](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Breakout.md)
- ![Chromeminer](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/ChromeMiner.md)
- ![Lina's Inventation](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Lina's%20Invitation.md)

## Closing Thoughts

The HTB Business CTF 2022 was my first *major* CTF event ever, *and* my first CTF of any kind in over two years. But I'm getting back in the swing! The challenges were tougher than expected, and I was thrown off by not being able to use a lot of recon/enum tools that platforms and certification courses get you used to. 

I've been back in infosec (w/ a major focus on and passion for pentesting) for only two weeks and have done some decent brushing up and studying, but this was a humbling experience. I walked in expecting to waltz through the easy level challenges, but that was not the case.

In the end, I was able to only get three flags, but it left me determined, not down or upset. Determined to get better, learn more, and really excel in this field.

That said, I came **so** close with the only hardware challenge, State of Emergency. I was really excited to see hardware as a category for this ctf and wish there had been more than one, but it's awesome that the *only* hardware challenge was SCADA/ICS/PLC related! I had almost got working modbus commands, but gave up after beating my head against the wall. (Come to find out, I was only missing two additional bytes in my commands and I would've been spot on the money! [This](https://ipc2u.com/articles/knowledge-base/modbus-rtu-made-simple-with-detailed-descriptions-and-examples/) is a great article on modbus that I wish I had read *just* a little bit harder.)

## Lessons Learned

So I showed up, hey-- at least I did that, and I did 'ok' (and that's a gracious okay), but I did learn about some fun new toys and techniques.

### oletools

Firstly, [oletools](https://github.com/decalage2/oletools)! Thanks to the pre-ctf kickoff event presentations for bringing this to my attention. This suite of tools is super fun to dig around Microsoft docs with. Even from a non-forensics standpoint, it's a great, hands-on way to learn about their composition.

### Unzip more things

Second, I should just sit around and try unzipping various file types to see where it gets me. In over 10 years of general IT experience (with 3 of those being infosec, and 2 as a full stack dev), I had somehow missed the boat on the fact that lots of file types behave the same as `.zip` archives. ***How*** on earth did I miss out on that knowledge?! Better late than never though! 
