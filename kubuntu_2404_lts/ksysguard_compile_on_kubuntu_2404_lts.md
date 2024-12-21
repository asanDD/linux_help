 
ksysguard: Compile on kubuntu 24.04 LTS
=====================================

**Description:**<br>
KDE has dropped ksysguard in favor of their new systemmonitor. Kubuntu doesn't offer ksysguard in their repositories anymore. Therefor, if you need a functionality of ksysguard that isn't provided by systemmonitor, you need to compile ksysguard yourself.

**Workaround:**<br>
\# Install Git<br>
`sudo apt install git`<br><br>
\# Create a build folder<br>
`mkdir -p ${HOME}/Documents/git/ksysguard`<br><br>
\# cd into the folder<br>
`cd ${HOME}/Documents/git/ksysguard`<br><br>
\# Download ksysguard<br>
`git clone --depth 1 --branch master https://invent.kde.org/plasma/ksysguard.git`<br><br>
\# cd into the ksysguard root dir<br>
`cd ksysguard`<br><br>
\# Install dependencies<br>
`sudo apt install \`<br>
`build-essential \`<br>
`extra-cmake-modules \`<br>
`libkf5config-dev \`<br>
`libkf5coreaddons-dev \`<br>
`libkf5dbusaddons-dev \`<br>
`libkf5doctools-dev \`<br>
`libkf5i18n-dev \`<br>
`libkf5kio-dev \`<br>
`libkf5iconthemes-dev \`<br>
`libkf5itemviews-dev \`<br>
`libkf5kio-dev \`<br>
`libkf5newstuff-dev \`<br>
`libkf5notifications-dev \`<br>
`libkf5windowsystem-dev \`<br>
`libkf5sysguard-dev`<br><br>
\# Generate the Project Buildsystem<br>
`cmake -B build -S .`<br><br>
\# cd into the build system<br>
`cd build`<br><br>
\# Compile<br>
`make`<br><br>
\# Install<br>
`sudo make install`<br><br>
\# Remove<br>
`sudo make remove`<br><br>
