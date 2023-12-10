# macOS-Pro

### Disable heavy login screen wallpaper

```bash
sudo defaults write /Library/Preferences/com.apple.loginwindow DesktopPicture ""
```

### Disable the “Are you sure you want to open this application?” dialog

```bash
defaults write com.apple.LaunchServices LSQuarantine -bool false
```


### Disable disk image verification
```bash
defaults write com.apple.frameworks.diskimages skip-verify -bool true
defaults write com.apple.frameworks.diskimages skip-verify-locked -bool true
defaults write com.apple.frameworks.diskimages skip-verify-remote -bool true
```

### Deactivate and Stop the Remote Management Service
```bash
sudo /System/Library/CoreServices/RemoteManagement/ARDAgent.app/Contents/Resources/kickstart -deactivate -stop
```

### Disable ARD Agent and Remove Access Privileges for All Users (Default)
```bash
sudo /System/Library/CoreServices/RemoteManagement/ARDAgent.app/Contents/Resources/kickstart -deactivate -configure -access -off
```

### Remove Apple Remote Desktop Settings
```bash
sudo rm -rf /var/db/RemoteManagement ; \
sudo defaults delete /Library/Preferences/com.apple.RemoteDesktop.plist ; \
defaults delete ~/Library/Preferences/com.apple.RemoteDesktop.plist ; \
sudo rm -r /Library/Application\ Support/Apple/Remote\ Desktop/ ; \
rm -r ~/Library/Application\ Support/Remote\ Desktop/ ; \
rm -r ~/Library/Containers/com.apple.RemoteDesktop
```

### TextEdit: Create an Untitled Document at Launch
```bash
defaults write com.apple.TextEdit NSShowAppCentricOpenPanelInsteadOfUntitledFile -bool false
```

### TextEdit: Use Plain Text Mode as Default
```bash
defaults write com.apple.TextEdit RichText -int 0
```

### Disable Time Machine
```bash
sudo tmutil disable
```

### Prevent Time Machine from Prompting to Use New Hard Drives as Backup Volume
```bash
sudo defaults write /Library/Preferences/com.apple.TimeMachine DoNotOfferNewDisksForBackup -bool true
```

### Toggle Folder Visibility in Finder
By default, the ~/Library folder is hidden. You can easily show it again. The same method works with all other folders.
```bash
chflags nohidden ~/Library
```

### Expand Save Panel by Default
```bash
defaults write -g NSNavPanelExpandedStateForSaveMode -bool true && \
defaults write -g NSNavPanelExpandedStateForSaveMode2 -bool true
```

### Metadata Files
Disable Creation of Metadata Files on Network Volumes
Avoids creation of .DS_Store and AppleDouble files.
```bash
defaults write com.apple.desktopservices DSDontWriteNetworkStores -bool true
```

### Disable Creation of Metadata Files on USB Volumes
Avoids creation of .DS_Store and AppleDouble files.
```bash
defaults write com.apple.desktopservices DSDontWriteUSBStores -bool true
```

### Always search within the current Folder
```bash
defaults write com.apple.finder FXDefaultSearchScope -string "SCcf"
```

### Disable Homebrew analytics
```bash
brew analytics off
```

### Disable AutoCorrect
```bash
defaults write -g NSAutomaticSpellingCorrectionEnabled -bool false
```

### Expand Save and Print Dialogs by Default
This one can save you many clicks. By default, the “print” and “save” dialogs are very small with some default options selected, like Desktop. These four commands will expand those for you.
```bash
defaults write NSGlobalDomain NSNavPanelExpandedStateForSaveMode -bool true && \
defaults write NSGlobalDomain NSNavPanelExpandedStateForSaveMode2 -bool true && \
defaults write NSGlobalDomain PMPrintingExpandedStateForPrint -bool true && \
defaults write NSGlobalDomain PMPrintingExpandedStateForPrint2 -bool true
```

### Key Repeats
This one is crucial as well, if you try to delete a word or letters, you can use shortcuts, but by default pressing “delete/backspace” multiple times in a row seems to be faster than holding it; this is definitely odd. You can make it faster by the following commands:
Key repeat (default is 2 or 30 ms)
```bash
defaults write -g KeyRepeat -int 0.02
```
When the Key repeat starts (default is 15 or 225ms):
```bash
defaults write -g InitialKeyRepeat -int 10
```

### Safari Default Web Page
```bash
defaults write com.apple.Safari HomePage -string "about:blank"
```

### 'Are you sure you want to open this application?'
```bash
defaults write com.apple.LaunchServices LSQuarantine -bool false
```

### Allow apps downloaded from "Anywhere" to be opened
```bash
sudo spctl - master-disable
```

### Change the Screen Shot image type from PNG to JPG
```bash
defaults write com.apple.screencapture type jpg && killall SystemUIServer
```

### Dock to the left
```bash
defaults write com.apple.Dock orientation -string left
```

### Hide Finder status bar
```
defaults write com.apple.Finder ShowStatusBar -bool false
```


### Hide Finder path bar
```
defaults write com.apple.Finder ShowPathbar -bool false
```

### Hide internal hard drives on desktop
```
defaults write com.apple.Finder ShowHardDrivesOnDesktop -bool true
```
### Hide external hard drives on desktop
```
defaults write com.apple.Finder ShowExternalHardDrivesOnDesktop -bool true
```
### Hide removable media on desktop
```
defaults write com.apple.Finder ShowRemovableMediaOnDesktop -bool true
```
### Hide mounted servers on desktop
```
defaults write com.apple.Finder ShowMountedServersOnDesktop -bool true
```
### Disable the warning before emptying the Trash
```
defaults write com.apple.Finder WarnOnEmptyTrash -bool false
```

disable safari auto open files
```
defaults write com.apple.Safari AutoOpenSafeDownloads -bool false
```

hide bookmarks bar
```
defaults write com.apple.Safari ShowFavoritesBar -bool false
```

disable crash reporter
```
defaults write com.apple.CrashReporter DialogType none
```
### Disable GateKeeper
```
sudo spctl --master-disable
sudo defaults write /Library/Preferences/com.apple.security GKAutoRearm -bool false
```

### Enable Touch ID for sudo
```
cd /etc/pam.d
sudo cp sudo_local.template sudo_local
sudo pico sudo_local
```
In that file, navigate to the line that contains with pam_tid.so and delete the hashtag (#) at the beginning. Save the file out by pressing Control-X, typing ‘Y’ to save your changes, and hitting Return.

### Don't display screeshot thumbnail and save immediately
```
defaults write com.apple.screencapture "show-thumbnail" -bool "false"
```
### Do not display the warning when changing a file extension
```
defaults write com.apple.finder "FXEnableExtensionChangeWarning" -bool "false" && killall Finder
```
### Set light click weight (threshold)
```
defaults write com.apple.AppleMultitouchTrackpad "FirstClickThreshold" -int "0"
```
### Do not autogather large files when submitting a feedback report
```
defaults write com.apple.appleseed.FeedbackAssistant "Autogather" -bool "false"
```
### Disable application quarantine message
```
defaults write com.apple.LaunchServices "LSQuarantine" -bool "false"
```
### Set machine sleep to 2 minutes on battery
```
sudo pmset -b sleep 2
```
### Set machine sleep to 3 minutes while charging
```
sudo pmset -b sleep 3
```

# Require password immediately after sleep or screen saver begins
```
defaults write com.apple.screensaver askForPassword -int 1
defaults write com.apple.screensaver askForPasswordDelay -int 0
```
### Disable bottom right corner quick note
```
defaults write com.apple.dock wvous-br-corner -int 0
defaults write com.apple.dock wvous-br-modifier -int 0
```

# Safari disable Warn about fraudulent websites
```
defaults write com.apple.Safari WarnAboutFraudulentWebsites -bool false
```

# Disable "Ask Siri"
```
defaults write com.apple.assistant.support 'Assistant Enabled' -bool false
```

# Disable Siri voice feedback
```
defaults write com.apple.assistant.backedup 'Use device speaker for TTS' -int 3
```


# Disable Siri telemetry
```
defaults write com.apple.assistant.support 'Siri Data Sharing Opt-In Status' -int 2
```

Improving Bluetooth audio quality
```	
 defaults write com.apple.BluetoothAudioAgent "Apple Bitpool Min (editable)" -int 40
	defaults write com.apple.BluetoothAudioAgent "Apple Bitpool Max (editable)" 80
	defaults write com.apple.BluetoothAudioAgent "Apple Bitpool Min (editable)" 40
	defaults write com.apple.BluetoothAudioAgent "Apple Initial Bitpool (editable)" 80
	defaults write com.apple.BluetoothAudioAgent "Apple Initial Bitpool Min (editable)" 80
	defaults write com.apple.BluetoothAudioAgent "Negotiated Bitpool" 80
	defaults write com.apple.BluetoothAudioAgent "Negotiated Bitpool Max" 80
	defaults write com.apple.BluetoothAudioAgent "Negotiated Bitpool Min" 80
```

 Disable potential DNS leaks
 ```
 sudo defaults write /Library/Preferences/com.apple.mDNSResponder.plist NoMulticastAdvertisements -bool YES
```
