# MDM_Bypass_guide
A guide for MDM Bypass for all devices vulerable to checkm8 beneath ios 15.0


Ok so for this to work you NEED TO BE ON THE SETUP SCREEN. so if you're not jailbroken erase all contents and settings via settings app or if you're jailbroken re-flash your device with futurerestore and the blob.

1. Jailbreak with checkra1n.

2. go to the terminal and if you don't have it yet for mac type: brew install libusbmuxd-tools and for linux: sudo apt install libusbmuxd-tools. Type in the terminal windows the following: 
```
iproxy 2222 44
```
open a new terminal window (DONT CLOSE THE OLD ONE!) and type in there:
```
ssh root@localhost -p 2222
```

it will ask you for authentication. type yes and press enter. Then it will ask for the password. The default password is alpine

Once you're inside type: cd /private/var/containers/Shared/SystemGroup/systemgroup.com.apple.configurationprofiles/ConfigurationProfiles/Library. And press enter. Once you're in the directory type: ls and press enter. You should see 2 files. the first one is CloudconfigurationDetails.plist and the second one is CloudConfigurationSetAsideDetails.plist
These files are by default binary so you need to convert them first. No biggy just type:
```
plutil -convert xml1 CloudConfigurationDetails.plist
```
Do the same for the other one
then type:
```
nano CloudConfigurationDetails.plist
```
Search for lines that say the following things:
```
ismdmunremovable and set it to 0 (or false)

is supervised to false (or 0)

isMandatory to false (or 0 if the value is 1)
```
then ctrl + o to save it and ctrl+x to leave nano
Do the same for CloudConfigurationSetAsideDetails.plist
once you're done type: killall backboardd and it'll respring
Now if you follow the setup it should ask you if you want to skip the configuration or apply it. Just hit skip configuration and you're ready to go!
NOTE!
This is not permanent until the host of the mdm profile removes you're device. So if you re-flash the mdm lock will still haunt you.
Enjoy!
This works on ios 14 too so don't worry
