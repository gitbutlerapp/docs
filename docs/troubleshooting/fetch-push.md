# 🌎 Fetch / Push issues

If you are having trouble pushing or fetching from a remote, this is likely related to git authentication. Here are a few configuration options you can try out, found in the project settings.

## Available authentication methods

GitButler can be configured to use several different git authentication methods. You can switch between them in your project settings. You can try multiple different options and see if any of them are appropriate for your setup.

### Auto detect

This is the default setting. GitButler will attempt multiple authentication methods (which may make this option slower in some cases). If you have a GitHub integration set up, the app will also attempt to use that.

### Use an existing SSH key

If you already have an SSH key set up (eg. `~/.ssh/id_rsa`), you can instruct GitButler to use it. In case the key is password protected, you can also provide the password to it (which will be stored locally).

### Use locally generated SSH key

This option generates a new SSH key which will be stored locally in the application [data dir](../development/debugging.md#data-files). For this to work you will need to add the new public key to your Git remote provider.

### Use a git credential helper

If your system is set up with a credential helper, GitButler can use that. For more info on git credential helpers, see this [article](https://git-scm.com/doc/credential-helpers)

## Not yet implemented authentication methods

### FIDO security keys (YubiKey, etc.)

Tracked in GitHub issue [#2661](https://github.com/gitbutlerapp/gitbutler/issues/2661)

### Keys managed by 1Password

Tracked in GitHub issue [#2779](https://github.com/gitbutlerapp/gitbutler/issues/2779)

### Host certificate checks

There is an option to ignore host certificate checks when authenticating with SSH. This may be a helpful option to enable in some cases.

## Other known issues

### Git remote servers with a non-standard SSH port

In some cases, the git remote may be set up on a port number other than 22. If the port is set in your `~/.ssh/config` file, GitButler will not be able to recognize that - tracked in GitHub issue [#2700](https://github.com/gitbutlerapp/gitbutler/issues/2700).

As a workaround you may set your remote in the [SSH format](https://git-scm.com/book/en/v2/Git-on-the-Server-The-Protocols) (e.g. `ssh://git@example.com:3022/foo/bar.git`)

#### Updating virtual branches when the respective remote has new commits

If you have added a remote branch to your active workspace in GitButler, or pushed a virtual branch to the remote, and new commits are added to the remote branch, there is currently no way to sync those new commits into the existing virtual branch in GitButler. This is being tracked in GitHub issue [#2649](https://github.com/gitbutlerapp/gitbutler/issues/2649). 

The current workaround is to undo any local commits and then stash your local changes manually using [git stash](https://git-scm.com/docs/git-stash) and then delete the virtual branch that has upstream changes. Then you can update the trunk by clicking the update button next to the word "Trunk" in the sidebar on the left to make sure all new upstream changes are synced, then select the remote branch that has the new changes and click the "Apply +" button above the list of commits for the branch. Once the updated branch is applied to your working directory, you can manually `git stash pop` your stashed changes and then resolve any merge conflicts. 

### Help on Discord

If none of the available options helps, feel free to hop on our [Discord](https://discord.gg/MmFkmaJ42D) and we will be happy to help you out.
