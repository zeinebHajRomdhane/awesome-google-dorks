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
| `daterange:2455340-2455634`                        | `daterange:2455340-2455634 intext:confidential`| Search within pages indexed during a date range (Julian format)             |
| `info:abc.com`                                     | `info:example.com`                             | Displays Google’s info about the site                                       |
| `link:abc.com`                                     | `link:wikipedia.org`                           | Shows pages linking to a given site                                         |
| `-keyword`                                         | `password -reset`                              | Exclude results containing a specific word                                  |
| `OR`                                               | `intitle:password OR inurl:login`              | Search for one or the other (logical OR)                                    |

*And many more!*

---

## 🎯 Practical Examples

- Find PDF files about cybersecurity:  
  `filetype:pdf sécurité`
- Find pages linking to Wikipedia:  
  `link:fr.wikipedia.org`
- Look for open "directory listings":  
  `intitle:"index of /"`
- Find admin login pages:  
  `allinurl:"admin login"`
- Search specific credentials exposure:  
  `intext:password filetype:txt`
- Get only French results about admin passwords:  
  `inurl:password admin site:fr`

Check more examples [below](#dork-examples-in-action)!

---

## 🔒 Security Tips & Ethical Use

- **Always have explicit authorization before probing sites with dorks!**
- Use personal/private search windows or tools to limit footprint and avoid leaking intent.
- Combine with `site:` to restrict your queries and avoid scanning the entire web.
- Watch out for sensitive discoveries: **report responsibly** (responsible disclosure).
- Don’t download or exploit data found without consent; it's illegal and unethical.
- Try your dorks on test environments first to build confidence.

---

## 📈 Boost Your Search Efficiency

- Combine multiple operators for pinpoint accuracy.
  - Example: `site:edu filetype:xls intext:email`
- Use quoted strings for exact match searches (“password list”).
- Exclude undesired results with `-`.
- Use `daterange:` for only recent results.
- Remember: Results may change as Google updates its index!

---

## 📚 More Resources

- [Exploit-DB Google Hacking Database (GHDB)](https://www.exploit-db.com/google-hacking-database) – The most comprehensive reference for Google Dork queries and real-world attack scenarios!

---

## 🚩 Disclaimer

This project is for **educational and ethical purposes** only.  
Unauthorized probing of networks or systems is prohibited by law.

---

**Want to contribute your own favorite dorks or usage tips? Pull requests welcome!**

---
