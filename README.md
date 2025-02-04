```
                                   
mmmmmmm                          # 
   #     mmm    mmm    m mm   mmm# 
   #    #" "#  "   #   #"  " #" "# 
   #    #   #  m"""#   #     #   # 
   #    "#m#"  "mm"#   #     "#m## 
                                   
                                   
```

A text-only bulletin board.

## Requirement
- Node >= 16
- SQLite3 libs installed.
- That's all.

## Setting up
* Clone the repo
* Install the dependencies with `npm install`
* Run it by executing `npm start`, and done!

## Security
### IP Blocklist
The IP Blocklist is actually just used to block any POST request.

Check `ip_block` tables in `config.db` file.
```
~ $ sqlite3 config.db
SQLite version 3.41.2 2023-03-22 11:56:21
Enter ".help" for usage hints.
sqlite> SELECT * from ip_block;
....
```

To block an IP, Insert `ip` column into `ip_block`.

```
sqlite> INSERT INTO ip_block VALUES ("127.0.0.1");
```

To remove an IP from blocklist, Delete an column of an IP from `ip_block`
```
sqlite3> DELETE FROM ip_block WHERE ip = '127.0.0.1';
```

### IP Whitelist
The IP whitelist will prevent an certain IP to get into captcha sessions, or even getting ratelimited.

The settings are the same as the [IP Blocklist](#ipblocklists).

### Captcha
When the first wall was not enough, There goes another two verification layers.

To enable, Insert the following column into `config` table at `config.db` database:
```
sqlite3> INSERT INTO config VALUES ("captcha", "yes");
```

To disable, Simply delete the column.
```
sqlite3> DELETE FROM config WHERE name = 'captcha';
```

#### Also remember to do backup.

## Modifying Frontend
Make a folder called `local`, Then copy `views` and `public` folders to `local`.

And then start modify inside `local` folder.

## modtools

- To lock a thread, `./modtools/lock_thread.sh [threadid]`
- To unlock a thread, `./modtools/unlock_thread.sh [threadid]`
- To nuke a thread, `./modtools/nuke.sh [threadid]`
- To ban an IP, `./modtools/ip_block.sh [ipaddr]` (Not effective if the IP is whitelisted)

- To whitelist an IP, `./modtools/ip_white.sh [ipaddr]`
- To unban an IP, `./modtools/ip_unblock.sh [ipaddr]`
- To unwhitelist an IP, `./modtools/ip_unwhite.sh [ipaddr]`

- To block an ISP, for instance, `CLOUDFLAREWARP`, `./modtools/isp_block.sh [ispname]`
- To unblock an ISP, `./modtools/isp_unblock.sh [ispname]`

- To locking down the entire server, `./modtools/lockdown.sh`
- To unlocking down the entire server, `./modtools/unlockdown.sh`
- To make the server read only, `./modtools/read_only.sh`
- To make the server unlocked from read only, `./modtools/unread_only.sh`

- To block open port from client, `./modtools/block_open_port.sh [port]`
- To unblock open port from client, `./modtools/unblock_open_port.sh [port]`

## Community
* Telegram: https://t.me/yonlecoder
* #yonle at irc.lecturify.net

