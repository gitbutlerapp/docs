---
description: Changelog for our GitButler client releases
---

# 🐿 Releases

## v0.3.0

#### Friday, May 22, 2023

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

![](<../.gitbook/assets/CleanShot 2023-04-21 at 09.31.00@2x.png>) ![](<../.gitbook/assets/CleanShot 2023-04-21 at 09.33.06@2x.png>)

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
