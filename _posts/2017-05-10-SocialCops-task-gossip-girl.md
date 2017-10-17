---
layout: post
title: "SocialCops Task: Gossip Girl"
comments: true
description: "Task Solution for SocialCops Internship 2017"
keywords: "socialcops, social cops, flask, python, heroku, mongodb, web app, analysis, analytic, automation, graph, data analysis, data visualisation, socket, socketio, asynchronous, real time, notification, pub sub pattern, publisher, subscriber, pattern"
---

## A Real Time notification system task for SocialCops

### Problem Task: 

Create a real time notification system to notify subscribers about the changes in the MongoDB database.
[Link](https://drive.google.com/file/d/0B2wvr5gjqmj3U2Q0ZXhHS0JUMkk/view?usp=sharing) to complete task.

### Solution:

Due to lack of knowledge about Gossip Girl and their characters, I have updated the task to notify us about the updates of various TV shows instead of characters of Gossip Girl.

### Tech Stack: 

Web app = Flask + Heroku + SocketIO + MongoDB/MongoLab

### Screenshots and how to use it:

![login](https://raw.githubusercontent.com/akul08/gossip_girl/master/static/img/1.png?raw=true)

- First Register and Login:
    username: `akul`
    password: `1234`



![index](https://raw.githubusercontent.com/akul08/gossip_girl/master/static/img/2.png?raw=true)

- Then Goto `/Rooms` and subscribe to your favourite TV Shows

![rooms](https://raw.githubusercontent.com/akul08/gossip_girl/master/static/img/3.png?raw=true)

- Goto `/Notification` for real time subscribed Notifications, notifications of not subscribed TV shows are not shown here.

![notifs](https://raw.githubusercontent.com/akul08/gossip_girl/master/static/img/4.png?raw=true)

- Goto `/All Notifs` for real time Notifications for all TV shows

![all notifs](https://raw.githubusercontent.com/akul08/gossip_girl/master/static/img/5.png?raw=true)

- Open `/Update DB` in new tab and send an update for a TV show to MongoDB. This is inserted in the MongoDB db and a notification is sent to `/Notifications` if subscribed and `/All Notifs` in real time via SocketIO.

![updatedb](https://raw.githubusercontent.com/akul08/gossip_girl/master/static/img/6.png?raw=true)

- Notification about update on Flash TV show is sent to both `/Notifications` and `/All Notifs`.

![notifs & all notifs](https://raw.githubusercontent.com/akul08/gossip_girl/master/static/img/7.png?raw=true)

- Again sending Notification about `Game of Thrones` which is not subscribed by `akul`

![updatedb again](https://raw.githubusercontent.com/akul08/gossip_girl/master/static/img/8.png?raw=true)

- On Sending notification about `Game of Thrones`, only `/All Notifs` will receive as `akul` is not following `Game of Thrones` and hence no notification in `/Notifications`

![notifs & all notifs again](https://raw.githubusercontent.com/akul08/gossip_girl/master/static/img/9.png?raw=true)

- `Logout` and Exit the program

---

Link to Github Repo: [Here](https://github.com/akul08/gossip_girl)

#### Resources:

- [The Mega Flask tutorial](https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world)

- [SocketIO for Flask for Real time connection and exchange of Data](flask-socketio.readthedocs.io)

- [Pub/Sub pattern & notification on MongoDB updates](http://blog.pythonisito.com/2013/04/mongodb-pubsub-with-capped-collections.html)
