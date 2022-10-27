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
