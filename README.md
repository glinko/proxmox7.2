# proxmox7.2

echo "deb http://download.proxmox.com/debian bullseye pve-no-subscription" > /etc/apt/sources.list.d/pve-enterprise.list 
#add repo key
wget http://download.proxmox.com/debian/key.asc
apt-key add key.asc
apt update && apt dist-upgrade -y
sed -Ezi.bak "s/(Ext.Msg.show\(\{\s+title: gettext\('No valid sub)/void\(\{ \/\/\1/g" /usr/share/javascript/proxmox-widget-toolkit/proxmoxlib.js && systemctl restart pveproxy.service
grep -n -B 1 'No valid sub' /usr/share/javascript/proxmox-widget-toolkit/proxmoxlib.js
apt-get install fail2ban -y
apt-get install mc -y
echo -e "\r\n[proxmox]\r\nenabled = true\r\nport = https,http,8006\r\nfilter = proxmox\r\nlogpath = /var/log/daemon.log\r\nmaxretry = 3\r\nfindtime = 3600\r\nbantime = 103600" >> /etc/fail2ban/jail.conf
echo -e "[Definition]\r\nfailregex = pvedaemon\[.*authentication failure; rhost=<HOST> user=.* msg=.*\r\nignoreregex =" > /etc/fail2ban/filter.d/proxmox.conf 
systemctl start fail2ban

  
  #GUI
  #certificates from lets encrypt
  #wipe disks
  #install ceph
