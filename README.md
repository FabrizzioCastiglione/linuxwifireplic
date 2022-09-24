# linuxwifireplic
Linux como Punto de Acceso wifi

sudo apt update
sudo apt upgrade -y

sudo apt install dnsmasq hostapd -y

sudo nano /etc/dhcpcd.conf

sudo systemctl restart dhcpcd

sudo mv /etc/dnsmasq.conf /etc/dnsmasq.conf.orig    

sudo nano /etc/dnsmasq.conf

sudo systemctl reload dnsmasq

sudo nano /etc/hostapd/hostapd.conf

sudo nano /etc/default/hostapd

Esta línea debe estar así:

DAEMON_CONF="/etc/hostapd/hostapd.conf"


sudo systemctl unmask hostapd
sudo systemctl stop hostpad # importante para procesos cada vez que se haga un cambio en hostpad.conf
sudo systemctl enable hostapd
sudo systemctl start hostapd


Editamos:

sudo /etc/sysctl.conf

Descomentamos esta línea:

net.ipv4.ip_forward=1
- Añadimos una máscara de salida a eth0

sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
- Guardamos las reglas de iptables.

sudo sh -c "iptables-save > /etc/iptables.ipv4.nat"
Editamos:

sudo /etc/rc.local

Añadimos esto encima de "exit 0" para instalar las reglas de inicio.

iptables-restore < /etc/iptables.ipv4.nat
