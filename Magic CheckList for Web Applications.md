# Magic CheckList for Web Applications

**Information Gathering:**

- [ ]  OSINT
    - [x]  [Googl](https://www.google.com/?client=safari)e

        Aprovechar los dorks, site, inurl, intext, intitle, etc.

    - [x]  [Bing](https://www.bing.com/?setlang=es)
    - [x]  [Duckduckgo](https://duckduckgo.com)
    - [x]  [Censys](https://censys.io)
    - [x]  [Shodan](https://www.shodan.io)

        Usar los filtros

        - [Shodan Firefox Addon](https://addons.mozilla.org/en-US/firefox/addon/shodan_io/)
    - [x]  [Github](https://github.com)
        - [GitGot](https://github.com/BishopFox/GitGot)
        - [Gitrob](https://github.com/michenriksen/gitrob)
    - [x]  [Gitlab](https://gitlab.com/)
    - [x]  [Pastebin](https://pastebin.com)
        - [PasteLert](https://andrewmohawk.com/pasteLert/)
    - [ ]  [Trello](https://trello.com)

        Ejemplo de un dork para Google: inurl:[https://trello.com](https://trello.com/) AND intext:target.com

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
- [x]  Encontrar los dominios únicos

    for i in $(cat nombre_archivo_dominios.txt); do echo""; echo "ASN $i";echo ""; amass intel -active -asn $i;echo ""; done

- [x]  Buscar subdominios
    - [Findomain](https://github.com/Edu4rdSHL/findomain)
    - [Sublist3r](https://github.com/aboul3la/Sublist3r)
    - [Acamar](https://github.com/si9int/Acamar)
    - [Assetfinder](https://github.com/tomnomnom/assetfinder)

        assetfinder --subs-only [dominio.com](http://dominio.com/) | httprobe | tee -a salida.txt

    - [Amass](https://github.com/OWASP/Amass)

        amass net -asn 12345

    - [Altdns](https://github.com/infosec-au/altdns)

        altdns -i subdominios.txt -o salida.txt -w wordlist.txt -r -s results_output.txt

    - [x]  Subdomain Takeover
        - [Subjack](https://github.com/haccer/subjack)
        - [Subzy](https://github.com/LukaSikic/subzy)

        Chequear en "[Can I take over XYZ](https://github.com/EdOverflow/can-i-take-over-xyz)" según el mensaje de error

- [x]  Screenshot de Webs
    - [Aquatone](https://github.com/michenriksen/aquatone)

        cat targets.txt | aquatone

    - [Gowitness](https://github.com/sensepost/gowitness)
- [x]  Buscar directorios
    - [Dirsearch](https://github.com/maurosoria/dirsearch)
    - [Gobuster](https://tools.kali.org/web-applications/gobuster)
    - [ffuf](https://github.com/ffuf/ffuf)

    El secreto es armarse un diccionario propio, personalizado! pero se pueden usar por ejemplo los siguientes: [all.txt](https://gist.github.com/jhaddix/f64c97d0863a78454e44c2f7119c2a6a) [dirbuster wordlists](https://github.com/daviddias/node-dirbuster/tree/master/lists) [SecLists](https://github.com/danielmiessler/SecLists)

- [x]  Scanner CMS
    - [CMSMap](https://github.com/Dionach/CMSmap)
    - [WPscan](https://github.com/wpscanteam/wpscan)
- [ ]  Buscar Aplicaciones en el Webserver (Virtual hosts/Subdomain), puertos no comunes, DNS zone transfers
    - [Masscan](https://github.com/robertdavidgraham/masscan)

        masscan -iL targets.txt -p0-65535 --max-rate 10000 -sS -Pn -n --randomize-hosts --send-eth -oX output.xml
        -p0-65535 (todos los puertos)
        -max-rate 10000 (cantidad de paquetes por segundo a transmitir, por defecto 100 paquetes/segundo)

    - [Nmap](https://nmap.org)

        nmap target -sC -sV -vvv -p-65535
        -sC Scripts
        -sV Detección de versiones
        -vvv Verbosity
        -p-65535 (todos los puertos)

    - [HTTProbe](https://github.com/tomnomnom/httprobe)

        ./httprobe - -subs-only target.com

    - [Nikto](https://github.com/sullo/nikto)
    - [Virtual Host Discovery](https://github.com/jobertabma/virtual-host-discovery)
- [x]  Identificar "entry points" en la aplicación (Identificarlos desde campos ocultos, parámetros, metodos HTTP, análisis de headers)
- [x]  Fingerprints (Framework, tecnología, etc.)
    - [Wappalyzer](https://www.wappalyzer.com) (extensión navegador)
- [x]  Mapear la arquitectura de la Aplicación (Identify application architecture including Web language, WAF, Reverse proxy, Application Server, Backend Database)
- [x]  Robots.txt y revisar el código fuente HTML
- [x]  Web Crawler
    - Crawl burp (ex spider)
- [x]  Waybackmachine
    - [Waybackurls](https://github.com/tomnomnom/waybackurls)
- [x]  Análisis de archivos js
    - [Relative-url-extractor](https://github.com/jobertabma/relative-url-extractor) (extrae los js de una url para su posterior análisis)
    - [JSParser](https://github.com/nahamsec/JSParser) (busca URL's en los js)
    - [LinkFinder](https://github.com/GerbenJavado/LinkFinder) (BuscaURL's en los js)
- [x]  Fuzzear parámetros
    - f[fuf](https://github.com/ffuf/ffuf)
    - [Wfuzz](https://wfuzz.readthedocs.io/en/latest/)
    - [Arjun](https://github.com/s0md3v/Arjun)

## **Análisis Dinámico de la Aplicación:**

### **Autenticación:**

- [x]  Proceso de registración de usuarios
- [x]  Proceso de password reset
    - Password reset tokens (caducidad/reutilización)
- [x]  Bloqueo de cuenta por reintentos fallidos
- [x]  Política de Passwords
- [x]  Update de información de cuenta sin pedir contraseña
- [x]  Claves por defecto o de fácil adivinación
- [x]  Enumeración de usuarios
- [x]  Autenticación por HTTP
- [x]  Bypass de autenticación
- [x]  Identificar canales de autenticación alternativos débiles (Encontrar el mecanismo principal e identificar otros mecanismos secundarios (App Mobile, Call center, SSO)

### **Autorización:**

- [x]  Acceso a funcionalidades/datos no disponibles para el rol actual
- [x]  Testing Directory traversal/file include
- [x]  Escalamiento de privilegios (horizontal y vertical)

    Ejemplo: Acceso a funcionalidades de administración desde usuario sin privilegios (crear, borrar, modifcar usuarios...)

- [x]  IDORs

    Ejemplo: La siguiente URL traería nuestra información personal: 
    target.com/perfil?idUser=123 
    Cambiar por target.com/perfil?idUser=12**4** 
    Trae información? Deberíamos tener acceso a 124?

### 

### **Sesión:**

- [x]  No validación de cookie
- [x]  No seteo de nueva cookie de sesión (session fixation)
- [x]  Cookie fácilmente reversible (base64/Hash ID)
- [x]  Seteo de cabeceras de seguridad (secure/HttpOnly)

    No setea HttpOnly? hay un XSS? <script>alert(document.cookie)</script>

- [x]  Testing for **C**ross **S**ite **R**equest **F**orgery

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

- [x]  Logout

    Cierra la sesión realmente?

- [x]  Session timeout

    La sesión caduca luego de un tiempo prudente?

- [x]  JWT

    Chequeo de firma
    Chequeo de claims (especialmente aud "salto de entorno")
    Algoritmo de firmado
    Información sensible dentro del token

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