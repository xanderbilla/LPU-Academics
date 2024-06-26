[**Back to Main**](https://github.com/xanderbilla/LPU-Academics/blob/main/README.md) | [**Table of Contents**](https://github.com/xanderbilla/LPU-Academics/blob/main/Navs/INT362/INT362.md)

# **Apache Cloud Stack**

![](https://upload.wikimedia.org/wikipedia/commons/7/70/Apache_CloudStack_Logo.svg)

# UNIT 3 | Basic Zone Configuration using KVM

### KVM Installation

First we need to install the Q Emulator for KVM to enable nested virtualization. Using following command

```bash
apt install -y qemu-kvm cloudstack-agent openssh-server cpu-checker

sed -i -e 's/\#vnc_listen.*$/vnc_listen = "0.0.0.0"/g'  /etc/libvirt/qemu.conf

systemctl mask libvirtd.socket libvirtd-ro.socket libvirtd-admin.socket libvirtd-tls.socket libvirtd-tcp.socket
systemctl restart libvirtd
apt-get install uuid
UUID=$(uuid)
echo host_uuid = \"$UUID\" >> /etc/libvirt/libvirtd.conf
sudo nano /etc/libvirt/libvirtd.conf

interface_name=$(ip route | grep default | awk '{print $5}')

gateway_addr=ip route | grep default | awk '{print $3}'

echo 'listen_tls=0' >> /etc/libvirt/libvirtd.conf
echo 'listen_tcp=1' >> /etc/libvirt/libvirtd.conf
echo 'tcp_port = "16509"' >> /etc/libvirt/libvirtd.conf
echo 'tls_port = "16514"' >> /etc/libvirt/libvirtd.conf
echo "listen_addr=\"${gateway_addr}\"" >> /etc/libvirt/libvirtd.conf
echo 'mdns_adv = 0' >> /etc/libvirt/libvirtd.conf
echo 'auth_tcp = "none"' >> /etc/libvirt/libvirtd.conf

systemctl restart libvirtd

ln -s /etc/apparmor.d/usr.sbin.libvirtd /etc/apparmor.d/disable/
ln -s /etc/apparmor.d/usr.lib.libvirt.virt-aa-helper/etc/apparmor.d/disable/

apparmor_parser -R /etc/apparmor.d/usr.sbin.libvirtd
apparmor_parser -R /etc/apparmor.d/usr.lib.libvirt.virt-aa-helper
exit
```


Once KVM configuration complete, you should check if KVM is running OK on your machine

```bash
sudo modprobe kvm 
lsmod | grep kvm
hostname -f
```
### Create Zone using Management server

To create a zone we must do the following: 

**Step 1 -** Open https://localhost:8080

**Step 2 -** Go to the infrastructure tab 

**Step 3 -** Select the zones.

**Step 4 -** Click on Add zone

**Step 5 -** A create zone wizard will appear.

**Step 6 -** Select Zone type as Basic and click on Next

**Step 7 -** Select Core Zone type as Advance and click on Next

**Step 8 -** Enter Zone details and click on Next

**Step 9 -** Select public traffic details and click on Next

**Step 10 -** Select Pods details to create a pod and click on Next

**Step 11 -** For guest traffic enter the VLAN range and click on Next

**Step 12 -** For adding cluster add the cluster name and click on Next

**Step 13 -** Add cluster details and Primary storage details and click on Next

**Step 14 -** Add secondary storage details and click on Launch Zone.

It will start creating the zone

Go to Infrastructure > Zones to view all zones.

Select the zone you want to open 

## Support

For support or colab, [email](mailto:dev.xanderbilla@gmail.com) or visit [website](https://xanderbilla.com)

## Authors

[Xander Billa](https://xanderbilla.com)
