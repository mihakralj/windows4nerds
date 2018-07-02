# How to Setup Windows 10 for real Nerds

You can force Windows to push through all windows updates by calling `explorer ms-settings:windowsupdate-action` either through Run (Win-R) or from the command prompt

## Making bare Windows complete

Installed and updated vanilla Windows 10 is just the beginning. Microsoft doesn't provide any sane app packager with Windows, so we have to use add-ons such as [Chocolatey](chocolatey.org/) to programmatically add all apps we need to turn m

This is a superset of my Chocolatey.cmd file that you need to trim and prune for your needs; run it from the elevated command prompt.

```Batchfile
REM install Chocolatey package manager via PowerShell
@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))"
SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
choco feature enable -n allowGlobalConfirmation
choco feature disable -n stopOnFirstPackageFailure
choco install -f chocolatey
choco install choco-upgrade-all-at-startup chocolateygui

REM Bare essentials to keep devs sane
choco install 7zip adobereader qbittorrent sysinternals
choco install git github sourcetree zeal -ignorechecksum
choco install python nodejs golang

REM Browsers, because Windows 10 doesn't come with any
choco install vivaldi googlechrome firefox

REM Editor, terminals and fonts for die-hard nerds
choco install vscode atom sublimetext3 vim
choco install markdownmonster markdown-edit makrdownpad2 markpad
choco install putty mobaxterm consolez
choco install sourcecodepro hackfont

REM Collaboration and cloud storage to share stuff
choco install microsoft-teams slack
choco install dropbox googledrive

REM Cloudy stuff - AWS, Azure, GCP
choco install awscli cloudberryexplorer.amazons3
choco install azure-cli microsoftazurestorageexplorer
choco install gcloudsdk cloudberryexplorer.googlestorage

REM Containers-oh-my
choco install docker-for-windows docker-kitematic
choco install minikube kubernetes-cli kubernetes-helm
choco install minishift openshift-cli

REM Big heavy clunkers that take hours to install
choco install vmawreworkstation office365proplus
```

## Installing and customizing LSW

Open PowerShell as Administrator and run:

```PowerShell
#--- Add Windows Subsystem for Linux ---
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux

#--- Install Ubuntu 16.04 LTS from MS Store ---
Invoke-WebRequest -Uri https://aka.ms/wsl-ubuntu-1604 -OutFile ~/Ubuntu.appx -UseBasicParsing
Add-AppxPackage -Path ~/Ubuntu.appx
Ubuntu.exe
```

If you prefer to get straight to Bionic Beaver, head to Microsoft store and [download the 1804 Ubuntu image](https://www.microsoft.com/en-us/p/ubuntu-1804/9n9tngvndl3q) 

Launch `Ubuntu` from the start menu, create your Linux account and update the Linux distro:

```
sudo apt-get update && sudo apt-get -y upgrade
```
I also like to remove password off my Linux account as this is a subsystem of already-protected Windows system. If you feel that's a bad practice, simply ignore.

1. Run `sudo visudo`
2. Add the following line for your user: `<username> ALL=(ALL) NOPASSWD:ALL`
3. Delete the password: `sudo passwd -d <username>`

## Configuring ConsoleZ

We are ready to run the **real** console - if you installed ConsoleZ as part of choco script above. If not, [download it now](https://github.com/cbucher/console/wiki/Downloads).

1. `Ctrl-S` will open ConsoleZ settings
2. Under Appearance/Font choose **Source Code Variable Medium** (should be installed prior by Choco)
3. Under Tabs add CMD, PowerShell and any other shells you want

## Setting up fish and oh-my-fish
