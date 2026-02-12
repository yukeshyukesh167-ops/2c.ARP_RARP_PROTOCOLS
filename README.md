# 2c.SIMULATING ARP /RARP PROTOCOLS
## AIM
To write a python program for simulating ARP protocols using TCP.
## ALGORITHM:
## Client:
1. Start the program
2. Using socket connection is established between client and server.
3. Get the IP address to be converted into MAC address.
4. Send this IP address to server.
5. Server returns the MAC address to client.
## Server:
1. Start the program
2. Accept the socket which is created by the client.
3. Server maintains the table in which IP and corresponding MAC addresses are
stored.
4. Read the IP address which is send by the client.
5. Map the IP address with its MAC address and return the MAC address to client.
P
## PROGRAM - ARP
Server:

#arp_server.py
import socket
#Create socket
s = socket.socket()
s.bind(('localhost', 9999))
s.listen(1)
print("ARP Server started...")
print("Waiting for client request...")
#ARP table (IP → MAC)
arp_table = {
    "192.168.1.1": "AA:BB:CC:DD:EE:01",
    "192.168.1.2": "AA:BB:CC:DD:EE:02",
    "192.168.1.3": "AA:BB:CC:DD:EE:03"
}
conn, addr = s.accept()
print("Connected to client:", addr)
ip = conn.recv(1024).decode()
print("Received IP Address:", ip)
mac = arp_table[ip]
conn.send(mac.encode())
conn.close()
s.close()
Client:

#arp_client.py
import socket
s = socket.socket()
s.connect(('localhost', 9999))
ip = input("Enter IP Address: ")
s.send(ip.encode())
mac = s.recv(1024).decode()
print("MAC Address:", mac)
s.close()
## OUPUT - ARP
server:
<img width="1492" height="796" alt="image" src="https://github.com/user-attachments/assets/7544e5c3-bb02-4fb4-a763-9ca9e1be48f4" />
client:
<img width="1477" height="791" alt="image" src="https://github.com/user-attachments/assets/6532fa95-bca1-49e0-93e9-3e82bc33fa8c" />


## PROGRAM - RARP
Server:

#rarp_server.py
import socket
# RARP Table (MAC : IP)
rarp_table = {
    "AA:BB:CC:DD:EE:01": "192.168.1.1",
    "AA:BB:CC:DD:EE:02": "192.168.1.2",
    "AA:BB:CC:DD:EE:03": "192.168.1.3"
}
server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.bind(("localhost", 6000))
server.listen(1)
print("RARP Server is waiting for connection...")
conn, addr = server.accept()
print("Connected with", addr)
mac = conn.recv(1024).decode()
print("Received MAC:", mac)
ip = rarp_table.get(mac, "MAC address not found in RARP table")
conn.send(ip.encode())
conn.close()
server.close()
Client:

#rarp_client.py
import socket
client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect(("localhost", 6000))
mac = input("Enter MAC address: ")
client.send(mac.encode())
ip = client.recv(1024).decode()
print("IP Address:", ip)
client.close()
## OUPUT -RARP
server:
<img width="1478" height="812" alt="image" src="https://github.com/user-attachments/assets/4223c1b1-0e94-4c5d-b892-869c84694573" />
client:
<img width="1479" height="793" alt="image" src="https://github.com/user-attachments/assets/c8c04623-fb67-404c-a30a-f71ed3069a00" />


## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
