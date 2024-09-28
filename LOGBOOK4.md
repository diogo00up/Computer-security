### Task 1
-We start by listin the environment variables in the terminal by using ``printenv``
-To create a new environment variable we proced to use ``export MYVAR=...`` and to make sure that it was set correctly we tried ``printenv MYVAR`` 
- Using ``unset MYVAR`` we understood that by running ``printenv MYVAR`` in the terminal it would return nothing since the variable was removed.

### Task 2
- Using ``fork()``, we compile and run the program creating a child process, that prints environment variables in the terminal. The parent process executed no tasks.
- In step 2, the child process executes no tasks while the parent is the one thay prints environment variables in the terminal. Comparing the results there was no difference so we can assume that child and parent processes share the same environment variables.

### Task 3
- Running the program given in the first step, there was nothing printed in the terminal.
- After making the changes listed in the second step, the environment variables were printed to the terminal.
- The new program gets its environment variables from the ``extern char **environ`` variable that must be declared in the user program, but is declared in the header file ``unistd.h`` and therefore doesn't need to be defined by the user.

### Task 4
- In this task, we print the environment variables in the terminal
- We create a new shell by using  the ``system()`` function that calls the function ``execl()`` that executes the /bin/sh program first. 
- ``execl()`` calls ``execve()``passing to it the environment variables array.
- Verifying that using the function ``system()`` the environment variables are passed to the new program /bin/sh.

### Task 5
- All of the environment variables set in step 3 were printed to the console.

### Task 6
- By using ``export PATH=/home/ourCommands:$PATH`` we can add the directory /home/ourCommands to the beginning of the PATH environment variable.
- After this, we can create an executable file ls (gcc ls.c -o ls) in this directory, where ls.c instead of listing the content of the current directory can do what we want, in this case, just print "Hello World".
- It will not do its proper function but whatever we defined in the executable ls, every time ls is executed in this directory.
