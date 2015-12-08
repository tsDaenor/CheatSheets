Exploring the Defaults

We can see which zone is currently selected as the default by typing:

firewall-cmd --get-default-zone
output
public
Since we haven't given firewalld any commands to deviate from the default zone, and none of our interfaces are configured to bind to another zone, that zone will also be the only "active" zone (the zone that is controlling the traffic for our interfaces). We can verify that by typing:

firewall-cmd --get-active-zones
output
public
  interfaces: eth0 eth1
Here, we can see that we have two network interfaces being controlled by the firewall (eth0 and eth1). They are both currently being managed according to the rules defined for the public zone.

How do we know what rules are associated with the public zone though? We can print out the default zone's configuration by typing:

firewall-cmd --list-all
output
public (default, active)
  interfaces: eth0 eth1
  sources: 
  services: dhcpv6-client ssh
  ports: 
  masquerade: no
  forward-ports: 
  icmp-blocks: 
  rich rules:
We can tell from the output that this zone is both the default and active and that the eth0 and eth1 interfaces are associated with this zone (we already knew all of this from our previous inquiries). However, we can also see that this zone allows for the normal operations associated with a DHCP client (for IP address assignment) and SSH (for remote administration).

Setting Rules for your Applications
The basic way of defining firewall exceptions for the services you wish to make available is easy. We'll run through the basic idea here.

Adding a Service to your Zones

The easiest method is to add the services or ports you need to the zones you are using. Again, you can get a list of the available services with the --get-services option:

firewall-cmd --get-services
output
RH-Satellite-6 amanda-client bacula bacula-client dhcp dhcpv6 dhcpv6-client dns ftp high-availability http https imaps ipp ipp-client ipsec kerberos kpasswd ldap ldaps libvirt libvirt-tls mdns mountd ms-wbt mysql nfs ntp openvpn pmcd pmproxy pmwebapi pmwebapis pop3s postgresql proxy-dhcp radius rpc-bind samba samba-client smtp ssh telnet tftp tftp-client transmission-client vnc-server wbem-https
Note
You can get more details about each of these services by looking at their associated .xml file within the /usr/lib/firewalld/services directory. For instance, the SSH service is defined like this:

/usr/lib/firewalld/services/ssh.xml
<?xml version="1.0" encoding="utf-8"?>
<service>
  <short>SSH</short>
  <description>Secure Shell (SSH) is a protocol for logging into and executing commands on remote machines. It provides secure encrypted communications. If you plan on accessing your machine remotely via SSH over a firewalled interface, enable this option. You need the openssh-server package installed for this option to be useful.</description>
  <port protocol="tcp" port="22"/>
</service>
You can enable a service for a zone using the --add-service= parameter. The operation will target the default zone or whatever zone is specified by the --zone= parameter. By default, this will only adjust the current firewall session. You can adjust the permanent firewall configuration by including the --permanent flag.

For instance, if we are running a web server serving conventional HTTP traffic, we can allow this traffic for interfaces in our "public" zone for this session by typing:

sudo firewall-cmd --zone=public --add-service=http
You can leave out the --zone= if you wish to modify the default zone. We can verify the operation was successful by using the --list-all or --list-services operations:

firewall-cmd --zone=public --list-services
output
dhcpv6-client http ssh
Once you have tested that everything is working as it should, you will probably want to modify the permanent firewall rules so that your service will still be available after a reboot. We can make our "public" zone change permanent by typing:

sudo firewall-cmd --zone=public --permanent --add-service=http
You can verify that this was successful by adding the --permanent flag to the --list-services operation. You need to use sudo for any --permanent operations:

sudo firewall-cmd --zone=public --permanent --list-services
output
dhcpv6-client http ssh
Your "public" zone will now allow HTTP web traffic on port 80. If your web server is configured to use SSL/TLS, you'll also want to add the https service. We can add that to the current session and the permanent rule-set by typing:

sudo firewall-cmd --zone=public --add-service=https
sudo firewall-cmd --zone=public --permanent --add-service=https