## Modify Admin account name on Mac


#### Implications
> 🛑 Before changing your account name and (or) home directory with this approach you must understand that,
> - Account name or home directory used anywhere in configuration of installations i.e. SSH host configuration or keys etc. will not going to be updated automatically.
> - Stored preferences of your softwares using your older accout name or home directory will not understand the changes automatically. i.e. VPN, IDEs
> - You are giving a new ***identity*** to your current account.

> So, if you are *sure* with this, only then I would recommend you to go with this option.

> One more safer option is to use aliases instead of going for this hacky way where you can create multiple aliases of your account and use them for your convinience. However, this will not be able to help when you work with shell, it will display the account name all the time.

#### Modify the account name, with a temporary admin

Actually, I was not really happy with the account name of my Mac, as it was my email address (`.` and `@` characters removed) previously. Since this account name is used at multiple places including the home directory name, it was bit annoying for me to see the email everytime I open my terminal, whenever I do list files and folders etc.

I wanted to change the account name but as it seems to be disabled I thought it won't be possible to change it any way. But I found one tricky way which worked for me and I was able to modify this account name easily without loosing my most of user settings.

If you don't want to retain whatever installations and preferences your current account hold, you can simply create a new admin account and start using it instead.

But if you don't want to loose your user settings, you can follow below steps.

- Login to your admin account
- Create a new admin account, Go to `System Preferences > Users & Groups`, click on lock at the bottom and enter password, then click on plus icon at the bottom of user list.

![Screenshot 2022-03-06 at 8.45.18 AM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1646538210278/DN65Wjffe.png)

![Screenshot 2022-03-06 at 8.48.18 AM.png.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1646538664258/Yn13VMTMu.png)

- Logout and Login to this newly created account
- Modify the account name of your actual admin user, Go to `System Preferences > Users & Groups`, click the lock at the bottom and enter password, right click on user and open `Advanced Options`, you will find the account name field is editable.

![Screenshot 2022-03-06 at 8.45.33 AM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1646538792610/J1rsU6tWz.png)

- Restart your system
- Login to your actual admin user
- Delete the temporary admin

#### **Modify the home directory**

Better to rename the home directory as well along with the account if you want to keep them in sync. However, better to have a ***back up*** before modifying the home directory, although you don't need temporary admin account for that you can do it from the same account. 

> Note that your user home will have all user settings and preferences which we do not loose during such change.

- Create new directory in parallel to your home directory with the name you want for your home
- Copy all files and folders from old home directory to new directory
- Go to `System Preferences > Users & Groups`, click the lock at the bottom and enter password, right click on user and open `Advanced Options`.
- Modify home directory
- Restart the system

> 🤔 Since my system was quite new and was having minimal configurations, it was easier for me to do these changes. Better to avoid such modifications if your system is heavily loaded with installations and configurations. 




