# Wireshark-Cheat-Sheet
 Essential capture filters, display filters, common protocol fields, and tips.

 Wireshark is a powerful, open-source packet analyzer widely used by network professionals for monitoring, troubleshooting, and analyzing network traffic. It offers deep visibility into real-time data flows, supports a broad range of protocols, and provides an intuitive interface for filtering and inspecting packets. With Wireshark, users can quickly identify performance bottlenecks, uncover security vulnerabilities, and gain valuable insights into the intricate details of network communication.

## Logical operators
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


## Capturing modes
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


## Filtering types
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

