# 🌐 Remote Management Center (RMC)

A **zero-dependency, air-gap ready, single-file dashboard** for managing network connections (SSH, RDP, and HTTP/S). 

Built entirely in HTML, CSS, and vanilla JavaScript, this tool requires absolutely no backend, no database setup, and no external CDN libraries. You can drop it onto any machine, double-click it, and instantly have a fully functional management dashboard.

![Status](https://img.shields.io/badge/Status-Active-success)
![Environment](https://img.shields.io/badge/Environment-Air--Gapped-blue)
![Dependencies](https://img.shields.io/badge/Dependencies-None-brightgreen)

## ✨ Features

* 🚀 **Zero-Install Architecture:** Runs entirely in the browser using a single `.html` file.
* 💾 **Local Persistence:** Data is safely stored in your browser's Local Storage. No data is ever sent to an external server.
* 🖥️ **Protocol Handlers (SSH & RDP):** Instantly launch native OS applications directly from the browser:
  * `ssh://` -> Native OS Terminal
  * `putty://` -> PuTTY Client
  * `rdp://` -> Microsoft Remote Desktop (mstsc)
* ⚙️ **Custom Client Preferences:** Choose between Native SSH, PuTTY, or set your own custom protocol prefix directly from the Settings menu.
* 📊 **Dashboard Analytics:** Real-time gauge charts and metric cards displaying network security compliance (Secure vs. Unsecure connections) and a hierarchical Category/Subcategory table.
* 🗂️ **Advanced Organization:** Tag, filter, and search nodes by Protocol, Location, Category, and Subcategory.
* 🧹 **Metadata Management:** Built-in tools to bulk-delete misspelled or obsolete Locations and Categories across all nodes.
* 📥 **Bulk CSV Ingestion:** Import hundreds of nodes instantly via a simple comma-separated list, with built-in duplicate prevention.
* 📤 **Data Portability:** Export your entire database back to a CSV at any time, or safely purge the local database with a single click.

---

## 🛠️ How It Works

### The Local Storage Database
Because RMC is designed for strict, offline environments, it does not use a traditional SQL database. Instead, it utilizes the HTML5 `localStorage` API. When you add a node, it is converted into a JSON object and saved securely within your browser's local cache.

### Overcoming the Browser Sandbox (The Protocol Fix)
Modern web browsers sandbox websites, preventing them from arbitrarily launching local executable files (like `mstsc.exe` or `putty.exe`) for security reasons. 

To bypass this and allow 1-click remote management, RMC uses **Custom URI Schemes**. Included in the dashboard's "Settings" menu is an automated **Windows Registry Fix Generator**. When downloaded and run, it writes a safe delayed-expansion command (`cmd /V:ON`) into the Windows Registry. This tells the Windows Shell exactly how to handle these links, stripping the web prefixes and securely forwarding the target IP/Hostname to your local command line or RDP client.

---

## 🚀 Getting Started

1. Download the `Update new_version.html` file.
2. Double-click the file to open it in your preferred web browser (Chrome, Edge, Firefox, Safari).
3. Click **Add New** to manually add your first node, or click **Import** to upload a CSV file.
4. *(Windows Users Only)*: Go to the **Settings** menu and download the **.REG Fix** to enable 1-click launching of SSH and RDP clients.

### CSV Import Format
When importing data in bulk, use a plain text `.csv` file without headers. The system expects 6 columns:

`type, name, target, location(optional), category(optional), subcategory(optional)`

**Supported Types:** `url`, `ssh`, `rdp`

**Example:**
```csv
url, Core-FW, [https://10.0.0.1](https://10.0.0.1), HQ, Firewalls, FortiGate
ssh, Dist-SW-1, admin@10.0.0.2, HQ, Switches, Core Switches
rdp, Main-Server, 10.0.0.5, HQ, Servers, Windows Server 2022
