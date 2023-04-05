# 💻 Git Client

GitButler is also a basic Git client. While we aim to be a full featured client soon, currently in the beta it has a small but growing set of capabilities. You can also use any normal Git commands in the terminal side by side with GitButler, it doesn't modify your repo in any weird ways or expect certain states.

Here are some of the things it can do today.

## Status

On your project dashboard, GitButler will show you if you have modified files in your working directory that are not included in your last commit. This is the equivalent of the `git status` command. It will also indicate which branch you're currently on.

<figure><img src="broken-reference" alt=""><figcaption></figcaption></figure>

## Committing

From that page, or from the command palette, you can commit the changes to your Git history. Our commit page allows you to choose a subset of files to include, view individual diffs for any of the files and write a commit summary and optional description for your changes.

There is also an AI-powered commit message generator to help you write your commit message. It sends the selected diff to OpenAI through our servers and returns  a well formatted commit message that you can use or edit.

<figure><img src="broken-reference" alt=""><figcaption></figcaption></figure>
