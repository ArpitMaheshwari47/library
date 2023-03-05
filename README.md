

## Assignment - Library Management

### Key points
we need you to create a system using following information and scenario
First we will create an Author, after that the particular authenticate user can create their book, they can update their book, delete their book, can check their all book.

####Technology Stack Used

 Backend - Node js
 Database - Mongodb

###Installing

###npm install

Start command

npm start

### Models
- User Model
```yaml
{ 
  title: {string, mandatory, enum[Mr, Mrs, Miss]},
  name: {string, mandatory},
  phone: {string, mandatory, unique},
  email: {string, mandatory, valid email, unique}, 
  password: {string, mandatory, minLen 8, maxLen 15},
  createdAt: {timestamp},
  updatedAt: {timestamp}
}
```

- Books Model
```yaml
{ 
  title: {string, mandatory, unique},
  excerpt: {string, mandatory}, 
  userId: {ObjectId, mandatory, refs to user model},
  ISBN: {string, mandatory, unique},
  deletedAt: {Date, when the document is deleted}, 
  isDeleted: {boolean, default: false},
  releasedAt: {Date, mandatory, format("YYYY-MM-DD")},
  createdAt: {timestamp},
  updatedAt: {timestamp},
}
```

## User APIs 
### POST /register
- Create a user -
- Create a user document from request body.
- Return HTTP status 201 on a succesful user creation. Also return the user document. The response should be a JSON object
- Return HTTP status 400 if no params or invalid params received in request body. The response should be a JSON object

### POST /login
- Allow an user to login with their email and password.
- On a successful login attempt return a JWT token contatining the userId, exp, iat. The response should be a JSON object 
- If the credentials are incorrect return a suitable error message with a valid HTTP status code. The response should be a JSON object

## Books API
### POST /books
- Create a book document from request body. Get userId in request body only.
- Make sure the userId is a valid userId by checking the user exist in the users collection.
- Return HTTP status 201 on a succesful book creation. Also return the book document. The response should be a JSON object like
- Return HTTP status 400 for an invalid request with a response body

### GET /books
- Returns all books in the collection that aren't deleted. Return only book _id, title, excerpt, userId, releasedAt
- Return the HTTP status 200 if any documents are found.
- If no documents are found then return an HTTP status 404 

### GET /books/:bookId
- Return the HTTP status 200 if any documents are found. The response structure (#successful-response-structure) 
- If no documents are found then return an HTTP status 404 with a response like (#error-response-structure) 

### PUT /books/:bookId
- Update a book by changing its
  - title
  - excerpt
  - release date
  - ISBN
- Make sure the unique constraints are not violated when making the update
- Check if the bookId exists (must have isDeleted false and is present in collection). If it doesn't, return an HTTP status 404 with a response body
- Return an HTTP status 200 if updated successfully 
- Also make sure in the response you return the updated book document. 

### DELETE /books/:bookId
- Check if the bookId exists and is not deleted. If it does, mark it deleted and return an HTTP status 200 with a response body with status and message.
- If the book document doesn't exist then return an HTTP status of 404 with a body



