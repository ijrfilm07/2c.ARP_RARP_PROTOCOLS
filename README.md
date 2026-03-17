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
##  ARPsever.py
```
import socket
s = socket.socket()
s.bind(('127.0.0.1',12345))
s.listen(5)
print("Server is listening...")
c, addr = s.accept()
print(f"Connection established with {addr}")
address = {
    "192.168.12.7": "6A:08:AA:C2",
    "10.12.6.70": "8A:BC:E3:FA"
}
while True:
    ip = c.recv(1024).decode()
if not ip:  
        break
    try:
        mac = address[ip]
        print(f"IP: {ip} and MAC: {mac}")
        c.send(mac.encode())  
    except KeyError:
        print(f"IP: {ip} not found in ARP table.")
        c.send("Not Found".encode())
c.close()
s.close()
```

## ARPserver.py
```
import socket
c = socket.socket()
c.connect(('127.0.0.1',12345))
while True:
    ip = input("Enter IP address to find MAC (or type 'exit' to quit): ")
    if ip.lower()=="exit" or ip.lower()=="quit":  
        break
    c.send(ip.encode())
    mac = c.recv(1024).decode()
    print(f"MAC Address for {ip}: {mac}")
c.close()
```
## OUPUT - ARP
<img width="1041" height="307" alt="image" src="https://github.com/user-attachments/assets/c9a75fb5-c5e3-4ba8-bd04-c502dc9fdee9" />

## PROGRAM - RARP
## RARPserver.py
```
import socket
s = socket.socket()
s.bind(('127.0.0.1',12345))
s.listen(5)
print("Server is listening for RARP requests...")
c, addr = s.accept()
print(f"Connection established with {addr}")
rarp_table = {
    "6A:08:AA:C2": "192.168.12.7",
    "8A:BC:E3:FA": "10.12.6.70"
}
while True:
    mac = c.recv(1024).decode()
    if not mac:
  break
    try:
        ip = rarp_table[mac]  
        print(f"MAC: {mac} = IP: {ip}")
        c.send(ip.encode())  
    except KeyError:
        print(f"MAC: {mac} not found in RARP table.")
        c.send("Not Found".encode())
c.close()
s.close()
```
## RARPclient.py
```
import socket
c = socket.socket()
c.connect(('127.0.0.1',12345))
while True:
    mac = input("Enter MAC address to find IP (or type 'exit' to quit): ")
    if mac.lower()=="exit" or mac.lower()=="quit":  
        break
    c.send(mac.encode())
    ip = c.recv(1024).decode()
    print(f"IP Address for {mac}: {ip}")
c.close()
```
## OUPUT -RARP
<img width="1042" height="337" alt="image" src="https://github.com/user-attachments/assets/7af499a4-e5d7-4cdd-8d21-9689207660c0" />

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
