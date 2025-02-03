 ## How to Install React Native on Arch Linux with Physical/Real Android Devices 

This guide will walk you through installing React Native and setting up your physical Android device for development on an Arch-based Linux distribution.

## Step 1: Install Yay (AUR Helper)
If you haven't installed `yay` yet, do so with the following commands:
```sh
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
```

## Step 2: Configure Android Environment
Instead of installing Android Studio, we'll install the Android SDK separately. Follow these steps:

1. [Download the custom Android Command Line Tools](https://github.com/1xrohit/Setup-ReactNative-on-Ubuntu-without-Android-Studio/releases/download/AndroidSDK/Android.zip)
2. Extract the downloaded archive to a suitable location on your system. e.g., `home/user/Android/`
3. Add the Android SDK tools directory to your system PATH. You can do this by adding the following lines to your `.bashrc` file:

```sh
nano ~/.bashrc
```

Then add these lines at the end of the file:

```sh
export ANDROID_HOME=$HOME/Android/Sdk
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/platform-tools
export PATH=$PATH:$ANDROID_HOME/cmdline-tools/latest/bin
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
export PATH=$PATH:$JAVA_HOME/bin
```

Save and exit, then apply the changes:
```sh
source ~/.bashrc
```

## Step 3: Install JDK (Java Development Kit)
To install JDK, run the following command:
```sh
yay -S jdk-openjdk
```

## Step 4: Install Android Tools and Udev Rules
```sh
sudo pacman -S android-tools android-udev 
sudo gpasswd -a $USER adbusers
newgrp adbusers 
sudo udevadm control --reload-rules
sudo udevadm trigger
```

## Step 4: Install and Configure NVM (Node Version Manager)
```sh
yay -S nvm
echo 'source /usr/share/nvm/init-nvm.sh' >> ~/.bashrc
source ~/.bashrc
```

## Step 5: Install Node.js and Package Managers
```sh
nvm install --lts
nvm alias default lts/*
npm install -g yarn
yarn global add react-native-cli
```

## Step 6: Initialize a React Native Project
```sh
npx react-native@latest init MyApp
OR
npx @react-native-community/cli init MyApp
```

## Step 7: Install Android SDK Build Tools
```sh
sdkmanager "build-tools;35.0.0"
```

## Step 8: Verify Your Configuration and Run the App
To check if your setup is correct, run:
```sh
npx react-native doctor
```
If everything is correctly configured, proceed with building and running your app:
```sh
npx react-native run-android
```
After the build process completes, stop it using `Ctrl + C`, then start the Metro bundler separately:
```sh
npx react-native start
```

Now, you should be able to use your physical device for React Native development!

## Social MEDIA LINKS
I hope you've found this guide helpful

Follow me on Twitter for more tips. <a href="https://x.com/1xrohit"><img src="https://img.shields.io/badge/Follow%20Rohit-blue.svg?logo=twitter"></a>


