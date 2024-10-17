---
layout: default
---

# Command-Line Course

## Introduction
This course aims to provide a gentle introduction to the UNIX command line environment. The command line is a useful tool for language technology in today’s fast changing world, where many libraries and software are being published and updated rapidly, therefore
providing only the most basic command line interfaces. Moreover, command line is a very efficient interface, which can substantially improve the speed of development when used properly. 

<img src="https://imgs.xkcd.com/comics/fight.png" alt="Photo" hspace="80" width="60%">

(photo source: https://imgs.xkcd.com/comics/fight.png)
## Weekly Content

Week | Content | 
1 | Introduction to the Command Line |
2 | Navigating a UNIX System |
3 | Introduction to Corpus Processing |
4 | Advanced Corpus Processing |
5 | Scripting and UNIX Configuration Files |
6 | Installing and Running Programs |
7 | Version Control |

### Week 1: Introduction to the Command Line
In this week we set up our command-line environement and learned basic commands. To list just a few examples: 
- `ls`: list the contents of the current directory; 
- `cd`: change directory; 
- `wget`: download contents from the internet;
- `nano` : edit text.


### - Week 2: Navigating a UNIX system
In this week we continued to learn more about the UNIX system, such as `cp` for copying files, `mv` for moving files and `rm` to remove files. We also learned about remote servers.
```
ssh <username>@puhti.csc.fi
```
This is the command to connect to the puhti server.

### - Week 3: Basic Corpus Processing
This week was about using text processing tools in UNIX. First we learned about character encodings. Then we learned some useful commands of text processing, for example:
```
cat file.txt| tr '[:space][:punct:] ' '\n' | sort -f | uniq -i > word_list.txt
```
This command will generate a word list of file.txt.
We also learned simple regular expressions and the `egrep` command which is for searching for contents in text files.\

### - Week 4: Advanced Corpus Processing
This week we learned more about text processing using UNIX commands. We learned to combine simple commands into more complex command pipelines. First we learned the `sed` command which is for finding and replacing strings, and also for insertion, deletion, search, and other common requirements. Then we learned, for example, creating a sentence-per-line file by using this command:
```
cat file.txt | dos2unix | sed 's/^$/^#/' | tr '\n' ' ' | sed -E 's/([.?!]) ([A-Z])/\1#\2/g' | tr '#' '\n' | sed 's/^ #//' | sed 's/ *$//' | grep -v "^$" > sentence_per_line.txt
```

### - Week 5: Scripting and Configuration Files
This week we learned about combining commands in scripts. For example, we wrote a script to generate frequence lists:
```

#! /bin/bash
if [ $# -ne 2 ]
then
	echo "error"
	echo "$0 input_text_file output_freq_file
	exit 1
fi

cat $1|
dos2unix|
tr -s "[:space:]" "\n"|
tr -d "[:punct"]" |
sort |
uniq -c |
sort -nr > $2
```
We would also use `chmod u+x` to obtain access to this script.
We also learned about setting environment variables, as well as the `source` command to source .bashrc file.

### - Week 6: Installing and Running Programs
This week we first learned about intalling programs. The `sudo apt-get` is used for installing software and `pip install` for installing python packages. We also learned why it's important to create a virtual enviroment for each project and to use `python3 -m venv venv` to create a venv. 
Finally, we learned `make` command, for example:
```
%.freq: %.no_md.txt
    bin/freqlist.sh $< $@
```
This is a make rule which has a target %.freq and dependency %.no_md.txt. We could also use `make clean` command to remove all the files that `make` generated. 

### - Week 7: Version Control
This week we learned version control using Git and Github. We also learned how to use `git add`, `git commit` and `git push` commands to add, commit and push changes to the Github repository. We also learned about creating and merging branches. Lastly, we learned to build our own webpages using Github.
