# GitHub Overview
Today you will set up a GitHub project to help you track the progress of the development of a piece of software in a repository using Gitflow. 

## `{github_username}`
Whenever you see `{github_username}`, make sure to replace it with your actual GitHub username.

## Setup
- Go to `https://github.com/new` and create a repo named `gitflow-example` in your GitHub account (mark _Add README_).
- Gitflow uses two long lived branches: `main` and `develop`. `main` is created by default, so you need to go to https://github.com/{github_username}/gitflow-example/branches and create a new branch named `develop`.
- Clone the repository in your laptop `git clone https://github.com/{github_username}/gitflow-example.git`

- Move inside the repository `cd gitflow-example`
## Create a GitHub Project
- GitHub Projects is a useful tool for software development management.
- Go to https://github.com/users/{github_username}/projects and create a new project. Select the Kanban template and give it a name like `Gitflow Example`.
## Add an item to the board
- Let's create a new feature: a login for an app.
- In the backlog column of your project, click on _Add item_, name it `Add login` and create a new issue. Choose the `{github_username}/gitflow-example` repository and click on _Blank issue_ when prompted.
- Add a description to the issue like 
```
As a user
I need to log into the app
So that I can adjust my data
```
- Click on `Create` and the issue will appear, with the number 1 assigned most likely.
- Since you're going to start developing it, you can drag it to the _In progress_ column.

## Develop the new feature
- In gitflow, all feature development happens in branches that stem from `develop`.
- Back in your local copy of the repository,
 switch to branch `develop`: `git switch develop`.
- Create and switch to a new branch `feature/login`: `git switch -c feature/login`
- Create the file `login.py` with the following content:
```python
def login(username):
    print(f"Logging in user: {usrname}")  # The typo here is intentional
```
- Stage the changes: `git add login.py`
- Commit the changes: `git commit -m "Add login #1"` (replace #1 with the number your issue got assigned).
- Push your changes to the remote: `git push -u origin feature/login`

## Create a pull request
- When you have some work ready, you typically want to incorporate it into the `develop` branch so it will be merged into `main` in the next release.
- You typically want someone else to review your code before incorporating it into `develop`, so we will create a pull request (PR) for this.
- Go to https://github.com/{github_username}/gitflow-example/pulls and click on _New pull request_
- Select `develop` as the base branch and `feature/login` as the compare branch and click on _Create pull request_.
- On the right hand side panel of the PR, click on the
⚙️ next to Development and add link the issue you created.
- This issue will be closed when the PR approved and the branch is merged.
- You now should go back to the project board and move the item associated with the login feature to the _In review_ column. That way, the rest of your team knows that feature needs to be reviewed.

## Merge feature into develop
- Let's assume that your reviewer was satisfied with your work and approved your PR. Go back to the PR page and merge it.
- Now your changes are in the `develop` branch.
- Move the item associated with the login feature to the _Done_ column.

## Release 1.0.0
- We want to put our changes in `main` so they are available for all the users.
- We need to repeat the steps above in a similar way.
- Create an item in the project board with the name `Release 1.0.0`.
- Create a PR with base branc `main` and compare branch `develop`.
- Have someone review your PR, put `Release v1.0.0` in the _In review_ column.
- Assume your PR was approved, merge `develop` into `main`.
- Move the item associated with the release to the _Done_ column.
- Go to https://github.com/{github_username}/gitflow-example/releases and create a new release with _Tag:_ `v1.0.0` and _Release title_: `Add login functionality`.

## Hotfix
- Oh no! A bug made its way to the main branch. You need to fix it!
- Create an issue in the project board with the name `Hotfix login`. Make sure you keep the information on the board up to date during this process.
- In your local copy of the repository, go to `main`: `git switch main`
- Make sure your local repo is up to date: `git pull`
- Create a branch for the hotfix: `git switch -c hotfix/login`
- Update the file `login.py` with the following content:
```python
def login(username):
    print(f"Logging in user: {username}")  # Typo is now gone
```
- Stage, commit (with an appropriate message) and push your changes to the repo as you did with the feature branch.
- Create a PR with base branch `main` and compare branch `hotfix/login` (there is no time to go through `develop` in this case).
- Have your PR reviewed and approved, and merge your changes into `main`.
- Checkpoint: did you keep the project board up to date the whole time?
- Create a new release with tag `1.0.1` and an appropriate title.
- You saved the day!
- But wait! You're not done yet...

## Update develop after hotfix
- There are changes in `main` that are not yet in `develop`.
You need to merge `hotfix/login` into `develop` too. Create a PR just like before.
- Is the project board up to date?
