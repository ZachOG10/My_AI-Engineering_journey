## Dev Environment

## Your tools shape your thinking, set them up once, set them up right.

## AI environment has four layers:
1. system foundation
- os,shell,editor,git, GPU drivers
2. program managers
-uv,pnpm,cargo,juliaup
3. language runtimes
- python 3.11+,node20+,Rust,Julia
4. Ai/ML libraries
- PyTorch, JAX

## Git and collaboration

- Initial setup: Configure your identity
Before making your first commit, Git needs to know who you are. This ensures your contributions are properly credited. Open your terminal and run the following commands, substituting your actual name and email:

- Bash: 
git config --global user.name "Your Full Name"
git config --global user.email "your.email@example.com"

# To verify set up:
* Run "git config --list" to check that your settings were saved correctly.

## The daily work flow: Add, Commit, and Push

Version control revolves around three core steps. Think of it like taking snapshots of your project as it evolves.
1. git status: Always check where you stand before making changes. It shows
which files are modified or untracked.
2. git add <filename> (or git add . this adds all the files in the curent directory): Stages your changes, preparing them to be saved. This moves files from your working directory to the staging area.
3. git commit -m "Descriptive message": Takes a snapshot of your staged changes and saves it permanently to your local history. Tip: Write clear, concise commit messages (e.g., git commit -m "Add data preprocessing script").
4. git push: Uploads your local commits to a remote repository (like GitHub) so your work is safely backed up in the cloud.

## Keeping Your Repo Clean: The .gitignore File

When working on machine learning or coding projects, you generate massive files—like model checkpoints (.pt, .h5, .weights), virtual environments (venv/), and logs—that do not belong in version control.

Create a file named .gitignore in your project root directory and list the files or folders you want Git to ignore:
# Ignore Python virtual environments
venv/
__pycache__/

# Ignore large machine learning model checkpoints and data
*.pt
*.h5
*.weights
data/

# Ignore system files
.DS_Store

## Branching & Merging: Safe Experimentation

Working directly on the main branch can be dangerous when trying out new, untested ideas. Branches let you create an isolated copy of your code to experiment freely.
# Create and switch to a new branch:
- git checkout -b feature/experiment-model

# Switch back to main:
- git checkout main

# Merge your changes back into main: Once your experiment works and you're ready to integrate it:
- git checkout main
- git merge feature/experiment-model 

# Three things to remember:
- Save often (git commit)
- Push to remote (git push)
- Branch for experiments (git checkout -b experiment)

## Term 	What people say 	What it actually means
- Commit 	"Saving" 	A snapshot of your entire project at a point in time
- Branch 	"A copy" 	A pointer to a commit that moves forward as you work
- Merge 	"Combining code" 	Taking changes from one branch and applying them to another
- Remote 	"The cloud" 	A copy of your repo hosted somewhere else (GitHub, GitLab)

## APIs and KEYS:
- Every AI API works the same way: sends requast, recieves a response. The details change, the pattern doesn't.

# Every API call has:
- An endpoint (URL)
- An API key (authentication)
- A request body (what you want)
- A response body (what you get back)

## 