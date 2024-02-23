---
description: Find anything that you've ever typed.
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# ⌛ Timeline

{% hint style="danger" %}
The timeline feature has been temporarily hidden from the UI while we focus our alpha work on the Virtual Branch functionality. It will come back very soon. :pray:
{% endhint %}

Another feature of GitButler is the project timeline. This tool allows you to find any version of any file that has ever existed in your project from the moment you downloaded GitButler.

### Always Watching

When you add a project to GitButler, we will always be in the background, watching the directory like a hawk. Any files that you change that are not in your `.gitignore` file will be automatically saved every time you change them.

{% hint style="info" %}
The actual implementation of this is that we store CRDT data for all observed file changes inside your `.git` directory under `gb-[long-id-number]`. When we see you've stopped making changes for a few minutes, we flush all of that information to a meta-commit and update a hidden Git reference which you can find by running `git show-ref | grep gitbutler`. If you sign up for GitButler Cloud, we push that data to our servers so your working directory history is backed up.
{% endhint %}

These changes allow us to reconstruct what your working directory looked like at any point in time. You can see visualizations of this data on your project homepage and you can drill into any day or file to play back the changes. You can use this to remind yourself what you did, find previous versions of files that were never committed, revert sections or code you want to go back to, etc.

### The Project Dashboard

The Project dashboard shows you a summary of all the changes we have observed for the last few days. This includes any changes to any files and also any git commands (commits, pushes, fetches) that we've seen.

<figure><img src="../../.gitbook/assets/CleanShot 2023-03-14 at 16.11.48@2x.png" alt=""><figcaption><p>My project dashboard</p></figcaption></figure>

We also show you what branch you're currently on, if there are uncommitted changes (sort of like `git status`) and allow you to quick commit from here, but we'll cover that more in the [Broken link](broken-reference "mention") docs.

### The Player

<figure><img src="../../.gitbook/assets/CleanShot 2023-03-16 at 17.20.07@2x.png" alt=""><figcaption><p>Working directory history player</p></figcaption></figure>

Once you have some work saved, you can rewind your working directories time to see every change. Load in day playlists of sessions to find by time, or filter down to the history of a single file. Hit play to watch your changes happen in the order you applied them.

### GitButler Cloud Backup

If you sign in to GitButler Cloud then you can go into the settings of your project (the little gear icon on the top right of the project view) and opt into sending your data to your account on our servers. This will back up all your local history several times a day if you're online.

<figure><img src="../../.gitbook/assets/CleanShot 2023-03-14 at 16.16.45@2x.png" alt=""><figcaption></figcaption></figure>

This can be toggled off at any time to stop backing up your data.
