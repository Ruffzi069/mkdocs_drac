## 🔍 Reconnaissance Techniques (Recon)

### 🔗 Passive Recon
Gathers information **without directly interacting** with the target.

#### Tools and Usage:

- **theHarvester** – Gathers emails, subdomains, hosts, and more.
  ```bash
  theHarvester -d example.com -b google
  ```

- **Subfinder** – Fast passive subdomain enumeration.
  ```bash
  subfinder -d example.com
  ```

- **crt.sh** – Public certificate transparency log viewer.
  ```bash
  curl https://crt.sh/?q=%.example.com&output=json
  ```

- **GitHub Search/Dorking** – Search for secrets in code.
  ```bash
  site:github.com "example.com password"
  ```

- **Waybackurls** – Fetch historical URLs.
  ```bash
  echo example.com | waybackurls
  ```

- **Shodan** – Search for devices/servers online.
  ```bash
  shodan search "http.title:'Example Domain'"
  ```

---

### 🛠️ Active Recon
Interacts **directly** with the target.

#### Tools and Usage:

- **Sublist3r** – Subdomain enumeration via OSINT.
  ```bash
  sublist3r -d example.com
  ```

- **Nmap** – Network scanner for open ports and services.
  ```bash
  nmap -sV -p- example.com
  ```

- **Masscan** – Very fast port scanner.
  ```bash
  masscan -p1-65535 --rate=10000 example.com
  ```

- **ffuf** – Fuzzing URLs for hidden files and directories.
  ```bash
  ffuf -u https://example.com/FUZZ -w /usr/share/wordlists/dirb/common.txt
  ```

- **Dirsearch** – Command-line directory brute-forcer.
  ```bash
  python3 dirsearch.py -u https://example.com -e php,html
  ```

- **Gobuster** – Directory and DNS scanner.
  ```bash
  gobuster dir -u https://example.com -w /usr/share/wordlists/dirb/common.txt
  ```

- **Wappalyzer** / **WhatWeb** – Detects technologies used.
  ```bash
  whatweb example.com
  ```

- **ParamSpider** – Finds hidden GET/POST parameters.
  ```bash
  python3 paramspider.py --domain example.com
  ```

- **Arjun** – Finds hidden HTTP parameters.
  ```bash
  python3 arjun.py -u https://example.com/search
  ```

- **LinkFinder** – Extracts endpoints from JavaScript files.
  ```bash
  python3 linkfinder.py -i https://example.com/script.js -o cli
  ```

---

## 🧰 Summary of Tools and Purpose

| Tool         | Purpose                          | Usage Example                                  |
|--------------|----------------------------------|------------------------------------------------|
| theHarvester | Email & domain harvesting        | `theHarvester -d example.com -b google`        |
| Amass        | Subdomain enum                   | `amass enum -d example.com`                    |
| Subfinder    | Subdomain enum                   | `subfinder -d example.com`                     |
| Sublist3r    | Subdomain enum                   | `sublist3r -d example.com`                     |
| Nmap         | Port scanning                    | `nmap -sV -p- example.com`                     |
| Masscan      | Fast port scan                   | `masscan -p1-65535 example.com`                |
| ffuf         | Directory fuzzing                | `ffuf -u https://site.com/FUZZ -w wordlist`    |
| Dirsearch    | Directory bruteforcing           | `dirsearch -u https://example.com -e php`      |
| Gobuster     | Dir & DNS brute force            | `gobuster dir -u https://example.com -w wordlist` |
| ParamSpider  | Hidden param discovery           | `paramspider.py --domain example.com`         |
| Arjun        | Param brute-forcing              | `arjun.py -u https://site.com`                |
| LinkFinder   | JS endpoint extraction           | `linkfinder.py -i URL -o cli`                  |
| Burp Suite   | Manual security testing          | Intercept, modify, generate CSRF PoC           |
| Postman      | API testing                      | Send raw HTTP requests                         |
| WhatWeb      | Detect tech stack                | `whatweb example.com`                          |

