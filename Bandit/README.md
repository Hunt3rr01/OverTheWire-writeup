# Bandit
Bandit wargame is aimed at beginners. Those tasks are really great to learn Linux commands, or revise your knowledge after a long break from using Linux based OS.

You definitelly should try to beat this game at your own. Use this writeup only if you're stuck at some point.

Jump to:
(Not sure how to make this ;d i'll figure it out)

## Level 0
Your task is to connect to the remore host using SSH protocol. Address, port and credentials are provided in level description.

The way i recommend is using Linux shell command:
~~~bash
ssh username@host_address -p port_number
~~~ 

![image missing?](./content/bandit00.png)

That's it, you are ready to go.

## Level 0 -> Level 1
Description says, that password for user bandit1 is stored in readme file. Lets find it.
Use ls command to list content of directory you are in. There is a readme file that you can print into terminal using cat command.

![image missing?](./content/bandit01.png)

## Level 1 -> Level 2
Use SSH again to login into remote host, this time use bandit01 and password that we've found in prievous task.

This time we are dealing with file called "-". Trying to print it using cat will fail, beacause shell recognise - char as that command parameters start with.
We can bypass this by using relative path to the file. Try using "./", which means "in this directory".

![image missing?](./content/bandit02.png)

And now we have the password for bandit2 user.

## Level 2 -> Level 3
To obtain password, we need to open file called "--spaces in this filename--". Trying to use it directly will not work. 
Firstly, "--" is also recognized as command parameter, but we already know how to bypass this. Secondly, each space will break filename into separate parts. 
You can tell the shell to include space as part of the string, by using escape character "\\".

![image missing?](./content/bandit03.png)

Let's go to the next level.

## Level 3 -> Level 4
We have to look for a hidden file in "inhere" directory. Let's get inside and list content of it. At first, we wont see nothing. In Linux you can add '.' to hide file, it wont be visible until using special flag. To list all files including hidden ones, use ls -a. And there it is, bandit4 password.

![image missing?](./content/bandit04.png)

We are ready to go further.

## Level 4 -> Level 5
This time we have to find file containing password. There are several files, and description says that we will find credentials in the only human-readable file. Humans can read text, so we are looking for text file, right?
Use "file" command to find out what is type of specific file. Do you have to do it for every file? No, you can use * to check all files at once. Remember to use './'!
There is one ASCII text file, and thats our password.

![image missing?](./content/bandit05.png)

Now you can login into bandit5 account.

## Level 5 -> Level 6
File that we are looking for is human-readable, 1033 bytes in size and is not executable. When we list contents "inhere" directory we see a lot of subdirectories, each containing even more files. We could brute-force this challange by manualy checking each file, but that would take a lot of time. Command "find" will be usefull. 
First flag is -perm, which specify what permissions should file have. We can use "!" to negate criteria, so "! -perm /111", this mean that we are looking for file that have no execute bite set. Second flag is "-size 1033c", "c" stands for bites. After executing command that i've written bellow, we will see only one file matching those criteria. And thats password for bandit6 user.

~~~bash
find ./ ! -perm /111 -size 1033c
~~~

Lets move on to the next one.

![image missing?](./content/bandit06.png)

## Level 6 -> Level 7
Another challenge where find command will be usefull. This time we are looking for file that is owned by bandit7, owned by group bandit6, and have 33 bytes in size. We know that file is stored "somewhere on the server", so this time we will use "find /", where "/" means to start searching from root directory. Parameters -user and -group will let us specify user and group that file is owned by. After command execution, there are a lot of mess in terminal saying that we have no permission, and thats true. We can get rid of it by addind 2>/dev/null. And now there is only one file, and this is what we are looking for. 

~~~bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
~~~
![image missing?](./content/bandit07.png)

Continue by logging into bandit7 user.

## Level 7 -> Level 8
Password is stored in data.txt file next to the word "millionth". Firstly we should check how file looks like inside. In each line there is a word and string of random chars. This time we will use "grep" command, which will let us find line containing "millionth" word. 
~~~bash
cat data.txt | grep millionth
~~~

![image missing?](./content/bandit08.png)

Bandit8 password is captured, time to move forward.

## Level 8 -> Level 9
Another data.txt file, but this time password is the only one unique line in whole file. Use "cat data.txt | sort | uniq -u" to find it. Sort is neccesary, because uniq works only in nearest line. Flag "-u" means that we are looking for unique value.

![image missing?](./content/bandit09.png)

We are ready to go.

## Level 9 -> Level 10
And another one data.txt file. But is it text? No. Printing it in terminal with "cat" will result in messing up it. We can check file type with "file" comman, and we will see that this is data file. To search for ASCII strings, we can use "strings" command. Also, we know that password is preceded by several "=" charcters. Grep will also be usefull. There are four results, only one looks like a password.

![image missing?](./content/bandit10.png)

First 10 challenges done, let's go further. 

