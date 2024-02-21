---
description: Import your existing Git branches to treat them as virtual branches
---

# 🎋 Remote Branches

GitButler's virtual branches are stored in a different format than Git's normal branches, but we still need to work with them, especially when it comes to remote branches.

For instance, when a coworker pushes a new branch to the server and opens a pull request, GitButler will automatically see it when it does a background fetch, which is every few minutes.

We will show these new remote branches in this sidebar.

<figure><img src="../../.gitbook/assets/CleanShot 2023-11-30 at 17.24.49@2x.png" alt=""><figcaption><p>Remote branches will show up here automatically.</p></figcaption></figure>

### Applying Remote Branches

Remote branches cannot be applied like virtual branches, we need to convert them to the more rich virtual branch data structure first. To do this, just click on a branch to see the "Apply" button.

<figure><img src="../../.gitbook/assets/CleanShot 2023-11-30 at 17.26.46@2x.png" alt=""><figcaption><p>Click Apply to add this remote branch to your list of applied branches and pull it's changes into your working directory.</p></figcaption></figure>

Clicking the "apply" button will turn that remote branch into a tracked virtual branch (sort of like `git checkout -b branch-name origin/branch-name`) and will immediately try to apply it to your working directory as an applied virtual branch. If it can't do so cleanly, it will simply store it as an unapplied virtual branch that you can try to apply later.



