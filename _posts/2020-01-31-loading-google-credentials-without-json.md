---
layout: post
title:  "Loading Google Credentials without .json"
date:   2020-01-31 06:00:00 +0200
categories: blog
tags: [clojure,gcloud,ci,cd,useful]
group: dev
---

I primarily use heroku to run my applications and Travis for CI/CD. I'm also currently giving Github Actions a try. So what do all those have in common? Well, for starters they have generous free tiers, but more importantly they're not in the Google Cloud. Google cloud has some really nifty capabilities and so I end up using them pretty often. That's where my problem started. 

When you want to authenticate your application from outside the Google Cloud you need to read in a `.json` file that contains the service account information.

```java
File credentialsPath = new File("/home/user/Downloads/[FILE_NAME].json");  
```

or

```bash
export GOOGLE_APPLICATION_CREDENTIALS="/home/user/Downloads/[FILE_NAME].json"
```

So we basically need to get this `.json` file into all our CI/CD pipelines and our application servers. Obviously we can't store the credentials in `git` so we need to encrypt and upload the file. Admin! 

[alekcz/google-credentials](https://github.com/alekcz/google-credentials) solves exactly this problem. Your clojure app can now load credentials from an environment variable using `alekcz/google-credentials`.You need not keep that super secret `.json` file anymore. Copy its contents into the environment and delete the file!

And there you go. Nothing but net.

![Kobe!](https://media.giphy.com/media/UYlu2EDUdiVl6/giphy.gif)


_May your build always pass._

_Alex_


P.S. Rest in peace Kobe. 