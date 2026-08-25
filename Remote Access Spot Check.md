# Remote Access Spot Check
This assignment was just a simple check to make sure our cyber.local proxmox environment was working as intended! Barring any further complications with IT, I should be good to go!

### How To Navigate the Environment
You can reach the proxmox env by going to http://prox01.cyber.local and logging in with cyber.local creds.  
If the user is not on the Champlain network, viewportal.champlain.edu can be used as a proxy to get onto the network remotely.
All 4 VMs are located on pve5, named in shorthand for what their purpose is.

### Snapshots
Snapshots are used to save the state of the VM and provide a restore point if needed. Prior to any labs, snapshots labeled "Fresh" were taken on each VM.
To take further snapshots:
* Ensure the system is turned off
* Right-click the VM in the left pane or go to the Snapshots menu in the right pane after selecting the VM
* Take and name the snapshot
