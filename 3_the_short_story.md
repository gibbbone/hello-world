## Full git procedure
No output, no explanations, no bullshit.

```bash    
# clone the original repository
$ git clone https://github.com/giovannibonaccorsi/hello-world
	    
# move inside the directory
$ cd hello-world

# make a new branch and check it 
$ git branch hello3
$ git checkout hello3 

# make a change
$ cp file1.md file2.md

# add some random stuff
$ echo "Git is like an old marriage: commit early, commit often. And never forget to leave a message." >> file2.md

# stage the file 
$ git add file2.md

# finally commit
$ git commit -m "Added new test file."

# switch to master
$ git checkout master

# merge master with new updated branch
$ git merge hello3

# push upstream the master folder. Here you'll need username+password
$ git push

# delete used branch
$ git branch -d hello3

# optionally:  git push origin --delete hello3

# delete git folder to stop git
$ rm -rf .git/
```     
