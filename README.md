# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
## Server
```
import socket

s = socket.socket()
s.bind(('localhost', 9999))
s.listen(1)
print("Server ready...")

c, _ = s.accept()
while True:
    data = c.recv(1024).decode()
    if not data:
        break

    print("Received:", data)
    c.send(f"ACK: {data}".encode())

c.close()
s.close()
```

## Client
```
import socket

c = socket.socket()
c.connect(('localhost', 9999))

n = int(input("No. of frames: "))
w = int(input("Window size: "))
frames = list(range(n))

i = 0
while i < n:
    send = frames[i:i+w]
    print("Sending:", send)
    c.send(str(send).encode())

    ack = c.recv(1024).decode()
    print("ACK:", ack)
    i += w

c.close() 
```
## OUPUT
## Server

<img width="783" height="266" alt="image" src="https://github.com/user-attachments/assets/10077438-c39c-4e7f-8921-bf4dfce10944" />

## Client

<img width="792" height="262" alt="image" src="https://github.com/user-attachments/assets/510401d9-319e-4f18-b3e9-e2f92a7a7a77" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
