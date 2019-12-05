# Practical Guide for Git

This is not an advanced but really practical guide of git for the developer who has already grasped some basic knowledge and skill for git. It would almost satisfy for your common development.

(i.e.: For following below steps, you need to create your remote repository in GitHub first.)



According to this article, you might get:

1. How to set up your first repository by Https or SSH-Key

2. How to share the remote repositories to your friends or colleagues

3. Use stash-commit rather than commit-merge (Recommended for Team Cooperation)

4. Create branch, switch branch and merge from other branch

5. Rollback your added request, your committed request and even push request



## Contents

Pending...



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




## 3. Stash-Commit

For personal use, you can ignore this phase. But if you are working within a group or team, you would be better to try stash-commit. Do not think it is more complicated, it would actually help you to reduce the cost for resolving conflict, it would be more efficient!

**Optimal Situation (No Changes in Remote Branch):**

3.1~>3.6~>3.7~>3.8

**General Situation (Changed in Remote Branch without Conflict):**

3.1~>3.2~>3.3~>3.4~>3.6~>3.7~>3.8

**Worst Situation (Changed in Remote Branch with Conflict):**

3.1~>3.2~>3.3~>3.4~>3.5~>3.6~>3.7~>3.8

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



## 4. Create, Switch and Merge New Branch

### 4.1 Create New Branch

```bash
$ git branch uat
```

### 4.2 Switch to Other Branch

```bash
$ git checkout uat
```

### 4.3 Push the New Branch to Remote Repository

You need to do a push command to remote repository, then the new branch would be effective to others.

While you are pushing, it would remind you to use below command to push (just follow the notes) :

```bash
$ git push --set-upstream origin uat
```

### 4.4 Merge from New/Old Branch

```bash
$ git merge --no-ff uat
```

With `--no-ff`, create a merge commit in all cases, even when the merge could instead be resolved as a fast-forward.

![image-20191205115731977](/images/image-20191205115731977.png)

Check the history, you would see a merged record by "**--no-ff**":

![image-20191205115937448](/images/image-20191205115937448.png)

## 5. Rollback (Add, Commit and Push)

While working, we might wrongly add, commit or push some files. Then we need to know how to rollback them.

Here we have some new and some changed files.

![image-20191205174505275](/images/image-20191205174505275.png)

### 5.1 Rollback Add Request

Add them all:

```bash
$ git add -A
```

![image-20191205174551926](/images/image-20191205174551926.png)

And you can easily find the note, "**(use "git restore --staged <file>..." to unstage)**". Let's just follow the note and rollback them.

```bash
$ git restore --staged *
```

![image-20191205174836453](/images/image-20191205174836453.png)

### 5.2 Rollback Commit Request

Let's add them back then commit them and check the current status.

![image-20191205175518842](D:\Workspace\practical-guide-for-git\images\image-20191205175518842.png)

We can use below command to rollback committed request:

```bash
$ git reset --mixed head^
```

![image-20191205175719462](/images/image-20191205175719462.png)

Now they are become unstaged and untracked files again. **And actually, the command could also apply on rollback added request.**

For the above command:

```bash
$ git reset [--soft | --mixed [-N] | --hard | --merge | --keep] [-q] [<commit>]
```

[mode]

***

**--soft**
Does not touch the index file or the working tree at all (but resets the head to <commit>, just like all modes do). This leaves all your changed files "Changes to be committed", as git status would put it.

**--mixed**
Resets the index but not the working tree (i.e., the changed files are preserved but not marked for commit) and reports what has not been updated. This is the default action.

If -N is specified, removed paths are marked as intent-to-add (see git-add(1)).

**--hard**
Resets the index and working tree. Any changes to tracked files in the working tree since <commit> are discarded.

[commit]

***

**Head^**

Rewind the branch to the last commit

**Head~3**

Rewind the branch to get rid of those 3 commits.

**commit-id**

Rewind the branch to one specific commit

For further information, you could use below command,

```bash
$ git reset --help
```

### 5.3 Rollback Pushed Request

Please push to the remote branch carefully and avoid doing this step frequently.

Firstly, let's push a commit for test.



 
