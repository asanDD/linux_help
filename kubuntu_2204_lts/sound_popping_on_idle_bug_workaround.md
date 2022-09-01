 
Sound popping on idle bug workaround
====================================

**Description:**<br>
The sound is constantly popping when the sound card is idle. It seems that the sound card is constantly turned on and off.

**Workaround:**<br>
Turn off the powersaving function for the soundcard.<br>
<br>
Open the config for PulseAudio.<br>
`$ sudo nano /etc/pulse/default.pa`<br>
<br>
Mark the following line as a comment.<br>
`# load-module module-suspend-on-idle`<br>
<br>
Restart PulseAudio<br>
`$ pulseaudio -k`<br>
