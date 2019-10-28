![](./img/git.png)

---
### clone
```
git clone https://github.com/<REPOSITORY>
git clone https://<USER>@github.com/<REPOSITORY>
```

### checkout
```
git checkout .
git checkout -b <BRANCH>
git checkout --orphan <BRANCH>
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

### pull
```
git pull --rebase --tags origin <BRANCH>
```

### fetch
```
git fetch --prune --prune-tags
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
git status
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

### filter-branch
```
git filter-branch -f --index-filter "git rm -rf --cached --ignore-unmatch <DIRECTORY>/" --prune-empty -- --all
```

### .git/config
```
[user]
  name = ***
  email = ***
```
```
[user]
  useConfigOnly = true
[includeIf "gitdir/i:C:/home/git/"]
  path = .gitconfig.global
[includeIf "gitdir/i:C:/home/git.hub/"]
  path = .gitconfig.github
```


<br><br>![](./img/redmine.png)

---
### upgrade
```
sudo su -
systemctrl stop httpd
cd /var/lib
unlink redmine
cp -rp redmine-x.x.x-old redmine.x.x.x-new
cd redmine-x.x.x-new
svn update
bundle update
bundle exec rake db:migrate RAILS_ENV=production
bundle exec rake redmine:plugins:migrate RAILS_ENV=production
bundle exec rake tmp:cache:clear RAILS_ENV=production
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


<br><br>![](./img/gitlab.png)

---
### upgrade
```
gitlab-ctl stop
touch /etc/gitlab/skip-auto-backup
yum install -y gitlab-ce
rm /etc/gitlab/skip-auto-backup
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


<br><br>![](./img/mysql.png)

---
### dump
```
mysqldump --single-transaction --quick -u root -h localhost -p --databases <DB_NAME> > <FILE_NAME>
mysql -u root -h localhost -p <DB_NAME> < <FILE_NAME>
```

### login
```
/etc/my.cnf
#skip-grant-tables
#skip-networking
```

### user
```
mysql -u root -p
use mysql;
update user set authentication_string=password("<PASSWORD>") where user='root';
flush privileges;
exit;
```
```
select user, host from mysql.user;
select user(), current_user();
```
```
create user '<USER_NAME>'@'<HOST_NAME>' identified by '<PASSWORD>';
```
```
drop user '<USER_NAME>'@'<HOST_NAME>';
```

### grant
```
show grants for '<USER_NAME>'@'<HOST_NAME>';
```
```
grant all on <DB_NAME>.<TBL_NAME> to '<USER_NAME>'@'<HOST_NAME>' identified by '<PASSWORD>';
flush privileges;
```
```
grant select on *.* to '<USER_NAME>'@'<HOST_NAME>' identified by '<PASSWORD>';
```
```
revoke all on <DB_NAME>.<TBL_NAME> to '<USER_NAME>'@'<HOST_NAME>' identified by '<PASSWORD>';
flush privileges;
```

### database
```
show databases;
show create database <DB_NAME>¥G
```
```
create database <DB_NAME> default character set utf8mb4;
```
```
drop database <DB_NAME>;
```

### table
```
show full tables;
show tables from <DB_NAME>;
show create table <TBL_NAME>¥G
```
```
drop table <TBL_NAME>;
```

### columns
```
show columns from <DB_NAME>.<TBL_NAME>;
select * from <TBL_NAME>;
```


<br><br>![](./img/nodejs.png)

---
### nodebrew
```
nodebrew install-binary stable
nodebrew use <VERSION>
```

### npm
```
npm install -g npm
npm ls -g --depth=0
```


<br><br>![](./img/centos.png)

---
### Patch
```
patch -p1 < <PATCH_NAME>.diff
patch -p1 -R < <PATCH_NAME>.diff
```

### Network Statistics
```
netstat -tlpn
ss -nltup
```

### FireWall
```
firewall-cmd --add-service=mysql --zone=public --permanent
firewall-cmd --list-services --zone=public  --permanent
firewall-cmd --reload
```

### MySQL
```
systemctl start mysqld
systemctl stop mysqld
systemctl restart mysqld
```

### Apache
```
systemctl start httpd
systemctl stop httpd
systemctl restart httpd
```

### GitLab
```
gitlab-ctl start
gitlab-ctl stop
gitlab-ctl restart
gitlab-ctl status
```


<br><br>![](./img/macos.png)

---
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

### HomeBrew
```
brew <cask> install <PACKAGE>
brew <cask> uninstall <PACKAGE>
brew update
brew upgrade
```
```
brew search <PACKAGE>
brwe info <PACKAGE>
brew doctor
brew cleanup
```
```
brew deps --installed --tree --1
```
```
brew bundle --global
brew bundle --global dump
```

### SSH
```
puttygen xxx.ppk -O private-openssh -o xxx.pem
ssh -i <KEY_PAIR>.pem <USERNAME>@<HOSTNAME> -p <PORT>
```

### MySQL
```
mysql.server start
mysql.server stop
```

### FFmpeg
```
ffmpeg -i sample.mp4 -s 1280x720 sample.mp4
ffmpeg -i sample.mov -vf scale=1280:-1 -r 10 sample.gif
```


<br><br>![](./img/windows10.png)

---
### Network Statistics
```
netstat -ano
```


<br><br>![](./img/android.png)

---
### packages
```
adb shell pm list packages | grep <com.package.name>
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

