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
