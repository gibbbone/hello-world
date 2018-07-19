## Intro 
This is a test markdown file. It has been used to test the command line procedure outlined [here](https://guides.github.com/introduction/git-handbook/). It is loosely based on the previous one here. 

This is the second version of the procedure, hopefully with less errors. It aims to document:

- a full git workflow: 
    - clone
    - branch
    - stage
    - commit
    - push upstream
    - merge
    - delete branch
    - 'ungit' folder
- on a remote repository
- through command line
- including output

## First commit
 Starting from a test folder on Desktop:

    # clone the original repository
    $ git clone https://github.com/giovannibonaccorsi/hello-world
    Cloning into 'hello-world'...
    remote: Counting objects: 46, done.
    remote: Compressing objects: 100% (15/15), done.
    remote: Total 46 (delta 3), reused 5 (delta 1), pack-reused 30
    Unpacking objects: 100% (46/46), done.
    Checking connectivity... done.
    
    # move inside the directory
    $ cd hello-world
    
    # make a new branch and check it 
    $ git branch hello3
    $ git checkout hello3 
    Switched to branch 'hello3'
    
    # ask git what is happeninng
     $ git status
     On branch hello3
     nothing to commit, working directory clean

    # create a new file by copying its previous version
    $ cp file1.md file2.md
    
    # do some file editing stuff
    # remarkable is a markup editor 
    # if you don't want to use it just type 'gedit file2.md'
    $ remarkable file2.md
    
    # here's where the magic happens

We edit the file while git is monitoring. After finishing let's go back to command line:

    # let's ask git again what is happening
    $ git status 
    On branch hello3
    Untracked files:
      (use "git add <file>..." to include in what will be committed)

        file2.md
    
    # stage the file and ask again
    $ git add file2.md
    $ git status
    On branch hello3
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

        new file:   file2.md
    
    $ remarkable file2.md
    
Now after this every change to the file will be tracked. To demonstrate this I've reopened the file and added some lines. Now let's inspect status and commit:
    
    # inspect
    $ git status
    
    # finally commit
    $ git commit -m "adding a new file with new full git procedure"
    $ git push --set-upstream origin hello3

With these I have committed the new file and pushed the results to the original folder. Then I've logged to my Github account, accepted the pull request and merged. Finally I've deleted the branch on Github (not on my local machine, remember this).

## Looking for troubles
     
    # To see which branch are available on remote:
    $ git ls-remote
     
    # To see all my active branches:
    $ git branch --all
    
    
   
After this I've proceeded as before with the first commit: log onto Github, merge the pull request and delete the branch.

## Clean after yourself
Ok, now according to my online reference I was done. The problem is that my previous branch kept showing on my local machine whenever I ran `git status` or `git branch -all`. On the contrary git log showed that merging happened upstream. 

Turns out, kids, that you have to delete your local branch once your finished:

    $ git branch -d hello2

(There's another possibility that the infamous `hello2` branch will keep haunting your dream: a remote reference to it may remain on the remote master hence showing up when you type `git ls-remote`. In this case you have to [prune it](https://stackoverflow.com/questions/5094293/git-remote-branch-deleted-but-still-appears-in-branch-a): `git remote prune origin`)

