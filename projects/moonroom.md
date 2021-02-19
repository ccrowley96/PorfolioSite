---
title: MoonRoom
subtitle: Private community spaces.
date: 2021-02-19
externalLink: https://www.moonroom.app/
github: https://github.com/ccrowley96/moonroom
tags:
  - mongo
  - docker
  - graphql
  - apollo
  - oauth
  - node
  - react
  - javascript
  - scss
---

![daFam](/img/moonroom/dafam.png)

## Problem

Do you have iMessage, Facebook, Discord, WhatsApp, Hangouts, and other chat groups? Do you like sharing links, music, favorite recipes, books and TV suggestions with those closest to you? I do too.

The problem is, these links we share often get lost in the quickly scrolling chronological chat histories between multiple platforms.

What if there was a centralized link library where you could share, tag, comment on and search the media you share with your private communities? And what if you could easily share these ‘posts’ across communities? Something like a communal Google keep, or a (very simplified) private Reddit.

## Idea

MoonRoom is my attempt at answering these questions. It’s a place to share with your private communities in a more than chronological way. A place to backup, categorize, and share anything with your family, colleagues, and close friend groups.

## Creating MoonRoom

Here are some of my early sketches on the tech / UI for MoonRoom.

![daFam](/img/moonroom/sketches.png)

Ok, so MoonRoom is a place to share with private communities in a categorized and searchable way. The app is built around a few main concepts. I’ll do a quick overview of these high level concepts and the application architecture before getting into more detail. The four concepts below also happen to be the four database models (collections of data) used in the app.

**Moons**
Moons represent a community of people. Anyone can create a moon, becoming the ‘Mission commander’. The commander can share a unique moon link with anyone, inviting them to their moon.

![daFam](/img/moonroom/moons.png)

**Rooms**
Rooms are a way to categorize ideas shared on a moon - like subreddits for Reddit. Some example rooms might be: Books, Movies, Music, Podcasts and Recipes.

![daFam](/img/moonroom/rooms.png)

**Posts**
Posts are, well, posts. Reddit, Facebook, Twitter, Instagram, etc… You get the idea. These posts can be tagged allowing an additional level of organization and are easily searchable using the search bar. Posts are paginated into pages using an ‘infinite scroll’ technique, only loading small batches of data onto the client at a time.

![daFam](/img/moonroom/posts.png)

**Users**
Users login via Google OAuth login. This provides a one-click login which is extremely secure. It also means I don't have to hash, encrypt, store, or worry about passwords. The only user information I store is name, email, and profile picture, which Google provides. People are often scared when they see 'Login with Facebook' or 'Login with Google', but this simply means, use my Google account, which has a whole FLEET of security engineers, rather than sending a new plain text password to a less established website.

Users just press 'Log in with google'. Google logs the user in and sends MoonRoom a token. MoonRoom verifies that token with Google and asks for the user's name, email, and profile picture. Finally, MoonRoom sends its own token back to the client which represents the active, logged in, session. Any future request to the server needs to attach this token in order to be authenticated.

The first time a user logs in, they are entered in the user database. Subsequent logins search the database for that user. Tokens are used to verify a user is who they say they are, protecting the API and data and persisting sessions on the client. These allow you to refresh the page and stay logged in.

![daFam](/img/moonroom/users.png)

## Tech stack in depth

This project builds off of a [boilerplate repository](https://github.com/ccrowley96/fullstack-auth-docker-boilerplate) I created for setting up dockerized fullstack Google OAuth, GraphQL, Mongo, Express and React applications.

**HTTP Server**

- Node / Express to serve files and and respond to incoming requests.
- Spins up an Apollo GraphQL server.
- `/auth` API route for logging user in and returning session token

**GraphQL**
Query language for APIs which allows client to query exactly what they need from the server.

- Makes evolving APIs easier
- Creates a schema, which provides a contract between client and server.

**Apollo Server**
Simple and performant GraphQL server.

- Integration with Express.js
- `/graphql` endpoint exposes GraphQL
- Dev playground for testing queries
- Provides structure for setting up GraphQL backend (schema, resolvers, datasources)

**Database**
MongoDB using Mongoose to interact with the Mongo database using JavaScript.

**Docker**
Containerizes dev environment, making it easy to develop on any machine and quickly deploy to the cloud.

- Server container
- Client container
- MongoDB container
- Containers are locally networked together

**React**
A Javascript library for building user interfaces.

**React router**
Navigation between pages for React apps.

**Apollo client**
A state management library for JS which manages both local and networked data.

- Auto caching
- Works well with React hooks
- Fetches, caches, and modifies application data

**SCSS**
Used to style web pages in a more extensible and reusable way.

- Class nesting
- Re-usable variables
- Importing / extending styles

**provideAppState**
Custom React hook which combines react-context and useReducer to provide global application state. Very similar to Redux, but implemented with React hooks.
