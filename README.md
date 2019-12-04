# Git Command

This article would share the experience for git command while using.

Following the below steps, I hope it would also help you to get more and more familiar with git.



## $ git clone

Below would introduce 2 different ways to clone the remote repositories.

### 1. Clone with HTTPS

You can clone any open-source repositories into your local workspace directly without any checking.

![image-20191204173857551](D:\Workspace\git-command-guide\images\image-20191204173857551.png)

![](D:\Workspace\git-command-guide\images\image-20191204152322646.png)

Check the folder where you used 'Git Bash Here', you successfully cloned the remote repository into your local drive.

**For further, you would find you have no right to commit or push to the origin/xxx. **

### 2. Clone with SSH

Let's try this command directly.

![image-20191204153416233](D:\Workspace\git-command-guide\images\image-20191204153416233.png)

Check the note, it pops '**Permission denied**' due to you don't have the public SSH key.

#### 2.1 Generate SSH Key

Generate your own SSH key and add to your GitHub account.

```bash
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

arguments:

- -t: key type (dsa | ecdsa | ed25519 | rsa)
- -b: bits (recommend 2048 or 4096, higher is safer)
- -C: comment (e.g.: email address...)

for more detail, you can use the below command to check all the meanings of arguments.

```bash
$ ssh-keygen help
```

![image-20191204171611847](D:\Workspace\git-command-guide\images\image-20191204171611847.png)

After ran the generating script, you would see:

![image-20191204172503296](D:\Workspace\git-command-guide\images\image-20191204172503296.png)

#### 2.2 Adding your SSH key to the ssh-agent

1. Ensure the ssh-agent is running:

   ```bash
   # start the ssh-agent in the background
   $ eval $(ssh-agent -s)
   > Agent pid 59566
   ```

2. Add your SSH private key to the ssh-agent:

   ```bash
   $ ssh-add ~/.ssh/id_rsa
   ```

#### 2.3 Adding a new SSH key to your GitHub account

I would pass the step, please follow the below official guide.

#### 2.4 Official Guide

Please refer to the official guide from: [here](https://help.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh)





#### 

