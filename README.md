# Gobuster
Indepth detail explaination of directory bruteforcing tool: Gobuster
# What is Gobuster?

Gobuster is a brute-force directory and file discovery tool written in Go. It’s used in penetration testing to enumerate hidden resources on web servers. Instead of crawling, it uses a wordlist to try different paths, files, or DNS subdomains.

It’s fast because it’s written in Go and uses concurrency (parallel threads).

It’s commonly used to:

Find backup files (backup.zip, site.bak)

Reveal exposed directories like .git/ or configuration files such as .env

Enumerate subdomains for recon

Discover hidden admin panels or API endpoints
