## CTF

### Goal
- Using the buffer-overflow attack, retrieve the flag located in the file flag.txt.

### Challenge 1
- Starting off we use ``checksec`` to verify with which protection the program had been compiled. 
- We noticed that the ``scanf`` was reading up to 28 bytes and storing it in a ``char buffer[]`` of size 20 which could lead to an overflow attack. Also, the variable used to store the file path was a ``char`` array of size 8, which means we could probably rewrite all its content because of the vulnerability we had found before.
- Trying to explore the vulnerability using the given python script, we instructed the script to input "aaaaaaaaaaaaaaaaaaaaflag.txt", which should write 20 'a' to the ``buffer`` and continue writing in the next memory block, which we were expecting to be where the ``meme_file`` variable was stored, writing "flag.txt".
- Our buffer-overflow attack was successful using the program we had been given, printing to the screen the content of the flag.txt. Next, we set the script to run the program version in the ctf-fsi.fe.up.pt server, successfully retrieving the flag.

### Challenge 2
- Once again, we used ``checksec`` to analyse the program.
- We looked through the main.c file and found out that the vulnerability was identical to the first challenge. The difference was that there was another variable declared between the ``buffer`` and the ``meme_file``, which we would also need to rewrite before rewriting the scope of the ``meme_file``.
- This new variable ``char val[4]`` required to have a specific value so that we could read the content of the file. We got to work and after a few attempts, the input "aaaaaaaaaaaaaaaaaaaa\x22\x21\xfc\xfeflag.txt" gave us the expected result.
