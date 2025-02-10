# pretool
Supports service listen in both host and bridge network modes, and includes an automatic network capture utility specifically designed for DNS traffic ,and extends go nmap to implement an efficient port scanner, supporting the following automatic scanning methods: UDP, TCP complete connection, ICMP, FIN, ACK, SYN half-open, XMAS, NULL, IP protocol layer and feature code scanning.

* [x] micro container network listen
* [x] micro dns packet capture
* [x] micro nmap port detection


## Installation

To use pretool, download the appropriate binary for your architecture:

- pretool_amd64
- pretool_arm64

## Usage
### Scanning Non-System Processes

Specifically designed for safe process scanning, that is, to retrieve information about non-system processes (PID greater than 1024 and without square brackets in the name), use the -c flag:

```
./pretool_amd64 -c

```

### Specify Target Type and Port

To listen services in a specific network mode (host or bridge) and customize the port number:

#### SSL/TLS

SSL/TLS can be enabled for the server only in host network mode. The certificate files must have .crt and .key extensions (e.g., domain.crt and domain.key).

```
./pretool_amd64 -t host -p 443 -s

```

#### For amd64 architecture:

Specify host mode with the default port 8000:

```
./pretool_amd64 -t host

```

Or, specify a custom port number (e.g., 9000):

```
./pretool_amd64 -t host -p 9000

```

#### For arm64 architecture:

Specify bridge mode with the default port 8000:

```
./pretool_arm64 -t bridge

```

Or, specify a custom port number (e.g., 9000):

```
./pretool_arm64 -t bridge -p 9000

```

#### Specify dns to capture packets

To capture DNS packets, specify the domain name:

```
./pretool_arm64 -d www.infvie.com

```

#### Nmap written entirely in go

Extends go nmap to implement an efficient port scanner, supporting the following automatic scanning methods: UDP, TCP full connection, ICMP, FIN, ACK, SYN half-open, XMAS, NULL, IP protocol layer and feature code scanning.

```
# pretool_amd64 -n <target ip/domain> <21-25,80> <tcp,udp> <threads> <ai> (default threads is 10000)
./pretool_amd64 -n 192.168.200.129,192.168.5.87 21-25,80 tcp,udp 
./pretool_amd64 -n 192.168.200.129-130 21-25,80 tcp,udp
```

#### High-Risk Port AI Analysis (DeepSeek Agent)
pretool integrates AI-driven high-risk port analysis using the DeepSeek AI agent. When scanning open ports, it automatically evaluates their security risks and provides concise mitigation recommendations.
##### AI config Env Init:

```
./pretool_amd64 -k http://183.1x.2x.1xx:11434/api/generate deepseek-r1:8b ll7
[2025-02-07 09:17:47] INFO ai/ai_crypto.go:77 Ai agent related config encryption initialization successfully, Check .env file for encrypted values.

cat .env 
AI_AGENT_SALT=qLWZaXmSNOmwwJkuKl_2cw
AI_AGENT_KEY=D66UUMp3lPuiqZ20FiJ5hmxg4OPqRA8z88TaIeZEUw
AI_AGENT_URL=aHR0cDovLzE4My4xeC4yeC4xeHg6MTE0MzQvYXBpL2dlbmVyYXRl
AI_AGENT_MODEL=ZGVlcHNlZWstcjE6OGI
AI_AGENT_STREAM=false
AI_AGENT_TIMEOUT=30

```
##### AI Response Format: 

```
./pretool_amd64 -n 192.168.5.58 80,22,3306 tcp 10 ai
[1] Scanning ports on 192.168.5.58 using tcp protocol with 10 threads...
GoNmap scan report for 192.168.5.58
PORT PROTO SERVICE STATE
3306 tcp   mysql   open  
22   tcp   sshd    open  
80   tcp   unknown closed

Summary: 
	tcp-Open: 2
	tcp-Closed: 1

Found high-risk ports! Requesting AI analysis...
AI Recommendation:
1. **Port 22 - Risk: Unsecured SSH access can lead to unauthorized entry. Solution: Change the default SSH port to a less common number and implement two-factor authentication for added security.**

2. **Port 3306 - Risk: Unprotected MySQL services can result in data breaches or SQL injection attacks. Solution: Secure MySQL with strong passwords, regular updates, and consider a VPN for remote access to safeguard data integrity.**

GoNmap done: 1 IP address (1 host up) scanned in 0.02 seconds

```

## Options

```
-c, --check  Get information on non-system processes.
-t, --type   Specify the network mode (host or bridge).
-p, --port   Specify the port number (default is 8000).
-s, --ssl    Enable SSL/TLS for the server.
-d, --domain Specify domain for tcpdump filter.
-n, --nmap   Enable an efficient port scanner, [-n <target ip/domain> <21-25,80> <tcp,udp> <threads> <ai>].

```

## Other Options

```
-v, --version  Print the version number and MD5 hash of the tool.
-h, --help     Show the help message and usage information.

```

## Auxiliary commands

```
ip link delete veth-host;
ip link set br0 down;
ip link delete br0;
ip netns delete container;
umount /var/run/netns;
rm -rf /var/run/netns;

ip addr show br0;
ip addr show veth-host;
ip netns list;
ip netns exec container ip a show;
ip netns exec container ss -tuln;

```

## Notes
>- **System Processes**: By default, system processes with PIDs less than 1024 and those containing square brackets in their names (e.g., [watchdog]) are filtered out.
>- **Customization**: You can customize the tool's behavior by specifying the target type (host or bridge) and port number according to your requirements.
>- **Go Nmap**: To implement an efficient port scanner, supporting the following automatic scanning methods: UDP, TCP complete connection, ICMP, FIN, ACK, SYN half-open, XMAS, NULL, IP protocol layer and feature code scanning.

## Images
![Image text](https://mirrors.infvie.org/image/pretool/20240717211427.png)
![Image text](https://mirrors.infvie.org/image/pretool/20240717211532.png)
![Image text](https://mirrors.infvie.org/image/pretool/20240717211902.png)
![Image text](https://mirrors.infvie.org/image/pretool/20240717213057.png)
![Image text](https://mirrors.infvie.org/image/pretool/20240717213356.png)
![Image text](https://mirrors.infvie.org/image/pretool/20240717213735.png)
![Image text](https://mirrors.infvie.org/image/pretool/20240717214128.png)
![Image text](https://mirrors.infvie.org/image/pretool/20240720191150.png)