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
```
# Close connection
c.close()
s.close()

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


## Output
<img width="1918" height="1023" alt="Screenshot 2026-05-22 182515" src="https://github.com/user-attachments/assets/563eb977-c484-498a-81f1-2f0d5bea4c65" />
<img width="1919" height="1079" alt="Screenshot 2026-05-22 182530" src="https://github.com/user-attachments/assets/c43281da-96ea-4459-978f-eb704c5c620c" />


## Result
Thus Execution of Network commands Performed 
