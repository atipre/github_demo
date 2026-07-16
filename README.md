# GitHub Demo Repo

This repo is a simple walkthrough for teaching someone how Git and GitHub work.
It is designed to be used live: paste the commands in order, pause after each
section, and explain what changed.

## Big Picture

Git is the version control tool on your computer.

GitHub is a website that stores Git repositories online and makes collaboration
easier.

A repository, or repo, is a project folder whose history is tracked by Git.

A commit is a saved checkpoint.

A branch is a separate line of work.

A remote is a copy of the repo hosted somewhere else, usually GitHub.

`git push` uploads your commits to GitHub.

`git pull` downloads commits from GitHub.

## 1. Check Your Setup

Run these commands to confirm Git is installed and your identity is configured.

```bash
git --version
git config --global user.name
git config --global user.email
```

If name or email are blank, set them:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

## 2. Create Or Enter A Project Folder

If you are starting from scratch:

```bash
mkdir github-demo
cd github-demo
```

If you are already inside this repo, check where you are:

```bash
pwd
ls
```

## 3. Initialize Git

This turns the current folder into a Git repository.

```bash
git init
```

Check the repo status:

```bash
git status
```

Concept: `git status` is the command you run constantly. It tells you what Git
sees, what changed, and what is ready to commit.

## 4. Create A File

Create a small file:

```bash
echo "Hello from Git" > hello.txt
```

Check what changed:

```bash
git status
```

Concept: Git notices the file, but it has not been saved into history yet.

## 5. Stage Changes With `git add`

Stage one file:

```bash
git add hello.txt
git status
```

Concept: staging means "include this change in the next commit."

You can stage everything changed in the repo with:

```bash
git add .
```

## 6. Commit A Checkpoint

Create the first commit:

```bash
git commit -m "Add hello file"
```

View the history:

```bash
git log --oneline
```

Concept: a commit is a named checkpoint. It stores the staged changes plus a
message explaining why the change exists.

## 7. Make Another Change

Append a second line:

```bash
echo "This is my second line" >> hello.txt
git status
git diff
```

Concept: `git diff` shows the exact unstaged edits.

Stage and commit it:

```bash
git add hello.txt
git commit -m "Add second line"
git log --oneline
```

## 8. Create And Use A Branch

Create a new branch:

```bash
git checkout -b feature/add-notes
```

Concept: a branch lets you work on an idea without changing the main line of
work until you are ready.

Make a file on the branch:

```bash
echo "Notes from a feature branch" > notes.txt
git add notes.txt
git commit -m "Add notes"
```

List branches:

```bash
git branch
```

Switch back to the main branch:

```bash
git checkout main
```

If your default branch is called `master`, use this instead:

```bash
git checkout master
```

Notice that `notes.txt` disappears when you leave the branch:

```bash
ls
```

Switch back to the feature branch:

```bash
git checkout feature/add-notes
ls
```

## 9. Merge A Branch

Go back to the main branch:

```bash
git checkout main
```

If your default branch is called `master`, use:

```bash
git checkout master
```

Merge the feature branch:

```bash
git merge feature/add-notes
```

Concept: merging brings the commits from one branch into another branch.

Check the result:

```bash
ls
git log --oneline --graph --all
```

## 10. Connect To GitHub

Create an empty repo on GitHub first.

Do not initialize it with a README, license, or `.gitignore` for this demo.

Then connect your local repo to GitHub. Replace `YOUR-USERNAME` and
`YOUR-REPO-NAME`.

```bash
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO-NAME.git
git remote -v
```

Concept: `origin` is the common nickname for your GitHub copy of the repo.

## 11. Push To GitHub

Upload your local commits:

```bash
git push -u origin main
```

If your default branch is called `master`, use:

```bash
git push -u origin master
```

Concept: `push` sends commits from your computer to GitHub. The `-u` option
remembers the connection so future pushes can be shorter.

After the first push, you can usually run:

```bash
git push
```

## 12. Pull From GitHub

To demonstrate `pull`, edit a file directly on GitHub:

1. Open the repo on GitHub.
2. Open `hello.txt`.
3. Click the pencil edit button.
4. Add one line.
5. Commit the change on GitHub.

Then download that change locally:

```bash
git pull
cat hello.txt
```

Concept: `pull` fetches new commits from GitHub and merges them into your
current branch.

## 13. Clone A Repo

Cloning makes a local copy of a GitHub repo.

Move somewhere outside this folder, then run:

```bash
cd ..
git clone https://github.com/YOUR-USERNAME/YOUR-REPO-NAME.git cloned-demo
cd cloned-demo
ls
git log --oneline
```

Concept: `clone` is how a collaborator gets their own copy of a repo.

## 14. Show A Common Collaboration Flow

Create a new branch:

```bash
git checkout -b feature/change-greeting
```

Make a change:

```bash
echo "A collaborator added this line" >> hello.txt
git add hello.txt
git commit -m "Update greeting"
```

Push the branch:

```bash
git push -u origin feature/change-greeting
```

Concept: teams usually push branches, open pull requests on GitHub, review the
change, then merge it into `main`.

## 15. Undo And Inspect

Show changed files:

```bash
git status
```

Show recent commits:

```bash
git log --oneline --decorate --graph --all
```

Show branch names:

```bash
git branch
```

Show remote connections:

```bash
git remote -v
```

Unstage a file that was added by mistake:

```bash
git restore --staged hello.txt
```

Discard local edits to a file:

```bash
git restore hello.txt
```

Concept: be careful with discard commands. They remove local work that has not
been committed.

## Command Cheat Sheet

```bash
git init                         # Start tracking a folder with Git
git status                       # See what changed
git add FILE                     # Stage one file
git add .                        # Stage all changed files
git commit -m "Message"          # Save staged changes
git log --oneline                # Show commit history
git diff                         # Show unstaged changes
git checkout -b BRANCH           # Create and switch to a branch
git checkout BRANCH              # Switch branches
git branch                       # List branches
git merge BRANCH                 # Merge a branch into the current branch
git remote add origin URL        # Connect local repo to GitHub
git push -u origin main          # First push to GitHub
git push                         # Push after upstream is set
git pull                         # Download and merge GitHub changes
git clone URL                    # Copy a GitHub repo locally
```

## Teaching Script

Use this order for a clean live demo:

1. Explain Git versus GitHub.
2. Run `git init`.
3. Create `hello.txt`.
4. Run `git status`.
5. Run `git add hello.txt`.
6. Run `git commit -m "Add hello file"`.
7. Make a second change and show `git diff`.
8. Create a branch with `git checkout -b`.
9. Commit on the branch.
10. Switch back and merge.
11. Create an empty GitHub repo.
12. Add the remote.
13. Push.
14. Edit on GitHub.
15. Pull locally.
16. Clone into a second folder to show how collaborators start.

