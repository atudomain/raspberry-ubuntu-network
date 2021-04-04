# raspberry-ubuntu-network
Automatic config of wifi and static ips for fresh ubuntu 20.04 server raspberry pi device.

# initial SSH connection
Having official preconfigured ubuntu 20.04 server image on your raspberry,
plug in ethernet cable to your pc and to the device.

Run using your own interface:
```bash
# This command uses enp4s0 ethernet interface
ping6 -I enp4s0 ff02::1
```
You will see responses from the device with its ipv6 address.

Remember to append interface (ie. %enp4s0) when connecting to SSH
using ipv6 address (should already be appended in ping6 output).

Use default credentials to log in and set new password when asked.

# configuring wifi and static ips

Copy you SSH key to the device:
```bash
ssh-copy-id username@ipv6address%interface
```

Copy variables-template.yaml to variables.yaml:
```bash
cp variables-template.yaml variables.yaml
```
Fill variables.yaml file with values or
define the variables in environment (file still needs to be copied).

Run the playbook using your values (remember to keep that comma):
```bash
ansible-playbook -i 'username@ipv6address%interface,' network.yaml
```

The device should now be reachable via:
 - local network using wifi
 - internal network using ethernet and vlan VLAN_ID
 - direct connection using ethernet and DHCP
