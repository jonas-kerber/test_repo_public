# test_repo_public
testing a workflow with a public main branch and private develop branch


## How this was set up
To set this up I did the following steps

- Created a public and private repository on Github
- Followed this [this](https://docs.github.com/en/repositories/creating-and-managing-repositories/duplicating-a-repository) to dulicate the repository
- in private repo I renamed the branch `main` to `main-private` and added a branch `develop`
- cloned private repo locally
- `git branch main`to create a branch locally
- `git remote add public <PUBLIC_REPO>.git` to add a remote named `public` with the address of the public repo
- made first public commit with `git push --set-upstream public main`
- -> now all commits from `main` branch will automatically go the public repo instead of the private

## Workflows
Development is done in 3 steps.

* 1. Regular development on `develop` branch (private repo)
* 2. Updating `main` once a working version is achieved 
    * 2.1 `develop` is merged in branch `main-private` in the private repo (this step is not necessary but allows a sanity check for beginner git users)
    * 2.2 After a successful sanity check, `main-private` is merged into `main` and pushed to the public repo

In this workflow you only commit to develop and should not commit to any other branches (if you decide to do so you have to merge any commits to made to `main`/`main private` to `develop` before you continue working on `develop` to prevent possible merge conflicts)
### 1. Developing on branch `develop`
This describes your normal workflow when your are writing new code
1.  `git checkout develop` to make sure you are on branch develop
2. `git commit` to commit your changes (`git add <CHANGED_FILE>` first)
3. `git push` to commit to your private repository

### 2. Updating the public repo with the changes
Steps 1-4 are optional for beginner git users to provide a sanity check before making changes public. If you don't need this start directly at step 5
1. `git checkout main-private` to change branch
2. `git merge develop` to pull in change from develop
3. `git push`to update branch `main-private` in private repo
4.  Go to your private repo on github.com and check if your commit history etc. looks ready for public release.
5. `git checkout main` to change branch
6. `git merge main-private` to update main (`git merge develop` if you skipped 1-4)
7. `git push` to update the public repo
