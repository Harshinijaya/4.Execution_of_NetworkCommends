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
```
1.server code
import socket
import subprocess

# Create socket
s = socket.socket()

# Bind IP and Port
s.bind(('localhost', 8000))

# Listen for client
s.listen(1)

print("Server listening on port 8000...")

# Accept connection
c, addr = s.accept()

print("Connected:", addr)

while True:

    # Receive command
    command = c.recv(1024).decode().strip()

    # Exit condition
    if not command or command.lower() == 'exit':
        print("Client disconnected.")
        break

    try:

        # Execute command
        completed = subprocess.run(
            command,
            capture_output=True,
            text=True,
            shell=True
        )

        # Combine output and error
        output = completed.stdout + completed.stderr

        # If no output
        if not output:
            output = "Command executed successfully."

    except Exception as e:

        output = f"Command failed: {e}"

    # Send result to client
    c.sendall(output.encode())

Close connection
c.close()
s.close()
```
2.client code
import socket

# Create socket
s = socket.socket()

try:

    # Connect to server
    s.connect(('localhost', 8000))

    print("Connected to server.")
    print("Type commands or 'exit' to quit.\n")

    while True:

        # Get command
        cmd = input("Enter command: ").strip()

        if not cmd:
            continue

        # Send command
        s.send(cmd.encode())

        # Exit
        if cmd.lower() == 'exit':
            print("Closing connection...")
            break

        # Receive result
        data = b""

        while True:

            part = s.recv(4096)

            data += part

            if len(part) < 4096:
                break

        # Display output
        print("\n----- RESULT -----")
        print(data.decode())
        print("------------------\n")

except ConnectionRefusedError:

    print("Server is not running!")

finally:

    s.close()
```


## Output##
<img width="1050" height="518" alt="Screenshot 2026-05-25 083034" src="https://github.com/user-attachments/assets/158dd37b-2a6f-4ded-8430-cb08729024b6" />
<img width="1030" height="560" alt="Screenshot 2026-05-25 083045" src="https://github.com/user-attachments/assets/cbb0fdfe-c4ef-4017-9177-5c446085d181" />
<img width="1054" height="491" alt="Screenshot 2026-05-25 083056" src="https://github.com/user-attachments/assets/41ef139c-692f-492b-97d2-2b6164f2e148" />
<img width="1028" height="828" alt="Screenshot 2026-05-25 083119" src="https://github.com/user-attachments/assets/35903caf-5b63-4fea-ad33-9ddcb287f74b" />





## Result
Thus Execution of Network commands Performed 
