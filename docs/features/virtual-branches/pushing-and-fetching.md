---
description: How to setup GitButler to communicate with your upstream server
---

# 🛤️ Pushing and Fetching

GitButler can authenticate with an upstream Git server in several different ways.

&#x20;You can just tell us to use the system Git executable, which you can setup however you want. You can use our built in SSH protocol with either your own SSH key or a key we automatically generate for you (this does not require you to have Git installed), or you can use the default [Git credentials helper](https://git-scm.com/doc/credential-helpers).

You can set your preference (and test if it works) in your project's "Git authentication" section:

<figure><img src="../../.gitbook/assets/CleanShot 2024-06-03 at 16.51.42@2x.png" alt=""><figcaption></figcaption></figure>

## GitButler's Key

In case that you don't have an SSH key or authentication method set up, you can always use the SSH key that we automatically generate.

If you go to your Account area (click on the link in the top right corner of your window), you should see the public version of this key under the "Git Stuff" area. Copy that (there is a button to copy it to your clipboard) and upload it as an authorized ssh key for your Git server.

In GitHub, you can do that [here](https://github.com/settings/ssh/new). In GitLab, it's [here](https://gitlab.com/-/profile/keys). If you're running something else, it should be a similar process, but it has to be SSH and able to handle Ed25519 keys.

<figure><img src="../../.gitbook/assets/CleanShot 2024-06-03 at 16.55.58@2x.png" alt=""><figcaption></figcaption></figure>

Once that's done, GitButler will be able to automatically fetch upstream work and push new branches to your upstream server.
