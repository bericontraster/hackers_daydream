# FFUF

## VHost Fuzzing with FFuF  
```bash
ffuf -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt:FUZZ -u http://mailroom.htb/ -H 'Host: FUZZ.mailroom.htb' -ac -c -ic
```

Here is a breakdown of the command and its options:

    -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt:FUZZ specifies a wordlist to use for fuzzing. In this case, it is using the "subdomains-top1million-20000.txt" file located in the "/usr/share/seclists/Discovery/DNS" directory, and replacing the "FUZZ" placeholder with each word in the file.
    -u http://mailroom.htb/ specifies the target URL to fuzz.
    -H 'Host: FUZZ.mailroom.htb' adds a custom Host header to the HTTP request. This will replace the "FUZZ" placeholder in the header with each word in the wordlist.
    -ac prints all HTTP responses, including those with a non-2xx status code.
    -c colorizes the output.
    -ic ignores HTTP response codes with the 401 status code.

In summary, this command is using a wordlist to fuzz the subdomains of "mailroom.htb" by sending HTTP requests with a custom Host header. The output will be colorized and will include all HTTP responses except those with a 401 status code.
