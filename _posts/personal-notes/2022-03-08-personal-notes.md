---
layout: post
title: "Personal Notes"
tags: [notes]
---
# IP Address
IP (Internet Protocol) address allows computers to send and receive data over the internet. 

IP address is a 4 set of numbers from 0 to 255. Range -> 0.0.0.0 to 255.255.255.255

# Types of IP address
Public (outside of network): A public IP address is about the whole network. Every connected device has the same public IP address. Is provided to your router by your ISP. 

Private (inside a network): A private IP address assigned to every device that connects to your home network.

Private IP Address Ranges:
```
10.0.0.0 to 10.255.255.255
172.16.0.0 to 172.31.255.255
192.168.0.0 to 192.168.255.255
```

Find Private IP Address:
```
$ ip addr
$ hostname -I
```

Static: A static IP address is manually created and never changes.

Dynamic: A dynamic IP address always keep changing automatically.

# Port
Port is where information is sent. Ports are software-based, each port is associated with a specific process or service.

There are 65,535 ports, for example 22 -> SSH

```json
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```


```python
print('hello world')
``` 


```
print('hello world')
```
