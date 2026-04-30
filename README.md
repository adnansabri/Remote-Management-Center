🌐 Remote Management Center (RMC)
A zero-dependency, air-gap ready, single-file dashboard for managing network connections (SSH, RDP, and HTTP/S).
Built entirely in HTML, CSS, and vanilla JavaScript, this tool requires absolutely no backend, no database setup, and no external CDN libraries. You can drop it onto any machine, double-click it, and instantly have a fully functional management dashboard.
✨ Features
●	🚀 Zero-Install Architecture: Runs entirely in the browser using a single .html file.
●	💾 Local Persistence: Data is safely stored in your browser's Local Storage. No data is ever sent to an external server.
●	🖥️ Protocol Handlers: Instantly launch native OS applications directly from the browser:
○	ssh:// -> Native OS Terminal
○	putty:// -> PuTTY Client
○	rdp:// -> Microsoft Remote Desktop (mstsc)
●	📊 Dashboard Analytics: Real-time gauge charts and metric cards displaying network security compliance (Secure vs. Unsecure connections) and category distribution.
●	🗂️ Hierarchical Organization: Tag and filter nodes by Protocol, Location, Category, and Subcategory.
●	📥 Bulk CSV Ingestion: Import hundreds of nodes instantly via a simple comma-separated list.
●	📤 Data Portability: Export your entire database back to a CSV at any time, or purge the local database with a single click.
🛠️ How It Works
The Local Storage Database
Because RMC is designed for strict, offline environments, it does not use a traditional SQL database. Instead, it utilizes the HTML5 localStorage API. When you add a node, it is converted into a JSON object and saved securely within your browser's local cache.
Overcoming the Browser Sandbox (The Protocol Fix)
Modern web browsers sandbox websites, preventing them from arbitrarily launching local executable files (like mstsc.exe or putty.exe) for security reasons.
To bypass this and allow 1-click remote management, RMC uses Custom URI Schemes (ssh://, rdp://). Included in the dashboard's "Settings" menu is an automated Windows Registry Fix Generator. When downloaded and run, it tells the Windows Shell exactly how to handle these links safely, stripping the prefixes and forwarding the IP/Hostname to your local command line.
🚀 Getting Started
1.	Download the dashboard.html file.
2.	Double-click the file to open it in your preferred web browser (Chrome, Edge, Firefox, Safari).
3.	Click Add New to manually add your first node, or click Import to upload a CSV file.
4.	(Windows Users Only): Go to the Settings menu and download the .reg fix to enable 1-click launching of SSH and RDP clients.
CSV Import Format
When importing data in bulk, use a plain text .csv file without headers. The system expects up to 6 columns:
type, name, target, location(optional), category(optional), subcategory(optional)
Example:
url, Core-FW, [https://10.0.0.1](https://10.0.0.1), HQ, Firewalls, FortiGate
ssh, Dist-SW-1, admin@10.0.0.2, HQ, Switches, Core
rdp, Main-Server, 10.0.0.5, HQ, Servers, Windows

🔒 Security & Privacy Disclaimer
●	This application is completely client-side. It makes zero outbound network requests.
●	Passwords or confidential keys should never be stored in the "Target" field. Rely on local SSH key-pairs (e.g., ~/.ssh/id_rsa) or native Windows Credential Manager for authentication.
●	If deploying on a shared computer, be aware that anyone with access to that specific browser profile can view the saved IP addresses and hostnames.
