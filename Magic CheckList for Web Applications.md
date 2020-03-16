# Magic CheckList for Web Applications

**Information Gathering:**

- [ ]  OSINT
    - [ ]  [Google](https://www.google.com/?client=safari)

        Aprovechar los dorks, site, inurl, intext, intitle, etc.

    - [ ]  [Bing](https://www.bing.com/?setlang=es)
    - [ ]  [Duckduckgo](https://duckduckgo.com)

        site:target.com inurl:'&'

    - [ ]  [Censys](https://censys.io)
    - [ ]  [Shodan](https://www.shodan.io)

        Usar los filtros

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

        Ejemplo de un dork para Google: inurl:[https://trello.com](https://trello.com/) AND intext:target.com
        site:trello.com target.com

    - [ ]  [Linkedin](https://www.linkedin.com/uas/login?_l=es)

        Buscar desarrolladores de la empresa objetivo y luego buscar sus repos en github/gitlab

    - [ ]  Acquisition
        - [Crunchbase](https://www.crunchbase.com)
        - [Wikipedia](https://es.wikipedia.org)

        Muy útil para scopes sin definir (ejemplo AT&T)

- [ ]  Encontrar ASNs (Número de Sistema Autónomo)

    Encontrar el nombre de la org. que registra los dominios [mediante Whois](http://whois.domaintools.com)

    - [http://asnmap.com](http://asnmap.com/) (Obtener mapa ASN)
    - [https://bgp.he.net](https://bgp.he.net/) (Obtener ASNs)
    - [https://mxtoolbox.com/asn.aspx](https://mxtoolbox.com/asn.aspx)
- [ ]  Obtener Dominios/Subdominios a partir de rangos IP
    - [https://github.com/zeropwn/spyse.py](https://github.com/zeropwn/spyse.py)

    spyse -target xxx.xxx.xxx.0/24 --domains-on-ip

- [ ]  Encontrar los dominios únicos

    for i in $(cat nombre_archivo_dominios.txt); do echo""; echo "ASN $i";echo ""; amass intel -active -asn $i;echo ""; done

- [ ]  Buscar subdominios
    - [Findomain](https://github.com/Edu4rdSHL/findomain)
    - [Sublist3r](https://github.com/aboul3la/Sublist3r)

        python3 [sublister.py](http://sublister.py) -d target.com

    - [Acamar](https://github.com/si9int/Acamar)

        python3 acamar.py [t](http://twitter.com/)arget.com

    - [Assetfinder](https://github.com/tomnomnom/assetfinder)

        assetfinder --subs-only [dominio.com](http://dominio.com/) | httprobe -t 40000 | tee -a salida.txt

        -t  Timeout en milisegundos (40000 es el doble del default)

    - [Amass](https://github.com/OWASP/Amass)

        amass net -asn 12345
        amass enum --passive -d <DOMAIN>

    - [Altdns](https://github.com/infosec-au/altdns)

        altdns -i subdominios.txt -o salida.txt -w wordlist.txt -r -s salida_final.txt

    - [http://arthusu.xyz/subdomainScanner/](http://arthusu.xyz/subdomainScanner/)
    - [ ]  Subdomain Takeover
        - [Subjack](https://github.com/haccer/subjack)
        - [Subzy](https://github.com/LukaSikic/subzy)
        - [Subdomain-Takeover](https://github.com/antichown/subdomain-takeover)

        Chequear en "[Can I take over XYZ](https://github.com/EdOverflow/can-i-take-over-xyz)" según el mensaje de error

- [ ]  Screenshot de Webs
    - [Aquatone](https://github.com/michenriksen/aquatone)

        Ejemplo:
        cat hosts.txt | aquatone -ports (xlarge, small, medium, large, xlarge) -out ~/path/output  -scan-timeout 500 -screenshot-timeout 50000 -http-timeout 6000

    - [Gowitness](https://github.com/sensepost/gowitness)
- [ ]  Buscar directorios
    - [Dirsearch](https://github.com/maurosoria/dirsearch)

    Ejemplo:
    python3 [dirsearch.py](http://dirsearch.py/) -u target.com -E -w ./directory-list-lowercase-2.3-medium.txt -f -t 20 --plain-text-report=/tmp/salida.txt

    - [Gobuster](https://tools.kali.org/web-applications/gobuster)
    - [ffuf](https://github.com/ffuf/ffuf)

    El secreto es armarse un diccionario propio, personalizado! pero se pueden usar por ejemplo los siguientes: [all.txt](https://gist.github.com/jhaddix/f64c97d0863a78454e44c2f7119c2a6a) [dirbuster wordlists](https://github.com/daviddias/node-dirbuster/tree/master/lists) [SecLists](https://github.com/danielmiessler/SecLists)

    Se puede usar [CeWL](https://github.com/digininja/CeWL) para crear Wordlists personalizadas o el plugin de para Burp "Wordlist Extractor"

- [ ]  Scanner CMS
    - [CMSMap](https://github.com/Dionach/CMSmap)
    - [WPscan](https://github.com/wpscanteam/wpscan)
- [ ]  Buscar Aplicaciones en el Webserver (Virtual hosts/Subdomain), puertos no comunes, DNS zone transfers
    - [Masscan](https://github.com/robertdavidgraham/masscan)

        Ejemplo:
        ./masscan -iL targets.txt -p0-65535 --max-rate 10000 -sS -Pn --randomize-hosts -banners -oX output.xml

        -p0-65535 (todos los puertos)
        -max-rate 10000 (cantidad de paquetes por segundo a transmitir, por defecto 100 paquetes/segundo)

        Escaneo de puertos Web mas comunes:
        ./masscan -p443,8443,80,8080,8000 165.183.102.0/23,165.183.106.0/24,165.183.108.0/24 --rate 1000

    - Massdns

        Resuelve los registros AAAA de una lista de dominios (domains.txt) y los guarda en results.txt:

        ./bin/massdns -r lists/resolvers.txt -t AAAA -w results.txt domains.txt
        (AAAA es el record para ipv6 mientras que el A es para ipv4)

        [Lista de resolvers actualizada:](https://github.com/bberastegui/fresh-dns-servers)
        ./bin/massdns -r <(curl -s https://raw.githubusercontent.com/BBerastegui/fresh-dns-servers/master/resolvers.txt)

        ./bin/massdns -r lists/resolvers.txt -t AAAA -w results.txt domains.txt

        (AAAA es el record para ipv6 mientras que el A es para ipv4)

        ./scripts/ptr.py | ./bin/massdns -r lists/resolvers.txt -t PTR -w ptr.txt

    - [Nmap](https://nmap.org)

        nmap target -sS -A -PN -sC -sV -vvv -p-65535

        -sS syn scan
        -A OS + service fingerprint
        -PN No Ping
        -sC Scripts
        -sV Detección de versiones
        -vvv Verbosity
        -p-65535 (todos los puertos)

    - [HTTProbe](https://github.com/tomnomnom/httprobe)

        Ejemplo:
        cat archivo.txt | ./httprobe -p http:81 -p https:8443 -p http:8000 -p http:8001 -p http:8080 -p http:8181 -t 40000 

        -t  Timeout en milisegundos (40000 es el doble del default)

    - [Nikto](https://github.com/sullo/nikto)

        Ejemplo:
        nikto -host <IP> -output <salida> -port 

    - [Virtual Host Discovery](https://github.com/jobertabma/virtual-host-discovery)
- [ ]  Identificar "entry points" en la aplicación (Identificarlos desde campos ocultos, parámetros, metodos HTTP, análisis de headers)
- [ ]  Fingerprints (Framework, tecnología, etc.)
    - [Wappalyzer](https://www.wappalyzer.com) (extensión navegador)
- [ ]  Mapear la arquitectura de la Aplicación (Identify application architecture including Web language, WAF, Reverse proxy, Application Server, Backend Database)
- [ ]  Robots.txt y revisar el código fuente HTML
- [ ]  Web Crawler
    - Crawl burp (ex spider)
    - [Hakrawler](https://github.com/hakluke/hakrawler)

    Ejemplo:
    ./assetfinder target.com | hakrawler

    ./hakrawler -url target.com -depth 1

    - [http://arthusu.xyz/crawler/index.php?menu=crawler](http://arthusu.xyz/crawler/index.php?menu=crawler)
- [ ]  Waybackmachine
    - [Waybackurls](https://github.com/tomnomnom/waybackurls)
    - [WaybackurlSqliScanner](https://github.com/ghostlulzhacks/waybackSqliScanner)
    - [http://arthusu.xyz/crawler/index.php?menu=urls](http://arthusu.xyz/crawler/index.php?menu=urls)
- [ ]  GetAllUrls ([GAU](https://github.com/lc/gau))

    Ejemplo:
    gau example.com

- [ ]  Análisis de archivos js
    - [Relative-url-extractor](https://github.com/jobertabma/relative-url-extractor) (extrae los js de una url para su posterior análisis)
    - [JSParser](https://github.com/nahamsec/JSParser) (busca endpoints en los js)
    - [LinkFinder](https://github.com/GerbenJavado/LinkFinder) (BuscaURL's y Parámetros en los js)
    - [http://arthusu.xyz/crawler/index.php?menu=JsScanner](http://arthusu.xyz/crawler/index.php?menu=JsScanner)
- [ ]  Fuzzear parámetros
    - f[fuf](https://github.com/ffuf/ffuf)
    - [Wfuzz](https://wfuzz.readthedocs.io/en/latest/)
    - [Arjun](https://github.com/s0md3v/Arjun)

        Ejemplo:
        python3 arjun.py -u https://api.example.com/endpoint --get -o result.json

        python3 arjun.py --urls targets.txt --get -o result.json

- [ ]  Tools que hacen "TODO"
- [Photon](https://github.com/s0md3v/Photon)

    Ejemplo:
    python3 [photon.py](http://photon.py/) -u https://www.target.com -l 3 -t 100 --wayback -o /output/dir/ -v --keys --dns

- [Lazyrecon](https://github.com/nahamsec/lazyrecon)

    Ejemplo:
    ./lazyrecon.sh -d [target.com](http://target.com)

## **Análisis Dinámico de la Aplicación:**

### **Autenticación:**

- [ ]  Proceso de registración de usuarios
- [ ]  Proceso de password reset
    - Password reset tokens (caducidad/reutilización)
- [ ]  Bloqueo de cuenta por reintentos fallidos
- [ ]  Política de Passwords
- [ ]  Update de información de cuenta sin pedir contraseña
- [ ]  Claves por defecto o de fácil adivinación
- [ ]  Enumeración de usuarios
- [ ]  Autenticación por HTTP
- [ ]  Bypass de autenticación
- [ ]  Identificar canales de autenticación alternativos débiles (Encontrar el mecanismo principal e identificar otros mecanismos secundarios (App Mobile, Call center, SSO)

### **Autorización:**

- [ ]  Testing Directory traversal/file include
- [ ]  Acceso a funcionalidades/datos no disponibles para el rol actual (escalamiento de privilegios, horizontal y vertical)

    Ejemplo: Acceso a funcionalidades de administración desde usuario sin privilegios (crear, borrar, modifcar usuarios...)

- [ ]  IDORs

    Ejemplo: La siguiente URL traería nuestra información personal: 
    target.com/perfil?idUser=123 
    Cambiar por target.com/perfil?idUser=12**4** 
    Trae información? Deberíamos tener acceso a 124?

### 

### **Sesión:**

- [ ]  No validación de cookie
- [ ]  No seteo de nueva cookie de sesión (session fixation)
- [ ]  Cookie fácilmente reversible (base64/Hash ID)
- [ ]  Seteo de cabeceras de seguridad (secure/HttpOnly)

    No setea HttpOnly? hay un XSS? <script>alert(document.cookie)</script>

- [ ]  Testing for **C**ross **S**ite **R**equest **F**orgery

    Eliminar token (parámetro y header)
    Forjar un token propio
    Usar un segundo parámetro CSRF idéntico
    Cambiar POST por GET

    Funcionalidades donde conviene testear:
    . Agregar/Subir archivo 
    · Cambio de Email 
    · Eliminación de archivos 
    · Cambio de Password 
    · Transferencia de dinero
    · Edición de perfil

- [ ]  Logout

    Cierra la sesión realmente?

- [ ]  Session timeout

    La sesión caduca luego de un tiempo prudente?

- [ ]  JWT

    Chequeo de firma
    Chequeo de claims (especialmente aud "salto de entorno")
    Algoritmo de firmado
    Información sensible dentro del token

    - [c-jwt-cracker](https://github.com/brendan-rius/c-jwt-cracker)

        Fuerza bruta, ejemplo:
        ./jwtcrack eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.cAOIAifu3fykvhkHpbuhbvtH807-Z2rI1FS3vX1XMjE

    - [jwt_tool](https://github.com/ticarpi/jwt_tool)

        Chequea varias vulns, crackeo por diccionario
        Ejemplo: python3 jwt_tool.py <JWT>

    - [JWT2Jhon](https://raw.githubusercontent.com/Sjord/jwtcrack/master/jwt2john.py)

    Para convertir los JWT a formato crackeable por John
    python3 [jwt2john.py](http://jwt2john.py) <JWT>

    Ejecutar John:
    ./john /tmp/token.txt —wordlist=wordlist.txt

### **Generales:**

- [ ]  Testear Métodos HTTP
- [ ]  Inyección de Cabeceras

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
    - [Como usar las claves de los servicios](https://github.com/streaak/keyhacks#AWS-Access-Key-ID-and-Secret)

### XSS

[XSS Payloads](https://github.com/nettitude/xss_payloads)

- [ ]  [XSpear](https://github.com/hahwul/XSpear)