# Gobuster Usage

## Directory/File Fuzzing
The commands that we have given allready have the best wordlists. If
you are confused which wordlist to use, here.
```bash
gobuster dir -u URL -w wordlist
gobuster dir -u http://144.126.192.55:30886 -w /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt
```

## Virtual Host Fuzzing
```bash
gobuster vhost -u URL -w wordlist
gobuster vhost -u http://bagel.htb:8000 -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-110000.txt
```

