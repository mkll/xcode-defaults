# Xcode defaults

![Check Markdown links](https://github.com/ctreffs/xcode-defaults/workflows/Check%20Markdown%20links/badge.svg) [![License: CC BY-ND 4.0](https://img.shields.io/badge/License-CC%20BY--ND%204.0-green.svg)](https://creativecommons.org/licenses/by-nd/4.0/)

#### Backup Xcode defaults

```sh
defaults read com.apple.dt.Xcode > ~/Desktop/XcodeDefaults.plist
```

#### Restore Xcode vanilla defaults 

If you delete/move the current plist, Xcode will write a fresh one next time you run it.

```sh
killall Xcode
mv ~/Library/Preferences/com.apple.dt.Xcode.plist ~/Desktop/XcodeDefaults.plist
open -b com.apple.dt.Xcode
```

### Enable project build time

```sh
defaults write com.apple.dt.Xcode ShowBuildOperationDuration -bool YES
```


### Enable parallel builds for Swift

```sh
defaults write com.apple.dt.Xcode BuildSystemScheduleInherentlyParallelCommandsExclusively -bool YES
```

### Disable parallel builds for Swift 

Xcode 9.3 now runs more Swift build tasks in parallel with other commands. This may improve build times for Swift projects, but may also increase memory use during the build. This feature can be disabled from Terminal by setting a user default with 

```sh
defaults write com.apple.dt.Xcode BuildSystemScheduleInherentlyParallelCommandsSerially -bool YES
```

### Enable multi-cursor editing

```sh
defaults write com.apple.dt.Xcode PegasusMultipleCursorsEnabled -bool YES
```

### Enable maximum number of concurrent compile tasks

```sh
defaults write com.apple.dt.Xcode IDEBuildOperationMaxNumberOfConcurrentCompileTasks `sysctl -n hw.ncpu`
```

### Enable/Disable indexing

##### Enable indexing

```sh
defaults delete com.apple.dt.Xcode IDEIndexDisable
defaults write com.apple.dt.Xcode IDEIndexEnable -bool YES
```

##### Disable indexing

```sh
defaults delete com.apple.dt.Xcode IDEIndexEnable
defaults write com.apple.dt.Xcode IDEIndexDisable -bool YES
```

### Show Indexing numeric progress

```sh
defaults write com.apple.dt.Xcode IDEIndexerActivityShowNumericProgress -bool YES
```

### Show Indexing logging

This will show you why a particular file is having trouble being compiled for indexing.

```sh
defaults write com.apple.dt.Xcode IDEIndexShowLog -bool YES
```

### Show prebuild step logs

```sh
defaults write com.apple.dt.Xcode IDEShowPrebuildLogs -bool YES
```

### Set SourceKit log level

If set to SourceKit will write a log to /tmp with all the details of what it is doing while indexing. 
A lot of people find they have header hygiene problems or module problems that happen to work while building in certain configurations but aren't actually correct, resulting in missing modules or broken headers from the indexer's point of view.
May not work anymore.

```sh
defaults write com.apple.dt.Xcode IDESourceKitServiceLogLevel -int 3 
```

### Disable Main Thread Checker

Deactivates the Main Thread Checker:

```sh
defaults write com.apple.dt.Xcode DVTDisableMainThreadChecker 1
```
Found in [Xcode 12 release notes](https://developer.apple.com/documentation/xcode-release-notes/xcode-12-beta-release-notes)

### Enable internal Xcode (debug) menu

```sh
defaults write com.apple.dt.Xcode ShowDVTDebugMenu -bool YES
```

### Disable automatic reopening of last project

Prevents Xcode from automatically restoring the last open project. 
This enables running multiple Xcode versions for different projects.

```sh
defaults write com.apple.dt.Xcode ApplePersistenceIgnoreState -bool YES
```

### Some minimal additional logging 

```sh
defaults write com.apple.dt.XCBuild EnableDebugActivityLogs -bool YES
```

### Enable build debugging mode

This slows down the build system & litters DerivedData/<project>/Build/Intermediates.noindex), generally should only be enabled when trying to capture a trace for incremental build debugging purposes.
  
```sh
defaults write com.apple.dt.XCBuild EnableBuildDebugging -bool YES
```

## Simulator

### Enable Simulator fullscreen mode

```sh
defaults write com.apple.iphonesimulator AllowFullscreenMode -bool YES
```

## XCBuild

### Enable Build Debugging 

Creates an XCBuildData folder in `~/Library/Developer/Xcode/DerivedData/<your target>/Build/Intermediates.noindex/` which contains debugging info for xcodebuild.

```sh
defaults write com.apple.dt.XCBuild -bool YES
```
