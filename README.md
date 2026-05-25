# 2c.SIMULATING ARP /RARP PROTOCOLS

## Name: KAILASH PRABHU S
## Register No: 212224240068
## AIM
To write a python program for simulating ARP protocols using TCP.
## ALGORITHM:ARP Server
Objective: To receive an IP address from the client and send the corresponding MAC address.

Algorithm Steps:

1. Start the program.

2. Create a TCP socket.

3. Bind the socket to the local host and port number 8000.

4. Put the server socket into listening mode.

5. Display a message indicating the server is ready.

6. Accept a connection request from the client.

7. Initialize a table containing IP address – MAC address pairs.

8. Repeat the following steps:

    •Receive the IP address from the client.

    •Search the received IP address in the ARP table.

    •If the IP address is found, get the corresponding MAC address.

    •If the IP address is not found, set the response as "Not Found".

    •Send the MAC address (or "Not Found") back to the client.

9. Continue until the connection is terminated.

10. Stop the program.

## Algorithm: ARP Client
Objective: To send an IP address to the server and receive the corresponding MAC address.

Algorithm Steps:

1. Start the program.

2. Create a TCP socket.

3. Connect the socket to the server using localhost and port number 8000.

4. Repeat the following steps:

    •Read the logical address (IP address) from the user.

    •Send the IP address to the server.

    •Receive the MAC address from the server.

    •Display the received MAC address.

5. Continue until the user terminates the program.

6. Stop the program.

## Algorithm: RARP Server
Objective: To receive a MAC address from the client and return the corresponding IP address.

Algorithm Steps:

1. Start the program.

2. Create a TCP socket.

3. Bind the socket to localhost and port number 8001.

4. Put the socket into listening mode.

5. Display a message indicating that the RARP server is ready.

6. Accept a connection request from the client.

7. Initialize a RARP table containing MAC address – IP address pairs.

8. Repeat the following steps:

    •Receive the MAC address from the client.

    •Search the MAC address in the RARP table.

    •If the MAC address is found, retrieve the corresponding IP address.

    •If the MAC address is not found, set the response as "Not Found".

    •Send the IP address (or "Not Found") back to the client.

9. Continue until the connection is terminated.

10. Stop the program.

## Algorithm: RARP Client
Objective: To send a MAC address to the server and receive the corresponding IP address.

Algorithm Steps:

1. Start the program.

2. Create a TCP socket.

3. Connect the socket to the server using localhost and port number 8001.

4. Repeat the following steps:

    •Read the physical address (MAC address) from the user.

    •Send the MAC address to the server.

    •Receive the IP address from the server.

    •Display the received IP address.

5. Continue until the user terminates the program.

6. Stop the program.

## PROGRAM - ARP
client_arp.py
~~~
import socket

s = socket.socket()

s.connect(('127.0.0.1', 8000))

while True:
    ip = input("Enter IP Address: ")

    s.send(ip.encode())

    print("MAC Address:", s.recv(1024).decode())
~~~
server_arp.py
~~~
import socket

server = socket.socket()

server.bind(('127.0.0.1', 8000))

server.listen(1)

print("Server started... Waiting for connection")

conn, addr = server.accept()

print("Connected to:", addr)

while True:
    data = conn.recv(1024).decode()

    if data == "192.168.1.1":
        mac = "AA:BB:CC:DD:EE:01"
    else:
        mac = "MAC Not Found"

    conn.send(mac.encode())
~~~

## OUPUT - ARP

<img width="626" height="365" alt="Screenshot 2026-05-25 111232" src="https://github.com/user-attachments/assets/8c3788dd-a58f-4072-88d0-59af663f648e" />



## PROGRAM - RARP
client_rarp.py
~~~
import socket

s = socket.socket()

s.connect(('127.0.0.1', 8000))

while True:
    mac = input("Enter Physical Address (MAC): ")

    s.send(mac.encode())

    print("Logical Address (IP):", s.recv(1024).decode())
~~~

server_rarp.py

~~~
import socket

server = socket.socket()

server.bind(('127.0.0.1', 8000))

server.listen(1)

print("RARP Server Started...")

conn, addr = server.accept()

print("Connected to:", addr)

# RARP Table
rarp_table = {
    "AA:BB:CC:DD:EE:01": "192.168.1.1",
    "AA:BB:CC:DD:EE:02": "192.168.1.2",
    "AA:BB:CC:DD:EE:03": "192.168.1.3"
}

while True:
    mac = conn.recv(1024).decode()

    ip = rarp_table.get(mac, "IP Address Not Found")

    conn.send(ip.encode())
~~~
## OUPUT -RARP

<img width="655" height="62" alt="image" src="https://github.com/user-attachments/assets/5e54ad9a-9fe9-4e8b-a0d6-108328bd44bc" />


## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
