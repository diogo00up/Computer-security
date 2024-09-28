# CTF4

### Goal
- The goal of this CTF is to log in to a WordPress server and use a known CVE to retrieve the flag.

### Tasks

- By searching the website we found out the version and the plugins of WordPress and two users "admin" and "Orval Sanford". 

- Looking for known CVE’s related to these versions and plugins we found the CVE-2021-34646 which is a vulnerability that affects the WooCommerce plugin version and it also allows us to bypass the authentication process and gain admin privileges.
 
-Accessing the python exploit in the exploit DB platform allows us to access the users' information we found out that the admin id was 1 and we proceeded to use this value as the one to execute the exploit.

-With the three links that were generated, we used the first one which lead to us being recognized as the “admin” and then we navigated to the private post and retrieved the flag{don’t bother me}.
