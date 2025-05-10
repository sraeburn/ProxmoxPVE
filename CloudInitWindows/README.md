# Cloudbase-Init for Windows for Proxmox

If you have attempted to use Cloudbase-Init / Cloud-Init on Windows for Proxmox, you have probably encountered problems with the password values not being successfully applied to the deployed machine.

If you are using the Administrator password, then the password from Cloud-Init is not successfully set and needs to be set on startup.

The steps described here provide a workaround. The full process is as follows:

- Create your Windows VM.
- Install drivers (VirtIO etc)
- Install applications, including Qemu Guest Agent.
- Add a cloud-init drive.
- Add a serial port.
- Shutdown and restart the machine to apply the cloud-init and serial hardware changes.

With the hardware changes applied, Open the VNC console to the Windows machine and do the following:

- Start installation of Cloudbase-Init
- Enter "Administrator" as the username.
- Untick "use metadata password".
- Select the serial port (eg COM1).
- Tick run as localsystem.
- Wait for install to run - do not click Finish yet.
- Open the C:\Program Files\Cloudbase Solutions\Cloudbase-Init\conf\unattend.xml in notepad.
- Add the Administrator password section to the "oobeSystem" pass "Microsoft-Windows-Shell-Setup" section, eg:
- Click "Finish" to apply the sysprep changes.



Wait for the sysprep to complete - you can now convert the VM to a VM template if you wish.
- Apply the cloud-init settings as normal.
- Make sure to use the "Administrator" user and same password as specified in the unattend.xml file.
- Start up the VM / clone

Note: Further settings can be applied using the unattend.xml answer file (including additional users) - the Assessment and Deployment Toolkit by Microsoft contains more information on this.

[https://learn.microsoft.com/en-us/windows-hardware/get-started/adk-install](https://learn.microsoft.com/en-us/windows-hardware/get-started/adk-install)

[https://cloudbase-init.readthedocs.io/en/latest/index.html](https://cloudbase-init.readthedocs.io/en/latest/index.html)