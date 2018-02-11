### Setup *RDP* as VRDE (not open-source)
- Install extension pack
```bash
sudo apt install virtualbox-ext-pack
```

- Set VirtualBox to use this extension
```bash
VBoxManage setproperty vrdeextpack "Oracle VM VirtualBox Extension Pack"
```

### Setup *VNC* as VRDE (open-source)
- Install VNC extension
```bash
```

- Set VirtualBox to use this extension
```bash
VBoxManage setproperty vrdeextpack VNC
```


### Create VM 
```bash
VBoxManage createvm --name "vm_name" --register
```

### Modify VM settings
- basic settings (CPU/RAM/NIC/OS type)
```bash
VBoxManage modifyvm "vm_name"  --cpus 4 --memory 1024 --acpi on --boot1 dvd --nic1 bridged --bridgeadapter1 enp0s31f6 --ostype Ubuntu_64
```
- virtual disc setup
```bash
VBoxManage createhd --filename ./vm_name.vdi --size 10000
```
```bash
VBoxManage storagectl "vm_name" --name "IDE Controller" --add ide
```
```bash
VBoxManage storageattach "vm_name" --storagectl "IDE Controller" --port 0 --device 0 --type hdd --medium ./vm_name.vdi
```
- boot image setup
```bash
VBoxManage storageattach "vm_name" --storagectl "IDE Controller" --port 1 --device 0 --type dvddrive --medium ~/Downloads/ubuntu-16.04.3-server-amd64.iso
```

---

- turn the VRDE on
```bash
VBoxManage modifyvm "vm_name" --vrde on 
```

- make VRDE available via external interfaces
```bash
VBoxManage modifyvm "vm_name" --vrdeaddress "0.0.0.0"
```

- *if RDP*, disable authentification
```bash
VBoxManage modifyvm "vm_name" --vrdeauthtype null
```

- *if VNC*, set password
```bash
VBoxManage modifyvm "vm_name" --vrdeauthtype external
```
```bash
VBoxManage modifyvm "vm_name" --vrdeproperty VNCPassword=password
```

### List VMs
- Show all VM
```bash
VBoxManage list vms
```
- Show VM details
```bash
VBoxManage showvminfo "vm_name"
```

### Delete VM
```
VBoxManage unregistervm "vm_name" --delete
```

### Commands
- Start VM
```bash
VBoxHeadless --startvm "vm_name" 
```

- Show all running VMs
```bash
VBoxManage list runningvms
```

- Stop VM
```bash
VBoxManage controlvm "vm_name" acpipowerbutton
```
```bash
VBoxManage controlvm "vm_name" poweroff
```

- Connect to *RDP* VRDE
```bash
rdesktop -a 16 -N localhost
```

- Connect to *VNC* VRDE, don't forget to specify port !!
```bash
vinagre
```

- Turn the VRDE off (after the system installation), !! this is remebered by the snapshot
```bash
VBoxManage modifyvm "vm_name" --vrde off
```

----------------------------------------------------

- Take snapshot
```bash
VBoxManage snapshot "vm_name" take "snapshot_name"
```
- List snapshots
```bash
VBoxManage snapshot "vm_name" list
```
```bash
VBoxManage snapshot "vm_name" list --details
```
- Restore snapshot
```bash
VBoxManage snapshot "vm_name" restore "snapshot_name"
```
- Delete snapshot
```bash
VBoxManage snapshot "vm_name" delete "snapshot_name"
```

---
