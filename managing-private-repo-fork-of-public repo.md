# How to sync code between the public repo and a private fork. #
Taken from [Stack Thread](http://stackoverflow.com/questions/10065526/github-how-to-make-a-fork-of-public-repository-private)

First, duplicate the repo as others said (details here):
Create a new repo (let's call it private-repo) via the Github UI. Then:

```shell
# Make a "Bare" Clone the public repo
git clone --bare https://github.com/exampleuser/public-repo.git

# Enter the repo
cd public-repo.git

# Push the public as a mirror to your private repo
git push --mirror https://github.com/yourname/private-repo.git

# Step up a folder 
cd ..

# Delete the copy of the public repo
rm -rf public-repo.git

# Clone the private repo so you can work on it:
git clone https://github.com/yourname/private-repo.git

# Enter your clone
cd private-repo

# Make some changes
git commit3/17/2016 10:38:27 AM 
git push origin master
```

# To pull new hotness from the public repo:

```shell
# Enter the Private Repo
cd private-repo

# Remote add public??
git remote add public https://github.com/exampleuser/public-repo.git

# Creates a merge commit
git pull public master 

# Push
git push origin master
```

Awesome, your private repo now has the latest code from the public repo plus your changes.

Finally, to create a pull request private repo -> public repo:

The only way to create a pull request is to have push access to the public repo. This is because you need to push to a branch there ([here's why](http://stackoverflow.com/questions/14821583/pull-request-without-forking)).
```
git clone https://github.com/exampleuser/public-repo.git
cd public-repo
git remote add private_repo_yourname https://github.com/yourname/private-repo.git
git checkout -b pull_request_yourname
git pull private_repo_yourname master
git push origin pull_request_yourname
```
Now simply create a pull request via the Github UI for public-repo, as described [here](https://help.github.com/articles/creating-a-pull-request/).

Once project owners reviewed your pull request, they can merge it.

Of course the whole process can be repeated (just leave out the steps where you add remotes).