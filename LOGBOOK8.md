## CTF

### Goal
-The goal of this CTF is to login into a web server in PHP using the admin user account. Challenge one gives access to the server's source code to interact with the database. Challenge 2 is done from a black-box perspective. 

### Challenge 1
- After downloading the index.php file, we discovered  the query used to log in: ``$query = "SELECT username FROM user WHERE username = '".$username."' AND password = '".$password."'" ``;

- When we download the index.php file, we find the query that is used to log in, which is,  ``$query = "SELECT username FROM user WHERE username = '".$username."' AND password = '".$password."'" ``;

- With this in mind, we get a grip that it is possible to overcome the ``AND`` and only validate the username(we should log in as admin).

- We start by inputting ``admin`` in the username. Then, in order to terminate the evaluation of ".$username", we add `` ' `` after admin and terminate the query with ``;``.
Doing this we are now ``admin';``. Knowing ``--`` comments a line in SQL, to ignore the password check, we input it after. Therefore finally it makes our username ``admin'; -- ``.


### Challenge 2

-We immediately discover that we are allowed to ping addresses without being authenticated.

- This can be our attack, so we started searching for vulnerabilities and found the documented CVE-2017-14127.

-Reading the CVE-2017-14127 documentation we understand that we can run shell commands through the existing input to ping addresses.

- That way if we input ``;`` we can use ``cat`` to read data from files giving their content as output. Being the file flag.txt by using the input ``; cat /flag.txt`` we can get the flag.

