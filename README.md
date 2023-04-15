### Web-Penetration-Testing-Algorithm
# Algorithm showing the order in which information is mined for web pages

---

## Tools we are using here
- NMAP
- GoBuster
- Responder
- Hydra

---

## General (enumeration)

```mermaid
graph TD;
    enum(((ENUMERATION))) --- nmap(((NMAP))) & gobuster(((GOBUSTER))) 
    
    %% ----------------------------- NMAP -----------------------------
    
    nmap --> host[/"Host -t A &lt;URL&gt;"/] 
    host --> nmap_cmd[/"sudo nmap -sV -sC -Pn -O -p- &lt;IP&gt;"/]
    nmap_cmd --> ftp[FTP] & rpcbind[RPC BIND] & nmap_other[Other ports]
    ftp --> ftp_anon[FTP ANONYMOUS LOGIN]
    ftp_anon ---> exploit[Exploiting]
    
    rpcbind --> rpcbind_showmount[/showmount -e <IP>/]
    rpcbind_showmount --> rpc_bind_showmount_if{If there are some files}
    rpc_bind_showmount_if -- YES --> rpc_bind_showmount_if_yes[/"sudo mount #45;t &lt;IP&gt;:&lt;PATH&gt; #47;mnt"/]
    rpc_bind_showmount_if_yes ---> exploit
    
    nmap_other --> nmap_other_hint[Looks for cve or some exploit using searchsploit. Try to use deafault login and passwords. Ultimately use Hydra]
    nmap_other_hint ---> exploit
    
    %% ----------------------------- GOBUSTER -----------------------------
    
    gobuster --> gobuster_hint[Look for some interesting dirs]
    gobuster_hint --> curl_check[Check your permission to see the website]
    curl_check --> curl_cmd[/"curl -I &lt;URL&gt;"/]
    curl_cmd --> exploit
    
    
    
    click nmap href "https://nmap.org" _blank
    click gobuster href "https://github.com/OJ/gobuster" _blank
    click nmap_other_hint href "https://github.com/vanhauser-thc/thc-hydra" _blank
```

---

##TO DO

-[ ] Checking what's webiste engine is running on
-[ ] XSS,CSRF,SQLi etc.
-[ ] Priviledge Escalation
