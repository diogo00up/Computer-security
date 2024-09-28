### Task 1

- We started by running the command ``$ docker-compose build`` so we can build the ``docker-compose.yml`` and then we run the command  ``$ docker-compose up`` to start it.

-Next we use run the command ``dockps`` so we can get the ID of the container. After getting the ID of the container. The server used for this task  is running the program ``format.c`` with a format-string vulnerability.

- We use the command ``docksh <id>`` to start a shell on that container.

- First we send a message to this server. In a shell we execute ``echo "hello" | nc 10.9.0.5 9090``, ``nc 10.9.0.5 9090`` will start the program on the server. That program reads data from the standard input (``stdin``) and then passes the data to ``myprintf()``, which calls ``printf()``to print out the data. So we use ``echo``to send the message ``hello`` to the ``stdin`` through the pipeline ``|``.

-We start by sending a message to the server using  ``echo "hello" | nc 10.9.0.5 9090``, ``nc 10.9.0.5 9090`` on the shell starting the program on the server.  This program reads the data from the standard input and passes it to ``myprintf()`` .We used ``echo`` to send the message through the pipeline ``|``.

- Then we use a file to save the data sent through the pipeline to the program.

-Next we send the data to the server with the command  `` cat <filename> | nc 10.9.0.5 9090``

-  we create a badfile  using ``build string.py``. 

- If we send ``"%s"`` the server will crash, because it will try to print a string from an address with random values(segmention fault)

-Finally we use  ``docker-compose down`` to shut down the container.

### Task 2

-To complete this task (2.A) we have to find out how many %x format specifiers we require in order to get the server program to print out the first four bytes of your input. Firstly we use the file ``build string.py`` to create a badfile with the data we want. Then, we change the number variable to 0xaaaaaaaa because using ``s = "%.8x-"*100`` we can print the first 100 addresses and its easy to locate it. Reducing the size from 100 to 80 and then to 65 we understand that it is needed to print 63 %x in order to print the first four bytes of the desired input.

-In task 2.B we need to find a secret message, which is a string, that is stored in the heap area. Given the known address for the secret message and with the results of the task 2.A we just have to change the way it is printed, because instead of expecting an address in binary we are expecting a string. 

- We start by copying the address of the message and put it in a variable number on ``build string.py``. Then we use `` s = "%.8x-"*63 + "%s" `` to print the address of the secret message as a string. We end up obtaining the string "A secret message". 


### Task 3

- Using ``build string.py``, we create a badfile with the information required to input to the server nc 10.9.0.5 9090 to modify the value of the target’s variable address.

- We replace the variable number for the target’s variable address in string.py, due to not wanting the secret message’s address.

- We still use ``s = "%.8x-"*64"`` to print the address at the position 64, even after replacing it with the new target variable address, because it maintains its position.

- Doing this we can change ``s = "%.8x-"*63 + "%n-" + "\n"``, modifying the target variable to a different value as asked in the part of this task.

- The second part of this task, asks us to change the target variable to a given value, that is 0x5000.

- By adding "%.19914x" to our 63 address, we change the value of the 64 position, using the expression  ``s = "%.8x-"*62 + "%.19914x" + "%n" + "\n"`` we have completed the second part of this task.
