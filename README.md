# cool
A repository for the study of the cool language and compiler, given in the Compilers class, by Stanford Online

`Cool` stands for **C**lassroom **O**bject **O**riented **L**anguage

The course project is to build a complete compiler that compiles Cool into MIPS Assembly

The project will be break down into 4 programming assingments (PAs)
- Lexical analysis
- Parging
- Semantic analysis
- Code Generation



# Assignments
There will be four programming assingments (pa), each one convering one component of the compiler:
- lexical analysis (PA2)
- parsing (pa02)
- semantic analysis (pa03)
- code generation (pa04)

- Optimization (optional assignment)

Each assignment will ultimately result in a working compiler pahse wich can interface with other phases.

I will choose doing this project in C++, as I can do it in C++ or in Java.

# Installation on Linux guide
Through the course highly recommends using a virtual machine, I'm doing this using a github codespaces in order to fit the study in my routine, in many computers I use daily. So, I will be following the course guide to setup the env in my onw machine.

### Steps
```bash

```

1. Install packages (If you only intend to use the C++ version, you don't need the jdk). For Ubuntu:
```bash
$ sudo apt-get install flex bison build-essential csh openjdk-6-jdk libxaw7-dev
```

2. Make the /usr/class directory:
```bash
$ sudo mkdir /usr/class
```

3. Make the directory owned by you:
```bash
$ sudo chown $USER /usr/class
```

4. Go to /usr/class and download the tarball:
```bash
$ cd /usr/class

$ wget https://courses.edx.org/asset-v1:StanfordOnline+SOE.YCSCS1+1T2020+type@asset+block@student-dist.tar.gz
```

5. Untar:
```bash
$ tar -xf student-dist.tar.gz
```


If you want things exactly like the VM:
1. Add a symlink to your home directory:
```bash
$ ln -s /usr/class/cs143/cool ~/cool
```

2. Add the bin directory to your $PATH environment variable. If you are using bash, add to your `.profile` (or `.bash_profile`, etc. depending on your configuration; note that in Ubuntu have to log out and back in for this to take effect):
```bash
PATH=/usr/class/cs143/cool/bin:$PATH
```



