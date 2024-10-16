# Introduction to Git and Working with Git

## **1\. Introduction to Git**

Git is the most widely used version control system in the world. It is essential for tracking changes to code and collaborating on projects with others. In this lesson, we will cover what Git is, how it works, and how to get started using Git to manage your projects effectively.

By the end of this lesson, you will understand:

- What Git is and why it's important.
- How to install and configure Git.
- How to use basic Git commands to track and manage changes.
- How to work with Git's branching and merging functionality for collaboration.

---

## **2\. What is Git?**

Git is a distributed version control system that tracks changes in your project files. It allows multiple developers to collaborate on the same project without overwriting each other's work. Here are some key features of Git:

- **Version Control**: Git records the history of changes, allowing you to revert to previous versions of your project.
- **Collaboration**: Multiple team members can work on different parts of the project simultaneously.
- **Distributed System**: Every developer has a full copy of the repository, including its history, allowing work to continue even when offline.
- **Efficiency**: Git handles branching and merging quickly, making it highly effective for large projects.

Git enables you to manage your project's code efficiently and ensures that team members can collaborate effectively without losing any code or progress.

## **3\. Installing and Configuring Git**

To get started with Git, you need to install it on your computer. Instead of following different steps for each operating system, you can download Git directly from the official website:

1.  Go to <https://git-scm.com/downloads>.
2.  Select your operating system (Windows, macOS, Linux, or others).
3.  Follow the installation instructions provided for your specific platform.

Once installed, open a terminal (Command Prompt on Windows or Terminal on macOS/Linux) and configure Git with your name and email, which will be attached to your commits.

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Real Example

```bash
git config --global user.name "Diego Zito"
git config --global user.email diegozito@gmail.com
```

Set your preferred text editor (e.g., Visual Studio Code) for writing commit messages:

```bash
git config --global core.editor "code --wait"
```

Finally, check your configuration to ensure everything is set up:

```bash
git config --list
```

---

## **4\. Basic Git Commands**

Understanding Git commands is essential for managing your project effectively. We'll explore each command, focusing on what it does and why it's important in your Git workflow.

For a complete list of commands covered in this lesson, refer to the `git-commands.md file`, where you’ll find examples and detailed explanations of each command we’ll use throughout the course.

If you ever need more information on a specific command, you can use `git help <command>` to display full documentation, or `git -h` for a shorter, more concise version of the command options and usage.

```bash
git help
```

or

```bash
git -h
```

Throughout this lesson, you’ll notice that many Git commands come with optional flags, like `-m` for providing a commit message, don't worry we will get into ddetails of that later.

The most important concept to understand about these flags; is that they offer additional functionality and flexibility, so be prepared to encounter and use them frequently as we dive deeper into Git's features.

---

## **5\. Git Workflow and the Staging Area**

Git follows a specific workflow to help manage changes:

1.  **Working Directory**: Where you make changes to your files.
2.  **Staging Area**: A space where changes are prepared before they are committed. You can think of it as a "draft" of changes you want to save.
3.  **Repository**: The saved history of your project, where committed changes are stored. Github would be where you store this repository online for easier version-control and collaboration.

<h1 align="center">
  <a href="">
    <img src="./assets/imgs/workflow.png" alt="Workflow">
  </a>
</h1>

The basic Git workflow looks like this:

1.  **Make Changes**: Modify files in your working directory.
2.  **Stage Changes**: Add the files you want to commit to the staging area using `git add`.
3.  **Commit Changes**: Commit your staged changes to the repository using `git commit`.
4.  **Push Changes**: Send your committed changes to a remote repository (like GitHub or GitLab) using git push. This makes your updates available to others or backs them up to the remote server.

For example:

```bash
git add <filename>
git commit -m "Describe what changed"
git push origin [name of branch]
```

Real example by applying changes to the `README.md` file:

```bash
git add README.md
git commit -m "update - expanded content of the readme file"
git push origin main
```

You can use logical expression combinators to write everything in 1 line for us OCD types

```bash
git add README.md && git commit -m "update - expanded content of the readme file" && git push origin main
```

The staging area gives you control over what goes into each commit, allowing you to review your changes and commit only those you are confident in.

---

## **6\. Branching and Merging**

One of Git's most powerful features is branching, which allows you to work on separate versions of your project simultaneously.

- **Branch**: A parallel version of your project. By default, every Git repository has a branch called `main` or `master`. You can create new branches to work on features or bug fixes without affecting the main codebase.

```bash
  git branch <branch-name>
```

- **Switching to a branch**: To work on a branch, use the `git checkout` or `git switch` command.

```bash
  git switch <branch-name>
```

- **Creating and Switching to a New Branch**: To create a new branch and switch to it in one step, use the git checkout -b command. This is helpful when you want to start working on a feature or bug fix in a separate branch without affecting the main branch.

  For example, This command creates a new branch called `fixBug01` and immediately switches to it, so you can start working in that branch right away.

```bash
  git checkout -b fixBug01
```

- **Merging**: Once you're done working on a branch, you can merge it back into the branch that is considered the `main` or `master` branch of your project. This incorporates your changes into the main project.

  - First, you need to switch to the branch where you want to merge the changes from the branch you were working. Let's say we want to incorporate the changes form the branch `bugFix01` into the `main` branch.

    ```bash
    git switch main
    ```

  - Now that you're on the main branch, use the git merge command to merge bugFix01 into main.

    ```bash
    git merge bugFix01
    ```

- **Resolving Conflicts**: If multiple people make changes to the same file on different branches, Git may produce a conflict during the merge. You will need to resolve the conflicting parts manually, and then commit the resolved changes.

When conflicts arise, Git marks the conflicting sections in the file. You can then manually edit these sections, stage the file, and commit the resolution.

- Scenario: **Resolving a Conflict Between `main` and `bugFix01` Branches**

  1.  **You're working on the `main` branch** and make changes to `example01.md`. You add some new content related to a feature you're working on.

  2.  **Create and switch to the `bugFix01` branch** to fix a bug. While on this branch, you modify the same file, `example01.md`, to address a bug found in the project.

  3.  **Switch back to the `main` branch** and make further changes to the same file, focusing on enhancing the feature.

  4.  **Attempt to merge `bugFix01` into `main`**. During the merge, Git identifies a conflict because both branches modified the same lines in `example01.md`.

  5.  **Open `example01.md`** and notice that Git has added conflict markers to highlight the differing sections from each branch. The sections from the `main` branch are marked separately from the changes made in `bugFix01`.

  6.  **Resolve the conflict manually** by deciding which changes to keep. You can choose to keep one branch's changes, combine both, or modify the content to integrate both sets of updates.

  7.  **Stage the resolved file** to let Git know that you've resolved the conflict.

  8.  **Commit the merge** to finalize the process and successfully combine the changes from both `main` and `bugFix01`.

  9.  **Verify the merge** by checking the status of your repository to ensure that everything has been properly merged.

---

## **7\. Avoiding Big Files, Folders, or Sensitive Files from Git**

In many projects, there are files and directories that shouldn't be tracked by version control, either because they are too large, irrelevant, or contain sensitive information. Git provides a way to handle this through the `.gitignore` file.

- **What it does**: The `.gitignore` file specifies which files and directories should be excluded from version control. By listing these files in `.gitignore`, Git will not track, stage, or commit them.

- **Why it's beneficial**: In most projects, there are files that do not need to be versioned, such as log files, build artifacts, large binaries, or sensitive configuration files. These files can unnecessarily bloat your repository, slow down performance, or expose sensitive information. Using `.gitignore` helps maintain a clean and efficient repository by avoiding irrelevant files.

- **How it works**: In the `.gitignore` file, you simply list the files or patterns for the files and folders you want Git to ignore. The file can contain:

  - Specific file names
  - File extensions
  - Directory names
  - Wildcard patterns to ignore multiple files with similar characteristics

#### **Examples of Common `.gitignore` Entries**:

1.  **Ignore specific files**:

    - `README.md` - This will ignore the specific file `README.md` in the repository. You can add any specific file name to exclude it from being tracked.

2.  **Ignore all files with a specific extension**:

    - `*.html` - This will ignore all HTML files in the repository, regardless of their name (e.g., `index.html`, `about.html`).

3.  **Ignore specific folders**:

    - `/images/` - This will ignore the entire `images` folder and its contents, useful if you don't want to track media or image assets.

4.  **Ignore `.env` files**:

    - `.env` - Useful for excluding sensitive environment configuration files that contain API keys, database credentials, etc.

5.  **Ignore temporary files generated by macOS**:

    - `.DS_Store` - `.DS_Store` is a system file created by macOS, often unnecessary and not needed in version control.

- **Practical Use**: When working in teams, `.gitignore` ensures that each contributor keeps their local environment-specific files out of the shared repository, reducing the chances of unnecessary merge conflicts or accidentally committing private information.

- **Additional Resources**: You can find various `.gitignore` templates for different programming languages and environments on GitHub's official repository here: [GitHub Gitignore Templates](https://github.com/github/gitignore).

---

## **8\. Conclusion**

In this lesson, you've learned the basics of Git, including what Git is, how it works, and how to install and configure it. You've also learned how to execute core Git commands, manage your project workflow, and work with branches for collaboration.

By mastering these fundamentals, you'll be well on your way to using Git effectively in your software development projects.
