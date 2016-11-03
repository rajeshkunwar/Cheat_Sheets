Performing common virtual machine-related tasks with command-line utilities (2012964)
In these examples:
 •	vcenter is your vCenter Server hostname
 •	esxhost is your ESX/ESXi hostname
 •	datastore is the display name of your datastore
 •	path_to_vmx_on_datastore is the path to the virtual machine's vmx file relative to the datastore on which it resides
 •	vm_name is the display name of a virtual machine
 •	path_to_vmx_file is the full path to a virtual machine's vmx file
 •	snapshot_name is the name given to a virtual machine snapshot
 •	guest_admin_user is a user account with administrative access within a virtual machine's guest OS
 •	guest_admin_password is the password for the account noted by guest_admin_user

Connecting  to the vcenter: Connect-VIServer –Server vcenterserver_name –User username –Password password

 	  | PowerCLI	| vMA	| cli
--- | --- | --- | --- |   
Register a VM	| New-VM –vmfilepath “[datastore] path_to_vmx_on_datastore” –vmhost esxhost	| vmware-cmd --server esxhost –s register path_to_vmx_file <br \>vmware-cmd --server vcenter --vihost esxhost –s register path_to_vmx_file	| vim-cmd solo/registervm path_to_vmx_file
Unregister a VM	| Remove-VM vm_name	| vmware-cmd --server esxhost –s unregister path_to_vmx_file <br \>vmware-cmd --server vcenter --vihost esxhost –s unregister path_to_vmx_file | vim-cmd vmsvc/unregister vmid
Delete a VM	| Remove-VM vm_name -deletepermanently	| vmware-cmd --server esxhost –s unregister path_to_vmx_file <br \>vmware-cmd --server vcenter --vihost esxhost –s unregister path_to_vmx_file vifs --server esxhost --rm “[datastore] path_to_vmx_on_datastore”	| vim-cmd vmsvc/destroy vmid
Get a listing of VMs on a host	| Get-VM –location esxhost	| vmware-cmd –-server esxhost –-username root –l <br \>vmware-cmd --server vcenter –-vihost esxhost -l	| esxcli vm process list <br \>vim-cmd vmsvc/getallvms
Determine if a VM has a snapshot	| Get-VM –name vm_name \| Get-Snapshot	| vmware-cmd --server esxhost path_to_vmx_file hassnapshot <br \>vmware-cmd --server vcenter --vihost esxhost path_to_vmx_file hassnapshot	| vim-cmd vmsvc/get.snapshot vmid
Take a snapshot of a VM	| Get-VM –name vm_name \| New-Snapshot –name snapshot_name	| vmware-cmd --server esxhost path_to_vmx_file createsnapshot snapshot_name <br \>vmware-cmd --server vcenter --vihost esxhost path_to_vmx_file createsnapshot snapshot_name	| vim-cmd vmsvc/snapshot.create vmidsnapshot_name
Remove a snapshot of a VM	| Get-VM –name vm_name \| Get-Snapshot –name snapshot_name \| Remove-Snapshot	| vmware-cmd --server esxhost path_to_vmx_file removesnapshots <br \>vmware-cmd --server vcenter --vihost esxhost path_to_vmx_file removesnapshots	| vim-cmd vmsvc/snapshot.remove vmid
Get the current power state of a VM	| Get-VM –name vm_name	| vmware-cmd --server esxhost path_to_vmx_file getstate <br \>vmware-cmd --server vcenter --vihost esxhost path_to_vmx_file getstate	| vim-cmd vmsvc/power.getstate vmid
Get the uptime for a VM	| Get-Stat -entity vm_name -stat sys.uptime.latest -MaxSamples 1	| vmware-cmd --server esxhost path_to_vmx_file getuptime <br \>vmware-cmd --server vcenter --vihost esxhost path_to_vmx_file getuptime	| vim-cmd vmsvc/get.summary vmid \|grep uptimeSeconds
Power on a VM	| Start-VM –vm vm_name	| vmware-cmd --server esxhost path_to_vmx_file start <br \>vmware-cmd --server vcenter --vihost esxhost path_to_vmx_file start	| vim-cmd vmsvc/power.on vmid
Shutdown a VM	| Shutdown-VMGuest –vm vm_name	| vmware-cmd --server esxhost path_to_vmx_file stop soft <br \>vmware-cmd --server vcenter --vihost esxhost path_to_vmx_file stop soft |	vim-cmd vmsvc/power.shutdown vmid
Power off a VM	| Stop-VM –vm vm_name	| vmware-cmd --server esxhost path_to_vmx_file stop hard <br \>vmware-cmd --server vcenter --vihost esxhost path_to_vmx_file stop hard	esxcli vm process kill –w world_id | vim-cmd vmsvc/power.off vmid
Reboot a VM	| Restart-VMGuest –vm vm_name	vmware-cmd --server esxhost path_to_vmx_file reset soft | vmware-cmd --server vcenter --vihost esxhost path_to_vmx_file reset soft	| vim-cmd vmsvc/power.reboot vmid
Reset a VM	| Restart-VM –vm vm_name	| vmware-cmd --server esxhost path_to_vmx_file reset hard <br \>vmware-cmd --server vcenter --vihost esxhost path_to_vmx_file reset hard	| vim-cmd vmsvc/power.reset vmid
Upgrade VMware Tools in a VM	| Update-Tools –vm vm_name	| N/A	| vim-cmd vmsvc/tools.upgrade vmid
Display the IP address of a VM	| Get-VMGuestNetworkInterface –vm vm_name -guestuser guest_admin_user -guestpassword guest_admin_password	| vmware-cmd --server esxhost path_to_vmx_file getguestinfo ip <br \>vmware-cmd --server vcenter --vihost esxhost path_to_vmx_file getguestinfo ip	| vim-cmd vmsvc/get.guest vmid \|grep -m 1 "ipAddress = \\""

