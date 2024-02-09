---
description: Changelog for our GitButler client releases
---

# 🐿 Releases

### We have moved our releases announcements to our Discord channel. Come join us for updates.

Join our Discord [#releases ](https://discord.com/channels/1060193121130000425/1183737922785116161)channel.

If you haven't joined our Discord server, you can join [here](https://discord.com/invite/MmFkmaJ42D).



***

## Older Announcements

_(this is no longer being kept up to date, but we'll leave them in here for fun)_

## v0.9.0

**Thu, Nov 30, 2023**

After a bit of a release pause, we're back! We've given our wonderful GitButler a total facelift and a lot more. Commit undoing, squashing, amending, GitHub integration and more!

**New Facelift**

<div data-full-width="true">

<figure><img src="../.gitbook/assets/CleanShot 2023-11-30 at 15.43.31@2x.png" alt=""><figcaption><p>The new, improved suit of armor that our Butler wears into battle now.</p></figcaption></figure>

</div>

As you can see, we've cleaned up a lot of the UI, made the multiple branches clearer and simplified the sidebar a lot. We find all of this much cleaner and clearer and we hope you do too.

**New Navigation**

You can now find your personal settings, your project specific settings and feedback buttons at the bottom of the sidebar, and you can change projects easily with our new dropdown menu.

<figure><img src="../.gitbook/assets/CleanShot 2023-11-30 at 15.46.17@2x.png" alt=""><figcaption><p>Project settings are now easy to get to.</p></figcaption></figure>

<figure><img src="../.gitbook/assets/CleanShot 2023-11-30 at 15.47.37@2x.png" alt=""><figcaption><p>Change your active project quickly with the new dropdown switcher.</p></figcaption></figure>

**Drill down into file diffs**

Now instead of diffs being expandable within the lane, clicking on a file path expands the diff to the right side. We've found that this makes the UI much cleaner and simpler to understand and navigate.

<figure><img src="../.gitbook/assets/CleanShot 2023-11-30 at 15.48.40@2x.png" alt=""><figcaption><p>Dark mode still looks good too.</p></figcaption></figure>

**Amend, Squash and Undo**

Now we have more ways to fix up your commit history. If you forgot one little change, you can edit the file and then drag that file path down into your last commit to amend it.&#x20;

<div align="center">

<figure><img src="../.gitbook/assets/CleanShot 2023-11-30 at 15.32.33@2x.png" alt=""><figcaption><p>Drag a file change down into the last commit to amend it.</p></figcaption></figure>

</div>

If you have multiple commits and want to squash them together, you can simply drag one commit on top of the previous one to squash. If you committed and decide that you want to undo that commit, you can just hit the new "Undo" button.

<figure><img src="../.gitbook/assets/CleanShot 2023-11-30 at 15.33.06@2x.png" alt=""><figcaption><p>Squash commits together or just undo them with a click.</p></figcaption></figure>

**GitHub Integration**

You can now authenticate with GitHub in your GitButler client. This allows us to open Pull Requests for you, or pull down PRs for you to inspect or apply locally, next to your existing branches. Just head to your user settings to authenticate GitHub.

<figure><img src="../.gitbook/assets/CleanShot 2023-11-30 at 15.56.42@2x.png" alt=""><figcaption><p>Integrate Pull Requests with GitHub authentication</p></figcaption></figure>

We took a while to lift this face, but now we will be back in the swing of things, releasing much more often. Hold on for a ride!

## v0.8.0

#### Fri, Sep 22, 2023

It's been a few weeks since our last release, so there are a lot of fun things in this one.

#### Partial Commits

You can now select individual files or lines and do partial commits, in case you want to split up some work into a couple of separated commits.

<figure><img src="../.gitbook/assets/CleanShot 2023-09-23 at 16.20.17@2x.png" alt=""><figcaption></figcaption></figure>

#### Verified Commits

We've added a new option to enable commit signing using the ed25519 key that GitButler generates, which means you can upload that key as a signing key to GitHub to get [verified commits](../features/virtual-branches/verifying-commits.md).

<figure><img src="../.gitbook/assets/CleanShot 2023-09-23 at 16.28.43@2x.png" alt="" width="563"><figcaption></figcaption></figure>

#### More AI Fun

Better and much faster AI commit message generation, including new "Extra concise" and "Use emojis" options. AI can now also automatically generate branch names for you.

<figure><img src="../.gitbook/assets/CleanShot 2023-09-23 at 16.27.14@2x.png" alt="" width="563"><figcaption><p>Better commit message generation</p></figcaption></figure>

#### Better authentication

You can now define your preferred authentication method per project and provide a password for private keys.

<figure><img src="../.gitbook/assets/CleanShot 2023-09-23 at 16.25.51@2x.png" alt=""><figcaption><p>More SSH key options</p></figcaption></figure>

#### Upstream Merging for Virtual Branches

If you push a virtual branch and then someone fetches it and does some work on it and pushes it up again, GitButler will now notice that there is upstream work on a virtual branch of yours and we will notify you and allow you to merge it into your local work.

#### And more!

There are also tons of smaller fixes, performance improvements, etc. For example, we've also updated a lot around remote authentication and supported types of remotes, fixed issues with larger repos, sped lots of operations up and more!



## v0.7.1

#### Fri, Sep 1, 2023

A couple of important UI updates in this release as we continue to figure out exactly how we want some of these interactions to feel like.

There is a new mini-tray under each applied branch name that list the changed files in that branch and shows your branch notes there. The sidebar no longer shows you applied branches, just unapplied ones, so there is a cleaner split between what is applied and unapplied.

<figure><img src="../.gitbook/assets/unnamed.png" alt=""><figcaption><p>Some new UI updates</p></figcaption></figure>

We've also made a lot of improvements to the networking code, so your push/fetches are more likely to not have issues. Plus a bunch of other little things, enjoy!

## v0.7.0

#### Fri, Aug 11, 2023

A few pretty new things, plus some fun behind the scenes stuff in this release.

We're still playing with finding a layout that feels best, so this release lets you preview commits that are in any virtual or remote branch, as well as see what incoming changes from upstream you are behind and need to merge in with a cool peek tray.

<figure><img src="../.gitbook/assets/CleanShot 2023-08-11 at 14.01.03@2x.png" alt=""><figcaption><p>See what commits are in any of your branches, including upstream.</p></figcaption></figure>

Another cool thing is that you can keep notes in each virtual branch. Write out your to do list or other notes for the feature or bugfix you're working on while you're working.

Some other things:

* We are now handling situations where you want to go back to using command line Git for some operations a little better.&#x20;
* We're now rebasing unpushed commits when you integrate upstream changes (if possible).
* We auto-resolve conflicted files when we see that there are no more conflict markers in the file.
* We're adding new refs for our virtual branches so you can access them directly if you want.
* Buncha bug fixen.

Enjoy!

## v0.6.2

#### Sun, Aug 6, 2023

Two bigger things in this release. The first is that we now have an initial **AppImage based Linux build!** So fire up your Ubuntu and try it out.

The second is that we have integrated our own basic **SSH key based workflow**. We had some auth issues due to a hundred ways people auth for Git stuff, so we've provided an option if you prefer to have us own it a bit more.

We generate a ed25519 SSH key for you and provide a simple way for you to add our key to your GitHub profile, which allows us to push and fetch for you without having to deal with that yourself. We will also first attempt to find a key you already use, but if it doesn't work, we have a nice backup.

<figure><img src="../.gitbook/assets/CleanShot 2023-08-07 at 10.01.03@2x.png" alt=""><figcaption><p>Just copy the public sig for our generated key to your server and *blamo*, no more network issues.</p></figcaption></figure>

## v0.6.0

#### Thu, Aug 3, 2023

Mostly bug fixes plus some UX improvements to help with more empty states. Creates an initial virtual branch that is based on whatever git branch you were on when you selected your base branch, which should be helpful from scratch. Improvements to the file watcher and refreshing code. Bunch of stuff like that.

## v0.5.0

#### Thu, July 24, 2023

Well, the wait has been long, but we're back in the swing of things. We came up with a smashing new idea for how to do branches in a way nobody has ever done before and it took us a while to get it all working.&#x20;

<figure><img src="../.gitbook/assets/spaces_Z5O7nIjz0ow1eQWGNs4v_uploads_BIlViOl6zDDdMpPVmI3R_CleanShot 2023-07-24 at 15.png" alt=""><figcaption><p>Virtual branches, light mode, oh my!</p></figcaption></figure>

This is a massive new feature and one you can check out in great detail in [our docs](../features/virtual-branches/).

For now, we've turned off access to the rest of the UI while we concentrate on getting this working, but boy is it cool. We'll get the timeline back in an even bigger and better way soon, but for now, please enjoy the best new way to work since hand tools.

## v0.4.0

#### Thu, May 25, 2023

Hot on the heels of our last release, we're introducing a new "bookmarking" feature. Now you can let GitButler know about important moments in your timelines that you might want to remember or go back to.

![](<../.gitbook/assets/CleanShot 2023-05-25 at 12.55.29@2x.png>)![](<../.gitbook/assets/CleanShot 2023-05-25 at 12.55.43@2x.png>)

You can either create bookmarks by hitting the little bookmark button in the bottom right corner in the timeline, or you can hit Cmd-K to bring up the palette and create a new bookmark from there, wherever you happen to be in the timeline.

## v0.3.0

#### Monday, May 22, 2023

With this new release, you can now link a project on multiple computers to sync the working directory history of both of them. You can't quite actually check out those working directory states from one into the other, but it's a step closer.

<figure><img src="../.gitbook/assets/CleanShot 2023-05-22 at 13.56.45@2x.png" alt=""><figcaption><p>Link multiple clients on multiple computers to the same GitButler project to sync history</p></figcaption></figure>

Another nice addition is the feedback icon (little envelope looking thing at the bottom) that you can click at any time to share feedback with us or send us your logs/data in case there was an issue so that we can recreate and debug it.

<figure><img src="../.gitbook/assets/CleanShot 2023-05-22 at 13.58.33@2x.png" alt=""><figcaption><p>Share yo feedback.</p></figcaption></figure>

There were also a number of speed increases and some more behind the scenes data structure changes, but don't worry about those.

## v0.2.1

#### Friday, April 28, 2023

Bug fixes and minor improvements.

## v0.2.0

#### Friday, April 21, 2023

New layout for the project page and redesign of the activity graphs in preparation for presenting more Git data in the sidebar. Also added some new styling to the commit page and have changed how we store our snapshot data so that it doesn't pollute the Git project space.

![](<../.gitbook/assets/CleanShot 2023-04-21 at 09.31.00@2x.png>) ![](<../.gitbook/assets/CleanShot 2023-04-21 at 09.31.43@2x.png>)

## v0.1.0

#### April 14, 2023

Some bug fixes and improvements, but the big thing is our new shiny icon!

![](../.gitbook/assets/icon.png)

## v0.0.24

#### Tue, April 11, 2023

Fixed the terminal :joy:

## v0.0.23

#### Thu, April 6, 2023

This update ships with a new command palette for (better) fast access to all your GitButler needs, as well as an integrated Terminal per project.

<figure><img src="../.gitbook/assets/CleanShot 2023-04-06 at 15.56.48@2x.png" alt=""><figcaption><p>New and improved command palette</p></figcaption></figure>

<figure><img src="../.gitbook/assets/CleanShot 2023-04-06 at 15.53.25@2x.png" alt=""><figcaption><p>New project terminal (soon to be recording)</p></figcaption></figure>

You can also see your git status as you go without having to run `git status` all the time.

The terminal is mostly to iron out the bugs. Next up will be recording anything you do in your project terminal along with your file history for even more historical project context.

## v0.0.21

#### Fri, Mar 31, 2023

It's AI time! Now it is possible to have GitButler write your commit message via gpt4, including a description of what changes you've made to your code. Make commit messages like a kernel hacker, finally!

<figure><img src="../.gitbook/assets/CleanShot 2023-04-05 at 13.54.44@2x.png" alt=""><figcaption></figcaption></figure>

We've also made improvements to the speed and performance of various pages and some interface polish.

## v0.0.20

#### Thu, Mar 23, 2023

This release adds a lot of speed and resource usage improvements, as well as our first real Git feature, the commit dialog.

Now you can go into commit mode, view the diff of any of the modified files you have, select which files to include or exclude from the commit and even ask our AI to look at the diff and come up with a commit message for you.

We're also releasing builds for Apple Intel chips in addition to the Silicon builds.

<figure><img src="../.gitbook/assets/CleanShot 2023-03-22 at 22.07.13@2x.png" alt=""><figcaption><p>Our new committer.</p></figcaption></figure>

## v0.0.18

#### Thu Mar 16, 2023

This version adds a new and improved player view to see the history of your file changes.

<figure><img src="../.gitbook/assets/CleanShot 2023-03-16 at 17.26.35@2x.png" alt=""><figcaption></figcaption></figure>
