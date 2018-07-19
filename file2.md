## Intro 
This is a test markdown file. It has been used to test the command line procedure outlined [here](https://guides.github.com/introduction/git-handbook/). It is loosely based on [the previous version](https://github.com/giovannibonaccorsi/hello-world/blob/master/file1.md).

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
    
Now after the first `add` new changes won't be tracked: if we check git status we see that our file has now a controlled version (the one before modiying it) and an unstaged version (the one after). To avoid this duplication, we must add again the file to obtain a unique one. After that we can commit :
    
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

We have now two strategies.

#### Push upstream, merge remotely, then pull locally
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

Then log in Github, create a pull request and after that merge if no conflicts arises. This will show in the log as a merge from an (external) pull request. 

Now if we want our local master to be in sync with the remote one we can type:

	$ git pull

#### Merge locally, then push upstream 
Merge with master locally then push everything remotely

	$ git checkout master
	Switched to branch 'master'
	Your branch is up-to-date with 'origin/master'.

	$ git merge hello3
	Updating 02d564e..066f2db
	Fast-forward
	 file2.md | 75 +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++--------
	 1 file changed, 67 insertions(+), 8 deletions(-)

	# This will require the password (skipped the output)
	$ git push
	....
	
After this both local and remote master should be on the same page:

	$ git pull
	Already up-to-date.

## Clean after yourself
FInally, if the branch is no long needed, delete it both locally and remotely:

	$ git branch -d hello3
	Deleted branch hello3 (was 02d564e).
	
	$  git push origin --delete hello3
	Username for 'https://github.com': giovannibonaccorsi
	Password for 'https://giovannibonaccorsi@github.com':
	To https://github.com/giovannibonaccorsi/hello-world
	 - [deleted]         hello3

If we want  we can stop tracking by deleting the .git folder on our machine with:
 
	$ rm -rf .git/
     
