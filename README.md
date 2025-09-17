
### Example Blog Section (Markdown)

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

```

---

### ✅ Result when rendered on GitHub Pages
- The **bold words** (`**like this**`) stand out in the text.  
- The commands are inside a **boxed code block** (triple backticks).  
- Headings with `##` create big section titles.  
- Emojis (🚀 📂 🔍 ✅) make sections pop (optional).  

---

👉 Question for you:  
Do you want me to **reformat your entire Gobuster blog draft** like this (with bold topics + boxed commands), so you can paste it straight into your GitHub Pages repo?
```

