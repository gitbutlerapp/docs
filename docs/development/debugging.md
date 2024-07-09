# 🐛 Debugging

If you are having technical issues with the GitButler client, here are a few things you can do to help us help you. Or help yourself.

If you get stuck or need help with anything, hit us up over on Discord, here's [GitButler Discord Server Link](https://discord.gg/MmFkmaJ42D)

## Logs

Often the most helpful thing is to look at the logs. GitButler is a Tauri app, so the logs are in your OS's [app log directory](https://docs.rs/tauri/latest/tauri/api/path/fn.app\_log\_dir.html). This should be:

* **Linux:** `~/.config/com.gitbutler.app/logs/`
* **macOS:** `~/Library/Logs/com.gitbutler.app/`
* **Windows:** `C:\Users\[username]\AppData\Roaming\com.domain.appname\logs`

In this directory, there should be rolling daily logs:

```
❯ cd ~/Library/Logs/com.gitbutler.app

❯ tree -L 1
.
├── GitButler.2023-09-02.log
├── GitButler.2023-09-03.log
├── GitButler.2023-09-04.log
├── GitButler.2023-09-05.log
├── GitButler.2023-09-06.log
├── GitButler.2023-09-07.log
├── GitButler.2023-09-08.log
├── GitButler.2023-10-10.log
├── GitButler.2024-01-30.log
└── tokio-console

❯ tail GitButler.log.2024-01-30 
2024-01-30T13:02:56.319843Z  INFO get_public_key: gitbutler-app/src/keys/commands.rs:20: new
2024-01-30T13:02:56.320000Z  INFO git_get_global_config: gitbutler-app/src/commands.rs:116: new key="gitbutler.utmostDiscretion"
2024-01-30T13:02:56.320117Z  INFO git_get_global_config: gitbutler-app/src/commands.rs:116: new key="gitbutler.signCommits"
2024-01-30T13:02:56.320194Z  INFO get_public_key: gitbutler-app/src/keys/commands.rs:20: close time.busy=317µs time.idle=47.0µs
2024-01-30T13:02:56.320224Z  INFO git_get_global_config: gitbutler-app/src/commands.rs:116: close time.busy=204µs time.idle=25.3µs key="gitbutler.utmostDiscretion"
2024-01-30T13:02:56.320276Z  INFO git_get_global_config: gitbutler-app/src/commands.rs:116: close time.busy=133µs time.idle=35.8µs key="gitbutler.signCommits"
2024-01-30T13:02:56.343467Z  INFO menu_item_set_enabled: gitbutler-app/src/menu.rs:11: new menu_item_id="project/settings" enabled=false
2024-01-30T13:02:56.343524Z  INFO menu_item_set_enabled: gitbutler-app/src/menu.rs:11: close time.busy=35.7µs time.idle=28.8µs menu_item_id="project/settings" enabled=false

```

## Data Files

GitButler also keeps it's own data about each of your projects. The virtual branch metadata, your user config stuff, a log of changes in each file, etc. If you want to inspect what GitButler is doing or debug or reset everything, you can go to our data directory.

* **Linux:** `~/.local/share/com.gitbutler.app/`
* **macOS:** `~/Library/Application Support/com.gitbutler.app/`
* **Windows:** `C:\Users\[username]\AppData\Roaming\com.domain.appname`

In this folder there are a bunch of interesting things.

```
❯ cd ~/Library/Application\ Support/com.gitbutler.app

❯ tree .
.
├── keys
│   ├── ed25519
│   └── ed25519.pub
├── projects.json
└── settings.json

4 directories, 4 files
```

The `projects.json` file will have a list of your projects metadata:

```
❯ cat projects.json 
[
  {
    "id": "71218b1b-ee2e-4e0f-8393-54f467cd665b",
    "title": "gitbutler-blog",
    "description": null,
    "path": "/Users/scottchacon/projects/gitbutler-blog",
    "preferred_key": "generated",
    "ok_with_force_push": true,
    "api": null,
    "gitbutler_data_last_fetch": null,
    "gitbutler_code_push_state": null,
    "project_data_last_fetch": {
      "fetched": {
        "timestamp": {
          "secs_since_epoch": 1706619724,
          "nanos_since_epoch": 202467000
        }
      }
    }
  }
]
```

The `settings.json` are some top level preferences you've set. A lot of stu

```
❯ cat settings.json
{"appAnalyticsConfirmed":true,"appNonAnonMetricsEnabled":true}%
```

Finally, the `keys` directory holds the SSH key that we generate for you in case you don't want to go through creating your own. It's only used if you want to use it to sign commits or use it for authentication.
