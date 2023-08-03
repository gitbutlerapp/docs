---
description: Import your existing Git branches to treat them as virtual branches
---

# 🎋 Remote Branches

GitButler's virtual branches are stored in a different format than Git's normal branches, but we still need to work with them, especially when it comes to remote branches.

For instance, when a coworker pushes a new branch to the server and opens a pull request, GitButler will automatically see it when it does a background fetch, which is every few minutes.

We will show these new remote branches in this sidebar.

<figure><img src="../../.gitbook/assets/CleanShot 2023-08-02 at 13.43.32@2x.png" alt=""><figcaption><p>Your remote (and also legacy local) Git branches</p></figcaption></figure>

### Applying Remote Branches

Remote branches cannot be applied like virtual branches, we need to convert them to the more rich virtual branch data structure first. To do this, just left (secondary) click on a branch to see the "Apply" button.

&#x20;

<figure><img src="../../.gitbook/assets/CleanShot 2023-08-02 at 13.46.16@2x.png" alt="" width="327"><figcaption></figcaption></figure>

Clicking the "apply" button will turn that remote branch into a tracked virtual branch (sort of like `git checkout -b branch-name origin/branch-name`) and will immediately try to apply it to your working directory as an applied virtual branch. If it can't do so cleanly, it will simply store it as an unapplied virtual branch that you can try to apply later.

### Ahead/Behind

You may also notice some numbers like `2/4` next to the branch name. This is the ahead/behind data, so 2/4 would mean that this branch has 2 commits on it that are not on your base branch (something like `origin/master`) and 4 commits behind (ie, `origin/master` has four commits on it that this branch does not have).

