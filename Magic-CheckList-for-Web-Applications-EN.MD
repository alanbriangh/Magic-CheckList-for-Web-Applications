# Magic CheckList for Web Applications

**Information Gathering:**

- [ ] OSINT
    - [ ] [Google](https://www.google.com)

        Use dorks, site, inurl, intext, intitle, etc.

    - [ ]  [Bing](https://www.bing.com)
    - [ ]  [Duckduckgo](https://duckduckgo.com)

        site:target.com inurl:'&'

    - [ ]  [Censys](https://censys.io)
    - [ ]  [Shodan](https://www.shodan.io)

        Use filters

        - [Shodan Firefox Addon](https://addons.mozilla.org/en-US/firefox/addon/shodan_io/)
    - [ ]  [Github](https://github.com)
        - [GitGot](https://github.com/BishopFox/GitGot)

        ./gitgot.py --gist -q CompanyName
        ./gitgot.py -q '"example.com"'
        ./gitgot.py -q "org:github cats"

        - [Gitrob](https://github.com/michenriksen/gitrob)
        - [https://shhgit.darkport.co.uk](https://shhgit.darkport.co.uk/)
    - [ ]  [Gitlab](https://gitlab.com/)
    - [ ]  [Pastebin](https://pastebin.com)
        - [PasteLert](https://andrewmohawk.com/pasteLert/)
    - [ ]  [Trello](https://trello.com)

        Example of google dork: inurl:[https://trello.com](https://trello.com/) AND intext:target.com
        site:trello.com target.com

    - [ ]  [Linkedin](https://www.linkedin.com/uas/login?_l=es)

        Find developers working at the target company and check their github/gitlab repos

    - [ ]  Acquisition
        - [Crunchbase](https://www.crunchbase.com)
        - [Wikipedia](https://es.wikipedia.org)

        Very useful for wide/undefined scopes (For example AT&T)

- [ ]  Find ASNs Autonomous System Number)

    Find which organization registered the domains [Use Whois](http://whois.domaintools.com)

    - [http://asnmap.com](http://asnmap.com/) (Get ASN Map)
    - [https://bgp.he.net](https://bgp.he.net/) (Get ASNs)
    - [https://mxtoolbox.com/asn.aspx](https://mxtoolbox.com/asn.aspx)
- [ ]  Get Domains / Subdomains for an IP range
    - [https://github.com/zeropwn/spyse.py](https://github.com/zeropwn/spyse.py)

    spyse -target xxx.xxx.xxx.0/24 --domains-on-ip

- [ ]  Find unique domains

    for i in $(cat domain_names.txt); do echo""; echo "ASN $i";echo ""; amass intel -active -asn $i;echo ""; done

- [ ]  Find Subdomains
    - [Findomain](https://github.com/Edu4rdSHL/findomain)
    - [Sublist3r](https://github.com/aboul3la/Sublist3r)

        python3 [sublister.py](http://sublister.py) -d target.com

    - [Acamar](https://github.com/si9int/Acamar)

        python3 acamar.py [t](http://twitter.com/)arget.com

    - [Assetfinder](https://github.com/tomnomnom/assetfinder)

        assetfinder --subs-only [dominio.com](http://dominio.com/) | httprobe -t 40000 | tee -a salida.txt

        -t  Timeout in milliseconds (40000 is double the default)

    - [Amass](https://github.com/OWASP/Amass)

        amass net -asn 12345
        amass enum --passive -d <DOMAIN>

    - [Altdns](https://github.com/infosec-au/altdns)

        altdns -i subdomains.txt -o out.txt -w wordlist.txt -r -s out_final.txt

    - [http://arthusu.xyz/subdomainScanner/](http://arthusu.xyz/subdomainScanner/)
    - [ ]  Subdomain Takeover
        - [Subjack](https://github.com/haccer/subjack)
        - [Subzy](https://github.com/LukaSikic/subzy)
        - [Subdomain-Takeover](https://github.com/antichown/subdomain-takeover)

        Check the error message on the page according to "[Can I take over XYZ](https://github.com/EdOverflow/can-i-take-over-xyz)"

- [ ]  Screenshots
    - [Aquatone](https://github.com/michenriksen/aquatone)

        Example:
        cat hosts.txt | aquatone -ports (xlarge, small, medium, large, xlarge) -out ~/path/output  -scan-timeout 500 -screenshot-timeout 50000 -http-timeout 6000

    - [Gowitness](https://github.com/sensepost/gowitness)
- [ ]  Find directories
    - [Dirsearch](https://github.com/maurosoria/dirsearch)

    Example:
    python3 [dirsearch.py](http://dirsearch.py/) -u target.com -E -w ./directory-list-lowercase-2.3-medium.txt -f -t 20 --plain-text-report=/tmp/out.txt

    - [Gobuster](https://tools.kali.org/web-applications/gobuster)
    - [ffuf](https://github.com/ffuf/ffuf)

    The secret is to make your own wordlist! But you can use the following as well: [all.txt](https://gist.github.com/jhaddix/f64c97d0863a78454e44c2f7119c2a6a) [dirbuster wordlists](https://github.com/daviddias/node-dirbuster/tree/master/lists) [SecLists](https://github.com/danielmiessler/SecLists)

    You can use the following tools to create custom Wordlists:
    - [CeWL](https://github.com/digininja/CeWL)
    - Burp "Wordlist Extractor"

- [ ]  Scanner CMS
    - [CMSMap](https://github.com/Dionach/CMSmap)
    - [WPscan](https://github.com/wpscanteam/wpscan)
- [ ]  Find apps on the Webserver (Virtual hosts/Subdomain), uncommon ports, DNS zone transfers
    - [Masscan](https://github.com/robertdavidgraham/masscan)

        Example:
        ./masscan -iL targets.txt -p0-65535 --max-rate 10000 -sS -Pn --randomize-hosts -banners -oX output.xml

        -p0-65535 (all ports)
        -max-rate 10000 (Number of packets pr. second to trasmit. Default is 100/second)

        Most common web ports:
        ./masscan -p443,8443,80,8080,8000 165.183.102.0/23,165.183.106.0/24,165.183.108.0/24 --rate 1000

    - Massdns

        Resolves AAAA records from a list of domains (domains.txt) and saves them in results.txt

        ./bin/massdns -r lists/resolvers.txt -t AAAA -w results.txt domains.txt
        (AAAA is for ipv6, A is for ipv4)

        [Updated list of resolvers:](https://github.com/bberastegui/fresh-dns-servers)
        ./bin/massdns -r <(curl -s https://raw.githubusercontent.com/BBerastegui/fresh-dns-servers/master/resolvers.txt)

        ./bin/massdns -r lists/resolvers.txt -t AAAA -w results.txt domains.txt

        (AAAA is for ipv6, A is for ipv4)

        ./scripts/ptr.py | ./bin/massdns -r lists/resolvers.txt -t PTR -w ptr.txt

    - [Nmap](https://nmap.org)

        nmap target -sS -A -PN -sC -sV -vvv -p-65535

        -sS syn scan
        -A OS + service fingerprint
        -PN No Ping
        -sC Scripts
        -sV Detección de versiones
        -vvv Verbosity
        -p-65535 (all ports, except 0) (-p-)

    - [HTTProbe](https://github.com/tomnomnom/httprobe)

        Example:
        cat archive.txt | ./httprobe -p http:81 -p https:8443 -p http:8000 -p http:8001 -p http:8080 -p http:8181 -t 40000 

        -t  Timeout in miliseconds (40000 is double the default [20000])

    - [Nikto](https://github.com/sullo/nikto)

        Example:
        nikto -host <IP> -output <out> -port 

    - [Virtual Host Discovery](https://github.com/jobertabma/virtual-host-discovery)
- [ ]  Identify "entry points" in the app (Identifies from hidden fields, parameters, HTTP methods, header analysis)
- [ ]  Fingerprints (Framework, technology, etc.)
    - [Wappalyzer](https://www.wappalyzer.com) (browser extention)
- [ ]  Maps the architecture of the app (Identify application architecture including Web language, WAF, Reverse proxy, Application Server, Backend Database)
- [ ]  Robots.txt and review the HTML source code
- [ ]  Web Crawler
    - Crawl burp (ex spider)
    - [Hakrawler](https://github.com/hakluke/hakrawler)

    Example:
    ./assetfinder target.com | hakrawler

    ./hakrawler -url target.com -depth 1

    - [http://arthusu.xyz/crawler/index.php?menu=crawler](http://arthusu.xyz/crawler/index.php?menu=crawler)
- [ ]  Waybackmachine
    - [Waybackurls](https://github.com/tomnomnom/waybackurls)
    - [WaybackurlSqliScanner](https://github.com/ghostlulzhacks/waybackSqliScanner)
    - [http://arthusu.xyz/crawler/index.php?menu=urls](http://arthusu.xyz/crawler/index.php?menu=urls)
- [ ]  GetAllUrls ([GAU](https://github.com/lc/gau))

    Example:
    gau example.com

- [ ]  File analysis js
    - [Relative-url-extractor](https://github.com/jobertabma/relative-url-extractor) (Extract JS from file for analysis)
    - [JSParser](https://github.com/nahamsec/JSParser) (find endpoints in the JS)
    - [LinkFinder](https://github.com/GerbenJavado/LinkFinder) (Find URLs and parameters in the JS)
    - [http://arthusu.xyz/crawler/index.php?menu=JsScanner](http://arthusu.xyz/crawler/index.php?menu=JsScanner)
- [ ]  Parameter fuzzing
    - f[fuf](https://github.com/ffuf/ffuf)
    - [Wfuzz](https://wfuzz.readthedocs.io/en/latest/)
    - [Arjun](https://github.com/s0md3v/Arjun)

        Example:
        python3 arjun.py -u https://api.example.com/endpoint --get -o result.json

        python3 arjun.py --urls targets.txt --get -o result.json

- [ ]  Tools that make "TODO" lists
- [Photon](https://github.com/s0md3v/Photon)

    Example:
    python3 [photon.py](http://photon.py/) -u https://www.target.com -l 3 -t 100 --wayback -o /output/dir/ -v --keys --dns

- [Lazyrecon](https://github.com/nahamsec/lazyrecon)

    Example:
    ./lazyrecon.sh -d [target.com](http://target.com)

## **Dynamic analysis of applications:**

### **Autentication:**

- [ ]  User registration process
- [ ]  Password reset process
    - Password reset tokens (expiration/reuse)
- [ ]  Failed retry lockout (DoS)
- [ ]  Password policies
- [ ]  Update profile information without asking password
- [ ]  Default or easy to guess keys
- [ ]  User enumeration
- [ ]  HTTP Authentication
- [ ]  Authentication Bypass
- [ ]  Identify weak authentication channels (Find primary mechanism and identify secondary mechanicsm / methods [Mobile App, Call Center, SSO])

### **Authorization:**

- [ ]  Testing Directory traversal/file inclusion
- [ ]  Access to features, functionality or data that should not be available for the current role (priviliege escalation, horizontal & vertical)

    Example: Access admin functionality from a user account without privileges (create, delete, modify users...)

- [ ]  IDORs

    Example: The following URL returns our profile: 
    target.com/profile?idUser=123 
    Cambiar por target.com/profile?idUser=12**4** 
    Do you have access? Should this profile be accessible to our current user?

### 

### **Session:**

- [ ]  No cookie validation
- [ ]  Not setting a new cookie (session fixation - logout -> Login again)
- [ ]  Cookieis easy to reverse engineer (base64/Hash ID)
- [ ]  Are security options set? (secure/HttpOnly)

    HttpOnly not set? is there an XSS? <script>alert(document.cookie)</script>

- [ ]  Testing for **C**ross **S**ite **R**equest **F**orgery

    Delete token (parameter y header)
    Forge your own token
    Use a second identical CSRF parameter
    Change POST to GET (or reverse, put, etc)

    Features that should be tested:
    . Add / Upload file
    · Change Email 
    · Delete files
    · Change Password 
    · Transfer money
    · Edit profile

- [ ] Logout

    Are you actually logged out? (Session is destroyed)

- [ ] Session timeout

    Does the session expire after a reasonable amount of time?

- [ ] JWT

    Signature check
    Check claims (Especially: **aud** -> "In practical use, this tends to be the "client id" or "client key" of the application that the JWT is intended to be used by."")
    Signature algorithm
    Sensitive information in the token
    How is it revoked? How is it used? How is it processed?

    - [c-jwt-cracker](https://github.com/brendan-rius/c-jwt-cracker)

        Brute force, example:
        ./jwtcrack eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.cAOIAifu3fykvhkHpbuhbvtH807-Z2rI1FS3vX1XMjE

    - [jwt_tool](https://github.com/ticarpi/jwt_tool)

        Check various vulns, crack with dictionary
        Example: python3 jwt_tool.py <JWT>

    - [JWT2John](https://raw.githubusercontent.com/Sjord/jwtcrack/master/jwt2john.py)

    Convert JWT to a format crackable by John
    python3 [jwt2john.py](http://jwt2john.py) <JWT>

    Execute John:
    ./john /tmp/token.txt —wordlist=wordlist.txt

### **General:**

- [ ]  Test HTTP Methods
- [ ]  Header Injections

    X-Forwarded-Host: xxxx.com
    X-Forwarded-For: 127.0.0.1
    X-Remote-IP: 127.0.0.1
    X-Remote-Addr: 127.0.0.1
    X-Originating-IP: 127.0.0.1

- [ ]  Test CORS
- [ ]  S3 AWS
    - [lazys3](https://github.com/nahamsec/lazys3)
    - [AWS Cli](https://aws.amazon.com/es/cli/)

    [http://bucket.s3.amazonaws.com](http://bucket.s3.amazonaws.com) / http://s3.amazonaws.com/bucket
    aws s3 cp test.txt s3://target --no-sign-request
    aws s3 ls s3://target --no-sign-request

    - [Metadata Cloud](https://gist.github.com/jhaddix/78cece26c91c6263653f31ba453e273b)
    - [How the AWS Access Key & Secret works](https://github.com/streaak/keyhacks#AWS-Access-Key-ID-and-Secret)

### XSS

[XSS Payloads](https://github.com/nettitude/xss_payloads)

- [ ]  [XSpear](https://github.com/hahwul/XSpear)

### Payloads

[PayloadAllTheTHings](https://github.com/swisskyrepo/PayloadsAllTheThings)
