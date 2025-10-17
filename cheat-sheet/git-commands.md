---
layout: default
---

## Git
> リポジトリのミラーリング
> ```shell
> git clone --mirror https://<project>.git
> cd <project>
> git lfs fetch --all
> git lfs push --all https://<mirror-project>.git
> git push --mirror https://<mirror-project>.git
> ```

## Git LFS
> シンボリックリンク
> ```shell
> ln -s "$(which git-lfs)" "$(git --exec-path)/git-lfs"
> ```

## GitHub
> SSH接続確認
> ```shell
> ssh -T git@github.com
> ```

## GitLab
> Dockerコンテナ バックアップ
> ```shell
> sudo docker exec -d gitlab-ce gitlab-backup create
> ```

> Tailscale接続
> ```shell
> sudo systemctl enable --now tailscaled
> sudo tailscale up
> tailscale ip -4
> ```

> VPN接続したSMB3ネットワークドライブのマウント
> ```shell
> sudo mount -t cifs //<IP>/<FOLDER> /mnt/<VOLUME_NAME> -o username=<USERID>,password=<PASSWORD>,uid=git,gid=git,file_mode=0640,dir_mode=0700,vers=3.0
> ```

> バックアップパスをマウントしたドライブに変更
> ```shell
> # /etc/gitlab/gitlab.rb
> gitlab_rails['backup_path'] = "/mnt/<VOLUME_NAME>/var/opt/gitlab/backups"
> sudo gitlab-ctl reconfigure
> ```
