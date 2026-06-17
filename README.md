# The Data Hub

A RESTful API built with Node.js, Express, MongoDB Atlas, and Mongoose. This project demonstrates cloud database integration, CRUD operations, schema modeling, middleware, authentication scaffolding, document relationships, and aggregation queries.

## Features

- MongoDB Atlas cloud database integration
- Mongoose schema and model architecture
- Persistent database storage
- Create, read, update, and delete posts
- User and Post relationship modeling
- Populate author information using Mongoose
- Custom request logging middleware
- Mock authentication endpoint using environment variables
- Top 3 recent posts endpoint
- Environment variable configuration with dotenv

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
cd data-storm
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

ADMIN_USERNAME=admin
ADMIN_PASSWORD=password123

AUTH_TOKEN=your_mock_token
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
data-storm/
│
├── models/
│   ├── post.js
│   └── user.js
│
├── server.js
├── package.json
├── README.md
└── prompts.md
```

---

## Database Models

### User Model

```js
{
  name: String,
  email: String
}
```

### Post Model

```js
{
  title: String,
  content: String,
  authorId: ObjectId,
  createdAt: Date,
  updatedAt: Date
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
  "content": "MongoDB stores data as documents.",
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

Successful Response:

```json
{
  "message": "Login successful",
  "token": "your_mock_token",
  "expiresIn": "1h"
}
```

---

## Middleware

Every request passes through a custom logger middleware.

Example:

```text
[GET] /posts - 10:05 AM
[POST] /posts - 10:06 AM
[DELETE] /posts/2 - 10:07 AM
```

---

## MongoDB Relationships

Posts are linked to users through the `authorId` field.

```js
authorId: {
  type: mongoose.Schema.Types.ObjectId,
  ref: "User"
}
```

When fetching posts, Mongoose automatically populates the author details using:

```js
.populate("authorId")
```

Example Response:

```json
{
  "_id": "123",
  "title": "Learning MongoDB",
  "content": "MongoDB stores data as documents.",
  "authorId": {
    "_id": "456",
    "name": "Sadashiv",
    "email": "sadashiv@example.com"
  }
}
```

---

## Aggregation / Recent Posts Endpoint

Returns the three most recently created posts.

```http
GET /posts/recent/top3
```

Implementation:

```js
Post.find()
  .populate("authorId")
  .sort({ createdAt: -1 })
  .limit(3);
```

---

## Testing Workflow

1. Create a user
2. Copy the generated user ID
3. Create multiple posts using that author ID
4. Fetch all posts
5. Verify populated author information
6. Fetch a single post
7. Update a post
8. Delete a post
9. View the top 3 recent posts
10. Test login endpoint
11. Verify data persistence in MongoDB Atlas

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

## Learning Outcomes

This project demonstrates:

- MongoDB Atlas cloud database setup
- Mongoose schemas and models
- CRUD operations with MongoDB
- Environment variable management
- REST API development with Express
- Middleware implementation
- Document relationships using ObjectId references
- Data population using `populate()`
- Sorting and limiting database queries
- API testing using Postman

---

## Author

**Sadashiv Kandgole**
