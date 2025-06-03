# Terraform with Cloud-Init / Cloudbase-Init for Windows on Proxmox

Note: Before using this configuration you will need to make sure you have a Windows image prepared using Cloudbase-Init with an updated unattend.xml answer file containing the Administrator password.

See the "CloudInitWindows" subdirectory in this repo for more details.

The Terraform configuration has been tested using the updated unattend.xml only and must contain the Administrator user as ciuser and the same password as in the answer file.

The main.tf file should be configured with hardware to match the Proxmox template VM. Please note that:

- The "boot" variable sets the boot order, and should specify the Windows boot disk - this was ide1 in my case.
- The agent_timeout should be set to allow for the Qemu agent to start up successfully - the value is in seconds and 1800 (30 minutes) was more than sufficient.
- The serial section is required for correct cloud-init operation and should show debug logs.
- Make sure the correct template name is specified.
- The usual proxmox config / node placement options apply as normal.
- The ciuser and cipassword should be set as per the unattend.xml file as already mentioned.

A video demonstration can be found [here](https://youtu.be/Ix-CCuKHBB0).