---
description: How to dig around our internal data to find (nearly) anything
---

# ⛏️ Recovering Stuff

GitButler saves data in a few different ways. As we're still in beta, sometimes things might break and it may look like you've lost work, but you almost certainly haven't. We're pretty good about saving stuff a lot. Here's how to recover almost anything you had in your working directory or virtual branches.

### GitButler References

If everything crashes or the UI isn't working at all, you may be surprised to know that even though your virtual branches don't show up in a normal `git branch` output, we _do_ actually constantly write them out as Git references (just not in `refs/heads`).

```
❯ git for-each-ref | grep gitbutler
e63b3bac82835dc17083a785d25db8b4b46744b9 commit	refs/gitbutler/add-can-create-method-to-notebook
98ef3cd6eea14ee4159a600e448271c0d777efe2 commit	refs/gitbutler/add-conditional-blocks-for-image-and-video
c7e27b9f99f25160a4d5f07d5972c217bdd44319 commit	refs/gitbutler/add-database-schema-conversion-script
4afdfed6c14b57491a9d295c31613fd79b92f63a commit	refs/gitbutler/add-gems-for-test-group
```

These references are just like git branches - they point to a commit that has the latest version of your branch. You can create other git branches off of them, you can push them to GitHub, etc.

You will have one for each virtual branch (applied or unapplied) that you've created (that you haven't deleted).

If you've committed everything on a virtual branch, the reference will just point to the latest commit. If you have work in progress on the branch, it will point to a WIP commit that includes those changes.

So for example, if I have the following two virtual branches, one fully committed and one with work pending:

<figure><img src="../.gitbook/assets/CleanShot 2024-02-23 at 10.30.27@2x.png" alt=""><figcaption></figcaption></figure>

&#x20;I can view the git branches like this:

```
❯ git show gitbutler/Convert-tables-to-utf8mb4
commit 841e4db701ca41206c03f1f4fe345f7e27d05eab
Author: Scott Chacon <schacon@gmail.com>
Date:   Fri Feb 23 10:30:17 2024 +0100

    my latest commit
    
❯ git show gitbutler/Add-database-schema-conversion-script
commit d95e7f4da1611ea6bb8a80da06e66ca923fbff55
Author: GitButler <gitbutler@gitbutler.com>
Date:   Fri Feb 23 10:30:18 2024 +0100

    GitButler WIP Commit
    
    This is a WIP commit for the virtual branch 'Add database schema conversion script'
    
    This commit is used to store the state of the virtual branch
    while you are working on it. It is not meant to be used for
    anything else.
```

See how the `Add-database-schema-conversion-script` reference points to a "WIP commit"? The tree of that commit has all those changed files in it as though we had committed them.

If you don't want to search through all your refs with `for-each-refs`, you can also just run a normal `git log` command and we'll show you what references we've written and which modified files are in each one:

<pre><code><strong>❯ git log
</strong><strong>commit 2d8afe0ea811b5f24b9a6f84f6d024bb323a2db5 (HEAD -> gitbutler/integration)
</strong>Author: GitButler &#x3C;gitbutler@gitbutler.com>
Date:   Fri Feb 23 10:30:18 2024 +0100

    GitButler Integration Commit
    
    This is an integration commit for the virtual branches that GitButler is tracking.
    
    Due to GitButler managing multiple virtual branches, you cannot switch back and
    forth between git branches and virtual branches easily.
    
    If you switch to another branch, GitButler will need to be reinitialized.
    If you commit on this branch, GitButler will throw it away.
    
    Here are the branches that are currently applied:
     - Add database schema conversion script (refs/gitbutler/Add-database-schema-conversion-script)
       - butler/Gemfile
       - butler/README.md
       - butler/db/schema.rb
       - butler/db/migrate/20240209144600_change_mysql_charset.rb
       - .pscale.yml
     - Convert tables to utf8mb4 (refs/gitbutler/Convert-tables-to-utf8mb4)
       branch head: 841e4db701ca41206c03f1f4fe345f7e27d05eab
       - butler/create_column_conversions.rb
    
    Your previous branch was: refs/heads/sc-branch-comments
    
    The sha for that commit was: 5e16e99667db9d26f78110df807853a896120ff3
    
    For more information about what we're doing here, check out our docs:
    https://docs.gitbutler.com/features/virtual-branches/integration-branch
</code></pre>

You can see the two `gitbutler` refs under the "Here are the branches that are currently applied" section.

Again, these are real git refs, just not under `refs/heads` so that we don't pollute your `git branch` output. But if GitButler crashes at some point, you can still push them to GitHub or whatever you want. Here is an example pushing my virtual branch to a GitHub branch called `convert-tables`:&#x20;

```
❯ git push origin refs/gitbutler/Convert-tables-to-utf8mb4:refs/heads/convert-tables
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 10 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 474 bytes | 474.00 KiB/s, done.
Total 4 (delta 2), reused 1 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
remote: 
remote: Create a pull request for 'convert-tables' on GitHub by visiting:
remote:      https://github.com/gitbutlerapp/web/pull/new/convert-tables
remote: 
To github.com:gitbutlerapp/web.git
 * [new branch]        refs/gitbutler/Convert-tables-to-utf8mb4 -> convert-tables

```

### GitButler Sessions

Ok, let's say that your work was not in one of those refs for some reason. Maybe you hit some weird bug and it completely changed everything in a way where now you're sitting on the couch in the dark with a glass of whisky, slowly mumbling the word "GitButler..." and plotting your revenge.

Well, before you put your plan into action, let's try something first.

{% hint style="warning" %}
Warning. The following gets into low level git objects.  You may want to brush up on [Git Internals](https://git-scm.com/book/en/v2/Git-Internals-Git-Objects) if you get confused at parts.
{% endhint %}

You see, GitButler actually sits in the background with a filesystem watcher and every time it sees a file change in a file that is not ignored by `.gitignore`, it will store a CRDT of the changes to every file it sees changed, all the time. It will store these changes and snapshots of the whole working directory at least once an hour, generally even more often.

These sessions are kept in your [Data Files directory](../development/debugging.md#data-files). If you go to your project data directory, you'll find that it's a _second_ git repository, just for this sideband sessions data. (It's also where we keep your virtual branch data). But let's look at the session data:

```
❯ cd ~/Library/Application\ Support/com.gitbutler.app.nightly/projects/1196ca33-119d-44ed-85be-83feb8b4bf20 

❯ cat HEAD 
ref: refs/heads/current

❯ git log
commit 6af3f528721f72f2e5f2a583555e736cf8a1e4bd (HEAD -> current, 1196ca33-119d-44ed-85be-83feb8b4bf20)
Author: Scott <schacon@gmail.com>
Date:   Fri Feb 9 15:36:31 2024 +0100

    gitbutler check

commit 07938f1a02ca6d7ac93919abc86de795ca72cf63
Author: Scott <schacon@gmail.com>
Date:   Fri Feb 9 15:24:28 2024 +0100

    gitbutler check

commit c500a0b7e38a3edc3de8570cdbbc01b54e263a48
Author: Scott <schacon@gmail.com>
Date:   Fri Feb 9 13:17:58 2024 +0100

    gitbutler check

commit 060e363d98636d4b320e25cf4317d1b415937388
Author: Scott <schacon@gmail.com>
Date:   Fri Feb 9 13:08:48 2024 +0100

    gitbutler check
```

Ok, so it's making "gitbutler check"s every once in a while (it will only do it while you're actively working on the project and it will record a snapshot if it doesn't see any changed files for 5 minutes). What is in this session snapshot? Let's take a raw look at the tree:

```
❯ git ls-tree HEAD
040000 tree d107382389c3612190d079b41a57dd1a340b6816	branches
040000 tree 235347291bbc88bdbd870f806e8c151b1f3d61d0	session
040000 tree cea59ceae4805aad34c324390e003a02cad3721b	wd
```

Ok, so there are three top level directories. Under `branches`, it stores the state of each virtual branch (applied or not). Under `session` it stores the data for things that have happened in this one session (from a few minutes up to an hour long). Under `wd` it has a snapshot of the working directory at the end of the session.

So, let's do a `--stat` so we can see what changed between one session and another:

```
❯ git log --stat
commit 07938f1a02ca6d7ac93919abc86de795ca72cf63
Author: Scott <schacon@gmail.com>
Date:   Fri Feb 9 15:24:28 2024 +0100

    gitbutler check

 branches/d49480f4-5013-4ae8-8046-db7abdfa27cc/meta/selected_for_changes                  |  1 -
 branches/d49480f4-5013-4ae8-8046-db7abdfa27cc/meta/updated_timestamp_ms                  |  2 +-
 session/deltas/butler/Gemfile                                                            |  1 +
 session/deltas/butler/README.md                                                          |  1 +
 session/deltas/butler/config/database.yml                                                |  1 +
 session/deltas/butler/config/initializers/cors.rb                                        |  1 +
 session/meta/commit                                                                      |  2 +-
 session/meta/id                                                                          |  2 +-
 session/meta/last                                                                        |  2 +-
 session/meta/start                                                                       |  2 +-
 wd/butler/Gemfile                                                                        |  2 +-
 wd/butler/README.md                                                                      |  2 +-
 wd/butler/config/database.yml                                                            |  4 ++--
 wd/butler/config/initializers/cors.rb                                                    | 16 ++++++++++++++++
 36 files changed, 57 insertions(+), 13 deletions(-)
```

While `branches` has interesting data (all our virtual branch coolness), we probably don't need to look at that for data recovery purposes.

### Recovering a Working Directory State

The nice thing about this is that we then have an automatic backup of our working directory at very regular intervals whenever we're touching any files in our project directory. You can use Git plumbing commands to do whatever you want with the `wd` subtree in any of those "check" commits.

For example, let's find a session from a month ago and extract the contents of our README as it looked a month ago.

```
❯ git log --before=1.month.ago -1
commit f5278569efebf6e183ef9d513642f334a27ca1db
Author: Scott <schacon@gmail.com>
Date:   Tue Jan 23 15:11:18 2024 +0500

    gitbutler check

❯ git ls-tree f52785:wd
040000 tree 63ee26541d5e5630745d1eef33ca7e1ff0dbd747	.gitbutler
040000 tree 875a876f7bcdf666d251e05206005fdfff47ddab	.github
100644 blob e43b0f988953ae3a84b00331d0ccf5f7d51cb3cf	.gitignore
100644 blob 71b88a34ced72a3b73063eba2b7e654e593a64a6	.pscale.yml
100644 blob 8c50098d8aed57b02fd10f40a670a7c673b7c5a5	.ruby_version
100644 blob 6c3073ecf95fed46916d46027569ee0315444ccf	Gemfile
100644 blob c9e585dfea27b95db2b0e94f6a5106270ed0e26e	Gemfile.lock
100644 blob 887d8af38bcafdfb63c2a6d4b3dea5af4621446e	README.md
040000 tree dcd03c50327360c1dd77a50321bff02b9c63322b	auth-proxy
040000 tree 5f7611e9f0fa3299c8fffddd2c77c28f1f675df8	butler
040000 tree 6419d6ff7f8e7686a61b2d0adae9ece1034fdd26	chain
100644 blob ae12c3c02b2a9858d3e150d773441273887b2131	check.rb
040000 tree 6d0b34e4d8385a8d3e532984b06f75deddb23849	copilot
040000 tree 764c8198d7a766f11cc20fa22cefd4a6c90b34f6	git

❯ git cat-file -p f52785:wd/README.md | head -5
# GitButler Web Services

This is the repository for the GitButler Web Services. It is a collection of 
services that are used by the GitButler application. Each service lives in its 
own folder and has its own Docker file used to deploy to AWS via Copilot.
```

Or let's say you want to create a git branch that looks like that and check it out. First we can get the tree sha of the working directory by finding the commit SHA and then running `ls-tree` to see what the `wd` tree is:

```
❯ git log --before=1.month.ago -1
commit f5278569efebf6e183ef9d513642f334a27ca1db
Author: Scott <schacon@gmail.com>
Date:   Tue Jan 23 15:11:18 2024 +0500

    gitbutler check

❯ git ls-tree f5278569efeb
040000 tree 1263cc14f784e7c620fc85811602c661c150948b	branches
040000 tree 7b09a9d7fa582f369d61bace512b991a427af523	session
040000 tree f32491037b81c91d5a7d8d8436af6d2a74b49bd0	wd
```

So now we know that the `wd` tree is `f32491037b81c91d5a7d8d8436af6d2a74b49bd0`. Now we can do lots of things.&#x20;

We could read it into our index with `read-tree`, then check it out into our working directory with `reset`. We could create a new branch with `commit-tree` and then check that out or push it somewhere, etc. Let's take a look at the latter.

First of all, this needs to be run in your _project directory_, not the GitButler data directory we've been working in. Most of the actual git object data is written there and referenced via alternates.

```
❯ cd ~/my-project

❯ git commit-tree f32491037b81c91d5a7d8d8436af6d2a74b49bd0 -p origin/master -m 'recovering a month ago'
3c31b43463c6b9f7d79f7124e09d179c8351d7b6

❯ git branch recovery-branch 3c31b43463c6b9f7d79f7124e09d179c8351d7b6

❯ git log recovery-branch
commit 3c31b43463c6b9f7d79f7124e09d179c8351d7b6 (recovery-branch)
Author: Scott Chacon <schacon@gmail.com>
Date:   Fri Feb 23 11:22:10 2024 +0100

    recovering a month ago

commit a473ce09a740dbfe529f7b6f8e26b26ee4f53651 (origin/master, origin/HEAD)
Merge: 10aa6a44 9678a685
Author: Scott Chacon <schacon@gmail.com>
Date:   Fri Feb 9 13:06:29 2024 +0100

    Add cors configuration (#241)

```

Now the working directory snapshot from a month ago looks like a new commit on top of `origin/master`. It's a real branch, we can check it out, push it, etc.

### CRDTs

Now, if you need a version of a file _between_ two session snapshots, you can also technically recover that, because we _also_ keep a CRDT of each file we see changed. These are found in the `session/deltas` tree in each session.&#x20;

Now, this gets a little more complicated, because we don't have a UI for reconstructing this data easily anymore. We will add it back at some point, but for now, since we _are_ still recording this data, let's see how we could use this raw data to reconstruct the state of a file at any moment.

Here is what the crdt file format looks like:

```
❯ git cat-file -p HEAD:session/deltas/butler/test/api/summarize_test.rb | jq | head -20
[
  {
    "operations": [
      {
        "insert": [
          194,
          "  # enable caching\n    Rails.cache.clear\n  "
        ]
      }
    ],
    "timestampMs": 1706785016658
  },
  {
    "operations": [
      {
        "delete": [
          372,
          9
        ]
      },
...
```

Here we see that this Ruby test file had a series of edits and GitButler kept each small file change as an array of deletions and insertions from byte offsets on a known state of the file.

So, let's recover every step of editing this file. Here is a simple Ruby script for recovering every single file save over the course of this single session:

```ruby
require 'json'

file_contents = File.read('/tmp/base')
crdt = JSON.parse(File.read('/tmp/crdt'))

recover_dir = "/tmp/recovered"
Dir.mkdir(recover_dir) unless File.directory?(recover_dir)

crdt.each do |change|
  ts = change['timestampMs']

  pre_file_contents = file_contents
  ops = change['operations']

  ops.each do |op|
    if insert = op['insert']
      offset, string = insert
      file_pre = file_contents[0, offset]
      file_post = file_contents[offset, file_contents.length - offset]
      file_contents = file_pre + string + file_post
    end
    if delete = op['delete']
      offset, len = delete
      file_pre = file_contents[0, offset]
      file_post = file_contents[offset, file_contents.length - offset]
      file_post = file_post[len, file_post.length - len]
      file_contents = file_pre + file_post
    end
  end

  puts file_path = "#{recover_dir}/#{ts}"
  File.write(file_path, file_contents)
end
```

This reads the base file from `/tmp/base`, the CRDT json data from `/tmp/crdt` and then writes out every file save that was recorded as a seperate file under `/tmp/recovered/[ts]`

Let's try it out:

```
# extract the crdt data from session/deltas/[path]
❯ git cat-file -p HEAD:session/deltas/butler/test/api/summarize_test.rb > /tmp/crdt

# extract the base content from the session's parent's wd (notice the ~)
❯ git cat-file -p HEAD~:wd/butler/test/api/summarize_test.rb > /tmp/base

# run our recovery script
❯ ruby recover.rb 
/tmp/recovered/1706785016658
/tmp/recovered/1706785046167
/tmp/recovered/1706785185102
/tmp/recovered/1706785317555
/tmp/recovered/1706785325283
/tmp/recovered/1706785337638
/tmp/recovered/1706785368227
/tmp/recovered/1706785372113
/tmp/recovered/1706785373236
```

Now we have a series of versions of this file that is every time we saw the file change on disk, saved by the timestamp we observed it. We can see that each is a little different from the base and each other:

```
❯ diff /tmp/base /tmp/recovered/1706785016658
8a9,10
>     # enable caching
>     Rails.cache.clear

❯ diff /tmp/base /tmp/recovered/1706785046167
8a9,10
>     # enable caching
>     Rails.cache.clear
15,17c17,23
<     post_auth_user(@user, '/api/summarize_branch_name/branch')
<     assert last_response.ok?
<     ap res = JSON.parse(last_response.body)
---
> 
>     # stub Summarizer.branch_name_from_diff
>     Summarizer.stub(:branch_name_from_diff, 'branch_name') do
>       post_auth_user(@user, '/api/summarize_branch_name/branch')
>       assert last_response.ok?
>       ap res = JSON.parse(last_response.body)
>     end
```

Again, eventually we'll add a nice UI into GitButler to do this type of recovery, but for now if you're in a bind, this should give you the tools to be able to recover almost any version of any file from the moment you import your project into GitButler.
