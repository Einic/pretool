# pretool

pretool is a versatile command-line tool designed to monitor services on amd64 and arm64 architectures in two network modes: host and bridge.

## Installation

To use pretool, download the appropriate binary for your architecture:

- pretool_amd64
- pretool_arm64

## Usage
### Monitoring Non-System Processes

To retrieve information about non-system processes (PID greater than 1024 and without square brackets in their name), use the -c flag:

```
./pretool_amd64 -c
```

### Specify Target Type and Port

To monitor services in a specific network mode (host or bridge) and customize the port number:

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

## Options

```
-c, --check  Get information on non-system processes.
-t, --type   Specify the network mode (host or bridge).
-p, --port   Specify the port number (default is 8000).
-s, --ssl    Enable SSL/TLS for the server.
-d, --domain Specify domain for tcpdump filter.
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

## Images
![Image text](https://mirrors.infvie.org/image/pretool/20240717211427.png)
![Image text](https://mirrors.infvie.org/image/pretool/20240717211532.png)
![Image text](https://mirrors.infvie.org/image/pretool/20240717211902.png)
![Image text](https://mirrors.infvie.org/image/pretool/20240717213057.png)
![Image text](https://mirrors.infvie.org/image/pretool/20240717213356.png)
![Image text](https://mirrors.infvie.org/image/pretool/20240717213735.png)
![Image text](https://mirrors.infvie.org/image/pretool/20240717214128.png)