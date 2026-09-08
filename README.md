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
<img width="1152" height="648" alt="Day5_Head_Tail" src="https://github.com/user-attachments/assets/7bc7e0dd-240b-4d53-954e-ee9d86921f76" />
<img width="1152" height="648" alt="Day5_Grep_success" src="https://github.com/user-attachments/assets/d6981dc5-5d57-440a-a240-96fdfff89614" />

As a challenge, I simulated a real security threat hunt. I created a mock server log and used the command `grep "10.0.0.50" auth.log` to instantly isolate a suspicious IP address and find out which usernames they were trying to target. 

Here's the proof of my progress:


<img width="1152" height="648" alt="Day5_Grep_messy_search1" src="https://github.com/user-attachments/assets/a6963517-d8a6-4081-a8ba-712ccf37a690" />

