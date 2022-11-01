# Highlight

## ***Linux aministration***
### Basic knowlegde
1. All in linux are files: commands, mouse, keyboard,...
2. Type of files in linux

File type | First character in file listing | Description
--- | :---: | ---
Regular file | - | Normal file as text, data or executable files
Directory | d | File that are lists of other files
Link | l | A shortcut that points to the location of the actual file
Special file | c | Mechanism used for input and output, such as files in /dev
Socket | s | A special file that provides inter-process networking protected by the file system's access control
Pipe | p | A special file that allows processes to communicate with each other without using network socket semantics

3. File permission
> Structure: filetype + user's permission + group's permission + other's permission

Symbol | Description
--- | ---
r | Permission to read a file or list a directory's content
w | Permission to write to a file or create, remove files from a directory
x | Permission to execute a program or change into directory and do a long listing of the directory
\- | No permission

sample:
  ```
  $ ls -l /bin/login
  -rwxr-x--- 1 root root 19080 Apr 1 18:26 /bin/login
  ```

  + "-" => file type: file
  + "rwx" => user's permission: read + write + execute
  + "r-x" => group's permission: read + execute
  + "---" => other's permission: not have any permission
  + 1 => user's id
  + root => user: root
  + root => group: root

> Add / remove / set permission by symbol: target (+ | -) symbol_permission
- Sample:
  ```
  $ chmod o+x /tmp/sample.txt => Add permission x for other's permission
  $ chmod g-w /tmp/sample.txt => Remove permission w from group's permission
  $ chmod u=rwx /tmp/sample.txt => Set full permission for user owner file
  ```
> Change permission by numeric
- Permissions are calculated by:
  - 4 (r)
  - 2 (w)
  - 1 (x)

- Sample
  ```
  $ chmod 640 /tmp/sample.txt
  => user's permission: rw-
  => group's permission: -w-
  => other's permission: ---

  $ ls -l /tmp/sample.txt
  -rw--w---- 1 drubyy devops 19080 Apr 1 18:26 /tmp/sample.txt
  ```

#### Most used Linux distros currently:
- RPM based: RHEL & Centos
- Debian based : Ubuntu Server

#### Some important directories
- Home: /root, /home/username
- User executables: /bin, /usr/bin, /usr/local/bin
- System executables: /sbin, /usr/sbin, /usr/local/sbin (like apt install, apt remove, etc...)
- Other mountpoints: /media, /mnt
- Configuration: /etc
- Temporary files: /tmp
- Kernels and Bootloader: /boot
- Server data: /var, /srv
- System information: /proc, /sys
- Shared libraries: /lib, /usr/lib, /usr/local/lib


### Commands
Structure
```
command + options + argruments
```

#### Add Group and users
```
addgroup groupname
adduser username
```
> Command valid just for root user

#### ls
Options | Description
--- | ---
-f | Long listing format of files, one per line
-a | List all hidden files and directories started with '.'
-F | Add a '/' classification at the end of each directory
-g | List all files and directories with the group name
-i | Print index number of each files and directories
-m | List all files and directories separated by comma
-n | List numeric UID and GID of owner and group
-r | List all file and directories with reverse order
-R | Short list all directories
-t | Shorted by modified of time, start with the newest file

#### grep
```
grep -i "hello wOrld" /path/to/file => Does not distinguish between uppercase and lowercase letters
grep "some words" /path/to/folder => Grep all files in that folder
```

#### find
```
find /path/to/directories/ -name "filename" => Find with file name in path
```

#### sed
```
sed "s/searchFor/replaceWith/g" /path/to/file => replace all "searchFor" to "replaceWith"
sed -R "s/searchFor/replaceWith/g" /path/to/directory => replace all "searchFor" to "replaceWith" at all files in directory
```

#### IO redirection

Sample command | Description
--- | ---
sudo apt install package_not_exist 2>> /tmp/error.log | Append error command to /tmp/error.log
sudo apt install vim 1>> /tmp/success.log | Append success command to /tmp/success.log
sudo apt install vim >> install_package.log | Append command to install_packate.log file
sudo apt install package_not_exist >> /tmp/server.log | Append both success and error to /tmp/server.log
sudo apt install vim > /tmp/server.log | remove all data in file if exist and write new data

## ***Vim***
- 3 modes:
  - Commands
  - Extended command
  - Insert

Command | Command mode | Extended command mode | Description
--- | :---: | :---: | ---
gg | x |  | To go to the beginning of the page
G | x | | Go to end of the page
w | x | | To move the cursor forward, word by word
b | x | | To move the cursor backward, word by word
nw | x | | To move the cursor forward to n words (SW)
nb | x | | To move the cursor backward to n words (SB)
u | x | | To undo last change (word)
U | x | | To undo the previous changes (entire line)
Ctrl + R | x | | To redo the changes
yy | x | | To copy a line
nyy | x | | To copy n lines (Syy or 4yy)
p | x | | To paste line below the cursor position
P | x | | To paste line above the cursor position
dw | x | | To delete the word letter by letter (like backspace)
dd | x | | To delete entire line
ndd | x | | To delete n no. of lines from cursor position
/ | x | | To search a word in the file
w | | x | To Save the changes
q | | x | To quit
wq | | x | To save and quit
w! | | x | To save forcefully
wq! | | x | To save and quit forcefully
x | | x | To save and quit
20(n) | | x | To go to line no 20 or n
se nu | | x | To set the line numbers to the file
se nonu | | x | To Remove the set line numbers
w | | x | To Save the changes

### systemctl
#### Make software run after reboot
```
$ systemctl start package_name
$ systemctl enable package_name
```

#### Checking status
```
$ systemctl status package_name
$ systemctl is-active package_name
$ systemctl is-enable package_name
```

#### tips kill PID
```
ps aux | grep "package_name" | awk '{print $2}' | xargs kill -9
=> kill processes of package_name
```