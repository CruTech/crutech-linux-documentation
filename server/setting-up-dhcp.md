# Setting up DHCP

{% hint style="info" %}
DHCP stands for Dynamic host configuration protocol.
{% endhint %}

Open a new terminal window and type the following:

```text
sudo nautilus
```

Navigate to /etc/ltsp and open the dhcp.conf file and enter the following:

## dhcp.conf

```text
authoritative;

subnet 192.168.0.0 netmask 255.255.255.0 {
    range 192.168.0.20 192.168.0.250;
    option domain-name "crutech.cru";
    option domain-name-servers 192.168.0.1;
    option broadcast-address 192.168.0.255;
    option routers 192.168.0.1;
#    next-server 192.168.0.1;
#    get-lease-hostnames true;
    option subnet-mask 255.255.255.0;
    option root-path "/opt/ltsp/i386";
    if substring( option vendor-class-identifier, 0, 9 ) = "PXEClient" {
        filename "/ltsp/i386/pxelinux.0";
    } else {
        filename "/ltsp/i386/nbi.img";
    }
}

host heraan {
        hardware ethernet f0:de:f1:40:a5:b7;
        fixed-address 192.168.0.251;
}

host rpi {
        hardware ethernet b8:27:eb:93:53:95;
        fixed-address 192.168.0.252;
    	option routers 192.168.0.64;
}
```

After entering this we need to restart the dhcp server, by entering the following into the terminal window:

```text
sudo service network-manager restart
```

