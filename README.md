# Prosper-ai Upvote/Curation Bot
A Steem bot, by [personz](https://steemit.com/@personz)

Forked by [Nolyoly](https://steemit.com/@noly) to continue development of this project.

## About the Prosper-ai Project
Prosper-ai is a bot built with Node.JS for the Steemit social network. It decides which posts to vote for and casts votes on behalf of a registered user. 

This project is also made open-source with documentation on how to set it up on your own server. This means that you too can set up your own bot to run seperately from our Prosper-ai project. You own the server and control it 100%. You control the running of the bot, set the algorithm configuration, and view stats and logs with a simple web dashboard. This will all be available at your Heroku URL. See [Usage] below for more details.

___Note:___ A plugin system was proposed on the original Fossbot project but never seemed to come to fruition. I will be investigating whether or not any of this was completed. I will be doing my best to try and implement this feature as it could bring a lot more functionality to this script.

## Prosper's Goal
The goal of this project is to develop a high quality Steemit bot to bring rewards to great content creators as well as generating curation rewards for votes cast. This is done by manualling adding authors to the bots upvote list. This can further be limited by the various configuration settings to determine a posts quality (more info below). Curation rewards are targeted by setting the time at which the bot votes after a post is made and by setting the percentages.

Also, by keeping this code open source and well documented, we make it easy for anyone who wishes to fork this project and make it their own, or simply copy it and use it the way they would like!

## How Prosper-ai Works
The bot works by scoring each new post using a collection of rules which are set by you. If a post scores above a threshold, it is voted for. The threshold is automatically adjusted based on a raised average of recent posts, and is also proportional to the number of votes in the last 24 hours, to keep votes per day at around a max of 40 by default (thid can be changed by editing the configuration of the bot).

Rules are based on a collection of metrics which this app interprets from raw Steem data. For example, you could add 10 score points for every image, or deduct 2 points for every minute since the post was created.

These rules, called an algorithm, are editable through the server app Dashboard, and you can also view, run statistics, logs, and tests here.

The server is designed to be triggered periodically for a bot run iteration, for example every 30 or 60 minutes. This can be done on Heroku with an add-on, or manually on the dashboard provided, or even by a HTTP GET method to ```/run-bot?json=true&api_key=BOT_API_KEY``` endpoint, which is used internally and can be used externally by a separate app.

## Usage
Open the bot dashboard using your Heroku app root URL, as above. All operations are available through the dashboard.

The operations you can perform are:

- Run bot now (WILL VOTE)
- Check bot stats
- Edit curation algorithm weights and white / black lists
- Edit configuration and settings of bot
- Run algorithm test (does not actually vote)
- View last log

_Dashboard with active session_

![](/img/dashboard-active-session-1.png)

---

_Stats for post metrics breakdown_

![](/img/bot-run-overview-2.png)

## Installation
See the [installation guide](/docs/installation.md). 

Alternatively, you can deploy this server to Heroku with one click. [![Deploy](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy?template=https://github.com/nolyoly/prosper-ai-node)

Be sure to read through the Heroku website. Check on their pricing (they offer a free account), features, terms of service, acceptable use policy, and other information available on their site.

## Keep your bot up to date
Please see also the [installation guide](/docs/installation.md) for instructions on how to keep your server up to date with further releases of Voter.

## Footnotes
See [the license](/LICENSE) for full legal text. You are at your own liability if you use this software. We are not running a service and therefore are not required to provide a terms of service policy.

Contributions via pull request are very welcome, as are issues logged via the GitHub issue tracker. You can also suggest features, such as metrics you'd like to see, UI upgrades, etc. We encourage these submissions to be submitted via [Utopian.io](https://utopian.io/) though! It is another great Steem project that rewards open-source developers for all of their hard work. ;)

I hope to revitalize this project with the help of the Steem community to make bot voting great again as we have recently seen a lot of backlash from some whales in the Steemit community. Our goal isn't to make anyone money, but to help good content creators get recognized and receive the credit they deserve for their hard work!

## License and acknowledgements
All original programming is under the CC0 license and thus completely open and free to use in any capacity. It's in the spirit of the project that it is open to all.

Credit for the original Fossbot is to [personz](https://steemit.com/@personz) and [Steem-FOSSbot)(https://github.com/Steem-FOSSbot). I have just forked this project since it seems to have been abandoned and I believe it has great potential and thus should continue to be developed.

Included in this repo are the following libraries, and all licenses are in the root folder of the project, except where stated:

- [Bootstrap](https://getbootstrap.com/) is used for web frontend, and so included in this repo, and is under the [MIT license](/LICENSE-Bootstrap), copyright to Twitter.
- [jQuery](https://github.com/jquery/jquery) is used as a dependency of Bootstrap, and for grabbing stats and algorithm data on request from the browser. It is copyright JS Foundation and other contributors and used by permission of the [license](/LICENSE-jQuery.txt)
- MD5 Hashing algorithm ([modified from this source](http://www.queness.com/code-snippet/6523/generate-md5-hash-with-javascript)) by Paul Johnston and Greg Holt is under copyright and licensed under the BSD license. Legal text [available here](http://pajhome.org.uk/site/legal.html) and [at source usage](/extra.js)).
- [C3js](http://c3js.org/) is used for charting stats data and is under [MIT license](/LICENSE-c3), copyright Masayuki Tanaka
- [D3js](https://d3js.org/) is a dependency for CSjs, and is under [3-part BSD license](/LICENSE-d3), copyright Michael Bostock

The [steem Node.js package](https://www.npmjs.com/package/steem) by adcpm is central to the app, a big thank you to the creators. Please [star it on GitHub](https://github.com/adcpm/steem) to support their development and check out their project [Busy](https://github.com/adcpm/busy).

Several other Node NPM libraries are used as dependencies. Their source is not included in this repo, but is downloaded when the server is built. Thanks to their creators!

- [express](https://www.npmjs.com/package/express), [express-session](https://www.npmjs.com/package/express-session), [body-parser](https://www.npmjs.com/package/body-parser), [cookie](https://www.npmjs.com/package/cookie) and [cookie-parser](https://www.npmjs.com/package/cookie-parser) by dougwilson, as widely used glue, used by many Node.js apps
- [Q](https://www.npmjs.com/package/q) by kriskowal, to promise-ify and de-callback-hell-ify the long process of running a bot iteration
- [redis](https://www.npmjs.com/package/redis) by bridgear, to access a redis simple database
- [glossary](https://www.npmjs.com/package/glossary) by harth, for keyword extraction from Steem post body contents using NLP
- [string](https://www.npmjs.com/package/string) by az7arul, for misc super powered string manipulation
- [remark](https://www.npmjs.com/package/remark) and [strip-markdown](https://www.npmjs.com/package/strip-markdown) by wooorm, for de-markdown-ing Steem post body contents
- [retext](https://www.npmjs.com/package/retext) and [retext-sentiment](https://www.npmjs.com/package/retext-sentiment) also by wooorm, for determining sentiment using NLP
- [languagedetect](https://www.npmjs.com/package/languagedetect) by fgribreau, to detect the written language of the content (latin script only) 
- [wait.for](https://www.npmjs.com/package/wait.for) by luciotato, for turning async functions into sync functions
- [moment](https://www.npmjs.com/package/moment) by ichernev and [moment-timezone](https://www.npmjs.com/package/moment-timezone) by maggiepint, for better date handling, formatting and time zone adjustment

## Changelog

- v0.0.1
  - Merge 'develop' branch from Foss bot to master branch of prosper-ai-node.
  - Update Readme.md to reflect the Prosper-ai project and not Fossbot.
