# Port-checking-commands
Port-checking-commands

## netstat

### Command for Checking which all ports are open in ec2 instance

```

[root@ip-172-31-45-113 ~]# netstat -ntlp
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      3317/sshd           
tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN      3027/master         
tcp        0      0 0.0.0.0:111             0.0.0.0:*               LISTEN      2583/rpcbind        
tcp6       0      0 :::22                   :::*                    LISTEN      3317/sshd           
tcp6       0      0 :::111                  :::*                    LISTEN      2583/rpcbind   

```

We are going to install httpd

> [root@ip-172-31-45-113 ~]#yum install httpd -y

> [root@ip-172-31-45-113 ~]# systemctl start httpd.service 


If we run the `netstat -ntlp` command once more we can see port **80**

```

[root@ip-172-31-45-113 ~]# netstat -ntlp
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      3317/sshd           
tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN      3027/master         
tcp        0      0 0.0.0.0:111             0.0.0.0:*               LISTEN      2583/rpcbind        
tcp6       0      0 :::22                   :::*                    LISTEN      3317/sshd           
tcp6       0      0 :::111                  :::*                    LISTEN      2583/rpcbind        
tcp6       0      0 :::80                   :::*                    LISTEN      3566/httpd  

```

If you want to search for a particular port (for example 80)

```

[root@ip-172-31-45-113 ~]# netstat -ntlp |  grep 80
tcp6       0      0 :::80                   :::*                    LISTEN      3566/httpd 

```

## lsof

We can do the same by using **lsof** command

Linux/Unix consider everything as file and maintains folder. So “Files or a File ” is very important in Linux/Unix. While working in Linux/Unix system there might be several file and folder which are being used, some of them would be visible and some not. 
lsof command stands for List Of Open File. This command provides a list of files that are opened. Basically, it gives the information to find out the files which are opened by which process. With one go it lists out all open files in output console. It cannot only list common regular files but it can list a directory, a block special file, a shared library, a character special file, a regular pipe, a named pipe, an internet socket, a UNIX domain socket, and many others. it can be combined with grep command can be used to do advanced searching and listing. 

Syntax: `$lsof [option][user name]`

```
# lsof -i TCP:22

COMMAND  PID    USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
sshd    1471    root    3u  IPv4  12683      0t0  TCP *:ssh (LISTEN)
sshd    1471    root    4u  IPv6  12685      0t0  TCP *:ssh (LISTEN)

```
#### Run any one of the following command on Linux to see open ports:
```
sudo lsof -i -P -n | grep LISTEN
sudo netstat -tulpn | grep LISTEN
sudo ss -tulpn | grep LISTEN
sudo lsof -i:22 ## see a specific port such as 22 ##
sudo nmap -sTU -O IP-address-Here  ## For Debian or Ubuntu Linux based system
```

## telnet

### Command for Checking If a particular port is open or not from an other mechine

Syntax : `telnet <Public IP> <port number>`

```
  
Aspire-A315-55G:~$ telnet 13.233.233.43 80
Trying 13.233.233.43...
Connected to 13.233.233.43.
Escape character is '^]'.
^C
Connection closed by foreign host.
Aspire-A315-55G:~$ telnet 13.233.233.43 443
Trying 13.233.233.43...
telnet: Unable to connect to remote host: Connection refused
Aspire-A315-55G:~$ 

```
From this we can understand that port **80** is open and port **443** is not open

