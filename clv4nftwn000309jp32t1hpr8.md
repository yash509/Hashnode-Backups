---
title: "KodeKloud Engineer task: Create a user in Linux"
datePublished: Thu Apr 18 2024 02:55:32 GMT+0000 (Coordinated Universal Time)
cuid: clv4nftwn000309jp32t1hpr8
slug: kodekloud-engineer-task-create-a-user-in-linux
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1713408852231/9ca77d8b-fe19-43fe-9d80-c891aa40c5e1.png
tags: linux, task, system-admin, kodekloud, kodekloudengineer

---

# *Step 1: Connect to the App Server*

```powershell
ssh app_server_username@server_name

# example
ssh tony@stapp01
```

# *Step 2: Switch to root User*

```powershell
sudo su
```

# *Step 3: Add the asked user, set the user UID as asked, and set the directory where the user will be created*

```powershell
useradd -m user_name -u UID -d directory_path

# example
useradd -m anita -u 1026 -d /var/www/anita
```

# *Step 4: Verify the User*

```powershell
cat /etc/passwd | grep -i user_name

# example
cat /etc/passwd | grep -i anita
```

Congratulation! you've successfully completed the very first Task!!! 🎉