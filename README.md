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


