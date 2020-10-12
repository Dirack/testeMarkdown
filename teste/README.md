## Welcome to Try it on docker Madagascar Environment!

This is a docker container with Madagascar package version 3.0 installed and pre-configured designed as a "try on" experience. 
This container has minimum resources configuration to allow portability, you can install other packages with apt-get if you need, use
the following user account:

- Your user is: tryitondocker
- Your password is (sudo included): 12345

#### About Madagascar

Madagascar is an open-source software package for multidimensional data analysis and reproducible computational experiments. You can get more
details in [http://www.ahay.org](http://www.ahay.org/wiki/Main_Page).

#### About your local Madagascar installation

- The Madagascar binaries are installed in the directory identified by your RSFROOT environment variable.
You can show its variable content with the following comand:

```sh
~$ echo $RSFROOT
```

- The Madagascar source code is installed in the directory identified by your RSFSRC environment variable.
You can show its variable content with the following comand:

```sh
~$ echo $RSFRSC
```

- The Madagascar data binaries that you generate will be stored in the directory identified by your DATAPATH environment variable.
You can show its variable content with the following comand:

```sh
~$ echo $DATAPATH
```

#### How to add new programs on my local version of Madagascar?

If you need to install new programs in your local Madagascar package you should know where Madagascar binaries and
source code is installed. Usually, Madagascar keeps the path of your local copy source files in the RSFSRC environment variable.
And Madagascar will install executable files on your RSFROOT directory. You can show that environment variables with the 'echo'
command described in the previous section.

Madagascar stores user programs in $RSFSRC/user directory. So, you can create a new directory on that, and put your programs inside.
In this directory, such as every user's directory in Madagascar, you need a compilation 
[SConstruct](https://github.com/Dirack/creGatherStack/files/5365605/SConstruct.zip) that compile your C programs.

For the main c program you have to add 'M' letter as prefix, for instance 'Mmyprogram.c' is a valid name. And in the compilation
SConstruct, in the variable progs, you should add your program name without 'M' preffix and '.c' suffix as follows:

```py
import os, sys, re, string
sys.path.append('../../framework') 
import bldutil

# Put your name programs in progs variable 
# without 'M' preffix and '.c' extension
progs = '''
myprogram
'''
```

So run 'scons' command on your directory that is installed in $RSFSRC/user directory to compile your programs
defined in progs variable:

```shell
~$ scons
```

And run 'scons install' in the top directory of your local Madagascar installation 
(the directory path in your $RSFSRC variable):

```shell
~$ sudo scons install
```

For more details, please check out the Madagascar official documentation wiki in the section 
["Adding new programs to Madagascar"](http://www.ahay.org/wiki/Adding_new_programs_to_Madagascar) and this 
[tutorial on Youtube](https://www.youtube.com/watch?v=3Kkh0KF_4G8)