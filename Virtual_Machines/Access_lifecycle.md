# VM Access and lifecycle


## Accessing a VM grants root privileges to the creator, who can use SSH (Linux machines) or RDP (Windows Machine), and the VM lifecycle includes provisioning, staging, and running states

- The creator of a VM instance has full root privileges and can grant SSH capability on a Linux instance or generate a username and password for a Windows instance.

- The VM lifecycle includes provisioning, staging, and running states where resources are reserved, acquired, and prepared for launch.

- While the instance is running, users can live migrate it to another host in the same zone without requiring a reboot for maintenance.


## VMs can be moved, snapshots taken, and metadata reconfigured without interrupting them, with options to stop, restart, delete, reset, or suspend the VM

- Actions like moving VM to a different zone, taking snapshots, exporting system image, and reconfiguring metadata can be done while the VM is running.

- Some actions require stopping the VM, like upgrading by adding more CPU.

- Resetting a VM wipes memory contents and brings it back to the initial state.

- Repairing state occurs when there is an internal error, and during this time, the VM is unusable.

## The section discusses VM shutdown processes, live migration, availability policies, and managing OS updates

- Shutdown process takes about 90 sec for rebooting, stopping, or deleting an instance.

- Compute Engine can live migrate VMs during maintenance events to prevent disruptions.

- Availability policies determine how instances behave during maintenance events.
OS updates and patch management are crucial for infrastructure maintenance.

## The OS patch management service for Compute Engine VM instances helps automate patch updates and provides insights on patch status

- Patch compliance reporting offers insights and recommendations for patch status across Windows and Linux distributions.

- Patch deployment automates the update process by scheduling patch jobs to apply patches to VM instances.

- Tasks like creating patch approvals, setting up flexible scheduling, and applying advanced patch configurations can be performed with patch management.

- When a VM is terminated, charges apply for attached disks and reserved IP addresses, but not for memory and CPU resources.