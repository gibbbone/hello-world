## Intro 
This is a test markdown file. It has been used to test the command line procedure outlined [here](https://guides.github.com/introduction/git-handbook/).

This is the first command line procedure I've used  with git. It started with the idea of creating a file detailing git procedures, then I've made errors and I've decided to detail them. 

## First commit
Here's the code I've actually used. Starting from a test folder on Desktop:

    # clone the original repository
    $ git clone https://github.com/giovannibonaccorsi/hello-world
    
    # move inside the directory
    $ cd hello-world
    
    # make a new branch and check it 
    $ git branch hello2
    $ git checkout hello2 

    # create a new file and write on it
    $ gedit file1.md
    
    # do some file editing stuff

After exiting the editor. I've provided the following commands: 

    $ git add file1.md
    $ git commit -m "adding a new file and testing markdown"
    $ git push --set-upstream origin hello2

With these I have committed the new file and pushed the results to the original folder. Then I've logged to my Github account, accepted the pull request and merged. Finally I've deleted the branch on Github (not on my local machine, remember this).

## Looking for troubles
Now my new file was synced with the original folder and added. Obviously all the stuff you see written after the `gedit file1.md` command was missing.

Here comes the fun. To add new changes to my file I ran:

    $ git pull

Which resulted in:

    remote: Counting objects: 1, done.
    remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
    Unpacking objects: 100% (1/1), done.
    From https://github.com/giovannibonaccorsi/hello-world
    c9b5ca3..66088c3  master     -> origin/master
    Your configuration specifies to merge with the ref 'refs/heads/hello2'
    from the remote, but no such ref was fetched.

That was unexpected, from my point of view. Turns out that I was doing things wrong (which is obvious since I was poking things randomly) and I was trying to pull a branch which I had just deleted. More info can be found [here](https://stackoverflow.com/questions/36984371/your-configuration-specifies-to-merge-with-the-branch-name-from-the-remote-bu) 

What I learned to do instead is:

    # Check always:
    $ git status
     
    # To see which branch are available on remote:
    $ git ls-remote
     
    # To see all my active branches:
    $ git branch --all
    
    
## Accidentally deleting things

I decided to go on and break some other stuff. I wanted to add the last 30 commands I had typed to my  file. So I tried:
    
    $ history 30 > file1.md

The problem is that this command cancels preexisting content from the file. What instead I needed was to append the content with the `>>` pipe. 

Panic: now my original file was erased. Lucky me that I've just started to use version control, am I right? *How this stuff works?* 

First failed attempt to solve the issue (again poking things without a clue):
    
    $ git push --set-upstream origin hello2
    
Then an hint from the command line:
    
    $ git checkout --file1.md

Et voilà back to square one with the original file.

## Second commit
Ok,after having broken enough stuff better finish our trip:

* I added the last 35 typed commands with the  `>>` pipe. 
* [By filtering out the line numbering](https://stackoverflow.com/questions/7110119/bash-history-without-line-numbers) 
* Then I commited and pushed upstream

  
    $ history 35 | cut -c 8- >> file1.md
    $ git add file1.md
    $ git commit -m "adding content to file with new adventures in gitland"
    $ git push --set-upstream origin hello2
    
After this I've proceeded as before with the first commit: log onto Github, merge the pull request and delete the branch.

## Clean after yourself
Ok, now according to my online reference I was done. The problem is that my previous branch kept showing on my local machine whenever I ran `git status` or `git branch -all`. On the contrary git log showed that merging happened upstream. 

Turns out, kids, that you have to delete your local branch once your finished:

    $ git branch -d hello2

(There's another possibility that the infamous `hello2` branch will keep haunting your dream: a remote reference to it may remain on the remote master hence showing up when you type `git ls-remote`. In this case you have to [prune it](https://stackoverflow.com/questions/5094293/git-remote-branch-deleted-but-still-appears-in-branch-a): `git remote prune origin`)

