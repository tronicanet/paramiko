<p align="center">
<img src="https://github.com/tronicanet/paramiko/blob/master/ssh-key.jpg"
     alt="Markdown Monster icon"
     style="float: left; margin-right: 60px;" />
</p>


# paramiko


ejemplo1

```python
from paramiko import client
 
class ssh:
    client = None
 
    def __init__(self, address, username, password):
        print("Connecting to server.")
        self.client = client.SSHClient()
        self.client.set_missing_host_key_policy(client.AutoAddPolicy())
        self.client.connect(address, username=username, password=password, look_for_keys=False)
 
    def sendCommand(self, command):
        if(self.client):
            stdin, stdout, stderr = self.client.exec_command(command)
            while not stdout.channel.exit_status_ready():
                # Print data when available
                if stdout.channel.recv_ready():
                    alldata = stdout.channel.recv(1024)
                    prevdata = b"1"
                    while prevdata:
                        prevdata = stdout.channel.recv(1024)
                        alldata += prevdata
 
                    print(str(alldata, "utf8"))
        else:
            print("Connection not opened.")
 
connection = ssh("<SERVER_ADDRESS>", "<SERVER_USERNAME>", "<SERVER_PASSWORD>")
connection.sendCommand("ls /")
```
