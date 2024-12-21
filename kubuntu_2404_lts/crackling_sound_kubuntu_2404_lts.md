 
Crackling sound under load on Kubuntu 24.04 LTS
=====================================

**Description:**<br>
Some older sound cards don't work well with the new timer based scheduling that Pipewire uses. Unfortunately, Pipewire doesn't support the old interrupt based scheduling. A solution to this problem is to switch back to Pulseaudio and enable the old interrupt based scheduling.

**Workaround:**<br>
\# Install Pulseaudio<br>
`sudo apt install pulseaudio pulseaudio-module-bluetooth pulseaudio-utils pavucontrol gstreamer1.0-pulseaudio`<br><br>
\# Stop Pipewire<br>
`systemctl --user stop pipewire.socket pipewire-pulse.socket`<br><br>
\# Disable Pipewire<br>
`systemctl --user disable pipewire.socket pipewire-pulse.socket`<br>
`sudo systemctl --global disable pipewire.socket pipewire-pulse.socket`<br>
`systemctl --user mask pipewire.socket pipewire-pulse.socket`<br>
`sudo systemctl --global mask pipewire.socket pipewire-pulse.socket`<br><br>
\# Enable Pulseaudio<br>
`systemctl --user enable pulseaudio.service pulseaudio.socket`<br>
`sudo systemctl --global enable pulseaudio.service pulseaudio.socket`<br><br>
\# Start Pulseaudio<br>
`systemctl --user start pulseaudio.service pulseaudio.socket`<br><br>
\# Disable powersaving (Needed if the sound makes a periodic popping sound every second)<br>
`sudo nano /etc/pulse/default.pa`<br>
\# Comment the following line (add a # at the front)<br>
`load-module module-suspend-on-idle`<br><br>
\# Disable timer based scheduling for the sound card and use interrupt based scheduling instead<br>
`sudo nano /etc/pulse/default.pa`<br>
\# change<br>
`load-module module-udev-detect`<br>
\# to<br>
`load-module module-udev-detect tsched=0`<br><br>
\# Restart Pulseaudio<br>
`systemctl --user restart pulseaudio.service`<br>



