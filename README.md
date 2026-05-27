# 🔄 MAC Address Changer

A powerful command-line tool written in Python that allows you to **spoof or change the MAC address** of any network interface on Linux — useful for network testing, privacy, and ethical hacking practice.

> ⚠️ **Disclaimer:** This tool is intended for **educational and ethical use only**. Only use it on networks and devices you own or have explicit permission to test.

---

## 📸 Preview

```
$ python mac_changer_algorithm.py -i eth0 -m 00:11:22:33:44:55

[*] Current MAC: aa:bb:cc:dd:ee:ff
[+] Changing MAC address for eth0 to 00:11:22:33:44:55
[+] MAC address successfully changed to 00:11:22:33:44:55
```

---

## ✨ Features

- 🔍 **Reads current MAC address** of any network interface
- 🔄 **Changes MAC address** to any user-specified value
- ✅ **Verifies the change** was applied successfully
- 🛡️ **Validates input** — gives helpful errors for missing arguments
- 🧠 Uses **regex** to accurately extract MAC from `ifconfig` output

---

## 🛠️ Requirements

| Requirement | Detail |
|-------------|--------|
| OS | Linux only (uses `ifconfig`) |
| Python | 3.x |
| Privileges | Must run as **root** (`sudo`) |
| Tool | `net-tools` (`ifconfig` must be installed) |

### Install Dependencies

```bash
# Install net-tools if ifconfig is missing
sudo apt install net-tools

# No external Python libraries needed — all standard modules
```

---

## 📁 Project Structure

```
mac-changer/
│
└── mac_changer_algorithm.py    # Main script
```

---

## ▶️ How to Run

### Basic Syntax

```bash
sudo python mac_changer_algorithm.py -i <interface> -m <new_mac>
```

### Options

| Flag | Long Form | Description |
|------|-----------|-------------|
| `-i` | `--interface` | Network interface (e.g. `eth0`, `wlan0`) |
| `-m` | `--mac` | New MAC address to assign |

### Examples

```bash
# Change MAC of eth0
sudo python mac_changer_algorithm.py -i eth0 -m 00:11:22:33:44:55

# Change MAC of wlan0 (WiFi)
sudo python mac_changer_algorithm.py -i wlan0 -m aa:bb:cc:dd:ee:ff

# View help
sudo python mac_changer_algorithm.py --help
```

---

## 🔍 How to Find Your Interface Name

```bash
ifconfig        # Lists all active network interfaces
ip link show    # Alternative command
```

Common interface names: `eth0`, `wlan0`, `ens33`, `enp0s3`

---

## 🧠 How It Works

```
┌─────────────────────────────────────────────────┐
│                 Program Flow                    │
├─────────────────────────────────────────────────┤
│  1. Parse -i (interface) and -m (mac) args      │
│  2. Read current MAC using ifconfig + regex     │
│  3. Bring interface DOWN  → ifconfig eth0 down  │
│  4. Set new MAC           → ifconfig hw ether   │
│  5. Bring interface UP    → ifconfig eth0 up    │
│  6. Read MAC again & verify the change          │
└─────────────────────────────────────────────────┘
```

---

## ✅ Expected Output

**Success:**
```
[*] aa:bb:cc:dd:ee:ff
[+] Changing MAC address for eth0 to 00:11:22:33:44:55
[+] MAC address successfully changed to 00:11:22:33:44:55
```

**Failure (wrong interface):**
```
[-] Could not read MAC address.
[-] MAC address did not get changed. Current MAC is None
```

**Missing argument:**
```
[-] Please specify an interface, use --help for more info.
```

---

## ⚠️ Important Notes

- 🔐 Always run with `sudo` — changing MAC requires root privileges
- 🐧 **Linux only** — `ifconfig hw ether` is not available on Windows/macOS
- 🔁 The MAC change is **temporary** — it resets after a reboot
- 📡 Changing WiFi MAC may disconnect you briefly

---

## 🤝 Contributing

Pull requests are welcome! For major changes, please open an issue first.

---

## 👨‍💻 Author

Built with 🐍 Python for ethical hacking & networking education.
