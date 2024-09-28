# CTF7


### Goal
- Exploring a format-string vulnerability attack, retrieve the flag located in the file flag.txt.


### Challenge 1
- By looking at the program’s code, we could see a  ```scanf ``` is used to get an input, and then it is followed by a  ```printf ``` of the same input without any type of value checking. Because of this, if we’re able to find the address of the global variable where the flag is stored, we can print the value of the flag, using ```%s```.


- To find out the address of the flag we use gdb with the command ```p &flag``` and get the address 0x804c060. 


- Finally, we sent the little endian memory address ```x60\xc0\x04\x08``` followed by ```%s```, which printed the flag stored in that memory address.
- Finally, by sending  ```x60\xc0\x04\x08%s```, this is the little-endian memory address followed by %s, we get the flag's value as an output.


### Challenge 2
- We noticed by looking at the code that there was once again a  ```scanf ``` followed by a ```printf ``` and that if we were able to change the value of ```key``` we would get access to a shell.


- By using the same technique as in the first challenge, using gbd we found out the address of the variable ```key```.


- Using the address we found, we tried sending the format string  ```1234\x34\xc0\x04\x08%x.%x ``` to find where 1234 and the variable’s address was being stored. Knowing this, we can write to the memory address in the string any value we choose by changing the first ```%x``` to ```%(value).x``` and the second ```%x``` to ```%n```.


- We then converted the value of ```0xbeef``` to a base 10 value and got 48879. Using this value and the method described in the previous topic, we get the format string ```1234\x34\xc0\x04\x08%48871.x%n```. Sending this string to the program we get access to a shell meaning we have successfully changed the value of ```key``` to ```0xbeef```.


- After getting access to a shell, we just run ```cat flag.txt``` and print out the value of the flag.