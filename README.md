# How to Merge the History of Git Repos

Credit: @x-yuri for their great [stackoverflow answer](https://stackoverflow.com/a/62096626)

## Set up project

1. Initialize a git repo in project_a `cd project_a && git init`
1. Make a commit in git `git add -A && git commit -m "Project_a: Initial commit"`
1. Return to root of project `cd ..`
1. Initialize a git repo in project_b `cd project_b && git init`
1. Make a commit in git `git add -A && git commit -am "Project_b: Initial commit"`
1. Return to root of project `cd ..`


## Scenario 1
We want to keep project_b and merge the history of project_a.

### Steps
1. Switch into the repo that you want to keep
```
cd project_b
```

2. Add the git repo from project_a and fetch the remote branch
```
git remote add -f <name> ../project_a
```

3. Merge the history from the remote added in the previous step
```
git merge --allow-unrelated-histories <name>/main
```

4. Remove the remote of the repo you have added
```
git remote remove <name>
```

## Scenario 2
We want to keep project_b and merge the history of project_a into a subdirectory of project_b

### Perquisites
1. Install the git tool [git-filter-repo](https://github.com/newren/git-filter-repo/blob/main/INSTALL.md) from homebrew
```
brew install git-filter-repo
```

### Steps
1. Change the path of the files in the repo that you want to merge into a subdirectory.
    1. Check the current path an view the path of the first line `diff --git a/... b/...`
    ```
    git log --oneline
    git show <commit_id>
    ```
    2. Update the path to what you want
    ```
    git filter-repo --path-rename [old_path]:project_a/
    ```
    3. Verify that the path is what you want `diff --git a/project_a/... b/project_b/...`
    ```
    git log --oneline
    git show <commit_id>
    ```
2. Switch into the repo that you want to keep
```
cd project_b
```

3. Add the git repo from project_a and fetch the remote branch
```
git remote add -f <name> ../project_a
```

4. Merge the history from the remote added in the previous step
```
git merge --allow-unrelated-histories <name>/main
```

5. Remove the remote of the repo you have added
```
git remote remove <name>
```

## Other Helpful Commands

1. `git config --list` or `git config -l` allows you to view the configured remote repos
