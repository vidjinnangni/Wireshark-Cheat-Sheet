# Wireshark-Cheat-Sheet
 Essential capture filters, display filters, common protocol fields, and tips.

 Wireshark is a powerful, open-source packet analyzer widely used by network professionals for monitoring, troubleshooting, and analyzing network traffic. It offers deep visibility into real-time data flows, supports a broad range of protocols, and provides an intuitive interface for filtering and inspecting packets. With Wireshark, users can quickly identify performance bottlenecks, uncover security vulnerabilities, and gain valuable insights into the intricate details of network communication.

## List of contents
- [Download and install](#download)
- [Logical operators](#logical-operators)
- [Capturing modes](#capturing-modes)
- [Filtering types](#filtering-types)

## <a name="download">Download and Instal Wireshark</a>
![Download Wireshark](/imgs/download.jpg)

### Windows
1. Go to the [official Wireshark website](https://www.wireshark.org/download.html).
2. Select the appropriate Windows installer (64-bit or 32-bit, typically 64-bit).
3. Run the downloaded installer and follow the on-screen prompts.
You can optionally install additional components like USBPcap for capturing USB traffic.
4. Once the installation is complete, launch Wireshark from the Start menu.

### macOS
1. Visit the [Wireshark downloads page](https://www.wireshark.org/download.html).
2. Download the macOS installer package (.dmg file).
3. Open the downloaded .dmg file and drag the Wireshark icon into your `Applications` folder.
4. Double-click Wireshark in `Applications` to start using it.
If you encounter permissions issues, go to `System Preferences > Security & Privacy` and grant the necessary permissions.

### Linux (Debian/Ubuntu-based)
1. Open a terminal.
2. Update your package list:
   ```bash
   sudo apt update -y
   ```
3. Install Wireshark:
   ```bash
   sudo apt install wireshark
   ```
4.	During installation, you may be prompted to allow non-superusers to capture packets. Select Yes if desired.
5.	Launch Wireshark from the Applications menu or by typing wireshark in a terminal.

### Linux (Fedora/CentOS/RHEL)
1. Open a terminal.
2. Update the DNF package repository information:
   ```bash
   sudo dnf updateinfo
   ```
3. Install Wireshark:
   ```bash
   sudo dnf install wireshark
   ```
(For older distributions, use yum instead of dnf.)
4.	Run Wireshark from your Applications menu or by typing wireshark in a terminal.

Tip: For additional installation details, visit the [official Wireshark documentation](https://www.wireshark.org/docs/). Depending on your platform, you may need to adjust permissions or group memberships to capture live network traffic without root privileges.


### Linux (Arch-based)
1. Open a terminal.
2. Synchronize the database:
   ```bash
   sudo pacman -Sy
   ```
3. Update all installed packages to their latest versions:
   ```bash
   sudo pacman -Su
   ```
4. Install Wireshark:
   ```bash
   sudo pacman -S wireshark-qt
   ```
(Alternatively, install wireshark-cli for the CLI version.)
5. Launch Wireshark from your Applications menu or by typing wireshark in a terminal.


## <a name="logical-operators">Logical operators</a>
| Operator          | Description                                     | Example                            |
|-------------------|-------------------------------------------------|------------------------------------|
| `and`            | Logical AND; both conditions must be true       | `ip.src == 192.168.1.1 and tcp`   |
| `or`             | Logical OR; either condition can be true        | `ip.src == 192.168.1.1 or tcp`    |
| `not`            | Logical NOT; negates a condition                | `not tcp.port == 80`              |
| `xor`            | Logical XOR; one condition is true, but not both| `ip.src == 192.168.1.1 xor ip.dst == 192.168.1.2` |
| `>`              | Greater than                                    | `frame.len > 1000`                |
| `<`              | Less than                                       | `frame.len < 1000`                |
| `>=`             | Greater than or equal to                        | `frame.len >= 1000`               |
| `<=`             | Less than or equal to                           | `frame.len <= 1000`               |
| `==`             | Equal to                                        | `ip.src == 192.168.1.1`           |
| `!=`             | Not equal to                                    | `ip.src != 192.168.1.1`           |


## <a name="captruting-modes">Capturing modes</a>
| Capturing Mode       | Description                                                                                  | Example Use Case                             |
|----------------------|----------------------------------------------------------------------------------------------|---------------------------------------------|
| **Promiscuous Mode** | Captures all packets on the network segment, regardless of whether they are addressed to the capturing device. | Useful for analyzing network traffic at a broad level. |
| **Monitor Mode**     | Captures packets at the data link layer, including packets not addressed to the capturing device. Only available for wireless networks. | Useful for analyzing Wi-Fi traffic or debugging wireless issues. |
| **Capture Filter**   | Limits the packets captured based on specified filter criteria.                              | Used when you want to capture only HTTP traffic (e.g., `port 80`). |
| **Specific Interface** | Captures packets on a specified network interface.                                          | Useful when you want to capture traffic only from a specific adapter. |
| **Ring Buffer**      | Captures data into a series of files and overwrites old ones when the buffer is full.         | Useful for long-term traffic monitoring.    |
| **Buffer Size Setting** | Allows adjustment of the buffer size to optimize capture performance and reduce packet loss. | Useful for high-traffic networks.           |
| **Promiscuous Disabled** | Captures only packets addressed to the capturing device.                                 | Useful for troubleshooting device-specific traffic issues. |
| **Capture in Background** | Runs the capture process without the GUI interface to reduce resource usage.             | Useful for remote or headless capturing.    |


## <a name="filtering-types">Filtering types</a>
| Filtering Type       | Description                                                                    | Example                                |
|----------------------|--------------------------------------------------------------------------------|----------------------------------------|
| **Display Filter**   | Filters packets after capture to refine the displayed results.                | `ip.src == 192.168.1.1 and tcp.port==80` |
| **Capture Filter**   | Filters packets during capture to limit which packets are captured.           | `host 192.168.1.1`                     |
| **Protocol Filter**  | Filters packets based on specific protocols.                                  | `tcp`, `udp`, `icmp`                   |
| **IP Address Filter**| Filters packets based on source or destination IP addresses.                  | `ip.src == 192.168.1.1` or `ip.dst == 192.168.1.2` |
| **Port Filter**      | Filters packets based on source or destination ports.                         | `tcp.port == 443` or `udp.port == 53`  |
| **MAC Address Filter**| Filters packets based on source or destination MAC addresses.                 | `eth.src == 00:11:22:33:44:55`         |
| **Wildcard Filter**  | Allows partial matches using wildcards like `contains`.                       | `http.request.uri contains "login"`    |
| **Logical Operators**| Combines multiple filters using logical operators such as `and`, `or`, `not`. | `tcp and not port 80`                  |
| **Length Filter**    | Filters packets based on their length.                                        | `frame.len > 1000`                     |
| **Time Filter**      | Filters packets based on capture time ranges.                                 | `frame.time >= "2023-12-01 10:00:00"`  |


