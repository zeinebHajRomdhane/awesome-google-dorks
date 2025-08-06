# 🔍 Awesome Google Dorks Cheat Sheet

> A curated guide to mastering **Google Dorks** for ethical hacking, cybersecurity, and effective OSINT investigations.  
> 🚀 Learn advanced Google search operators, real-world use cases, and security tips to safely leverage dorks.

---

## ✨ What are Google Dorks?

**Google Dorks** are advanced search queries used to identify sensitive data, vulnerabilities, and exposed information indexed by Google. Essential for penetration testers, bug bounty hunters, digital investigators, and anyone interested in web security.

---

## 🛠️ Useful Google Dorks & How to Use Them

| Operator                                            | Usage Example(s)                               | Description                                                                 |
|-----------------------------------------------------|------------------------------------------------|-----------------------------------------------------------------------------|
| `site:abc.com`                                     | `site:example.com`                             | Search only within a specific website                                       |
| `cache:abc.com`                                    | `cache:example.com`                            | See the cached (stored) version of a site                                   |
| `intext:keyword`                                   | `intext:password`                              | Pages containing the keyword in their text                                  |
| `intitle:keyword`                                  | `intitle:admin`                                | Pages with the keyword in their title                                       |
| `inurl:keyword`                                    | `inurl:login`                                  | Pages with the keyword in their URL                                         |
| `filetype:pdf`                                     | `filetype:pdf security`                        | Finds PDF files about security                                              |
| `related:abc.com`                                  | `related:example.com`                          | Find sites related to a specific site                                       |
| `allinurl:keyword1 keyword2`                       | `allinurl:admin login`                         | URL contains both keywords (space-separated)                                |
| `allintitle:keyword1 keyword2`                     | `allintitle:admin user`                        | Title contains both keywords                                                |
| `allinanchor:keyword1 keyword2`                    | `allinanchor:"login panel"`                    | Anchor text includes all listed keywords                                    |
| `daterange:2459340-2459634`                        | `daterange:2459340-2459634 intext:confidential`| Search within pages indexed during a date range (Julian format)             |
| `info:abc.com`                                     | `info:example.com`                             | Displays Google’s info about the site                                       |
| `link:abc.com`                                     | `link:wikipedia.org`                           | Shows pages linking to a given site                                         |
| `-keyword`                                         | `password -reset`                              | Exclude results containing a specific word                                  |
| `OR`                                               | `intitle:password OR inurl:login`              | Search for one or the other (logical OR)                                    |

*And many more!*

---

## 🎯 Practical Examples & Pro Tips

- **Find PDF files about security**
  - `filetype:pdf security`
- **Find pages linking to Github**
  - `link:fr.github.com`
- **Look for open directory listings**
  - `intitle:"index of /"`
- **Find admin login pages**
  - `allinurl:"admin login"`
- **Search for credential exposures in text files**
  - `intext:password filetype:txt`
- **List admin passwords on French sites**
  - `inurl:password admin site:fr`

### 🧠 Tips for Using Dorks Effectively

- ✨ **Chain operators for specificity:** Combine multiple operators to reduce noise. E.g., `site:.gov filetype:xls intext:email`.
- 🔍 **Focus on exposed directories:** Directory listings (`intitle:"index of /"`) with filetype filters (`filetype:log`, `filetype:bak`) help spot forgotten backups and logs.
- 🕵️ **Identify password leaks:** Use `intext:password | pass | pwd` with `filetype:txt OR filetype:log` to maximize keyword coverage.
- 🌍 **Target regions or languages:** Use `site:fr`, `site:edu`, or `site:gov` to focus on relevant TLDs. Use language-specific words in dorks.
- ⏱️ **Look for recent exposures:** Use `daterange:` for time-limited leaks or recently indexed content.
- 🃏 **Wildcard search:** Use `*` to capture variable parts, e.g., `intitle:"index of" inurl:ftp *backup*`.
- 🏷️ **Hunt for web shells or admin consoles:** `intitle:"shell" OR intitle:"upload" filetype:php -github` to avoid public source repositories.
- 👁️ **Spot exposed documents:** Try `filetype:xls intext:"login" intext:"password"` to find spreadsheets holding access data.

---

## 🚨 Security Tips & Ethical Use

- **Never scan or probe without explicit authorization.**
- Use `site:` operators to minimize collateral impact and avoid unnecessary attention.
- Prefer using VPNs, Tor, or proxies to separate recon from personal activity.
- Google may temporarily block you for too many similar queries—diversify your dorks and throttle your requests.
- If you discover sensitive data, engage in responsible disclosure to the site owner.
- Log your search queries to document ethical/research use if needed.

---

## #dork-examples-in-action

> Real-world dorks you can adapt:

- Discover sensitive PDF files about network configurations
  - `filetype:pdf intext:"configuration" intext:"network" site:.gov`
- Find public backup files on any French site:
  - `site:fr inurl:backup filetype:zip OR filetype:tar`
- Detect open admin interfaces with multiple keywords:
  - `allintitle:admin login "dashboard"`
- Search for emails on Brazilian university websites:
  - `site:br intext:@gmail.com OR intext:@yahoo.com`
- Hunt for SQL error messages:
  - `intext:"you have an error in your SQL syntax" -github`
- Find exposed WordPress login panels:
  - `inurl:wp-login.php -github`
- Locate cameras, printers, or embedded devices:
  - `inurl:view/view.shtml`  
  - `inurl:main.cgi admin`

---

## 📚 More Resources

- [Exploit-DB Google Hacking Database (GHDB)](https://www.exploit-db.com/google-hacking-database) – The most comprehensive reference for Google Dork queries and real-world attack scenarios!

---

## 🚩 Disclaimer

This project is for **educational and ethical purposes** only.  
Unauthorized probing of networks or systems is prohibited by law.

---

**Want to contribute your own favorite dorks or usage tips? Pull requests welcome!**
