This is a test markdown file. It has been used to test the command line procedure outlined [here](https://guides.github.com/introduction/git-handbook/).

The code I've actually used to create it is the following. Starting from a test folder on Desktop:

    # clone the original repository
    $git clone https://github.com/giovannibonaccorsi/hello-world
    
    # move inside the directory
    $cd hello-world
    
    # make a new branch and check it 
    $git branch hello2
    $git checkout hello2 

    # create a new file and write on it
    $gedit file1.md

After exiting the editor. I've provided the following commands: 

    $git add file1.md
    $git commit -m "adding a new file and testing markdown"
    $git push --set-upstream origin hello2

With these I have committed the new file and pushed the results to the original folder.Then I've logged to my Github account, accepted the pull request and merged. Finally I've deleted the branch.

Now new my file was synced with the original folder and added. Obviously all the stuff you see written after the `gedit file1.md` command was missing.

Here comes the fun. To add new changes to my file I ran

    $git pull

Which resulted in:

    remote: Counting objects: 1, done.
    remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
    Unpacking objects: 100% (1/1), done.
    From https://github.com/giovannibonaccorsi/hello-world
    c9b5ca3..66088c3  master     -> origin/master
    Your configuration specifies to merge with the ref 'refs/heads/hello2'
    from the remote, but no such ref was fetched.

That was unexpected, from my point of view. Turns out that I was doing things wrong and I was trying to pull a branch which I had just deleted. More info can be found [here](https://stackoverflow.com/questions/36984371/your-configuration-specifies-to-merge-with-the-branch-name-from-the-remote-bu) What I learned to do instead is:

To see which branch are available on remote:
    git ls-remote
To see all my active branches:
    git branch --all
To check always:
    git status

Finally I decided to go on and break some other stuff. I wanted to add the last 30 commands I had typed to this file. So I tried:
    history 30 > file1.md

The problem is that this command cancel preexisting content from the file. What instead I needed was to append the content with the `>>` pipe, now my original file was erased. Panic. Lucky me that I've just started to use version control, am I right? How this stuff work? 

First failed attempt:
    git push --set-upstream origin hello2
Then an hint from the command line:
    git checkout -- file1.md

Et voilà back to square one with the original file.

Finally: let's add the last 35 commands and filter out the line numbering:
    history 35 | cut -c 8- >> file1.md


