## Intro 
This is a test markdown file. It has been used to test the command line procedure outlined [here](https://guides.github.com/introduction/git-handbook/). It is loosely based on the previous one here. 

This is the second version of the procedure, hopefully with less errors. It aims to document:

- a full git workflow: 
    - clone
    - branch
    - stage
    - commit
    - merge
    - push upstream
    - delete local and remote branches 
    - 'ungit' folder
- on a remote repository
- through command line
- including output

## Init
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

## First commit
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
    
Now after the first `add` new changes won't be tracked: if we check git status we see that our file has now a controlled version (the one before modiying it) and an unstaged version (the one after). To avoid this duplication, we must add again the file to obtain a unque one. After that we can commit :
    
    # inspect
    $ git status
    On branch hello3
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

        new file:   file2.md

    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
        (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   file2.md

    # add again
    git add file2.md
    
    # check
    $ git status
    On branch hello3
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

        new file:   file2.md

    # finally commit
    $ git commit -m "Added new file with full procedure without errors"
    [hello3 02d564e] Added new file with full procedure without errors
     1 file changed, 106 insertions(+)
     create mode 100644 file2.md


## Pushing
After commiting we have now a branch which is ahead of master in our local directory and a remote master where no changes have been recorded. 

We have now two strategies

### Push upstream, then pull locally
Push to the remote folder:

	$ git push --set-upstream origin hello3
	Username for 'https://github.com': giovannibonaccorsi
	Password for 'https://giovannibonaccorsi@github.com':
	Counting objects: 3, done.
	Delta compression using up to 8 threads.
	Compressing objects: 100% (3/3), done.
	Writing objects: 100% (3/3), 1.93 KiB | 0 bytes/s, done.
	Total 3 (delta 0), reused 0 (delta 0)
	To https://github.com/giovannibonaccorsi/hello-world	
	 * [new branch]      hello3 -> hello3
	Branch hello3 set up to track remote branch hello3 from origin.

then log in Github, create a pull request and after that merge if no conflicts arises.

FInally if the branch is no long needed delete it both locally and remotely. 

	$ git branch -d hello3
	Deleted branch hello3 (was 02d564e).
	$  git push origin --delete hello3
	Username for 'https://github.com': giovannibonaccorsi
	Password for 'https://giovannibonaccorsi@github.com':
	To https://github.com/giovannibonaccorsi/hello-world
	 - [deleted]         hello3

Now master remote is up to date while master local is not. If we want we can update it with `git pull` otherwise we can stop tracking by deleting the .git folder on our machine with ` rm -rf .git/`

## Merge locally, then push upstream 

     
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

