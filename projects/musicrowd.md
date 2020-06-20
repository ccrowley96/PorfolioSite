---
title: MusiCrowd
subtitle: The crowdsourced DJ.
date: 2019-02-05
externalLink: http://musicrowd.ca
github: https://github.com/ccrowley96/MusiCrowd
images:
    - /img/musicrowd/musicrowd1.png
    - /img/musicrowd/musicrowd4.jpeg
    - /img/musicrowd/musicrowd3.jpeg
    - /img/musicrowd/musicrowd2.jpeg
tags: 
    - mern
    - javascript
    - spotify
---
## What it does
MusiCrowd is an interactive democratic music streaming service that allows individuals to vote on what songs they want to play next (i.e. if three people added three different songs to the queue the song at the top of the queue will be the song with the most upvotes). This system was built with the intentions of allowing entertainment venues (pubs, restaurants, socials, etc.) to be inclusive allowing everyone to interact with the entertainment portion of the venue. 

The system has administrators of rooms and users in the rooms. These administrators host a room where users can join from a code to start a queue. The administrator is able to play, pause, skip, and delete and songs they wish. Users are able to choose a song to add to the queue and upvote, downvote, or have no vote on a song in queue.

## How we built it
Our team used Node.js with express to write a server, REST API, and attach to a Mongo database.  The MusiCrowd application first authorizes with the Spotify API, then queries music and controls playback through the Spotify Web SDK.  The backend of the app was used primarily to the serve the site and hold an internal song queue, which is exposed to the front-end through various endpoints.  

The front end of the app was written in Javascript with React.js.  The web app has two main modes, user and admin.  As an admin, you can create a ‘room’, administrate the song queue, and control song playback.  As a user, you can join a ‘room’, add song suggestions to the queue, and upvote / downvote others suggestions.  Multiple rooms can be active simultaneously, and each room continuously polls its respective queue, rendering a sorted list of the queued songs, sorted from most to least popular.  When a song ends, the internal queue pops the next song off the queue (the song with the most votes), and sends a request to Spotify to play the song.  A QR code reader was added to allow for easy access to active rooms.  Users can point their phone camera at the code to link directly to the room.


## Challenges we ran into
- Deploying the server and front-end application, and getting both sides to communicate properly.
- React state mechanisms, particularly managing all possible voting states from multiple users simultaneously.
- React search boxes.
- Familiarizing ourselves with the Spotify API.
- Allowing anyone to query Spotify search results and add song suggestions / vote without authenticating through the site.


## Accomplishments that we're proud of
Our team is extremely proud of the MusiCrowd final product.  We were able to build everything we originally planned and more.  The following include accomplishments we are most proud of:
- An internal queue and voting system 
- Frontloading the development & working hard throughout the hackathon > 24 hours of coding
- A live deployed application accessible by anyone
- Learning Node.js

## What we learned
Garrett learned javascript :)  We learned all about React, Node.js, the Spotify API, web app deployment, managing a data queue and voting system, web app authentication, and so so much more.