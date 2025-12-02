# Bandit
Bandit wargame is aimed at beginners. Those tasks are really great to learn Linux commands, or revise your knowledge after a long break from using Linux based OS.

You definitelly should try to beat this game at your own. Use this writeup only if you're stuck at some point.

Jump to:
(Not sure how to make this ;d i'll figure it out)

## Level 0
Your task is to connect to the remore host using SSH protocol. Address, port and credentials are provided in level description.

The way i recommend is using Linux shell command:
ssh username@host_address -p port_number

![image missing?](./content/level00.png)

That's it, you are ready to go.

## Level 0 -> Level 1
Description says, that password for user bandit1 is stored in readme file. Lets find it.
Use ls command to list content of directory you are in. There is a readme file that you can print into terminal using cat command.

![image missing?](./content/level01.png)

## Level 1 -> Level 2
Use SSH again to login into remote host, this time use bandit01 and password that we've found in prievous task.

This time we are dealing with file called "-". Trying to print it using cat will fail, beacause shell recognise - char as that command parameters start with.
We can bypass this by using relative path to the file. Try using "./", which means "in this directory".

![image missing?](./content/level02.png)

And now we have the password for bantit2 user.

## Level 2 -> Level 3
To obtain password, we need to open file called "--spaces in this filename--". Trying to use it directly will not work. 
Firstly, "--" is also recognized as command parameter, but we already know how to bypass this. Secondly, each space will break filename into separate parts. 
You can tell the shell to include space as part of the string, by using escape character "\".

![image missing?](./content/level03.png)

Let's go to the next level.

## Level 3 -> Level 4
We have to look for a hidden file in "inhere" directory. Let's get inside and list content of it. At first, we wont see nothing. In Linux you can add '.' to hide file, it wont be visible until using special flag. To list all files including hidden ones, use ls -a. And there it is, bandit4 password.

![image missing?](./content/level04.png)

We are ready to go further.

## Level 4 -> Level 5
This time we have to find file containing password. There are several files, and description says that we will find credentials in the unly human-readable file. Humans can read text, so we are looking for text file, right?
Use "file" command to find out what is type of specific file. Do you have to do it for every file? No, you can use * to check all files at once. Remember to use './'!
There is one ASCII text file, and thats our password.

![image missing?](./content/level05.png)

Now you can login into bandit5 account.


 
