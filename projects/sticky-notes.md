---
title: Sticky Notes
subtitle: A (super basic) Google Keep clone I built with my brother Tim
date: 2020-07-18
github: https://github.com/ccrowley96/notes
tags: 
    - mongo
    - node
    - react
    - javascript
    - scss
---

My brother <a href = "https://timothycrowley.me" target="_blank">Tim</a> and I just built a very simple bulletin board sticky note app.  Similar to Google Keep (but with way less features), this app lets you jot down thoughts and notes online, and then return to them later.  Mostly, it was an exercise in the MERN stack, UI design, and persistent web data.

Here's what the app looks like now (as of July 19th 2020).

![Finished Sticky Note App](/img/sticky-notes/front-end.png)

### Here's how it works
The backend is a simple Node / Express API and web server.  The API sets up endpoint and listens for requests.  These include creating a board, verifying a board exists, getting all notes from a board, deleting a note, editing a note, and changing a notes' color.  Here's an overview of the API endpoints we set up.

```js
POST 'api/board' // Creates a new board 
```
```js
GET 'api/verifyBoard/:bid' // Verifies board exists in DB
```
```js
USE 'api/board/:bid' // Finds board by ID
```
```js
GET 'api/board/:bid/notes' // Get all notes
```
```js
POST 'api/board/:bid/note' // Create new note
```
```js
DELETE 'api/board/:bid//note/:id' // Delete note by ID
```
```js
POST 'api/board/:bid/note/:id/changeColor/:color' // Change color of a note
```
```js
POST 'api/board/:bid/note/:id/changeContent' // Edit note content
```

For those familiar with APIs, this likely needs no further explanation. For anyone else, this is a **very** simple REST API.  These endpoints will listen for requests from the front-end (a React app in our case) and take the actions shown above.  To create a note for example, the request would look something like this:

```js
    URL '/board/5f13613d79ab2f0217689f8e/note'
    {
        content: 'My first sticky note',
        color: 'yellow'
    }
```

This HTTP request is sent from the user's web client to the backend.  When the API we set up receives the request, it adds a new note to the board with ID `5f13613d79ab2f0217689f8e`.

### The Front End
After testing the API with <a href = "https://www.postman.com/" target="_blank">POSTMAN</a> (a sweet app that lets you test HTTP request before building a front-end), we began work on the front-end in React.

We used <a href = "https://github.com/facebook/create-react-app" target="_blank">Create React App</a> to breeze over the complexities of Babel, Webpack, SCSS, and hot reloading, and skip right to building in React.

The structure of this app is v simple. Here is our initial sketch on how we'd layout the React components.

- `App (top level component)`
    - `Bulletin Board (fetches notes)`
        - `Sticky Note (renders notes)`
            - `Color Picker (color picker triggers change color actions)`

![React Component Layout](/img/sticky-notes/react-components.jpg)

After setting up the React Components, we had a cool looking online bulletin board... but the problem was, every person who visited the site shared the same board.

To fix this, we added a **board** model to the database.  Every time a new user visits the site `api/board` is hit, automatically creating a new board, and returning the new board's ID to the client.  This ID is then saved in local storage, and inserted into any future request this user makes.  Doing it this way avoids creating user accounts, passwords, and bloating the app with user credentials.  Now, every user has their own board.  I used a very similar method when creating <a href = "https://corycrowley.me/projects/grocerylist/" target="_blank">Grocery List</a>.

The site is live <a href = "https://my-sticky-notes.herokuapp.com/" target="_blank">here</a> if you want to check it out : )



