---
description: >-
  Work on several branches at the same time, committing and stashing them
  independently and simultaneously.
---

# 🌳 Virtual Branches

The main feature of GitButler currently is our virtual branch functionality. Here is a quick video showing off some of what you can do when being able to work on multiple branches at the same time.

<div align="center">
  <a href="https://www.youtube.com/watch?v=MRcmnUwrP8A">
    <img src="https://img.youtube.com/vi/MRcmnUwrP8A/0.jpg" alt="Youtube Video Titled 'Intro to Virtual Branches'">
  </a>
</div>

Virtual branches are just like normal Git branches, except that you can work on several of them at the same time.

<div align="center">
  <figure>
    <img src="../../../.gitbook/assets/CleanShot 2023-11-30 at 16.25.19@2x.png" alt="">
    <figcaption>
      <p><i>An example of working on two branches at the same time, while pending upstream changes wait for you to merge them.</i></p>
    </figcaption>
  </figure>
</div>

{% hint style="warning" %}
You cannot use both GitButler virtual branches and normal Git branching commands at the same time, you will have to "commit" to one approach or the other.
{% endhint %}

The reason is that stock Git can only handle one branch at a time, it does not have tooling to use or understand multiple, so most commands having to do with the index or HEAD or branching (`commit`, `branch`, `checkout`, etc) may behave unexpectedly. Most importantly, do not use normal Git commit tooling or other GUIs.&#x20;

{% hint style="info" %}
To understand why and how to get out of this, please read our [integration-branch.md](integration-branch.md) docs.
{% endhint %}

## Base Branch

With virtual branches, you are not working off of local main or master branches. Everything that you do is on a virtual branch, automatically.&#x20;

Similar to GitHub, where you specify a default branch to use to merge your Pull Requests into by default, GitButler requires a "Base Branch". This is understood to be whatever your concept of "production" is. Typically what represents deployed, production code that cannot or should not be rolled back. Generally this would be something like `origin/master` or `origin/main`.

Once a base branch is specified, everything in your working directory that differs from it is branched code and must belong to a virtual branch.

This means that you don't have to create a new branch when you want to start working, you simply start working and then change the branch name later. There is no local "main" or "master" because it doesn't make sense. Everything is a branch, with work that is meant to eventually be integrated into your base branch.

## Virtual Branches

You can easily work in a single branch at a time, but GitButler can handle several virtual branches at the same time. If you have 3 different changes in one file, you can drag each of the changes to a different virtual branch lane and commit and push them independently.

Each virtual branch is kept in a vertical lane, similar to a kanban board, and every file and difference is similar to a card that you can drag between the lanes until they are committed there.

Each time you commit on a virtual branch, GitButler calculates what that branch would have looked like if the changes you dragged onto it were the only things in your working directory and commits a file tree that looks like that. If you push that commit and inspect it on GitHub (or whatever upstream service you use to collaborate), it should look like that was the only change you made, even though you could potentially still have multiple branches applied in your working directory.

## Applying and Unapplying Branches

Since there isn't just a single branch you can be on, you don't "switch" branches, which implies replacement. You simply "apply" branches, which takes whatever changes they represent and adds them to your working directory. If you don't want those changes in your working directory anymore, you can "unapply" them, which removes only those changes.

Each of these actions is as simple as checking or unchecking a box next to the branch name.

<div align="center">
  <figure>
    <img src="../../../.gitbook/assets/CleanShot 2023-11-30 at 16.26.58@2x.png" alt="" width="375">
    <figcaption>
      <p><i>Click "unapply" for any branch to stash it and remove it's changes from the working directory</i></p>
    </figcaption>
  </figure>
</div>

To delete a virtual branch, you simply unapply it, then left click on it and choose "delete".

## Merging Upstream

Eventually you will have work merged into the branch you chose as your base branch, which will need to be reconciled with all your virtual branches to keep them up to date with where they will eventually need to merge into.

<div align="center">
  <figure>
    <img src="../../../.gitbook/assets/CleanShot 2023-11-30 at 16.46.58@2x.png" alt="">
    <figcaption>
      <p><i>Click "Merge into common base" to integrate upstream changes into your virtual branches.</i></p>
    </figcaption>
  </figure>
</div>

Upstream work will automatically be shown in your sidebar in the "Trunk" section. When you click "Merge into common base" (or the "Update" button next to your "Applied Branches" section), we will attempt to integrate that work with your existing virtual branches. Each branch, applied or unapplied, will try to be updated with the new work.

{% hint style="info" %}
We will attempt to rebase any commits in your virtual branches on top of new work (similar to running a `git pull --rebase` on each branch).
However, if you already have commits in your branch, we have to create a merge commit to get them up to date.
{% endhint %}

If we cannot update a branch because of merge conflicts, we will unapply the branch automatically and leave it in an unmerged state. You can identify these branches with the blue dot next to them in your branch listing.

If a virtual branch is entirely integrated into upstream, it will be removed and deleted when those changes are integrated. So you can just keep a virtual branch applied locally until it is integrated and it will go away automatically.

## Conflicting Branches

You cannot have conflicting branches applied at the same time. Any virtual branch that conflicts with branches that are currently applied will be noted you cannot apply them until you have unapplied the branch or branches they conflict with.

## Merge Conflicts

If a virtual branch does have a conflict with your upstream branch and is in a blue dot state, you can fix it by applying it. Applying a conflicting branch will first un-apply all existing virtual branches, then put the merge conflict markers into your working directory and mark conflicted files for you.

<div align="center">
  <figure>
    <img src="../../../.gitbook/assets/CleanShot 2023-07-24 at 15.38.30@2x.png" alt="" width="375">
    <figcaption>
      <p><i>Files in a conflicted state</i></p>
    </figcaption>
  </figure>
</div>

You will need to resolve each file that is marked, then click "Resolve" under each one. Once all files are resolved, you need to commit to create the merge commit that resolves it. Now it is up to date and can be unapplied or applied again easily.

While you are in a conflicted state, you cannot apply or unapply any other branches.

## The End

That is our general overview of how Virtual Branches works. We've found that it's way easier and faster than constantly switching back and forth between branches, managing branches all the time, and all the other overhead that comes with branching in Git, while still being able to easily create pull requests and integrate features.
