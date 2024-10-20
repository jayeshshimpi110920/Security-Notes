
Sublist3r is a tool designed to enumerate subdomains of websites by using OSINT (Open Source Intelligence) techniques. It collects subdomains from multiple search engines like Google, Bing, Yahoo, and others, as well as services like VirusTotal. It's useful for penetration testing, especially during the reconnaissance phase.

> its come under Passive Recon (which basically search all subdomain with help of google/yahoo/and other search engine) 

### Steps to Use Sublist3r:
1. **Install Sublist3r:**
   - First, you need to install Sublist3r. It can be installed using `pip`:
     ```bash
     git clone https://github.com/aboul3la/Sublist3r.git
     cd Sublist3r
     pip install -r requirements.txt
     ```
   - Alternatively, you can install it directly:
     ```bash
     pip install sublist3r
     ```

2. **Basic Usage:**
   - To enumerate subdomains, simply run:
     ```bash
     python sublist3r.py -d example.com
     ```
     Here, `example.com` is the domain for which you want to find subdomains.

3. **Parameters/Options:**
   - `-d` : Specifies the domain to search.
   - `-o` : Save the results to a file.
     ```bash
     python sublist3r.py -d example.com -o subdomains.txt
     ```
   - `-t` : Number of threads (to speed up the process).
     ```bash
     python sublist3r.py -d example.com -t 50
     ```
   - `-b` : Enable brute force of subdomains.
   - `-v` : Enable verbose mode to see progress.

4. **Viewing Results:**
   - Once the tool completes the scan, it will display a list of discovered subdomains and save them in the file if the `-o` option was used.

### When to Use Sublist3r:
Sublist3r is typically used in the reconnaissance phase of penetration testing to identify subdomains of a target domain, which may reveal less-secure or forgotten web assets.

Let me know if you need more details or examples!
