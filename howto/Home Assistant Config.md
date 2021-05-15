## SSH

Go to Supervisor > Terminal & SSH
Configuration tab

Then

```
authorized_keys:
  - >-
    ssh-rsa
    <YOUR_KEY_HERE>
apks: []
password: ''
server:
  tcp_forwarding: false
```

Also don't forget to add the port forwarding (it seems the SSH service is a Docker container?)

For example, fill in 2222 in the Host field

For the ease of use, I also have a local ssh config file

```
Host hass
     HostName <IP ADDRESS>
     User root
     port 2222
```
