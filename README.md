# The Data Hub

A RESTful API built with Node.js, Express, MongoDB Atlas, and Mongoose. This project demonstrates database-driven CRUD operations, schema modeling, middleware, authentication scaffolding, and document relationships using MongoDB.

## Features

- MongoDB Atlas cloud database integration
- Mongoose schema and model architecture
- Create, read, update, and delete blog posts
- User and Post relationship modeling
- Populate author information on posts
- Custom request logging middleware
- Mock authentication endpoint
- Recent posts endpoint
- Environment variable configuration using dotenv

---

## Tech Stack

- Node.js
- Express.js
- MongoDB Atlas
- Mongoose
- Dotenv
- Nodemon

---

## Installation

### Clone Repository

```bash
git clone <your-repository-url>
cd data-hub
```

### Install Dependencies

```bash
npm install
```

### Environment Variables

Create a `.env` file in the project root:

```env
PORT=5000
MONGO_URI=your_mongodb_connection_string
```

### Run Development Server

```bash
npm run dev
```

### Run Production Server

```bash
npm start
```

Server URL:

```text
http://localhost:5000
```

---

## Project Structure

```text
data-hub/
│
├── models/
│   ├── post.js
│   └── user.js
│
├── server.js
├── package.json
├── .env
└── README.md
```

---

## Database Models

### User

```js
{
  name: String,
  email: String
}
```

### Post

```js
{
  title: String,
  body: String,
  authorId: ObjectId,
  createdAt: Date
}
```

---

## API Endpoints

### Authentication

| Method | Route |
|----------|----------|
| POST | /login |

### Users

| Method | Route |
|----------|----------|
| POST | /users |

### Posts

| Method | Route |
|----------|----------|
| GET | /posts |
| GET | /posts/:id |
| POST | /posts |
| PUT | /posts/:id |
| DELETE | /posts/:id |
| GET | /posts/recent/top3 |

---

## Example Requests

### Create User

**POST /users**

```json
{
  "name": "Sadashiv",
  "email": "sadashiv@example.com"
}
```

---

### Create Post

**POST /posts**

```json
{
  "title": "Learning MongoDB",
  "body": "MongoDB stores data as documents.",
  "authorId": "USER_ID_HERE"
}
```

---

### Update Post

**PUT /posts/:id**

```json
{
  "title": "Updated Title"
}
```

---

### Login

**POST /login**

```json
{
  "username": "admin",
  "password": "password123"
}
```

Response:

```json
{
  "message": "Login successful",
  "token": "eyJhbGciOi..."
}
```

---

## Middleware

Every request is logged to the console.

Example:

```text
[GET] /posts - 10:05 AM
[POST] /posts - 10:06 AM
[DELETE] /posts/2 - 10:07 AM
```

---

## Relationship Modeling

Each post stores an `authorId` that references a user document.

When fetching posts, Mongoose `populate()` is used to include author details automatically.

Example:

```json
{
  "_id": "...",
  "title": "Learning MongoDB",
  "body": "MongoDB stores data as documents.",
  "authorId": {
    "_id": "...",
    "name": "Sadashiv",
    "email": "sadashiv@example.com"
  }
}
```

---

## Recent Posts Endpoint

Returns the three most recently created posts.

```http
GET /posts/recent/top3
```

Implemented using sorting and limiting database results.

---

## Testing

Tested using Thunder Client and Postman.

Recommended testing sequence:

1. Create a user
2. Create multiple posts
3. Fetch all posts
4. Fetch a single post
5. Update a post
6. Delete a post
7. View recent posts
8. Test login endpoint
9. Verify documents in MongoDB Atlas

---

## HTTP Status Codes

| Code | Meaning |
|--------|--------|
| 200 | Success |
| 201 | Created |
| 400 | Bad Request |
| 401 | Unauthorized |
| 404 | Not Found |
| 500 | Internal Server Error |

---

## Author

**Sadashiv Kandgole**