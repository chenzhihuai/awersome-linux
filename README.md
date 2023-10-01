# Awesome linux
## awesome tools
- bat      - a color-full highlighted alternative to cat    
- fzf      - A command-line fuzzy finder                    
- tldr     - too long; don't read                           
- rg       - ripgrep: search content in directory            
- fd - A simple, fast and user-friendly alternative to 'find'
- fasd - fasd - Command-line productivity booster, offers quick access to files and directories 
- bd,up - Quickly go back to a parent directory
------------
- zsh      - a better alternative to bash                   
- tsp - task spooler. A simple unix batch system
- valgrind - c++ profiler [^4]                              
- mdlt - A command-line utility for quick math.
- ranger  - a file browers like vim                        

Other maybe useful: pipe_exec, parallel, column -t, colc, has, tmux, sslocal[^3], xsv, pget

reference: https://github.com/agarrharr/awesome-cli-apps and https://github.com/alebcay/awesome-shell


[^1]: add ~/.apt/usr/bin to $PATH and ~/.apt/usr/lib to `$LD_LIBRARY_PATH`, maybe some other directory.
[^2]:
[^3]: see shadowsocks.json 
[^4]: see http://senlinzhan.github.io/2017/12/31/valgrind/
[^5]: see https://github.com/rupa/v
## .profile vs .bashrc
|      | non-login   | login        |
|------|-------------|--------------|
| user | ~/.bashrc   | ~/.profile   |
| all  | /etc/bashrc | /etc/profile |

reference: https://www.baeldung.com/linux/bashrc-vs-bash-profile-vs-profile


## about user and group

tips: user file
| file        | note     | format                                    |
|-------------|----------|-------------------------------------------|
| /etc/passwd | user     | username:password:uid:gid:info:home:shell |
| /etc/group  | group    | group:password:gid:user1,user2,...        |
| /etc/shadow | password |                                           |

## linux file permission
```
-rw-r--r-- 12 linuxize users 12.0K Apr  28 10:10 file\_name
|[-][-][-]-   [------] [---]
| |  |  | |      |       |
| |  |  | |      |       +-----------> 7. Group
| |  |  | |      +-------------------> 6. Owner
| |  |  | +--------------------------> 5. Alternate Access Method
| |  |  +----------------------------> 4. Others Permissions
| |  +-------------------------------> 3. Group Permissions
| +----------------------------------> 2. Owner Permissions  
+------------------------------------> 1. File Type: regular file (-), directory (d), symblic (l)
```

about `s` flag:
- on directory's group triplet: New file inherits this directory's group id instead of current user's group id.
- on file: When the setuid or setgid flags are set on an executable file, the file is executed with the file’s owner and/or group privileges.


## about daemon
daemon represent '守护进程' aka '后台进程'. Lots of service command is end with 'd', such as mongod, sshd. The basic things: `/etc/init.d/` (OLD)
* it constains script to control service, e.g. /etc/init.d/sshd start
* `init` will invoke them at system start

Modern linux use systemd instead of init. it binds to command `systemctl`. It use catalogary such as `service`, `socket`, `timer`.

## about process and job
* fork-and-exec
* parent and children, process tree, 
* process group: exec pipeline from shell
* job: 
* session: share the terminal input and output
> Basically, a new session is created in two cases:
> When we need to log in a user with an interactive shell. A shell process becomes a session leader with a controlling terminal (about this later).
> A daemon starts and wants to run in its own session in order to secure itself (we will touch daemons in more detail later).

about nohup
> The nohup performs the following tricks:
>Changes the stdin fd to /dev/null.
>Redirects the stdout and stderr to a file on disk.
>Set an ignore SIG_IGN flag for SIGHUP signal. The interesting moment here is that the SIG_IGN is preserved after the execve() syscall.
>Run the execve().

## about single vs. double quotes
https://phoenixnap.com/kb/bash-single-vs-double-quotes

## about /proc
https://www.tecmint.com/exploring-proc-file-system-in-linux/

## expression in shell
int only:
echo $((1+2))
z=$(expr 1+3)  
let k=3+5

float:
echo $(echo 1 + 2.2 | bc)
y=$(bc <<< 1.1 + 2.2)

## loop
```bash
#split by whitespace
for var in a b c 
do 
  echo $var 
done
# use ; instead of newline
for var in $(ls);do echo $var; done

## The C-style Bash for loop ##
for (( initializer; condition; step ))
do
  shell_COMMANDS
done
```

