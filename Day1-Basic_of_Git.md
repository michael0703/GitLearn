# GitLearn
This is a tutorial for Git learn 

---

### What is Git?
There are many answers, but I will say that it is a Distributed Version Control Systems(which is also the most normal answer).
**So, Let's started!**

---
### Basics
#### What is a repository?
Think of it as a databases, but a magic one! It can help you control your working directory, keep track of the file changed, maintain all the version of your project. 

- How to make a repository?
    
    ```
    $ cd workproject
    $ git init      
    ```             
    ![](https://i.imgur.com/yZ2NpCE.png)
    
- What's is in **.git** directory?
    ![](https://i.imgur.com/HCONfpZ.png)

We will learn about some file in this picture later, now lets move on.

#### The component of the **Git System**

- blob : while git **only concerns about the content of the file**, every times git notice any changes of the file content, it will generate a **object** and **store this change only(instead of all files copy)**.

Example:
```
$ echo "hello world" > helloworld.txt
$ git add helloworld.txt                   # let git notice the change
```
and then we can check the **.git/objects** directory, and can see there is a new directory, and there is a new file in it, this is the file we just add : helloworld.txt
![](https://i.imgur.com/9MADUFl.png)
We can check by
```
$ git cat-file -p {dir_name(2)}{file name(38)}
$ git cat-file -p 3b18e512dba79e4c8300dd08aeb37f8e728b8dad
    
hello world    
```    
If we changed the content of existed file, it will also save the changed content and create a new object.
```
$ echo "hello git" >> helloworld.txt
$ git add helloworld.txt
$ git cat-file -p 08082ed01dd8bb293e4566f1fdd03bfdd0662bb3

hello world
hello git
```
---
- tree : Git uses a simpler file system to store all the file content(included changes) with **blob** and **tree** object, think of tree as a directory and blob as a file.

Example:
![](https://i.imgur.com/E8D1GmB.png)

---
- commit : To understand what is commit, let's first look at the structure of out local directory and repository.

![](https://i.imgur.com/0VKUlVs.png)
(ignore the checkout arrow, we will talk about that later)


when we add a new file or modify some files, git **wont care about them**, git will not record what content you add or modify, it will only tell you that these files(or contents) are currently not been tracked.

so here comes `git add {file_name}`, through `git add`, we put the files into staging area, and when the files are in staging area, git will create blob for these files(even if we didn't commit)

After we finally finish our changes or want to save the version, we finally put all the contents in staging area.We need to store all the content(blob) state, and maintain a **pointer points to this state.**

```
$ git commit -m "first commit"
```
![](https://i.imgur.com/wkQxpCh.png)

**Commit is ONLY a file contains the structure(tree object) of the state of the directory.**
```
$ git cat-file -p 5684169
tree 0f552a12c505f23b5b4734d1471aab08685d83bf
author michael <b05902059@ntu.edu.tw> 1564150933 +0800
committer michael <b05902059@ntu.edu.tw> 1564150933 +0800

first commit
```
we can see that the "5684169" commit only store the sha1 of the tree. And this tree stores all the blob and other tree(if exists).
```
$ git cat-file -p 0f552a12c505f23b5b4734d1471aab08685d83bf
100644 blob 8d0e41234f24b6da002d962a26c2495ea16a425f	git.txt
100644 blob b79fb18b6f21eb76783a91bfb696628ca14468f6	helloworld.txt
```
---
- So far, we have known that every content in repository is a blob or tree objects. And a **commit** is simply a file stores the current state of the repository with pointer points to tree and blob.
![](https://i.imgur.com/Xe8S5BN.png)
(green:blob, orange:tree, red:commit)





