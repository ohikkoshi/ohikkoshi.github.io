## Git

* **clone**
```
git clone https://github.com/<USER>/<REPOSITORY>
```

* **checkout**
```
git checkout -b <NAME>
git checkout --orphan <NAME>
```

* **branch**
```
git branch -a
git branch -m <OLD_NAME> <NEW_NAME>
git branch -D <NAME>
git push --delete origin <NAME>
```

* **pull**
```
git pull --rebase --tags origin <NAME>
```

* **fetch**
```
git fetch --prune
```

* **merge**
```
git merge --squash <NAME>
```

* **pick**
```
git cherry-pick <ID>
```

* **rebase**
```
git rebase -i HEAD~1
```

* **commit**
```
git add .
git commit -a
git commit --amend
```

* **revert**
```
git revert <ID>
```

* **push**
```
git push origin <NAME>
git push -f origin <NAME>
```

* **log**
```
git status
git log --oneline --graph --branches --decorate
```

* **tag**
```
git tag
git tag <TAG>
git push origin --tags
git tag -d <TAG>
git push --delete origin <TAG>
```

* **.git/config**
```
[user]
  name = ユーザー名
  email = メールアドレス
```
```
[user]
  useConfigOnly = true
[includeIf "gitdir/i:C:/git/"]
  path = .gitconfig.global
[includeIf "gitdir/i:C:/git.hub/"]
  path = .gitconfig.github
```








## Redmine

* **install**

```
sudo su -
bundle install
bundle exec rake db:migrate RAILS_ENV=production
bundle exec rake redmine:plugins:migrate RAILS_ENV=production
```




* **uninstall**

```
bundle exec rake redmine:plugins:migrate NAME=redmine_plugin VERSION=0 RAILS_ENV=production
rm -rf plugins/redmine_plugin
```








## CentOS7

* **httpd**
```
systemctl restart httpd.service
```

* **chXXX**
```
chown -R apache:apache /var/lib/redmine
```

* **apache user**
```
sudo su -s /bin/bash apache
sudo su -s /bin/bash - apache
```

* **user group**
```
gpasswd -a user apache
gpasswd -d user apache
less /etc/group
```








## ADB

* **devices**
```
adb devices
adb -s <DEVICE> <CMD>
```

* **packages**
```
adb install -g -r <FILE_PATH>
adb uninstall <com.package.name>
adb shell pm list packages | grep <com.package.name>
adb pull /data/app/<com.package.name>-1/base.apk
adb push <FILE_PATH> /sdcard/Download/
adb push <DIR_PATH>/. /sdcard/Download/
```

* **wifi**
```
adb shell ip addr show wlan0
adb shell settings put global captive_portal_detection_enabled 0
```

* **input**
```
adb shell input keyevent <KEY_EVENT>
```








## FFmpeg

* **resize**
```
ffmpeg -i movie.mp4 -s 1280x720 movie.mp4
```
