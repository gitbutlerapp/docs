---
description: Import your existing Git branches to treat them as virtual branches
---

# 🎋 Remote Branches

GitButler's virtual branches are stored in a different format than Git's normal branches, but we still need to work with them, especially when it comes to remote branches.

For instance, when a coworker pushes a new branch to the server and opens a pull request, GitButler will automatically see it when it does a background fetch, which is every few minutes.

We will show these new remote branches in this sidebar.

<div align="center">

<figure><img src="../../.gitbook/assets/CleanShot 2024-06-03 at 16.58.10@2x.png" alt=""><figcaption><p><em>Remote branches will show up here automatically.</em></p></figcaption></figure>

</div>

## Applying Remote Branches

Remote branches cannot be applied like virtual branches, we need to convert them to the more rich virtual branch data structure first. To do this, just click on a branch to see the "Apply" button.

<div align="center">

<figure><img src="../../../.gitbook/assets/CleanShot 2023-11-30 at 17.26.46@2x.png" alt=""><figcaption><p><em>Click Apply to add this remote branch to your list of applied branches and pull it's changes into your working directory.</em></p></figcaption></figure>

</div>

Clicking the "apply" button will turn that remote branch into a tracked virtual branch (sort of like `git checkout -b branch-name origin/branch-name`) and will immediately try to apply it to your working directory as an applied virtual branch. If it can't do so cleanly, it will simply store it as an unapplied virtual branch that you can try to apply later.
