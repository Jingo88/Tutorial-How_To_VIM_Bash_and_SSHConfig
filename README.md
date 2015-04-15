# Basic VIM Commands / Bash Profile / SSH Configuration

I am putting together this guide to help make things easier because lets face it, nobody wants to type "ssh root@yoursuperlongurl" every single time they log into their servers. This readme will cover some simple vim commands, how to put environmental variables in your bash profile, and how to configure your ssh config file to hold multiple ip addresses as shortcuts.

##### [I. VIM Commands](#vim)
##### [II. Env Var to Bash](#bash)
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



### <a name=bash>II. Add Enrivonmental Variables To Your Bash Profile</a>

* vim into your bash file

```
vi ~/.bashrc
```

* Add environmental variables to this file

```
export Portfolio_Home=/home/mystuff/portfolio/
```
* Make sure you input this after the line that says 

```
# User specific aliases and functions
```

* Once you exit and log back in the exported variable will take effect
* Find out if your variable persist

```
echo $Portfolio_Home

should show the path

/home/mystuff/portfolio
```

* For an organized view of all the environmental variables in your server input the following command

```
env | sort
```

* This will show you all your variables in alphabetical order




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