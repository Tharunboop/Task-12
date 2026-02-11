# 🔐 Task 12 – Log Monitoring & Analysis

## 📌 Objective
To monitor Linux authentication logs and detect failed login attempts using Kali Linux.

---

## 🖥 Environment
- OS: Kali Linux
- Service: OpenSSH Server
- Log Source: systemd journal (journalctl)

---

## ⚙ Step 1 – Install SSH Server

Command:
sudo apt install openssh-server -y


---

## ⚙ Step 2 – Start and Verify SSH Service

Commands:
sudo systemctl start ssh
sudo systemctl status ssh


Observation:
SSH service is active and running.

---

## 🔓 Step 3 – Simulate Failed Login Attempt

Command:
ssh fakeuser@localhost

Entered incorrect passwords multiple times.

Result:
Permission denied (publickey,password)


---

## 🔎 Step 4 – Detect Failed Password Logs

Command:
sudo journalctl -u ssh | grep "Failed password"

Observation:
Multiple failed authentication entries detected.


---

## 📊 Step 5 – Count Failed Login Attempts

Command:
sudo journalctl | grep "Failed password" | wc -l

Result:
4 failed login attempts detected.


---

## 🌐 Step 6 – Identify Source IP Address

Command:
sudo journalctl | grep "Failed password" | awk '{print $(NF-3)}' | sort | uniq -c | sort -nr

Result:
4 ::1

Meaning:
All failed attempts originated from localhost (::1 IPv6 loopback address).


---

## 🧾 Logs Analyzed
- SSH authentication logs
- systemd journal logs


## 🚨 Findings
- 4 failed login attempts detected.
- Source IP: ::1
- Demonstrated brute-force login simulation.
- Successfully correlated authentication events.



## ✅ Conclusion
Log monitoring and analysis was successfully performed.
Failed login attempts were identified and analyzed using journalctl.
Basic incident detection skills were demonstrated.
