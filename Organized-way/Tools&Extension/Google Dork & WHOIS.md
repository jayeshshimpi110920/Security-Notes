## Google Dorking 
**Google Dorking** (also known as **Google hacking**) is a technique used in **web application penetration testing** to gather information about targets by using advanced search operators in Google. It involves crafting specific search queries (known as "dorks") to identify exposed or sensitive information unintentionally made public on the internet.

> Similar to google dorking, then is one more search engine called **Shoden Search engine**

### **Key Information That Google Dorking Helps to Collect:**

1. **Discover Exposed Files and Directories**:
   - Use Google dorks to find sensitive files such as configuration files, database dumps, and backup files that may be publicly accessible but should not be.

   Example:
   - `filetype:sql "password"`: Finds SQL database dumps that contain the word "password".
   - `intitle:"index of" "backup"`: Searches for directory listings of backup files.

2. **Identify Vulnerable Pages**:
   - Google Dorking can be used to find pages that may have known vulnerabilities, such as those vulnerable to SQL injection or Cross-Site Scripting (XSS).

   Example:
   - `inurl:".php?id="`: This searches for PHP pages with a query parameter, often used for identifying pages vulnerable to SQL injection.

3. **Find Login Pages**:
   - Locating login portals is useful for further testing such as brute force or dictionary attacks.

   Example:
   - `inurl:/admin/login`: This helps find admin login portals.
   - `inurl:login`: General search for login pages.

4. **Exposed Sensitive Data**:
   - Dorks can help locate files that inadvertently expose sensitive information, such as passwords, usernames, or configuration data.

   Example:
   - `filetype:txt "password"`: Finds text files that may contain the word "password".
   - `filetype:env "DB_PASSWORD"`: Looks for environment configuration files (.env) containing database credentials.

5. **Search for Specific Technologies in Use**:
   - Identify the technologies and frameworks used in the web application, which can aid in determining potential vulnerabilities.

   Example:
   - `intitle:"Apache Status"`: Searches for Apache server status pages.
   - `inurl:"wp-admin"`: Searches for WordPress admin login pages.

6. **Unintended Public Documents**:
   - Locate sensitive documents like internal reports, policies, or presentations that may be unintentionally available.

   Example:
   - `filetype:pdf "confidential"`: Finds PDF files that may contain confidential information.

7. **Find Publicly Accessible Cameras or Devices**:
   - Sometimes, security cameras or other devices are publicly accessible due to misconfiguration. 

   Example:
   - `intitle:"Live View / - AXIS"`: Searches for live camera feeds from Axis security cameras.
   
8. **Find Indexable Website Directories**:
   - Google Dorks can locate open directory listings, revealing files that may not have been intended for public access.

   Example:
   - `intitle:"index of /" "site backup"`: Finds directories that are indexed and contain backups.

### **Important Google Dorking Operators**:

1. **`inurl:`**
   - Finds URLs containing specific words or strings. Useful for identifying specific paths or query parameters in a website’s URL.
   
   Example:
   - `inurl:login.php`: Finds pages that have "login.php" in the URL.
   - `inurl:register`: Looks for registration pages.

2. **`intitle:`**
   - Searches for keywords in the title of web pages. Useful for finding admin panels or status pages.

   Example:
   - `intitle:"Admin Login"`: Finds pages where the title contains "Admin Login".
   - `intitle:"index of"`: Helps to locate directory indexes.

3. **`filetype:`**
   - Limits search results to a specific file type, such as `.pdf`, `.xls`, `.txt`, `.sql`. This helps find documents, backups, or config files that may contain sensitive data.

   Example:
   - `filetype:txt password`: Looks for text files containing the keyword "password".
   - `filetype:sql`: Finds SQL database dumps.

4. **`site:`**
   - Limits search results to a specific domain or website. This is helpful for focusing the dorking effort on a particular target.

   Example:
   - `site:example.com inurl:admin`: Searches for admin pages only on the example.com domain.
   - `site:example.com filetype:pdf`: Finds PDF documents on example.com.

5. **`cache:`**
   - Displays Google's cached version of a page, which can reveal information no longer present on the live site.

   Example:
   - `cache:example.com`: View the cached version of a website to find outdated content or sensitive information that has been removed from the live version.

6. **`related:`**
   - Finds websites similar to the specified URL. This could help in identifying other websites owned by the same company or running similar software.

   Example:
   - `related:example.com`: Shows websites similar to example.com.

7. **`intext:`**
   - Searches for specific text within the content of web pages. This can help find pages containing sensitive keywords.

   Example:
   - `intext:"internal use only"`: Finds pages containing the phrase "internal use only".
   - `intext:"API key"`: Looks for web pages containing "API key".

8. **`allinurl:`** and **`allintitle:`**
   - These are extended versions of `inurl` and `intitle`, used when you want to search for multiple terms within a URL or title.
   
   Example:
   - `allinurl:login admin`: Finds pages where both "login" and "admin" appear in the URL.
   - `allintitle:admin login`: Finds pages with both "admin" and "login" in the title.

### **Useful Google Dorks for Penetration Testing**:

1. **Admin Portals and Login Pages**:
   - `inurl:admin`
   - `inurl:login`
   - `intitle:"admin login"`

2. **Exposed Databases**:
   - `filetype:sql "password"`
   - `filetype:sql inurl:backup`
   - `filetype:db inurl:backup`

3. **Exposed Configuration Files**:
   - `filetype:env "DB_PASSWORD"`
   - `filetype:ini inurl:config`
   - `filetype:xml inurl:config`

4. **Directory Listings**:
   - `intitle:"index of /"`
   - `intitle:"index of" "parent directory"`

5. **Vulnerable Web Pages**:
   - `inurl:"php?id="`
   - `inurl:"index.php?page="`

6. **Open Cameras and Devices**:
   - `intitle:"Live View / - AXIS"`
   - `inurl:"viewerframe?mode="`

7. **Sensitive Documents**:
   - `filetype:pdf "confidential"`
   - `filetype:xls "password"`

8. **Finding Default or Test Pages**:
   - `intitle:"Test Page for Apache Installation"`
   - `intitle:"Welcome to Nginx!"`

### **Best Practices for Using Google Dorking in Penetration Testing**:

- **Targeted Search**: Use the `site:` operator to limit searches to your target domain, avoiding unintentional searching of unrelated sites.
- **Legal Considerations**: Ensure you have proper authorization before conducting any searches on a particular website, especially when looking for sensitive data.
- **Combination of Operators**: Combine different operators (e.g., `inurl:` with `filetype:`) to narrow down results and increase the chances of finding useful information.
- **Be Discreet**: While Google Dorking itself is legal, it’s essential to follow ethical guidelines and never use it for illegal purposes.

### Summary:

Google Dorking is a powerful information-gathering technique for web application penetration testing. By using advanced search operators like `inurl:`, `intitle:`, `filetype:`, and `site:`, penetration testers can uncover sensitive information, misconfigurations, exposed files, and login portals that may lead to further vulnerabilities. However, always ensure that you have legal permission to conduct these searches on the target website.

---
## Whois
---
**WHOIS** is a protocol used to query databases that store registration information about domain names, IP addresses, and autonomous systems. It provides details about the ownership and administration of these resources, which can be very useful during the **information gathering** phase of **penetration testing**.

### **Key Information from WHOIS and How It’s Helpful in Penetration Testing**:

1. **Domain Ownership Details**:
   - **Registrant Information**: Includes the name, organization, and contact details of the person or entity that owns the domain.
   - **Purpose**: Knowing the **registrant** can help confirm the owner of the domain. Sometimes, large organizations manage multiple domains, and by looking up the WHOIS information, you can connect the domain to the broader infrastructure of the target.

   Example of Useful Info:
   - Organization name (e.g., “Company XYZ LLC”).
   - Email addresses or phone numbers of the administrative contacts.

   **How It Helps**:
   - **Social Engineering**: Email addresses or phone numbers found in WHOIS can be used for social engineering or phishing attempts.
   - **Target Expansion**: Identifying an organization’s other domains or infrastructure can help in targeting other parts of their network.

2. **Domain Registration Dates**:
   - **Creation Date**: The date the domain was first registered.
   - **Expiration Date**: The date when the domain registration will expire.
   - **Updated Date**: When the domain’s registration information was last updated.

   **How It Helps**:
   - **Old Domains**: Domains registered a long time ago may be using older technologies or configurations, which could expose outdated or vulnerable systems.
   - **New Domains**: Newly registered domains might indicate newly set up infrastructure, which could have configuration issues or unpatched vulnerabilities.
   - **Expiration Dates**: If a domain is close to expiring, the organization may overlook updates or patches, making the system more vulnerable.

3. **Domain Name Servers (DNS)**:
   - The **Name Servers** section provides information about the DNS servers handling the domain. These servers map domain names to IP addresses.
   
   **How It Helps**:
   - **DNS Attacks**: If outdated or misconfigured DNS servers are being used, it could lead to attacks such as DNS spoofing, cache poisoning, or subdomain takeovers.
   - **Subdomain Enumeration**: Once the name servers are known, penetration testers can perform **DNS enumeration** to discover subdomains that may not be directly visible, which could expose entry points into the network.

4. **IP Address Information**:
   - **Whois for IP Addresses**: In some cases, the IP address range used by the domain is included in WHOIS records, and you can query WHOIS databases for more details on the IP address block.
   
   **How It Helps**:
   - **Network Mapping**: Knowing the IP range of the organization allows you to map out the network for further penetration testing. This helps in planning port scans and vulnerability scans.
   - **Geolocation Information**: The physical location of the IP address can also be useful in understanding where the servers are hosted, which may impact the attack vector (e.g., different legal jurisdictions or cloud providers).

5. **Contact Information (Admin, Tech, Billing Contacts)**:
   - WHOIS records often include **administrative**, **technical**, and **billing contacts**. This typically includes names, phone numbers, and email addresses.
   
   **How It Helps**:
   - **Phishing or Social Engineering**: Attackers could use this information to impersonate someone from the company or launch phishing campaigns against the admin or technical teams.
   - **Email Harvesting**: These emails could potentially be used in password brute-force attempts or to discover reused credentials.

6. **Domain Registrar**:
   - The company that manages the domain registration (e.g., GoDaddy, Namecheap, Google Domains).
   
   **How It Helps**:
   - **Registrar Vulnerabilities**: Certain domain registrars may have their own vulnerabilities or weaknesses. For instance, exploiting poor registrar security could allow an attacker to modify DNS settings (domain hijacking).
   
7. **Domain History**:
   - Services like **Whois History** provide historical WHOIS data, allowing you to see how ownership or configuration of a domain has changed over time.
   
   **How It Helps**:
   - **Track Changes**: If the domain was previously owned by someone else or changed hands multiple times, it might expose inconsistencies in security practices, like outdated DNS records or leftover subdomains.

### **How WHOIS Information Helps in Penetration Testing**:

1. **Reconnaissance (Information Gathering)**:
   - WHOIS queries are an important part of **OSINT (Open Source Intelligence)**. Gathering information about the domain owner, DNS servers, and other technical details gives penetration testers insight into the target’s infrastructure.

2. **Network Mapping**:
   - Knowing the IP range and name servers through WHOIS allows you to map the target’s external network, which can then be scanned for open ports, running services, or vulnerabilities.

3. **Social Engineering**:
   - WHOIS can expose contact information that penetration testers can use in social engineering scenarios, such as **spear phishing** attacks, where highly targeted emails are sent to administrative contacts to steal credentials.

4. **DNS Vulnerabilities**:
   - Name servers listed in WHOIS records can be checked for misconfigurations or vulnerabilities such as zone transfers or DNS amplification.

5. **Domain Targeting**:
   - If WHOIS reveals related domains owned by the same organization, testers can widen the scope to test those domains for vulnerabilities as well. Often, subsidiary domains are less protected than the main website.

6. **Subdomain Takeover**:
   - WHOIS helps identify name servers, which can then be used to find **unclaimed subdomains**. If a subdomain points to a service that is no longer in use (like a cloud provider), a penetration tester can attempt to claim and take over that subdomain, potentially leading to sensitive data exposure.

7. **SSL/TLS and Certificate Information**:
   - WHOIS can sometimes reveal information about SSL certificates used by a domain, allowing testers to check whether the domain is using outdated, self-signed, or insecure certificates.

### **Example WHOIS Command**:

On a terminal, you can use the `whois` command to query domain information. For example:

```bash
whois example.com
```

This will return details such as:

- Registrar Information
- Domain Owner
- Admin/Tech Contact Information
- Name Servers
- Creation and Expiration Dates

### **Popular WHOIS Lookup Tools**:
- **Linux/Unix CLI**: `whois example.com`
- **Web-based Tools**:
  - [whois.domaintools.com](https://whois.domaintools.com)
  - [whois.net](https://www.whois.net)
  - [whois.icann.org](https://whois.icann.org/en)
- **API-based WHOIS Services** (for automation):
  - **WHOISXML API**
  - **WHOIS API** by DomainTools

### **Summary**:

WHOIS queries provide crucial insights about domain names, IP addresses, and their ownership details, which help in the reconnaissance phase of penetration testing. By identifying domain owners, name servers, contact details, and IP ranges, penetration testers can gather enough information to map the target’s infrastructure, explore DNS misconfigurations, and even plan social engineering attacks. However, always ensure that you operate within legal boundaries when performing WHOIS lookups and acting on the information gathered.

---
Shoden Search Engine
---
**Shodan** is a search engine designed to find and index **internet-connected devices** rather than web pages. In **penetration testing (PT)**, it is used during the **reconnaissance phase** to discover exposed systems and services, such as:

- **IoT devices** (cameras, routers, smart appliances)
- **Servers and databases** (e.g., Elasticsearch, MongoDB)
- **Industrial Control Systems** (ICS)
- **SCADA systems**

### **How Shodan Helps in Penetration Testing**:

1. **Identify Exposed Devices**:
   - Shodan reveals systems directly connected to the internet, including devices that may not be properly secured or patched.

2. **Find Misconfigured Services**:
   - It can find services running on default ports (like **RDP**, **SSH**, **FTP**) and check for default configurations, which may indicate security vulnerabilities.

3. **Discover Open Ports and Vulnerabilities**:
   - Shodan provides details about **open ports**, **service versions**, and potential vulnerabilities (based on CVEs) for discovered systems.

4. **Check SSL/TLS Configurations**:
   - Shodan can identify websites with weak or outdated SSL/TLS configurations, revealing encryption issues.

5. **Real-Time Monitoring**:
   - You can monitor an organization’s internet-exposed infrastructure to detect potential misconfigurations or vulnerabilities over time.

### **Example Use Cases in PT**:
- Finding **unprotected databases** (e.g., open MongoDB instances).
- Identifying **vulnerable servers** running outdated software.
- Discovering **IoT devices** with default or weak passwords.

Shodan is an essential tool for **external reconnaissance**, helping testers find potential entry points in a target’s public-facing systems.
