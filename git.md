# Git
Links:
- Cheat sheet: https://github.com/trufa/git-cheatsheet
- Git Reference: http://gitref.org/index.html
- Play this: https://github.com/Gazler/githug
- 中文教程: [史上最浅显易懂的Git教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000) and [猴子都能懂的GIT入门](http://backlogtool.com/git-guide/cn/)


Topics:
- How to Fork boilerplate to other branch, see examples from: https://github.com/koistya/react-static-boilerplate/tree/master

## Common comands

```bash
# merge from staging
git merge origin/staging
```

## Custom bash function

```bash
# add this to .zshrc

# usage: newUS sprint15/US-12345
function newUS() {
  git checkout -b feature/$1 --no-track origin/staging
}

# create PR on bitbucket from current branch to feature/paycard-staging
# you should publish the branch first: git push -u first
function newPR() {
  branch_name="$(git symbolic-ref HEAD 2>/dev/null)"
  open "https://bitbucket.com/sourceBranch=${branch_name}&targetRepoId=6565" 
}
```


## Tips: merge base when you have changes already commited locally

```bash
git reset --soft "HEAD^"
git stash
git merge origin/feature/paycard-staging
git stash apply
git add .
git commit
```

## Alias Command
~/.gitconfig
```
[alias]
    ac = !git add -A && git commit -am
    s = status
```
