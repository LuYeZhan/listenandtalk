
# listen&talk App

<br>

## Description

This is an social network app. You can finally interact in a social network, with just audio.

## User Stories

-  **404:** As an anon/user I can see a 404 page if I try to reach a page that does not exist so that I know it's my fault
-  **Signup:** As an anon I can sign up in the platform so that I can start recording talks or listen to newly created talks.
-  **Login:** As a user I can login to the platform so that I can either record or listen talks.
-  **Logout:** As a user I can logout from the platform so no one else can use it.
-  **Add Talks** As a user I can add a new talk, and listen to a talk created by someone else.
-  **Edit Talks** As a user I can edit my talks.
-  **Delete Talks** As a user I can delete my talks.
-  **Edit profiles** As a user I can edit my profile to my personal like.
-  **View Home** As a user I want to see all the talks that have been created.





## Backlog

User profile:
-  **View users profile** As a user I can see other user's profile, and their talks, if they accept my friend request.
-  **Interact with other users** As a user I can interact with others user's talks, responding to their talk.
-  **Search for a friend** As a user I can search other user's name and add them to friends



<br>


# Client / Frontend

## Routes
| Path                      | Component            | Permissions | Behavior                                                     |
| ------------------------- | -------------------- | ----------- | ------------------------------------------------------------ |
| `/splash`                 | Splash               | public      | Log in or Signup                                             |
| `/auth/signup`            | Signup               | anon only   | Signup form, link to login, navigate to homepage after signup|
| `/auth/login`             | Login                | anon only   | Login form, link to signup, navigate to homepage after login |
| `/auth/logout`            | n/a                  | anon only   | Navigate to splashpage after logout, expire session          |
| `/home`                   | Home                 | user only   | Shows all talks in a list                                    |
| `/profile`                | Profile              | user only   | Shows user's profile info                                    |
| `/talks/add`              | Talk                 | user only   | Adds a talk                                                  |
| `/profile/:id`            | TalkDetail           | user only   | Shows all the talks the user created, other user's can see and interact with the user |
| `/talks/:id`              | na                   | user only   | Delete talks                                                 |



## Components

- Login

- Splash

- SignUp

- Home

- Profile

- Talk

- TalkDetail

- Navbar

- Footer


 
## Services

- Auth Service
  - auth.login(user)
  - auth.signup(user)
  - auth.logout()
  - auth.me()
  - auth.getUser() // synchronous
- Tournament Service
  - tournament.list()
  - tournament.detail(id)
  - tournament.add(id)
  - tournament.delete(id)
  
- Player Service 

  - player.detail(id)
  - player.add(id)
  - player.delete(id)

- Game Service

  - Game.put(id)



<br>


# Server / Backend


## Models

User model

```javascript
{
  username - String // required
  email - String // required & unique
  password - String // required
  favorites - [ObjectID<Restaurant>]
}
```

Tournament model

```javascript
 {
   name:String,
   img:String,
   players: [{type: Schema.Types.ObjectId,ref:'Participant'}],
   games:[{type: Schema.Types.ObjectId,ref:'Game'}]
 }
```

Player model

```javascript
{
  name: String,
  img: String,
  score: []
}
```

Game model

```javascript
{
  player1: [{type: Schema.Types.ObjectId,ref:'Participant'}],
  player2: [{type: Schema.Types.ObjectId,ref:'Player'}],
  player2: [{type: Schema.Types.ObjectId,ref:'Player'}],
  winner: String,
  img :String
}
```


<br>


## API Endpoints (backend routes)

| HTTP Method | URL                         | Request Body                 | Success status | Error Status | Description                                                  |
| ----------- | --------------------------- | ---------------------------- | -------------- | ------------ | ------------------------------------------------------------ |
| GET         | /auth/profile               | Saved session                | 200            | 404          | Check if user is logged in and return profile page           |
| POST        | /auth/signup                | {name, email, password}      | 201            | 404          | Checks if fields not empty (422) and user not exists (409), then create user with encrypted password, and store user in session |
| POST        | /auth/login                 | {username, password}         | 200            | 401          | Checks if fields not empty (422), if user exists (404), and if password matches (404), then stores user in session |
| POST        | /auth/logout                | (empty)                      | 204            | 400          | Logs out the user                                            |
| GET         | /tournaments                |                              |                | 400          | Show all tournaments                                         |
| GET         | /tournaments/:id            | {id}                         |                |              | Show specific tournament                                     |
| POST        | /tournaments/add-tournament | {}                           | 201            | 400          | Create and save a new tournament                             |
| PUT         | /tournaments/edit/:id       | {name,img,players}           | 200            | 400          | edit tournament                                              |
| DELETE      | /tournaments/delete/:id     | {id}                         | 201            | 400          | delete tournament                                            |
| GET         | /players                    |                              |                | 400          | show players                                                 |
| GET         | /players/:id                | {id}                         |                |              | show specific player                                         |
| POST        | /players/add-player         | {name,img,tournamentId}      | 200            | 404          | add player                                                   |
| PUT         | /players/edit/:id           | {name,img}                   | 201            | 400          | edit player                                                  |
| DELETE      | /players/delete/:id         | {id}                         | 200            | 400          | delete player                                                |
| GET         | /games                      | {}                           | 201            | 400          | show games                                                   |
| GET         | /games/:id                  | {id,tournamentId}            |                |              | show specific game                                           |
| POST        | /games/add-game             | {player1,player2,winner,img} |                |              | add game                                                     |
| POST        | /games/add-all-games        |                              |                |              | add all games from a tournament. Gets a list of players and populates them via algorithm. |
| PUT         | /games/edit/:id             | {winner,score}               |                |              | edit game                                                    |
|             |                             |                              |                |              |                                                              |


<br>


## Links

### Trello/Kanban

[Link to your trello board](https://trello.com/b/PBqtkUFX/curasan) 
or picture of your physical board

### Git

The url to your repository and to your deployed project

[Client repository Link](https://github.com/screeeen/project-client)

[Server repository Link](https://github.com/screeeen/project-server)

[Deployed App Link](http://heroku.com)

### Slides

The url to your presentation slides

[Slides Link](http://slides.com)
