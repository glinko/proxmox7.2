# proxmox7.2

echo "deb http://download.proxmox.com/debian bullseye pve-no-subscription" > /etc/apt/sources.list.d/pve-enterprise.list 
#add repo key
wget http://download.proxmox.com/debian/key.asc
apt-key add key.asc
apt update && apt dist-upgrade -y
sed -Ezi.bak "s/(Ext.Msg.show\(\{\s+title: gettext\('No valid sub)/void\(\{ \/\/\1/g" /usr/share/javascript/proxmox-widget-toolkit/proxmoxlib.js && systemctl restart pveproxy.service
grep -n -B 1 'No valid sub' /usr/share/javascript/proxmox-widget-toolkit/proxmoxlib.js
