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
