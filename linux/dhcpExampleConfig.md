01
ddns-update-style interim;                                   # Required for dhcp 3.0+ / Red Hat 8.0+
02
ignore client-updates;
03
 
04
subnet 192.168.1.0 netmask 255.255.255.0 {
05
 
06
        range 192.168.1.128 192.168.1.254;                   # Range of IP addresses to be issued to DHCP clients
07
           option subnet-mask              255.255.255.0;    # Default subnet mask to be used by DHCP clients
08
           option broadcast-address        192.168.1.255;    # Default broadcastaddress to be used by DHCP clients
09
           option routers                  192.168.1.1;      # Default gateway to be used by DHCP clients
10
           option domain-name              "your-domain.org";
11
           option domain-name-servers      40.175.42.254, 40.175.42.253;           # Default DNS to be used by DHCP clients
12
           option netbios-name-servers     192.168.1.100;    # Specify a WINS server for MS/Windows clients.
13
                                                             # (Optional. Specify if used on your network)
14
 
15
#         DHCP requests are not forwarded. Applies when there is more than one ethernet device and forwarding is configured.
16
#       option ipforwarding off;
17
 
18
        default-lease-time 21600;                            # Amount of time in seconds that a client may keep the IP address
19
        max-lease-time 43200;
20
 
21
        option time-offset              -18000;              # Eastern Standard Time
22
#       option ntp-servers              192.168.1.1;         # Default NTP server to be used by DHCP clients
23
#       option netbios-name-servers     192.168.1.1;
24
# --- Selects point-to-point node (default is hybrid). Don't change this unless you understand Netbios very well
25
#       option netbios-node-type 2;
26
 
27
        # We want the nameserver "ns2" to appear at a fixed address.
28
        # Name server with this specified MAC address will recieve this IP.
29
 
30
        host ns2 {
31
                next-server ns2.your-domain.com;
32
                hardware ethernet 00:02:c3:d0:e5:83;
33
                fixed-address 40.175.42.254;
34
        }
35
 
36
        # Laser printer obtains IP address via DHCP. This assures that the
37
        # printer with this MAC address will get this IP address every time.
38
 
39
        host laser-printer-lex1 {
40
                hardware ethernet 08:00:2b:4c:a3:82;
41
                fixed-address 192.168.1.120;
42
        }
43
}
