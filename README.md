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
### Server Program
```
import socket

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(1)

print("Waiting for connection ... ")
conn, addr = s.accept()
print("Connected to", addr)

while True:
    data = conn.recv(1024).decode()

    if not data:
        break

    print("Frames received:", data)

    ack = "ACK for " + data
    conn.send(ack.encode())

conn.close()
```
### Client Program
```
import socket 

s = socket.socket() 
s.connect(('localhost', 8000))

n = int(input("Enter number of frames: ")) 
w = int(input("Enter window size: ")) 

frames = list(range(1, n+1)) 
i = 0 
while i <n:
    send_frames = frames[i:i+w]

    msg =" ".join(map(str, send_frames))
    print("Sending frames:", msg)

    s.send(msg.encode())

    ack = s.recv(1024).decode()
    print("Received:", ack)

    i += w

s.close()
```
## OUPUT
### Server Output
<img width="1920" height="1020" alt="Screenshot 2026-05-11 091541" src="https://github.com/user-attachments/assets/865215f8-4f38-440c-8e49-438de8ca03d8" />

### Client Output
<img width="1920" height="1020" alt="Screenshot 2026-05-11 091557" src="https://github.com/user-attachments/assets/496c24b2-e507-4797-b0f4-1d5500d2357e" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
