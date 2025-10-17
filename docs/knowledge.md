---
layout: page
title: Knowledge
---

## Gitlab

### docker

```shell
sudo docker exec -d gitlab-ce gitlab-backup create
```

```shell
sudo docker exec -it gitlab-ce gitlab-ctl stop puma
sudo docker exec -it gitlab-ce gitlab-ctl stop sidekiq
sudo docker exec -it gitlab-ce gitlab-ctl status
sudo docker exec -it gitlab-ce gitlab-backup restore BACKUP=0000000000_YYYY_MM_DD_VER
```

### rails console

```shell
sudo docker exec -it gitlab-ce gitlab-rails console
```

```ruby
usernames = %w[user1 user2 user3]
users = User.where(username: usernames)

Group.where(parent_id: nil).find_each do |group|
  users.each do |user|
    next if group.members.exists?(user_id: user.id)
    group.add_member(user, Gitlab::Access::DEVELOPER)
    puts "ADDED: #{user.username} -> #{group.full_path}"
  end
end
```

### systemd

```shell
sudo gitlab-ctl stop
sudo systemctl stop gitlab-runsvdir
sudo systemctl disable gitlab-runsvdir
```

```shell
sudo systemctl enable gitlab-runsvdir
sudo systemctl start gitlab-runsvdir
sudo gitlab-ctl start
```
