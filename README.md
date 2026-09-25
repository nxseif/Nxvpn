# NxVPN

Small Bash tool for managing a local WireGuard VPN lab on Linux.

NxVPN creates and manages a WireGuard client inside a Linux network namespace and connects it to a local WireGuard server through a virtual Ethernet pair.

## What it does

NxVPN can:

* create the VPN client namespace
* create the virtual Ethernet connection
* create the WireGuard interface
* configure the VPN IP
* load the WireGuard configuration
* add the VPN route
* show the current status
* stop and clean up the lab

## Commands

```bash
./nxvpn on
```

Start the VPN lab.

```bash
./nxvpn off
```

Stop the VPN and clean up the namespace and interfaces.

```bash
./nxvpn status
```

Show the current VPN status and WireGuard information.

```bash
./nxvpn menu
```

Open an interactive menu.

```bash
./nxvpn help
```

Show the available commands.

## How it works

The project uses a Linux network namespace as the VPN client.

```text
Host
│
├── veth-host
│   172.27.100.1
│
│   virtual Ethernet
│
└── vpn-client namespace
    │
    ├── nxseif-host
    │   172.27.100.2
    │
    └── wg0
        172.27.50.2
```

The namespace acts as the WireGuard client while the host provides the virtual network connection.

## Requirements

* Linux
* Bash
* WireGuard tools
* `iproute2`
* `sudo`

The project is currently designed for Linux and has been tested on Fedora.

## Installation

Clone the repository:

```bash
git clone https://github.com/nxseif/Nxvpn.git
cd Nxvpn
```

Make the script executable:

```bash
chmod +x nxvpn
```

Before using NxVPN, you need to create your own WireGuard keys and configuration files.

Private keys and local WireGuard configurations are intentionally not included in this repository.

## Example

Start the lab:

```bash
./nxvpn on
```

Check the status:

```bash
./nxvpn status
```

Test the VPN connection:

```bash
sudo ip netns exec vpn-client ping -c 3 172.27.50.1
```

Stop everything:

```bash
./nxvpn off
```

## Project status

NxVPN is a personal learning project.


More features and improvements will be added as I continue working on it 

## Security

**Do not commit private WireGuard keys to Git.**

Private keys and local configuration files are ignored with `.gitignore`.

## Author

Created by **nxseif**.

Personal project built while learning Linux networking, Bash, and DevOps
