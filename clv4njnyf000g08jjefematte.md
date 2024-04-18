---
title: "KodeKloud Engineer task: Create a user in Linux"
datePublished: Thu Apr 18 2024 02:58:31 GMT+0000 (Coordinated Universal Time)
cuid: clv4njnyf000g08jjefematte
slug: kodekloud-engineer-task-create-a-user-in-linux-1
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1713409071960/af23ac9b-6cfa-4c79-af48-c4079fa24e3b.png

---

# ***Step 1: Connect to the App Server***

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