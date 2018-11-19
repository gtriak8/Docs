# K8 Development Documentation

## Configure a User to access server via ssh

1. Generate a rsa key user on his/her development machine
```
ssh-keygen -t rsa
```
> Take note of the .pub file generated and copy its contents

2. Log in to remote server with root or an existing sudoer
If not root:
```
sudo -s
```

3. Create user on server
```
useradd <username>
```

4. Make user a sudoer
```
usermod -aG sudo <username>
```

5. Create a ssh folder on the newly created user's directory

     If the folder is not automatically created, just create one:
```
mkdir /home/<username>
```

```
cd /home/<username>
mkdir .ssh
```

6. Change .ssh folder access permissions
```
chmod 700 .ssh
```

7. Create an authorized_keys files inside the .ssh folder and paste contents of the pub file from the development's machine(see step 1)
```
cd .ssh
vim authorized_keys
```

8. Change access permission of the authorized_keys file
```
chmod 600 authorized_keys
```

9. Change ownership of .ssh dir and its contents for the new user
```
cd /home
chown -R <username>:<username> <username>
```

10. Check that .ssh folder and its contents are owned by the new user and on proper access permissions
```
ls -al
```

11. On the new user's local machine, try to connect to the development server with:
```
ssh <username>@<server_ip>
```

