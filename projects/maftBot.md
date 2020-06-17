---
title: Discord Meme Bot
subtitle: A meme generating discord bot.
date: 2020-05-15
externalLink: https://discord.com/api/oauth2/authorize?client_id=708407717349425223&permissions=0&scope=bot
github: https://github.com/ccrowley96/discord-bot
tags: 
    - reddit
    - javascript
    - node
    - bot
---
I created a meme generating discord bot.  The 'MAFT' bot can send random quotes and random hot / top reddit memes.

Currently, MAFT scrapes **r/dankmemes, r/memes, r/trebuchetmemes, r/prequelmemes, r/deepfriedmemes, r/nukedmemes, r/memeeconomy**.

When a discord user types $meme, the bot scrapes the 100 **hottest** memes from each of the subreddits listed above.

```text/2-3
$meme
```

**$topmeme**
When a user types $topmeme [hour | day | week | month | year | all], the bot srapes the 100 top memes of [timeframe] defaulted to all time if no timeframe is given.
```text/2-3
$topmeme
```

The memes are cached for 30 minutes on the node server.  If another meme request comes in after 30 minutes, MAFT bot will respond 
```text/2-3
Sec, finding hot memes...
```
And then fetch ~700 new memes :  )

### type '$help'
![meme bot](/img/maft/maft3.png)
### type $stats
![meme bot](/img/maft/maft4.png)
### type $meme
![meme bot](/img/maft/maft1.png)
### type $topmeme
![meme bot](/img/maft/maft2.png)