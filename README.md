# macOS-Pro

## Disable heavy login screen wallpaper

```bash
sudo defaults write /Library/Preferences/com.apple.loginwindow DesktopPicture ""
```


## Disable the “Are you sure you want to open this application?” dialog

```bash
defaults write com.apple.LaunchServices LSQuarantine -bool false
```


## Disable disk image verification
```bash
defaults write com.apple.frameworks.diskimages skip-verify -bool true
defaults write com.apple.frameworks.diskimages skip-verify-locked -bool true
defaults write com.apple.frameworks.diskimages skip-verify-remote -bool true
```

## Deactivate and Stop the Remote Management Service
```bash
sudo /System/Library/CoreServices/RemoteManagement/ARDAgent.app/Contents/Resources/kickstart -deactivate -stop
```

## Disable ARD Agent and Remove Access Privileges for All Users (Default)
```bash
sudo /System/Library/CoreServices/RemoteManagement/ARDAgent.app/Contents/Resources/kickstart -deactivate -configure -access -off
```

## Remove Apple Remote Desktop Settings
```bash
sudo rm -rf /var/db/RemoteManagement ; \
sudo defaults delete /Library/Preferences/com.apple.RemoteDesktop.plist ; \
defaults delete ~/Library/Preferences/com.apple.RemoteDesktop.plist ; \
sudo rm -r /Library/Application\ Support/Apple/Remote\ Desktop/ ; \
rm -r ~/Library/Application\ Support/Remote\ Desktop/ ; \
rm -r ~/Library/Containers/com.apple.RemoteDesktop
```


```bash
#!/bin/zsh

#
# Speed up Mail.app by vacuuming the Envelope Index
# Written by Marcel Bischoff
# AppleScript original by "pmbuko" with modifications by Romulo
#

OS_VERSION=$(sw_vers -productVersion | cut -d. -f 1,2)
MAIL_RUNNING=$(ps aux | grep -v grep | grep -c "Mail\$")
MAIL_VERSION="V2"

if [ $MAIL_RUNNING -gt 0 ]; then osascript -e 'tell application "Mail" to quit'; fi

if [ 1 -eq "$(echo "11 <= ${OS_VERSION}" | bc)" ]; then MAIL_VERSION="V8"; fi

SIZE_BEFORE=$(ls -lnah ~/Library/Mail/${MAIL_VERSION}/MailData | grep -E 'Envelope Index$' | awk {'print $5'})
/usr/bin/sqlite3 ~/Library/Mail/${MAIL_VERSION}/MailData/Envelope\ Index vacuum
SIZE_AFTER=$(ls -lnah ~/Library/Mail/${MAIL_VERSION}/MailData | grep -E 'Envelope Index$' | awk {'print $5'})

printf "Mail index before: %s\nMail index after: %s\n" $SIZE_BEFORE $SIZE_AFTER
```


## TextEdit
## Create an Untitled Document at Launch
```bash
defaults write com.apple.TextEdit NSShowAppCentricOpenPanelInsteadOfUntitledFile -bool false
```

## Use Plain Text Mode as Default
```bash
defaults write com.apple.TextEdit RichText -int 0
```


## Disable Time Machine
```bash
sudo tmutil disable
```

## Prevent Time Machine from Prompting to Use New Hard Drives as Backup Volume
```bash
sudo defaults write /Library/Preferences/com.apple.TimeMachine DoNotOfferNewDisksForBackup -bool true
```


## Toggle Folder Visibility in Finder
By default, the ~/Library folder is hidden. You can easily show it again. The same method works with all other folders.
```bash
chflags nohidden ~/Library
```


## Expand Save Panel by Default
```bash
defaults write -g NSNavPanelExpandedStateForSaveMode -bool true && \
defaults write -g NSNavPanelExpandedStateForSaveMode2 -bool true
```


## Metadata Files
Disable Creation of Metadata Files on Network Volumes
Avoids creation of .DS_Store and AppleDouble files.
```bash
defaults write com.apple.desktopservices DSDontWriteNetworkStores -bool true
```

## Disable Creation of Metadata Files on USB Volumes
Avoids creation of .DS_Store and AppleDouble files.
```bash
defaults write com.apple.desktopservices DSDontWriteUSBStores -bool true
```

## Set Current Folder as Default Search Scope
```bash
defaults write com.apple.finder FXDefaultSearchScope -string "SCcf"
```
