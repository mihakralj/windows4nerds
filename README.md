# Windows 10 Setup for Nerds

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

