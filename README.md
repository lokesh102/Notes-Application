# Project Name
Notes-Application is an app which helps user to create, read, update, delete notes, Implemented using microservices Architecture.

# Project Folders
1) notes-APP (main APP which can be used by any authenticated user)
2) OAuth2.0AuthorizationServer (which is used for authentication of user, and also for issuing user token to interact with notes-App)

## Table of Contents

## Features
- Application contains REST API's for all CRUD operations which can be used to interact with the resource created by user.
- This Application uses OAuth 2.0 Authorization service for authentication purpose which uses Spring OAuth Authorization Server library, which internally issues token for logged in user
- Implemented some other features like searching, rate limiting for better efficiency.

# Authorization App API's
- clone the project OAuth2.0AuthorizationServer
- Initially, user has to signup into application via postman by providing username and password as request body
  - This API was supported in OAuth2.0AuthorizationServer application, inorder to get the access token, follow these steps:
    1) send POST request to /api/auth/signup with username and password as request body.
    2) Now, the user account has created, he can login into the application, as we are using OAuth 2.0 we can generate token using Postman.
       - go to Authorization tab in postman, there Configure new token can be found and we need to use that for getting token
       - provide token name (can be anything)
       - Grant Type : Authorization-Code
       - Callback-URL : https://oauth.pstmn.io/v1/callback
       - Auth URL: http://localhost:5000/oauth2/authorize (change domain and port accordingly)
       - Access Token URL : http://localhost:5000/oauth2/token (change domain and port accordingly)
       - provide client-id and client-secret ( I used postman-client, postman-secret, which was created at initial stage of project)
       - provide scope for which the client has access
       - Client Authentication : send as Basic Auth Header
       - click on Generate New Access Token
       - you will get a pop-up asking for username and password, provide them if they are validated you will get new access token
       - use this access token for sending API request for notes API's.
       - change the Issuer Url in application.properties file of notes-App accordingly
       - Environment Variables used in OAuth2.0AuthorizationServer (note : change them accordingly)
          -  Authentication-Service-URL=jdbc:mysql://{MYSQL-HOST}:3306/user_authentication;
          -  Authentication-Service-Username=user_authentication;
          -  Authentication-Service-Password=user_authentication;
          -  Authentication-Service-Port=5000

- # notes-App API's
    - clone the project notes-App
    - GET /api/notes: get a list of all notes for the authenticated user.
    - GET /api/notes/ get a note by ID for the authenticated user.
    - POST /api/notes: create a new note for the authenticated user.
    - PUT /api/notes/ update an existing note by ID for the authenticated user.
    - DELETE /api/notes/ delete a note by ID for the authenticated user.
    - GET /api/search?q=:query: search for notes based on keywords for the authenticated user.
    - Environment Variables used in OAuth2.0AuthorizationServer (note : change them accordingly)
       -  Authentication-Service-URL=jdbc:mysql://{MYSQL-HOST}:3306/user_authentication;
       -  Authentication-Service-Username=user_authentication;
       -  Authentication-Service-Password=user_authentication;
       -  Authentication-Service-Port=5000
