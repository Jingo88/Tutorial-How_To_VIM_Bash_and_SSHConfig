# Basic VIM Commands / Bash Profile / SSH Configuration

I am putting together this guide to help make things easier because lets face it, nobody wants to type "ssh root@yoursuperlongurl" every single time they log into their servers. This readme will cover some simple vim commands, how to put environmental variables in your bash profile, and how to configure your ssh config file to hold multiple ip addresses as shortcuts.

##### [I. VIM Commands](#vim)
##### [II. Bashrc vs. Bash_Profile and Your Environmental Variables](#bash)
##### [III. SSH Config](#ssh)

### <a name=vim>I. Basic VIM Commands</a>

You can use the vi command to do anything from creating a new html file, to viewing a log file, to editing your bash file. Simply writing "vi" will open the targeted file, and if there isn't any file by that name then you will see a blank screen for the new file you just created. Some examples are:


* vi index.html
* vi ~/.bashrc
* vi /etc/hosts


Here are some commands for when you vim into a file:


* i - Insert. Pressing "i" allows you to edit the file
* esc - Escape. Press this to escape "insert" mode
* :q - Quit. This will quit the file, only if no changes were made
* :wq - Write, Quit. This will make the changes and quit the file. Cannot be in "insert" mode
* :q! - Quit Override. This will allow you to quit and discard the changes made
* :wq! - Write, Quit, Override. I just do this shit out of habit
* /findthis - searching for a word or phrase. Replace "findthis" with the word you want to find and then hit enter. This is case sensitive. Press "n" to go to the next instance of the searched word
* y - Yank. Pressing "y" once will copy the link the cursor is on. Pressing "y" again will end your copy for that line. 
* v - Visual Mode. Instead of copying the whole line with "y" you can enter visual mode to highlight certain text.
* p - Put. Puts the text you just yanked onto the line where your cursor is
* Copying and Pasting - simple cmd+c and cmd+v will work as well
* 0 - Zero. Goes to the beginning of the line you are on
* "z." - Center. Center's your screen to where your cursor is located
* u - Undo. Undo changes (just like ctrl+z)



### <a name=bash>II. Bashrc vs. Bash_Profile and Your Environmental Variables.</a>

Alright people, lets get into the nitty gritty as to the differences between your bashrc file and your bash_profile file. What's the difference? They do similar things in the sense that if you export a PATH in either file that path can be used. One main difference is the bash_profile will only run **once** on the login of the first terminal window. If you were to make a new terminal window (cmd+n on mac / Tmux on windows) the variables set in your bash_profile cannot be used in your second window. 

The bashrc file will be run on each instance of a new terminal window so your variables can be used anywhere. Yes it does sound more appealing to use the bashrc over the bash_profile. But when does the bash_profile come in handy? Lets take the example that on the loading of a terminal screen you have a command that runs some lengthy list that you only want once. Instead of having that list show up every time you launch a new terminal window it will show up only in your initial window. 

So what are some other similarities / differences / notes that we can take away from the bashrc and bash_profile:

* Your bashrc and bash_profile are normally hidden and in the same directory (usually your home directory)
* If you don't know which directory the bash files are in you can use the "find" command
* Since the files are most likely hidden files, you will need to use "sudo" to give access to locate hidden files
* If you do know which directory the bash files are in you can use the "ls -a | grep" command
 

```
* sudo find / -name bashrc
(Lets break this down a little more)

	* sudo - gives you temporary root power, you have to type in your password. We are using this ONLY BECAUSE the files are hidden
	* find - find or search
	* / - this is the home directory of your ROOT, not your user
	* -name - says you are searching by name of the file
	* bashrc - the name of the file being searched for
	
* ls -a | grep bash
(Lets break this command down now)

	* ls - List Setting - list all the files/folders in your current directory
	* -a - shows all hidden files
	* | grep - searches through the list 
	* bash - any file/folder containing the word bash

```

Now that we are finished with that super long explaination about how to find your bashrc and bash_profile files lets start editing them. For now we'll stick with going into the bashrc file and adding the environmentail variables there. The process will be the same either way. 

* vim into your bashrc file

```
vi bashrc
(This is only if you're in the current directory, if it is in a different directory and you know the directory path use that.)

Example: vi /etc/bashrc
```

* BUT WAIT IT'S A READ ONLY FILE?!?!?!
* Yes you cannot edit your bashrc file unless you have root access. Again we need "sudo" access (if you are not in root) 

```
sudo vi bashrc
```

* Now here is where you get to use your savvy vim skillz (yes with a "z")
* Press "i" to enter the INSERT mode
* Go to the last line and enter your Environmental Variables
* Below are examples of some exported variables and aliases

```
export portfolio=/mystuff/aboutme/portfoliopage
(Now portfolio can be used in the terminal)

cd $portfolio
(You will jump to the portfolio folder from whatever directory you were previously in)

alias c='clear'
(You have shorthanded your clear command)

In terminal instead of typing "clear" to clear out all the text you can now just type "c"
```

* LAST STEP!!!
* After saving the edits in your file and quitting vim (:wq!) please use the following command to make sure you can use your new variables and shortcuts

```
source bashrc
```

* Some more useful things
* To see your current variables

```
echo $portfolio
(This will return the path of that variable)

env | sort
(This will list all of your environmental variables in alphabetical order)
```


### <a name=ssh>III. SSH Configuration</a>

* Open your terminal and input the following command

```
vi ~/.ssh/config

```

* press “i” for insert and type in the following on a new line.

```
Host (whatever you want)
hostname (your ip-address)
user root
```

* If you get broken pipes because of idling while logged into your server you can also put the following two lines in your ssh config file. This part isn’t necessary.

```
ServerAliveInterval 30
ServerAliveCountMax 120
```

* This will sent a ping from your machine every 30 seconds for 120 times. 
* Now complete your edits and your configuration should take place

```
press “esc”
press “:wq!” - write, quit, override
```

* Here is an example of how the syntax should look.

```
Host abc
hostname 127.0.0.1
user root
ServerAliveInterval 30
ServerAliveCountMax 120
```

* Now when you are in terminal type “ssh abc"
* If you want to add more ip's, make sure there is a line space between each ssh configuration