 
Periodic popping sound on Kubuntu 24.04 LTS
=====================================

**Description:**<br>
The power saving feature in Ubuntu causes some older intel sound cards to make a periodic popping noise every second. A solution to this is to leave the sound card always on.

**Workaround:**<br>
\# Temporary for testing<br>
`echo "0" | sudo tee /sys/module/snd_hda_intel/parameters/power_save`<br><br>
\# Permanently (restart required for changes to take effect)<br>
`echo "options snd_hda_intel power_save=0" | sudo tee -a /etc/modprobe.d/audio_disable_powersave.conf`<br><br>

