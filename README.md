# DoS Attack Script - README

## Overview

This Python script is designed to simulate various types of Denial-of-Service (DoS) attacks. It can perform the following types of attacks:

1. **UDP Flood Attack** (DDoS UDP packets)
2. **HTTP Request Flood Attack** (Multiple connection attempts)
3. **HTTP Packet Connection Attack** (High-volume HTTP packet connections)
4. **SYN Flood Attack** (Simulate SYN packets to flood a target)
5. **ICMP Flood Attack** (Send multiple ICMP packets)

> **Disclaimer**: This script is for educational purposes only. Launching DoS attacks against systems or networks without authorization is illegal and unethical. Use this script only on networks or systems you have explicit permission to test.

## Requirements

To run this script, you'll need Python 3.x and the following dependencies:

- `socket` - for network communication
- `random` - for generating random data (packet contents)
- `time` - for pausing between requests
- `threading` - for handling multiple threads in attacks
- `os` - for generating random data for packets
- `requests` - for fetching external resources (e.g., IP address)
- `struct` - for creating raw socket headers

You can install required dependencies by running:

```bash
pip install requests
```

## Usage

1. Clone or download the script file.
2. Run the script using Python:

   ```bash
   python dos_attack_script.py
   ```

3. The script will present a menu where you can choose the type of attack you want to perform. The available options are:

   - **UDP Attack**: Perform a UDP-based DoS attack.
   - **HTTP Attack**: Perform a multi-threaded HTTP attack by sending multiple HTTP requests.
   - **HTTP Packet Connection Attack**: Send HTTP GET requests with random packets.
   - **SYN Flood Attack**: Perform a SYN flood attack, sending SYN packets to a target server.
   - **ICMP Flood Attack**: Send ICMP echo request (ping) packets to a target IP.

4. After choosing an attack type, you'll be prompted to provide the following parameters:

   - **Target IP Address**: The IP address of the server you want to target.
   - **Port**: The port number on the target system (e.g., port 80 for HTTP).
   - **Additional Parameters**: Depending on the attack type, you may need to specify additional options like the number of threads, fake IP, or the number of packets to send.

5. To stop the attack, press `Ctrl+C` (KeyboardInterrupt).

## Available Attack Types

### 1. **UDP Flood Attack**
   - **Description**: This attack sends a large number of UDP packets to the target server, overwhelming its resources.
   - **Required Input**: Target IP and port.

### 2. **HTTP Attack**
   - **Description**: This attack performs an HTTP flood using multiple threads to send numerous HTTP GET requests to the target.
   - **Required Input**: Target IP, port, number of threads (default 5000), and a fake IP.

### 3. **HTTP Packet Connection Attack**
   - **Description**: This attack sends multiple HTTP requests with random data at a high speed to a target server.
   - **Required Input**: Target IP, port, speed per run (default 10), and the number of threads (default 4).

### 4. **SYN Flood Attack**
   - **Description**: This attack sends a flood of TCP/SYN packets, causing the target machine to allocate resources for each half-open connection, leading to denial of service.
   - **Required Input**: Target IP and port.

### 5. **ICMP Flood Attack**
   - **Description**: This attack floods the target system with ICMP Echo Request packets, also known as ping floods, to exhaust its resources.
   - **Required Input**: Target IP and the number of packets to send (default 100).

## Important Notes

- **Legal Notice**: Always ensure you have explicit permission to test the target system. Unauthorized DoS attacks are illegal and could lead to severe consequences, including legal action.
  
- **Permissions**: Some attacks (e.g., SYN flood and ICMP flood) may require administrative privileges to execute due to the use of raw sockets.

- **Ethical Use**: Use this script for learning purposes in a controlled environment (e.g., penetration testing labs, authorized vulnerability testing) only.

- **System Requirements**: The script has been tested on Linux and macOS. If running on Windows, you may need to adjust socket permissions or run the script as an administrator.

## Contributing

If you want to contribute to the project or add new attack methods, feel free to fork the repository and submit a pull request. Contributions are welcome.

## License

This script is licensed under the MIT License.

---

By running this script, you acknowledge that you are responsible for your actions and will not use this tool for malicious purposes.
