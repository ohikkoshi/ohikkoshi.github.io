# ToC
- [Git](#git) / [.NET](#net) / [FFmpeg](#ffmpeg) / [ImageMagick](#imagemagick)
- [Redmine](#redmine) / [GitLab](#gitlab)
- [macOS](#macos) / [Android](#android)




# Git
### ssh
```
ssh -T git@github.com
```
### clone
```
git clone https://github.com/<REPOSITORY>
git clone https://<USER>@github.com/<REPOSITORY>
```
### checkout
```
git checkout .
git checkout <BRANCH>
git checkout -b <BRANCH>
git checkout --orphan <BRANCH>
```
### switch
```
git switch -c <BRANCH>
git switch <BRANCH>
```
### restore
```
git restore .
git restore <BRANCH>
```
### branch
```
git branch -a
git branch -m <OLD_BRANCH> <NEW_BRANCH>
git branch -D <BRANCH>
```
```
git push --delete origin <BRANCH>
```
### fetch
```
git fetch --prune --prune-tags
```
### pull
```
git pull --rebase --tags origin <BRANCH>
```
### rebase
```
git rebase -i HEAD~n
```
### merge
```
git merge --squash <BRANCH>
```
### pick
```
git cherry-pick <ID>
```
### add
```
git add .
git add -f <FILE>
```
### commit
```
git commit -a
git commit --amend
```
### revert
```
git revert <ID>
```
### reset
```
git reset --hard HEAD
git reset --hard HEAD~n
```
### clean
```
git clean -fxd
git gc
```
### push
```
git push origin <BRANCH>
git push -f origin <BRANCH>
```
### remote
```
git remote -v
```
### log
```
git status --ignored
git log --oneline --graph --branches --decorate
git reflog
```
### tag
```
git tag
git tag <TAG>
git push origin --tags
```
```
git tag -d <TAG>
git push --delete origin <TAG>
```
### git-lfs
```
git lfs install
git lfs version
```
```
git lfs track
git lfs ls-files
```
### .git/config
```
[user]
  name = ***
  email = ***
  useConfigOnly = true
[includeIf "gitdir/i:~/git.global/"]
  path = .gitconfig.global
[includeIf "gitdir/i:~/git.hub/"]
  path = .gitconfig.github
```


# .NET
### MSBuild
```
msbuild -t:Clean
msbuild -m -t:Rebuild -p:Configuration="Release"
```
### NuGet
```
nuget locals all -list
nuget locals all -clear
nuget restore
```

### dotnet
```
dotnet build -c Release
dotnet publish -c Release --sc true -r osx-x64 /p:PublishSingleFile=true
```
```
dotnet tool search <PACKAGE>
dotnet add package <PACKAGE>
```
```
dotnet run --roll-forward LatestMajor
```


# FFmpeg
```
ffmpeg -i <INPUT> -s 1280x720 <OUTPUT>
ffmpeg -i <INPUT> -vf scale=1280:-1 -r 10 <OUTPUT>.gif
ffmpeg -i <INPUT> -f image2 -ss 00:00:01 -vframes 1 -s 480x270 <OUTPUT>
```


# ImageMagick
```
convert <INPUT>.psd output%03d.png
```


# Redmine
### service
```
systemctl <start/stop/restart/status> httpd
```
### upgrade
```
sudo su -
systemctrl stop httpd
cd /var/lib
unlink redmine
cp -rp redmine-x.x.x-old redmine.x.x.x-new
cd redmine-x.x.x-new
```
```
svn update
bundle update
bundle exec rake db:migrate RAILS_ENV=production
bundle exec rake redmine:plugins:migrate RAILS_ENV=production
bundle exec rake tmp:cache:clear RAILS_ENV=production
```
```
ln -s /var/lib/redmine-x.x.x-new /var/lib/redmine
systemctrl start httpd
```
### plugins-install
```
sudo su -
bundle install
bundle exec rake db:migrate RAILS_ENV=production
bundle exec rake redmine:plugins:migrate RAILS_ENV=production
bundle exec rake tmp:cache:clear RAILS_ENV=production
```
### plugins-uninstall
```
sudo su -
bundle exec rake redmine:plugins:migrate NAME=<PLUGIN> VERSION=0 RAILS_ENV=production
rm -rf plugins/<PLUGIN>
```
### reminders
```
/etc/crontab -e
0 9 * * * cd /var/lib/redmine ; /usr/local/bin/bundle exec /usr/local/bin/rake redmine:send_reminders days=1 RAILS_ENV=production
```
### logrotate
```
/etc/logrotate.d/redmine
logrotate -d /etc/logrotate.d/redmine
logrotate -f /etc/logrotate.d/redmine
```
```
/var/lib/redmine/log/*log {
  monthly
  missingok
  notifempty
  copytruncate
  compress
}
```


# GitLab
### service
```
gitlab-ctl <start/stop/restart/status/reconfigure>
```
### upgrade
```
gitlab-ctl stop
touch /etc/gitlab/skip-auto-backup
touch /etc/gitlab/skip-unmigrated-data-check
yum install -y gitlab-ce
rm /etc/gitlab/skip-auto-backup
rm /etc/gitlab/skip-unmigrated-data-check
gitlab-ctl start
```
### redmine
```
gpasswd -a apache git
chmod 750 -R /var/opt/gitlab/git-data
```
```
/var/opt/gitlab/git-data/repositories/<GROUP>/<PROJECT>.git
/var/opt/gitlab/git-data/repositories/<@hashed>.git
```
```
https://<SERVER>/sys/fetch_changesets?key=<API_KEY>&id=<PROJECT_ID>
```
### gitlab-rake
```
gitlab-rake gitlab:check
```


# macOS
### Finder
```
defaults write com.apple.finder AppleShowAllFiles TRUE
defaults write com.google.android.studio AppleWindowTabbingMode manual
```
### GateKeeper
```
sudo spctl --master-disable
```
### NVRAM・SMC
```
sudo pmset -a restoredefaults
sudo nvram -c
```
### Kernel Extension
```
sudo kextcache --clear-staging
```
### Keychains
```
security list-keychains
security delete-keychain <KEY>
```
### SSH
```
puttygen xxx.ppk -O private-openssh -o xxx.pem
ssh -i <KEY_PAIR>.pem <USERNAME>@<HOSTNAME> -p <PORT>
```
### Metal3
```
export MTL_HUD_ENABLED=1
```
### Rectangle
```
defaults write com.knollsoft.Rectangle almostMaximizeWidth -float 0.75
defaults write com.knollsoft.Rectangle almostMaximizeHeight -float 1.00
```
### Homebrew
```
brew doctor
```
```
brew deps --installed --tree --1
```
```
brew bundle dump
brew bundle install
```


# Android
### packages
```
adb shell pm list packages -f -3
adb shell dumpsys package <com.package.name>
```
```
adb pull /data/app/<com.package.name>-1/base.apk
```
```
adb push <FILE_PATH> /sdcard/Download/
adb push <DIR_PATH>/. /sdcard/Download/
```
### prop
```
adb shell getprop ro.build.version.release
```
```
adb shell setprop persist.log.tag 0
adb shell setprop persist.log.tag
```
### wifi
```
adb shell ip addr show wlan0
adb shell settings put global captive_portal_mode 0
adb shell settings put global captive_portal_detection_enabled 0
```
### input
```
adb shell input keyevent <KEY_EVENT>
```
### settings
```
adb shell am start -a android.intent.action.MAIN -n com.android.settings/.Settings
```
