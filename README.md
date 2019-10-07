# RaspberryPi
Important notes on Pi usage

-------------------------------------------------
Notes for Status IP on Pi by /etc/dhcpcd.conf
-------------------------------------------------
Hi.

Since Raspbian Jessie setting a static IP on your pi has remained the same for both stretch and buster.

you just need to edit the file dhcpcd.conf with the command
Code: Select all

sudo nano /etc/dhcpcd.conf
in there you will find an example for setting a static IP, here is a copy from one of my pis
Code: Select all
----------------------------------
# A sample configuration for dhcpcd.
# See dhcpcd.conf(5) for details.

# Allow users of this group to interact with dhcpcd via the control socket.
#controlgroup wheel

# Inform the DHCP server of our hostname for DDNS.
hostname

# Use the hardware address of the interface for the Client ID.
clientid
# or
# Use the same DUID + IAID as set in DHCPv6 for DHCPv4 ClientID as per RFC4361.
# Some non-RFC compliant DHCP servers do not reply with this set.
# In this case, comment out duid and enable clientid above.
#duid

# Persist interface configuration when dhcpcd exits.
persistent

# Rapid commit support.
# Safe to enable by default because it requires the equivalent option set
# on the server to actually work.
option rapid_commit

# A list of options to request from the DHCP server.
option domain_name_servers, domain_name, domain_search, host_name
option classless_static_routes
# Respect the network MTU. This is applied to DHCP routes.
option interface_mtu

# Most distributions have NTP support.
#option ntp_servers

# A ServerID is required by RFC2131.
require dhcp_server_identifier

# Generate SLAAC address using the Hardware Address of the interface
#slaac hwaddr
# OR generate Stable Private IPv6 Addresses based from the DUID
slaac private

# static IP configuration:
interface eth0
static ip_address=192.168.1.14/24
#static ip6_address=fd51:42f8:caae:d92e::ff/64
static routers=192.168.1.1
static domain_name_servers=192.168.1.251 

# It is possible to fall back to a static IP if DHCP fails:
# define static profile
#profile static_eth0
#static ip_address=192.168.1.23/24
#static routers=192.168.1.1
#static domain_name_servers=192.168.1.1

# fallback to static profile on eth0
#interface eth0
#fallback static_eth0
which has a static IP set.
----------------------------------------
You do need to understand your network addressing and know what your routers IP and DNS server IP's as well, before you can set a static IP.
Your static Ip should also be out side of the address range that your DHCP server in your can assign or you will end up with address conflicts.

The safer and often simpler option is to use reserved IP addressing in your router if it supports it.
-------------------------------------------------
