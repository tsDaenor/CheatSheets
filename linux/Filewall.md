##Exploring the Defaults

We can see which zone is currently selected as the default by typing:
```
firewall-cmd --get-default-zone
```
We can verify our active zones that by typing:
```
firewall-cmd --get-active-zones
```
Example output
```
public
  interfaces: eth0 eth1
```

Here, in this example we see the interfaces controlled by the firewall and in wich zone they are situated.

We can check the configuration by typing:
```
firewall-cmd --list-all
```
Example output
```
public (default, active)
  interfaces: eth0 eth1
  sources: 
  services: dhcpv6-client ssh
  ports: 
  masquerade: no
  forward-ports: 
  icmp-blocks: 
  rich rules:
```
With this command we can see more information about again the interfaces but also what ports and services.

##Setting Rules for Applications

###Adding a Service to Zones

The easiest method is to add the services or ports you need to the zones you are using. Again, you can get a list of the available Services with the ´--get-services´ option:
```
firewall-cmd --get-services
```
You can get more details about each of these services by looking at their associated .xml file within the /usr/lib/firewalld/services directory.

You can enable a service for a zone using the ´--add-service= parameter´. The operation will target the default zone or whatever zone Is specified by the ´--zone=´ parameter. By default, this will only adjust the current firewall session. You can adjust the permanent Firewall configuration by including the ´--permanent´ flag.

Ef we want to add a service to the firewall we can do so with the following command:
```
sudo firewall-cmd --zone=public --add-service=http
```
The ´--zone=´ is not required when adding to the default zone, if adding to a different zone change ´default´ into the desired zone.
Adding a different service to the firewall is done by swapping ´http´ with the desired service.
To check if it was added you can use the following command, again changing out the ´public´with the desired zone.

```
firewall-cmd --zone=public --list-services
```

Example output
```
http ssh
```

The previous commands however will only add the services untill the next reboot of firewall to add a service permanently just add the ´--permanent´ parameter:
```
sudo firewall-cmd --zone=public --permanent --add-service=http
```
You can verify that this was successful by adding the --permanent flag to the --list-services operation. You need to use sudo for any --permanent operations:
```
sudo firewall-cmd --zone=public --permanent --list-services
```
Example output
```
http ssh
```
