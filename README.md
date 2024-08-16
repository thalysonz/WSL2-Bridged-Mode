#### WSL2-Bridged-Mode
- enable bridged

### Get Your Net Adapters

```powershell
Get-NetAdapter
```
### Create new VM-Switch, set your adapter in NetAdapterName
```powershell
New-VMSwitch -Name "VM-Ubuntu" -NetAdapterName "Ethernet" -AllowManagementOS $true
```
### Create or Edit C:\Users\<SeuUsuário>\.wslconfig

```ini
[wsl2]
networkingMode=bridged
vmSwitch=VM-Ubuntu
dhcp=false
macAddress=0E:00:00:00:00:00
```

### Edit in WSL file: /etc/wsl.conf

```ini
[boot]
systemd=true

[network]
hostname = UBUNTUWSL
generateResolvConf = false
```

### Edit in WSL file: /etc/systemd/network/20-wslbridged.network
```ini
[Match]
Name=eth0

[Network]
Description=VM-Ubuntu
DHCP=yes
```

### In powershel execute -> ```powershell wsl --shutdown ```

Reopen ubuntu wsl2

### Troubleshooting

- DNS problems:

```bash
   cat /etc/resolv.conf
```
type:

```
nameserver 8.8.8.8
nameserver 8.8.4.4
```
