# Lab 04 | DHCP
We will finally be configuring DHCP to avoid manual assignment of IP addresses.
## Installing Services
We can use the following command to install the dhcp service:
  * sudo dnf install -y dhcp-server
## Configuring the DHCP Service
**Create a backup of the configuration file!**
```
sudo -i
cp /etc/dhcp/dhcpd.conf /etc/dhcp/dhcpd.comf.bak
vi /etc/dhcp/dhcpd.conf
```
  * This allows us to edit the conf file and not worry is anything goes wrong
### Config for DHCPd.conf
```
subnet 10.0.5.0 netmask 255.255.255.0 {
        options routers 10.0.5.2;
        option subnet-mask 255.255.255.0;
        option domain-name "james.local";
        option domain-name-servers 10.0.5.5;
        range 10.0.5.101 10.0.5.125;
}
```
Then save + quit using shift+ZZ  

### Starting the Service
```
systemctl start dhcpd
systemctl stop dhcpd
systemctl status dhcpd
systemctl enable dhcpd
```
  * This generally needs to happen whenever changes are made to the service
**We need to enable the service when first configured so it will restart on boot**

## Configuring the firewall to allows DHCP requests
`firewall-cmd --list-all`
  * This lists all of the firewall rules

`firewall-cmd --add-service=dhcp --permanent`
  * This will add the DHCP service to the firewall and make it permanent

`firewall-cmd --reload`
  * This reloads it to make sure our changes were taken

## Change Adapter Settings
Change the IPv4 adapter to obtain IP and DNS automatically.  
Open an elevated powershell and enter the following commands:
```
Set-NetIPInterface -InterfaceAlias "Ethernet" -Dhcp Enabled
Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ResetServerAddresses
Remove-NetRoute -InterfaceAlias "Ethernet" -DestinationPrefix 0.0.0.0/0 -Confirm:$false
ipconfig /release
ipconfig /renew
ipconfig /all
```
  * This manually sets the interface to use dhcp and then renew an IP from the server
## Changing default lease time
We are going to append the max-lease time to the config file from earlier. It will look like this:
```
subnet 10.0.5.0 netmask 255.255.255.0 {
        options routers 10.0.5.2;
        option subnet-mask 255.255.255.0;
        option domain-name "james.local";
        option domain-name-servers 10.0.5.5;
        range 10.0.5.101 10.0.5.125;
        default-lease-time 3600;
        max-lease-time 14400;
}
```
 * The lease time will be global if set outside the subnet block
 * max-lease-time is in seconds  
Use the following command to make sure there are no syntax errors:
`sudo dhcpd -t -cf /etc/dhcp/dhcpd.conf`  
Now restart the service.
