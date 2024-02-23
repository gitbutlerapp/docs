---
description: >-
  GitHub and GitLab provide a mechanism to verify signed commits using an
  uploaded public SSH key. GitButler can automatically sign all your commits.
---

# ✅ Verifying Commits

Git provides a mechanism to sign your commits with a GPG key or SSH key. This enables other developers to make sure that you were actually the person who committed it, rather than someone else just setting their email to yours and committing it as if they were you.

To make this work, a signature is added to the commit header and then that signature is checked against public key stored somewhere, generally for most people the most useful way to verify these signatures is through GitHub or GitLab.

This is what a verified commit looks like on both systems:

<div align="center">
  <figure>
    <img src="../../../.gitbook/assets/CleanShot 2023-09-23 at 16.40.14@2x.png" alt="">
    <figcaption>
      <p><i>A verified commit on GitLab.</i></p>
    </figcaption>
  </figure>
</div>

<div align="center">
  <figure>
    <img src="../../../.gitbook/assets/CleanShot 2023-09-23 at 16.42.31@2x.png" alt="">
    <figcaption>
      <p><i>Verified and non-verified commits on GitHub.</i></p>
    </figcaption>
  </figure>
</div>

This means that the server has a public key that you used to sign the commits that is associated to your account and has verified that this user actually signed this commit.

In order for this to work, you need to:

1. Tell GitButler to sign your commits
2. Upload your key as a "signing key" to GitHub or GitLab (or elsewhere)

## Telling GitButler to Sign

Telling GitButler to sign commits is very easy. For simplicity, currently we will only sign with the ed25519 SSH key that we generate, so it's really just flipping a switch in your settings.

<div align="center">
  <figure>
    <img src="../../../.gitbook/assets/CleanShot 2023-09-23 at 21.40.52@2x.png" alt="">
    <figcaption>
      <p><i>Telling GitButler to sign your commits.</i></p>
    </figcaption>
  </figure>
</div>

This actually just sets a global Git setting named `gitbutler.signCommits`, so technically you could do this via `git config` instead if you prefer.

## Upload Your Signing Key

For GitHub or GitLab to verify your signatures, you need to say that the SSH key we generated and are using is a valid signing key for your user. You can copy the public key in the settings page by clicking the "Copy to Clipboard" button.

### Adding to GitHub

You can click on the "Add key to GitHub" link in the settings page right about the signing toggle, or you can go [here](https://github.com/settings/ssh/new) ([https://github.com/settings/ssh/new](https://github.com/settings/ssh/new)) to paste that public key in.

<div align="center">
  <figure>
    <img src="../../../.gitbook/assets/CleanShot 2023-09-23 at 21.48.05@2x.png" alt="">
    <figcaption>
      <p><i>Be sure to change the type to "Signing Key"</i></p>
    </figcaption>
  </figure>
</div>

Now your signed commits should show up as "Verified".

### Adding to GitLab

For GitLab you need to go to "SSH Keys" in your profile: [https://gitlab.com/-/profile/keys](https://gitlab.com/-/profile/keys) and click the "Add new key" button.

<div align="center">
  <figure>
    <img src="../../../.gitbook/assets/CleanShot 2023-09-23 at 21.50.22@2x.png" alt="" width="563">
    <figcaption>
      <p><i>Add new key here.</i></p>
    </figcaption>
  </figure>
</div>

Now paste in the public SSH key you copied from GitButler, name it and make sure the "Usage Type" is either "Signing" or "Authentication and Signing".

<div align="center">
  <figure>
    <img src="../../../.gitbook/assets/CleanShot 2023-09-23 at 21.51.22@2x.png" alt="" width="563">
    <figcaption></figcaption>
  </figure>
</div>

Now all your GitButler generated commits will be verified on that platform!
