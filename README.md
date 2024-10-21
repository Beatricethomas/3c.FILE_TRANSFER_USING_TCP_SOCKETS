# 3c.CREATION FOR FILE TRANSFER USING TCP SOCKETS
## AIM
To write a python program for creating File Transfer using TCP Sockets Links
## ALGORITHM:
1. Import the necessary python modules.
2. Create a socket connection using socket module.
3. Send the message to write into the file to the client file.
4. Open the file and then send it to the client in byte format.
5. In the client side receive the file from server and then write the content into it.
## PROGRAM
server.py 
```
import socket

def send_file(filename, client_socket):
    with open(filename, 'rb') as file:
        for data in file:
            client_socket.sendall(data)

def start_server():
    server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    server_socket.bind(('127.0.0.1', 5555))
    server_socket.listen(5)
    print("Server started, listening on port 5555")

    while True:
        client_socket, addr = server_socket.accept()
        print(f"Accepted connection from {addr}")

        filename = input("Enter filename to send: ")
        try:
            send_file(filename, client_socket)
            print(f"File '{filename}' sent successfully")
        except FileNotFoundError:
            print(f"File '{filename}' not found")

        client_socket.close()

start_server()

```
client.py
```
import socket

def receive_file(filename, server_socket):
    with open(filename, 'wb') as file:
        while True:
            data = server_socket.recv(1024)
            if not data:
                break
            file.write(data)

def start_client():
    client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    client_socket.connect(('127.0.0.1', 5555))

    filename = input("Enter filename to save: ")
    client_socket.sendall(filename.encode())

    receive_file(filename, client_socket)
    print(f"File '{filename}' received successfully")

    client_socket.close()

start_client()

```
## OUTPUT
![Screenshot 2024-10-21 094751](https://github.com/user-attachments/assets/a10fa579-9fef-49f3-9970-e441c52a9023)

![Screenshot 2024-10-21 094802](https://github.com/user-attachments/assets/25a9b240-ceec-4f45-b207-130e8da539c7)


## RESULT
Thus, the python program for creating File Transfer using TCP Sockets Links was 
successfully created and executed.
