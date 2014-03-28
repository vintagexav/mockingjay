Mockingjay
===========

A Twitter API 1.1 script to make a Twitter bot that retweets tweets that contain words in a RegEx. Built off of <a href="https://github.com/abelsonlive/regextweet" target="_blank">RegEx Tweet</a>, 

It currently powers [@YourRepsOnGuns](http://twitter.com/yourrepsonguns), retweeting members of congress when they tweet about firearms and related words. 

We originally made this project when we were working at The Daily Beast and compiling every member of congress's stance on gun control for [This Is Your Rep On Guns](http://thedailybeast.thisisyourreponguns.com). Read more about that project and the origins of this bot [here](http://newsbeastlabs.tumblr.com/post/41373060897/update-feb-10-repsguntweets-has-been-changed-to).

# Installation

````
npm install mockingjay
````

# Usage

````
var mockingjay = require('mockingjay');

var opts = {
  bot_name: "obamacare-bot",
	list_owner: "cspan",
	list_name: "members-of-congress",
	count: 200,
	regex: "(Obamacare|Obama)",
  credentials: {
    consumer_key:         ...,
    consumer_secret:      ...,
    access_token:         ...,
    access_token_secret:  ...
  }
}

mockingjay.retweet(opts, function(err, result){
  if (!err){
    console.log(result)
    /*{
      "retweeted_matches": true,
      "since_last": 20,
      "matching": 5
    }*/
  }else{
    console.log(err)
  }
})
````

### Options

Give your bot a filename-friendly name with the `bot_name` option. Mockingjay only checks new tweets since the last time it ran. It does this by saving the id of the most latest tweet in a file at `src/last-ids/<bot-name>-last-id.json`. Specifying a name will make sure that your bot flock won't get confused about when each one ran. 

`count` is how many tweets to return. 

### Callback

`result` returns an object. If `retweeted_matches` is true, it found new matching tweets and retweeted them without error. If everything went well but it didn't find any matches, `status` is `false`. `since_last` are the number of new tweets in that list since last it checked. `matching` is the number of new and matching tweets since last it checked.
