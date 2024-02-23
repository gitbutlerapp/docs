---
description: How to setup GitButler to communicate with your upstream server
---

# 🛤️ Pushing and Fetching

Currently GitButler will only do network communication over the SSH protocol, so you need to make sure that it can access an SSH key that is authorized to push to your upstream server.

There are three different keys that GitButler will look for and attempt to use. It cannot currently supply a password, so one of the three needs to be passwordless.

## The SSH Keys

The first we will look for and try to use is `~./ssh/id_rsa`, which you may already have set up. It's a fairly common key for existing Git users to have, so in many cases, things will just work.

We'll also look for `~/.ssh/id_ecdsa` and try that.

## GitButler's Key

In case that doesn't work (they doesn't exist, has a password, it's a format that [isn't accepted upstream](https://github.blog/2021-09-01-improving-git-protocol-security-github/), etc), we will look for `~/.ssh/id_ed25519`.&#x20;

If this key does not already exist, GitButler will automatically generate one for you, so after installing GitButler, you _will_ have one of these no matter what.

If you go to your Account area (click on the link in the top right corner of your window), you should see the public version of this key under the "Git Stuff" area. Copy that (there is a button to copy it to your clipboard) and upload it as an authorized ssh key for your Git server.

In GitHub, you can do that [here](https://github.com/settings/ssh/new). In GitLab, it's [here](https://gitlab.com/-/profile/keys). If you're running something else, it should be a similar process, but it has to be SSH and able to handle Ed25519 keys.

<div align="center">
  <figure>
    <img src="../../../.gitbook/assets/CleanShot 2023-08-09 at 13.08.18@2x.png" alt="">
    <figcaption>
      <p><i>A screenshot showcasing an ed25519 SSH Key.</i></p>
    </figcaption>
  </figure>
</div>

Once that's done, GitButler will be able to automatically fetch upstream work and push new branches to your upstream server.
