# Phriedman Systems
```
We want access to the CEO's secure data. Log in to their website using the CEO's account. [https://phriedmansystems.onrender.com/](https://phriedmansystems.onrender.com/)

Hints:

-   This is primarily a Recon challenge.
-   There is NO password cracking, brute force, or password guessing required.
-   There is NO steganography of any sort required.
-   The onrender.com website is just used for hosting. Attacking Render is not a part of the challenge; do not attack Render or attempt to break into the backend.
-   You don't need to use anything on the Internet at all apart from phriedmansystems.onrender.com.

Author: nb
```

This challenge was a recon. After searching through the site, the login page was discovered at https://phriedmansystems.onrender.com/login.html. The CEO's username was needed for the challenge.
![[Pasted image 20210508172959.png]]

Looking at the employee's page (https://phriedmansystems.onrender.com/employees.html), the format of an employee's username was found to possibly be: rfiddson@phriedmansystems

The CEO's username was `csmith`. 
Finding the password proved to be a little tricky as it was not on the website, but found by calling the phone number on the website. 
`Phone: (301) 902-0806`

The phone number was an automated system. One option was to learn about the company, this informed that the CEO was from Albany, NY. Another option was for IT/Technical Support, where the CEO's password could be reset. Confirming a security question of the CEO's hometown gave the password: `monkey_alpaca_excellent_button_7435`

![[Pasted image 20210508173733.png]]

`DawgCTF{y0ur_c4ll_1s_v3ry_1mp0rt4nt_t0_u5}`