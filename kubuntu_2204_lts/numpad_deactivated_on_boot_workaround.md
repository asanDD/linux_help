 
numpad deactivated on boot workaround
=====================================

**Description:**<br>
The numpad is deactivated on boot and has to be activated to use it as password input. The option in the KDE settings doesn't work.

**Workaround:**<br>
Create or edit the sddm config.<br>
`$ sudo nano /etc/sddm.conf` <br>
<br>
Add the following to the config:

<pre>[General]
Numlock=on</pre>

Reboot the system.
