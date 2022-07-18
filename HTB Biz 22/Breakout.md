# Breakout

## Prompt 
The CCSS suffered a ransomware attack that compromised the Unique Digital Medical File (EDUS) and the National Prescriptions System for the public pharmacies. They've reported that their infrastructure has been compromised, and they cannot regain access. The APT left their implant interface exposed, though, and you'll need to break into it and find out how it works. NOTE: This challenge is intended to be solved before 'Breakin'.

# Target
![[Pasted image 20220718112414.png]]

## Running Strings
![[Pasted image 20220718112512.png]]

### Check presence of flag
![[Pasted image 20220718112535.png]]

### Carving the clutter
Before: ![[Pasted image 20220718113005.png]]
After & confirming flag hasn't been cut:
![[Pasted image 20220718113052.png]]

## Getting there
![[Pasted image 20220718113251.png]]

## Flag
- flag = `HTB{th3_pr0c_f5_15_4_p53ud0_f1l35y5t3m_wh1ch_pr0v1d35_4n_1nt3rf4c3.....}`