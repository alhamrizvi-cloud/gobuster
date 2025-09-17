Gobuster — fast directory & subdomain discovery for web testers

TL;DR: Gobuster is a Go-based tool for brute-forcing directories, files, virtual hosts and DNS/subdomains. This post explains why it’s useful, how to install and run it, practical examples (including GitHub Pages), safety notes, and tips & wordlists to get better results.

Published: 2025-09-18
Author: Alham Rizvi

What is Gobuster?

Gobuster is a command-line tool (written in Go) used to discover hidden files, directories, virtual hosts, and DNS names by brute force using wordlists. Unlike crawlers, Gobuster does wordlist-driven requests in parallel, which makes it extremely fast for discovery tasks during penetration tests or CTFs.

It’s commonly used to:

Find backup files (backup.zip, site.bak)

Reveal exposed directories like .git/ or configuration files such as .env

Enumerate subdomains for recon

Discover hidden admin panels or API endpoints


### Installation

````markdown
## 🚀 Installation

**For Kali / Ubuntu:**

```bash
sudo apt update
sudo apt install gobuster
````

**From Source (requires Go):**

```bash
go install github.com/OJ/gobuster/v3@latest
```

---

## 📂 Core Modes

* **`dir`** → Directory / File enumeration
* **`dns`** → Subdomain brute force
* **`vhost`** → Virtual host brute force
* **`s3`** → Amazon S3 bucket discovery
* **`fuzz`** → Flexible fuzzing mode

---

## 🔍 Example: Directory Scan

**Command:**

```bash
gobuster dir -u https://your-username.github.io/ \
  -w /usr/share/seclists/Discovery/Web-Content/common.txt \
  -t 50 -x html,php,txt,zip,env
```

**Explanation:**

* **`-u`** → Target URL
* **`-w`** → Wordlist
* **`-t`** → Threads (speed)
* **`-x`** → File extensions to check

# Basic directory example

Scan a GitHub Pages site (or any website) for common files and folders:
```
gobuster dir -u https://your-username.github.io/ \

```
  -w /usr/share/seclists/Discovery/Web-Content/common.txt \
  -t 50 \
  -x html,php,txt,zip,env

Flags explained:

-u target URL

-w wordlist

-t threads (concurrency)

-x extensions to append to words

If the site contains /backup.zip or /admin/, Gobuster will show the path and status code.

Example: finding .git on a Pages site

Many testers set up a local playground or find misconfigured gh-pages. To look for an exposed .git:

```
gobuster dir -u https://demo-site.github.io/ -w /usr/share/wordlists/dirb/common.txt -x git -t 30
```
If .git/ is accessible, use git-dumper or wget to retrieve the repo only on assets you own or with explicit permission.

# Subdomain enumeration

Quick DNS brute force against example.com:

```
gobuster dns -d example.com -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt -t 50
```
Useful for finding dev.example.com, api.example.com, etc.

# Virtual-host (vhost) enumeration

Some servers respond differently depending on the Host: header:

```
gobuster vhost -u http://example.com -w vhosts.txt -t 40
```
# Wordlists & tips

SecLists is the go-to source: Discovery/Web-Content and Discovery/DNS folders.

Try multiple lists: common.txt, directory-list-2.3-medium.txt, and custom lists for your target (framework-specific names like wp-admin for WordPress).

Try extensions: .zip, .bak, .tar.gz, .env, .sql, .json, .yml.

Respect rate limits — reduce -t if you see 429/Blocking.

Combine with Burp or curl for manual verification.

Practical GitHub Pages note

If you’re testing GitHub Pages you control (like a blog you’re making), Gobuster is great for verifying you didn’t accidentally publish sensitive files (e.g., secret.txt, backup.zip or .env in docs/). Create a test backup file and ensure it’s not reachable publicly, or purposely host a honeypot file to practice discovery techniques on your own assets.

# Safety & legal reminder

Never run Gobuster against domains or services you don't own or don’t have explicit permission to test. Automated brute-force scanning can be considered abusive by hosting providers and may violate terms of service or local law. Use a sandbox/test repo or get written permission.

# Practical workflow (example)

Recon: passive (WHOIS, crt.sh, GitHub search) → identify targets.

Run gobuster dir on public pages you own (or have permission for).

Verify positive results manually (open in browser, curl -I) — don’t blindly trust 200/403 codes.

Download and inspect any discovered archives (only from your test site).

Document findings and patch/remove sensitive files.

Quick troubleshooting

No results? Try larger wordlists or fewer threads.

Getting lots of 403s? The site might filter by User-Agent — try -a "Mozilla/5.0" or lower concurrency.

Slow or blocked? Lower -t, add delays, or use authenticated requests (if testing an authenticated directory).

CLI cheatsheet
# Directory brute-force
```
gobuster dir -u https://target/ -w wordlist.txt -t 50 -x php,html,txt

```
# DNS/subdomain brute-force
```
gobuster dns -d target.com -w subdomains.txt -t 50

```
# Virtual host discovery
```
gobuster vhost -u http://target -w vhosts.txt -t 40
```

Where to go next

Learn how to build or modify custom wordlists.

Combine Gobuster with wfuzz or ffuf for more advanced fuzzing.

Set up a safe CTF-style target or GitHub Pages sandbox to practise.

# Conclusion

Gobuster is a simple but powerful discovery tool — extremely useful for web recon when used responsibly. If you’re writing a Gobuster blog post, include clear examples, safety/legal guidance, and a real-world demo (on a sandbox repo). Readers love a “play along” section where they can run commands on a sample site you provide.

# Excerpt / Tweet

Excerpt: Learn Gobuster: fast directory, virtual host, and subdomain discovery for web testing. Install, run, and use safe examples — including GitHub Pages—plus wordlists and tips.
Tweet: New on the blog — Gobuster 101: install, run, and hunter-tips for directory & subdomain discovery (with GitHub Pages demo). #infosec #CTF

