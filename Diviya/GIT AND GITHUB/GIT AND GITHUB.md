**What is Git?**

•Git is a version control system.

•It lets you track changes to your code over time.

•You can save snapshots (commits) of your work, go back to previous versions, and collaborate with others without overwriting each other’s changes.

•Git works locally on your computer, so you don’t need the internet to use it (except to sync with others).

•GitHub is a web-based platform that hosts Git repositories. All its core features—branches, commits, pull requests—are based on how Git works.

To track changes, commit code, create branches, and push/pull updates, you need 

Git installed locally. GitHub alone only provides the online interface.

---
**What is GitHub?**

•GitHub is a website (and cloud service) that hosts Git repositories online.

•It makes it easy to share your code, collaborate with others, and manage projects.

•GitHub adds features like issues (for bug tracking), pull requests (to propose code changes), and project management tools.

•You use Git on your computer and then push/pull code to/from GitHub to work with teammates.

    Think of Git as a notebook where you write and save versions of your work, and GitHub as a library where you store and share your notebook with friends.

---
  **(1) 1.Download and Install Git**

You should run these commands after you have installed Git on your computer.

•Git Official Website: [https://git-scm.com/](https://git-scm.com/)

**Standalone Installer: Git for Windows/x64 Setup**

**2.Create a GitHub Account**

•GitHub (for hosting repositories): [https://github.com/](https://github.com/)

(2)3.Open your terminal (Command Prompt, PowerShell, or Terminal) and run:

•git config --global user.name "Your Name"

•git config --global user.email [youremail@example.com](mailto:youremail@example.com)

4.Set Up Authentication for GitHub(optional)

•You may set up SSH keys or use a personal access token for secure access, especially when pushing to GitHub.

---
**• (3). Create a Repository**

###  A **repository** (often called a **repo**) is

A **repository** (often called a **repo**) is simply a **folder or storage space for your project’s files and their history**.

- It keeps all your code, documents, and other files in one place.
- It also tracks every change you make, so you can go back to an earlier version if needed.

**In simple words:**  
A repository is like a special project folder that remembers everything you do to your files.

**A**. On GitHub (Remote Repository)1. Go to [https://github.com/](https://github.com/) and log in.

**2**. Click the **+** icon (top right), then **New repository**.
**3**. Enter a repository name and click **Create repository**.

STEP 4: If you **already have files/folder** you want to upload:(otherwise create folder)

Open your terminal and go to your folder:  

     cd path/to/your/project 

  **2**. Initialize Git in this folder:   

    git init  

The command **`git init`** is used to **create a new Git repository** in your current folder

**3**. Connect your local repo to GitHub (replace with your repo link):   

    git remote add origin https://github.com/yourusername/your-repo.git
---
**• 4. Add, Commit & Push Files**
### **Add**

- `git add` is used to **stage** changes.
- It tells Git which files you want to include in your next commit.
- Example: `git add filename.txt` stages that file.

### **Commit**

- `git commit` is used to **save your staged changes** to the local repository.
- Commits record a snapshot of your project at a point in time, along with a message describing the changes.
- Example: `git commit -m "Add new feature"`

### **Push**

- `git push` is used to **upload your commits** from your local repository to a remote repository (like GitHub).
- This shares your changes with others and backs up your work online.
- Example: `git push origin main`

**Summary:**

- **Add** = select files to save
- **Commit** = save the selected files (with a message)
- **Push** = send your saved changes to GitHub

**• To Upload a Single File:**

•git add filename.txt

•git commit -m "Add filename.txt“

•git push origin main

**•``` To Upload **All Files** in the Folder:**

•git add .

•git commit -m "Add all project files“

•git push origin main
use this incase not push-- git push --set-upstream origin main
---

## 6. Pull Latest Changes from GitHub

To update your local folder with changes from GitHub:

```sh
git pull origin main
```

---
## 7. Branching (Optional, for Advanced Workflows)

- Create and switch to a new branch:
    ```sh
    git checkout -b new-branch-name
    ```
- Switch back to main branch:
    ```sh
    git checkout main
    ```

---

## 8. Common Git Commands Cheat Sheet

| Purpose                           | Command Example              |
| --------------------------------- | ---------------------------- |
| Check status                      | `git status`                 |
| View commit history               | `git log`                    |
| Stage one file                    | `git add filename.txt`       |
| Stage all files                   | `git add .`                  |
| Commit changes                    | `git commit -m "message"`    |
| Push to GitHub                    | `git push origin main`       |
| Pull from GitHub                  | `git pull origin main`       |
| Clone a repo                      | `git clone URL`              |
| New branch                        | `git checkout -b branchname` |
| Switch branch                     | `git checkout branchname`    |
| current branch check              | `git branch`                 |
| to initialize git to folder       | `git init`                   |
| Connect your local repo to GitHub | `git remote add origin URL`  |

---
10. **Tips**

- Always use `git status` to check what’s happening.
- Use clear commit messages.
- You must `git init` before using other Git commands in a new folder.
- `main` is the default branch name (older repos might use `master`).

---
# Full Guide: `git clone` Command

## What is `git clone`?

- `git clone` is used to **download (copy) an existing Git repository** from a remote server (like GitHub) to your local computer.
- It brings all the files, commit history, and branches to your machine, so you can work on the project locally.
	.
---

## When to Use `git clone`?

- When you want to **start working on a project** that already exists on GitHub.
- When you want to **contribute to open-source projects**.
- When you need a **local copy** of a project for learning or backup.

---

## Syntax

```sh
git clone <repository_url>
```

- `<repository_url>` is the link to the repository you want to clone.  
  Example: `https://github.com/username/reponame.git`

---

## Step-by-Step Guide

### 1. Copy the Repository URL

- Open the repository on GitHub.
- Click the green **Code** button, then copy the URL (choose HTTPS for beginners).

### 2. Open Terminal or Command Prompt

- On Windows: You can use Command Prompt, PowerShell, or Git Bash.
- On macOS/Linux: Use Terminal.

### 3. Navigate to the Folder Where You Want to Clone

Example:
```sh
cd Documents/Projects
```

### 4. Run the `git clone` Command

```sh
git clone https://github.com/username/reponame.git
```

### 5. What Happens Next?

- A **new folder** named `reponame` is created in your current directory.
- All files, folders, branches, and commit history are downloaded into this folder.

### 6. Go Into the Project Folder

```sh
cd reponame
```

You can now start editing files, creating branches, and committing changes.

---

## Cloning Options

- **Clone into a specific folder name:**
    ```sh
    git clone <repository_url> myfolder
    ```
    This will put the repo into `myfolder` instead of using the default repo name.

- **Clone with SSH (if you have SSH keys set up):**
    ```sh
    git clone git@github.com:username/reponame.git
    ```

---

## After Cloning: Useful Commands

- **Check remote URL:**
    ```sh
    git remote -v
    ```
- **Pull new changes from GitHub:**
    ```sh
    git pull origin main
    ```
    (Replace `main` with your branch name if needed.)

- **Create a new branch:**
    ```sh
    git checkout -b feature-branch
    ```

---

## Common Errors

- **Authentication failed:**  
  - Make sure you copied the correct URL.
  - If using HTTPS, you may be asked for your GitHub username and a personal access token.

- **Repository not found:**  
  - Check that the username and repo name are correct.
  - Make sure the repo is public or you have access if it’s private.

---

## Summary Table

| Step   | Action                                           | Example Command                                      |
|--------|--------------------------------------------------|------------------------------------------------------|
| 1      | Copy repo URL from GitHub                        | (via browser)                                        |
| 2      | Go to your working directory                     | `cd path/to/folder`                                  |
| 3      | Clone the repo                                   | `git clone https://github.com/user/repo.git`         |
| 4      | Enter the cloned folder                          | `cd repo`                                            |
| 5      | Pull updates in future                           | `git pull origin main`                               |

---

## Pro Tips

- You only need to `git clone` **once**. After that, use `git pull` to get updates.
- You can have multiple cloned repositories on your computer.
- Use `ls` (Linux/macOS) or `dir` (Windows) to list files and confirm cloning was successful.

---

**You are now ready to use `git clone` to work with any GitHub project!**