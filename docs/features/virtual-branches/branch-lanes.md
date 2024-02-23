---
description: How do you manage your virtual branches?
---

# 🔱 Branch Lanes

The main interface for Virtual Branches are a series of branch lanes. Each lane represents a scope of work that is different than what your current base branch (ie, `origin/master`) looks like. Work that is not yet in production.

This could be a local virtual branch that you're working on, or it could be a virtual branch that was created from a remote branch.

The interface looks something like this:

<div align="center">
  <figure>
    <img src="../../../.gitbook/assets/CleanShot 2023-11-30 at 16.23.30@2x.png" alt="">
    <figcaption><p><i>An example of working on two branches at the same time, while pending upstream changes wait for you to merge them.</i></p></figcaption>
  </figure>
</div>

## The Sidebar

The sidebar on the left shows you the stashed virtual branches that you have and the "other" branches that you have available (legacy git branches, remote branches and PRs). All of these branches can be converted into virtual branches by clicking them and then clicking the "Apply" button on the branch view.

### Trunk

The "Trunk" is the view of the base branch that you've set. It will show you essentially a `git log` of `origin/master` or whatever you set as your base branch, and it will show you if there are any commits upstream that you have not integrated locally yet. We will automatically check for new upstream changes every few minutes, but you can also click the update button to check immediately.

<div align="center">
  <figure>
    <img src="../../../.gitbook/assets/CleanShot 2023-11-30 at 17.07.10@2x.png" alt="">
    <figcaption><p><i>A screenshot showcasing the explaination above.</i></p></figcaption>
  </figure>
</div>

### Applied Branches

Clicking this will give you the list of applied virtual branches that are in your working directory. It is the main view you will be working in.

### Other Branches

Underneath that, we list the "remote" branches that you have. This is a list of Git branches that are ahead of your base branch commit (they have commits on them that your base branch does not have), and can be converted into a virtual branch.

Technically we also list local Git branches here that you may have been working on before using GitButler, so that you can convert them into virtual branches, but mostly this should be coworkers branches on your remote Git server.

### Stashed Branches

The next part shows "Stashed branches", which are the virtual branches that you have available but unapplied. You can click on them to view a preview and then click "Apply" to apply them. This is where virtual branches go when you unapply them.

## Applied Virtual Branches Lanes

When you click on "Applied Branches", you will see your main view, which is a list of the virtual branches that are currently applied into your working directory.

<div align="center">
  <figure>
    <img src="../../../.gitbook/assets/CleanShot 2023-11-30 at 17.12.07@2x.png" alt="">
    <figcaption>
      <p><i>Here we have two virtual branches. The first one has a PR open, local work that is not pushed and local work that is not committed.</i></p>
    </figcaption>
  </figure>
</div>

For each virtual branch lane, there is a list of uncommitted work and committed work. If there is uncommitted work, can type a commit message and commit it locally.

If you are logged in, you can also use our AI helper to generate your commit message automatically from the diffs of your in progress work by clicking the "Generate Message" button.

You can drag the uncommitted files from one lane to another in order to separate the work. You can also drag hunks from within files if you want to split up work in one file into multiple branches.

You can inspect any file change that is uncommitted by clicking on the file path. GitButler will expand a inspector to the right to show you the diff. If you are logged in, our AI system will try to summarize the work in each hunk as well.

<div align="center">
  <figure>
    <img src="../../../.gitbook/assets/CleanShot 2023-11-30 at 17.14.04@2x.png" alt="">
    <figcaption>
      <p><i>Inspecting our file change</i></p>
    </figcaption>
  </figure>
</div>

Once you have committed work, you will see it at the bottom as a list of commits under a tag that indicates that they are local. If you hit the "Push" button, it will attempt to push these commits to the same remote server that your base branch is on.

If you have authenticated to GitHub, you also have the option to create a Pull Request for that branch automatically.

Any further commits will be marked as local until you push them.

### Undoing Commits

You can always undo your last commit by hitting the "Undo" button on the commit.

<div align="center">
  <figure>
    <img src="../../../.gitbook/assets/CleanShot 2023-11-30 at 17.17.17@2x.png" alt="" width="375">
    <figcaption>
      <p><i>Hit undo to undo.</i></p>
    </figcaption>
  </figure>
</div>

### Amending Commits

If you made a commit and then make another small change and want it to be in your last commit, you can simply drag the file on top of the last commit to amend it.

<div align="center">
  <figure>
    <img src="../../../.gitbook/assets/CleanShot 2023-11-30 at 17.20.14@2x.png" alt="" width="563">
    <figcaption>
      <p><i>Drag a file onto the last commit to amend the commit to include that file change.</i></p>
    </figcaption>
  </figure>
</div>

### Squashing Commits

If you want to squash two commits together, just start dragging one of the commits and the squash targets will light up.

<div align="center">
  <figure>
    <img src="../../../.gitbook/assets/CleanShot 2023-11-30 at 17.18.25@2x.png" alt="" width="563">
    <figcaption>
      <p><i>Just drag and drop to squash commits.</i></p>
    </figcaption>
  </figure>
</div>
