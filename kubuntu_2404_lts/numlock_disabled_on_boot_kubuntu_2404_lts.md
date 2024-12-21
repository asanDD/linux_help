 
Numlock on boot on Kubuntu 24.04 LTS
=====================================

**Description:**<br>
Numlock is disabled on boot and has to be enabled to use it as password input. The option in the KDE settings doesn't work.

**Workaround:**<br>
Create or edit the sddm config.<br>
`$ sudo nano /etc/sddm.conf` <br>
<br>
Add the following to the config:<br>
`[General]`<br>
`Numlock=on`<br>
<br>
Reboot the system.
