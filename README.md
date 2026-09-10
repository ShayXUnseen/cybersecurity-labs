# 🐧 My Cybersecurity Labs Portfolio

Welcome to my hands-on learning log! This repository contains the documented proof of my daily progress as I build my foundational skills in operating systems, virtualization, and security analysis.

---

## 📁 Lab 1: Basic Terminal Navigation
*Completed on: 7 September 2026*

Let me give you an overview. The `ls` command lists the directories and files present in the current directory. The `cd` command changes the directory, while `cd ..` changes the directory one step up. The `mkdir` command creates a directory. `nano` is an editor, so `nano` followed by a file name opens that file for editing and creates it when you save it if it does not already exist.

The `cp` command copies a file, while `rm` deletes a file. The `mv` command is used to move as well as rename a file.

A special flag, `-r`, is used with the copy and remove commands when working with directories. It allows you to copy or remove a directory along with all its contents. `-r` stands for **recursive**.

Here's the proof of my progress:
<img width="1212" height="555" alt="image" src="https://github.com/user-attachments/assets/a4d24aed-cd00-49d1-ad8f-9a445ae3e670" />

---

## 🔍 Lab 2: File Reading and Searching (GREP)
*Completed on: 8 September 2026*

Today I learned how to read files and search through logs in the Linux terminal.

The `touch` command creates a completely blank file. To view what is inside a file without opening an editor, I learned three commands: `cat` dumps the entire file's text on the screen, `head` shows only the top lines, and `tail` shows only the bottom lines (which is useful for checking the most recent entries in a system log).

The real power tool is `grep`. It acts like a search bar to find specific words or patterns inside a text file.

I also learned how to use flags with `grep` to make it more useful:
- `-i` ignores whether the letters are uppercase or lowercase.
- `-v` excludes specific words from the search.
- `-n` displays the exact line number where the word was found.
<img width="848" height="422" alt="Day5_Head_Tail" src="https://github.com/user-attachments/assets/268f748e-371d-40f6-975b-5f28660dfd15" />
<img width="855" height="178" alt="Day5_Grep_success" src="https://github.com/user-attachments/assets/31f0fb25-469a-4995-9d54-15f844e88628" />


As a challenge, I simulated a real security threat hunt. I created a mock server log and used the command `grep "10.0.0.50" auth.log` to instantly isolate a suspicious IP address and find out which usernames they were trying to target. 

Here's the proof of my progress:


<img width="854" height="361" alt="Day5_Grep_messy_search1" src="https://github.com/user-attachments/assets/bc47f66d-55b2-4a40-a354-22aad92d3297" />

## 🕵️ Mini-Project: Web Server Log Audit
*Completed on: 9 September 2026*

Today I completed a practical log audit scenario to strengthen my terminal navigation and `grep` searching skills. 

- Created an organized directory structure (`server_audit/raw_logs` and `evidence`).
- Inspected web server access logs using `head` and `tail`.
- Used `grep -i` to hunt for critical error entries.
- Isolated suspicious scanning activity from IP `45.33.32.156` using line-number auditing (`grep -n`).
- Managed and backed up log evidence using `cp` and `mv`.

Here's the proof of my progress:
<img width="1295" height="737" alt="image" src="https://github.com/user-attachments/assets/4870e413-af43-41ad-a32e-2f5c8d925405" />

## 🔒 Lab 3: Linux Permissions & System Hardening
*Completed on: 9 September 2026*

Today I learned how to enforce system hardening and the Principle of Least Privilege (PoLP) using Linux file permissions and ownership controls.

- Understood the 10-character permission string (`rwx` breakdown for Owner, Group, and Others).
- Restricted access to sensitive secret files using `chmod 600` (`-rw-------`).
- Configured executable security script permissions using `chmod 755` (`-rwxr-xr-x`).
- Practiced file ownership concepts using `chown`.

Here's the proof of my progress:
<img width="1303" height="615" alt="image" src="https://github.com/user-attachments/assets/87694b91-295c-464b-bf05-fa5de4e1db04" />

## 🕵️ Mini-Project: Staging Server Forensic Audit & Hardening
*Completed on: 9 September 2026*

To test everything I learned from Day 1 to Day 6, I completed a practical incident response scenario on an unhardened staging server.

**The Scenario:**
A staging server contained exposed API keys, unconfigured backup scripts, and suspicious external login attempts. My task was to audit the logs, secure the sensitive files, and enforce proper access controls.

**What I Accomplished:**
- **Threat Hunting:** Used `grep -n` to track down suspicious login attempts from IP `198.51.100.42` in server audit logs.
- **System Hardening & PoLP:** Applied the Principle of Least Privilege to `key_backup.txt` using `chmod 600` (`-rw-------`) so only the file owner can read and write to it.
- **Script Security:** Made `backup_tool.sh` executable using `chmod 755` (`-rwxr-xr-x`) while restricting write permissions for others.
- **Ownership Management:** Transferred administrative ownership using `sudo chown` to verify access controls.

Here's the proof of my progress:
<img width="1291" height="471" alt="image" src="https://github.com/user-attachments/assets/e4ee03fe-3b0d-4380-9ded-e6b8763b8f6a" />
<img width="1293" height="447" alt="image" src="https://github.com/user-attachments/assets/be2103c4-708f-43c6-aafd-6128d734abdc" />

## 🌐 Lab 5: Network Interface & Connectivity Audit
*Completed on: 10 September 2026*

**Objective:**
Identify active network adapters, verify local loopback functionality, test external internet routing, and audit DNS resolution.

**Commands Run:**
- `ip a`
- `ping -c 4 127.0.0.1`
- `ping -c 4 8.8.8.8`
- `nslookup google.com`

**What I Observed:**
- Running `ip a` identified my primary network interface and my assigned private IP address.
- Pinging `127.0.0.1` confirmed that my system's internal TCP/IP network stack is healthy.
- Pinging `8.8.8.8` resulted in 0% packet loss, confirming my default gateway and NAT router are forwarding outbound traffic.
- `nslookup google.com` successfully queried DNS servers to translate the human-readable domain into its public destination IP address.

**Security Relevance:**
When performing incident response or host investigation, inspecting network interfaces helps determine if an infected system is actively connected to the network, isolated, or communicating with external IP addresses.

**Evidence:**
<img width="1292" height="508" alt="image" src="https://github.com/user-attachments/assets/e3807f83-3e5a-4f1c-967d-a59ad748f181" />
<img width="1287" height="394" alt="image" src="https://github.com/user-attachments/assets/f45ff4d6-8494-4cd8-a8ec-e83ef5acd10c" />





