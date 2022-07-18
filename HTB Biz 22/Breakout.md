# Breakout

## Prompt 
The CCSS suffered a ransomware attack that compromised the Unique Digital Medical File (EDUS) and the National Prescriptions System for the public pharmacies. They've reported that their infrastructure has been compromised, and they cannot regain access. The APT left their implant interface exposed, though, and you'll need to break into it and find out how it works. NOTE: This challenge is intended to be solved before 'Breakin'.

# Target

![Target Host](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/breakout_host.png)

## Running Strings

![Running Strings](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/breakout_running_strings.png)

### Check presence of flag

![Flag Check](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/breakout_flag_check.png)

### Carving the clutter
Before: 

![Before Carving](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/breakout_carving_the_clutter.png)

After & confirming flag hasn't been cut:

![After Carving](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/breakout_flag_check_2.png)

## Getting there

![Getting There](https://github.com/thebriandurham/CTFs/blob/main/HTB%20Biz%2022/Images/breakout_getting_there.png)

## Flag
- flag = `HTB{th3_pr0c_f5_15_4_p53ud0_f1l35y5t3m_wh1ch_pr0v1d35_4n_1nt3rf4c3.....}`
