# autokvm

A script library for high speed deployment of virtual machines using cloud images.
Autokvm allows near pain free deployment of virtual machines on your network.
Machines can be configures with static IP or DHCP from bridge interface.
No setup or configuration should be required to get things working in your guests.
Autokvm leverages libvirt for automation of QEMU/KVM.

Only RHEL based VMs are supported at this time.

These scripts were developed and tested on CentOS 8 and Fedora 30 and should be compliant with all RHEL8+ distributions.

## Requirements
- RHEL8+ Linux
- VT-x or AMD-V virtualization enabled in your system BIOS
- All scripts must be run with root privileges

## Installation
1. Clone the repository
2. CD to the repositories base directory
3. Run _autokvm-install.sh_

## Usage
**Example files can be found in _/etc/autokvm.cfg.d/example_ following the install.**
- _network-config-sample.conf_ can be used in both _cloud-vm-deploy.sh_ and _network-bridge-add.sh_
- _vm-config-sample.conf_ can be used in _cloud-vm-deploy.sh_ to provide the VM configuration parameters

Run the various scripts with _-h_ flag as the first argument for the usage message.

## Networks
By default, the guest networking will be configured via DHCP from the network on the bridge interface.
If the _network-config_ parameter is supplied, the guest will be deployed with a static IP as specified in the _network-config_ file argument when running _cloud-vm-deploy.sh_. Valid parameters must be supplied as specified in the example network config file in order to be able to connect to the VM following the install.

### Bridge Interfaces
The Default bridge interface generated by libvirt is _virbr0_
This interface provides a NAT network for accessing hosts from the hypervisor.

For hosts to be accessible from your LAN you should create a bridge for your systems Ethernet connection by using the included _network-bridge-add.sh_ or other means. This will then be used in the BRIDGE_INTERFACE parameter of your vm-config file.

### Notes
- Debian 10 image is not currently supported, associated issues with cloud-init