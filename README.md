# Guide for Your First Repository

This article would share the experience for setting up your first repository by 2 types of cloning methods, Https and SSH-Key. And how to share the remote repositories to your friends or colleagues.

(For following this article, you need to create your remote repository in GitHub first.)



## Contents





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

![image-20191204205138761](/images/image-20191204205138761.png)

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




## 3. Push to Remote Repository (Team)

Here I want to share a really good method to push your code from local to remote repository while you are developing in a **team**. 

**Optimal Situation (No Changes in Remote Branch):**

**3.1~>3.6~>3.7~>3.8**

**General Situation (Changed in Remote Branch without Conflict):**

**3.1~>3.2~>3.3~>3.4~>3.6~>3.7~>3.8**

**Worst Situation (Changed in Remote Branch with Conflict):**

**3.1~>3.2~>3.3~>3.4~>3.5~>3.6~>3.7~>3.8**



### 3.1 $ git pull (first time)

Remember, every time you wanna push your code to the remote branch, please always pull first!

```bash
$ git pull
```

If there is no conflict file, it would pull successfully and please just go to watch 3.6.

Or you will see below message: "Please commit your changes or stash them before you merge."

![image-20191204200439027](/images/image-20191204200439027.png)

Here I suggest you use stash to solve the conflict rather than commit. If you choose commit, it is actually a commit-merge action and sometimes would cause override other one's commit. For using stash could minimalize the cost while solving conflict. It is just like, you are always doing the develop based on the latest version of this branch.

### 3.2 $ git stash

This command would help to stash your changes into a liked buffer area. You can also check your revised file and all of your changes are gone. Do not be afraid, your changes are still existing.

```bash
$ git stash
```

![image-20191204202340471](/images/image-20191204202340471.png)

### 3.3 $ git pull (second time)

After stashing your local changes, now your local repository is in a clean version since your last pull request. Based on it, we can easily pull the latest version of this branch.

```bash
$ git pull
```

![image-20191204202728538](/images/image-20191204202728538.png)

### 3.4 $ git stash pop

For now, it's time to recover our changes to the branch.

```bash
$ git stash pop
```

If there is no conflict, or it means that you and your teammates didn't make any change on one same file. Then you can just follow the step .

Or unfortunately, there are one or more conflicting files, then you need to solve the conflict(s) manually. Please go to 3.5.

### 3.5 Resolve Conflict

Checked the conflicted file, you would find some symbols like "<<<<<<", they are conflicting area. Please solve the conflict carefully.

![image-20191204203510626](/images/image-20191204203510626.png)

### 3.6 $ git add

After resolving the conflict, you could just add~>commit~>push to the remote branch.

```bash
$ git add --all
```

### 3.7 $ git commit

```bash
$ git commit -m "your remark"
```

### 3.8 $ git push

```bash
$ git push
```
