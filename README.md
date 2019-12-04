# Guide for Your First Repository

This article would share the experience for setting up your first repository by 2 types of cloning methods, Https and SSH-Key. And how to share the remote repositories to your friends or colleagues.

(For following this article, you need to create your remote repository in GitHub first.)

## 1. $ git clone

Below would introduce 2 different ways to clone the remote repositories.

### 1.1 Clone with HTTPS

You can clone any open-source repositories into your local workspace directly without any checking.

![image-20191204173857551](/images/image-20191204173857551.png)

![image-20191204152322646](/images/image-20191204152322646.png)

Check the folder where you used 'Git Bash Here', you successfully cloned the remote repository into your local drive.

**For further, you would find you have no right to commit or push to the origin/xxx. It would pop a window and ask you to login with the GitHub account. After login successfully, then you can use git commands to work.**

### 1.2 Clone with SSH

Let's try this command directly.

![image-20191204153416233](/images/image-20191204153416233.png)

Check the note, it poped '**Permission denied**' due to you don't have the public SSH key.

#### 1.2.1 Generate SSH Key

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

![image-20191204171611847](/images/image-20191204171611847.png)

After ran the generating script, you would see:

![image-20191204172503296](/images/image-20191204172503296.png)

#### 1.2.2 Adding your SSH key to the ssh-agent

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

#### 1.2.3 Adding a new SSH key to your GitHub account

Please refer to the official guide from: [adding-a-new-ssh-key-to-your-github-account](https://help.github.com/en/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account)



## 2. Build a work group 

### 2.1 By HTTPS

If you want your friends to be your collaborators, you can go to setting and add your friend in. Once he/she wanna do some commands, he/she just needs to login with his/her account.

![image-20191204180211034](/images/image-20191204180211034.png)

### 2.2 By SSH-Keys

Please refer to the official guide: [Git-on-the-Server-Setting-Up-the-Server](https://git-scm.com/book/en/v2/Git-on-the-Server-Setting-Up-the-Server)
