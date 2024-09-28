# Work performed during week #5


## Task 1 

-We start the lab by disabling the address space randomization which randomizes the starting address of the heap and stack. To do this we run the command ``sudo sysctl -w kernel.randomize_va_space=0``.

-When prompted with the command make, we visualize two files, a32.out and a64.out. These will allow us to access the shell as a normal user( seed). We can confirm our identity by running the command ``whoami``. Running ``make setuid`` will differ from the previous one as their owner is now root and we need to use ``chmod`` with ``mode 4755`` to allow the other users to have the same permissions as the owner when he is executing these two files

-When running “make”, the program is compiled giving us the option of “execstack”, which allows code to be executed from the stack. If we don´t run the program with this option(“execstack”) our shellcode wouldn´t execute resulting in an error.

## Task 2
- This second task requires the use of the function strcpy, which copies the string pointed to by the second argument to the first, though, it does not check if the destination variable can store all the content from the origin. Going through the source code, we can see that we are reading 517 from the ``badfile`` into the ``str`` variable and with the use of the function ``bof`` we copy the content from the ``str`` variable which has size 517 into a ``buffer`` of only size 100. This is indeed the vulnerability in this program since someone can craft a ``badfile`` that rewrites certain parts of the memory.

## Task 3 
- We started by compiling the program from the previous task to create an empty “badfile”.

-Using ``gdb`` we can debug our program "stack-L1-dbg". To start this task we place a breakpoint in the function ``bof`` and use ``run`` to start executing our program

- We are able to see the address of the frame pointer and the start address of the buffer by using ``p $ebp`` and ``p &buffer``. By using ``x/100wx buffer`` we are able to print 100 words starting from the buffer address allowing us to see the content of the stack. 

- Using ``disassemble dummy_function``, we get the return address of the function.

- If we check the data inside the stack, we can see the return address, the data on the buffer and the ebp. We can use this information to build the script of the “badfile”. We start by setting the ret variable to the address of the buffer because this is where our malicious code will be.
After this, we calculate the offset between the address of the buffer and ebp, in our case 108. As the return address is right next to the ebp, and we want to rewrite the return address, our offset will be 108+4.


-Lastly, we are now able to craft the badfile by running the python script. Using ``gdb`` we launch a new shell and everything works. Nevertheless, if we try to run ``./stack-L1`` it results in a segmentation fault due to the address inside the debugger and outside differing slightly. To fix this we have to find out the address of the buffer when running ``./stack-L1``(``printf("buffer = %p\n\n", &buffer);``) and replace the ret value in the script with this new value and creating a badfile.
