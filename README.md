# 4.Execution_of_NetworkCommands
## AIM :Use of Network commands in Real Time environment
## Software : Command Prompt And Network Protocol Analyzer
## Procedure: To do this EXPERIMENT- follows these steps:
<BR>
In this EXPERIMENT- students have to understand basic networking commands e.g cpdump, netstat, ifconfig, nslookup ,traceroute and also Capture ping and traceroute PDUs using a network protocol analyzer 
<BR>
All commands related to Network configuration which includes how to switch to privilege mode
<BR>
and normal mode and how to configure router interface and how to save this configuration to
<BR>
flash memory or permanent memory.
<BR>
This commands includes
<BR>
• Configuring the Router commands
<BR>
• General Commands to configure network
<BR>
• Privileged Mode commands of a router 
<BR>
• Router Processes & Statistics
<BR>
• IP Commands
<BR>
• Other IP Commands e.g. show ip route etc.
<BR>
##PROGRAM##
server.py
```import socket
import os

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

host = "127.0.0.1"
port = 8000

server.bind((host, port))
server.listen(5)

print("Server waiting for connection...")

conn, addr = server.accept()
print("Connected to:", addr)

while True:
    data = conn.recv(1024).decode()

    if not data:
        break

    print("Command received:", data)

    result = os.popen(data).read()

    if result == "":
        result = "Command executed but no output"

    conn.send(result.encode())

conn.close()
server.close()
```
```
import socket

client = socket.socket()
client.connect(("127.0.0.1", 8000))

print("Connected to server")

while True:

    print("\nAvailable Commands:")
    print("1. ping google.com")
    print("2. tracert google.com")
    print("3. nslookup google.com")
    print("4. netstat")
    print("5. exit")

    cmd = input("Enter network command: ")

    if cmd.lower() == "exit":
        break

    client.send(cmd.encode())

    result = client.recv(4096).decode()

    print("\nOutput:\n")
    print(result)


client.close()
```

## Output
<img width="1050" height="518" alt="Screenshot 2026-05-25 083034" src="https://github.com/user-attachments/assets/7d814bc3-7f51-487d-9e55-5538fe7d6045" />
<img width="1030" height="560" alt="Screenshot 2026-05-25 083045" src="https://github.com/user-attachments/assets/46425fa3-f14a-4a39-95aa-7e585b94c19f" />
<img width="1054" height="491" alt="Screenshot 2026-05-25 083056" src="https://github.com/user-attachments/assets/90de0858-dc2c-475e-8a5e-7315bb3f21c9" />
<img width="1028" height="828" alt="Screenshot 2026-05-25 083119" src="https://github.com/user-attachments/assets/6aec8abd-a8e5-4cce-a2fc-d4c14e786f42" />





## Result
Thus Execution of Network commands Performed 
