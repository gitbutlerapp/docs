# 🌎 Fetch / Push issues

If you are having trouble pushing or fetching from a remote, this is likely related to git authentication. Here are a few configuration options you can try out, found in the project settings.

## Available authentication methods

GitButler can be configured to use several different git authentication methods. You can switch between them in your project settings. You can try multiple diffirent options and see if any of them are appropriate for your setup.

### Auto detect

This is the default setting. GitButler will attempt multiple authentication methods (which may make this option slower in some cases). If you have a GitHub integration set up, the app will also attempt to use that.

### Use an existing SSH key

If already have an SSH key set up (eg. `~/.ssh/id_rsa`), you can instruct GitButler to use it. In case the key is password protected, you can also provide the password to it (which will be stored locally).

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

There is an option to ignore host certificate checks when authenticating with ssh. This may be a helpful option to enable in some cases.

## Other known issues

### Git remote servers with a non-standard SSH port

In some cases, the git remote may be setup on a port number other than 22. If the port is set in your `~/.ssh/config` file, GitButler will not be able to recognize that - tracked in GitHub issue [#2700](https://github.com/gitbutlerapp/gitbutler/issues/2700).

As a workaround you may set your remote in the [SSH format](https://git-scm.com/book/en/v2/Git-on-the-Server-The-Protocols) (eg. `ssh://git@example.com:3022/foo/bar.git`)

## Help on Discord

If none of the available options helps, feel free to hop on our [Discord](https://discord.gg/MmFkmaJ42D) and we will be happy to help you out.
