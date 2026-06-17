# Prompts.md

## Sprint 10 – MongoDB Atlas, Mongoose ODM & Relational Data Modeling

This document records how AI was used as a learning and debugging assistant during development.

---

## Prompt 1: Understanding the Sprint Requirements

### Why I Asked

This was my first project using MongoDB Atlas and Mongoose. I wanted to understand what was changing compared to Sprint 09.

### Prompt

"Explain Sprint 10 requirements in simple terms and compare them with Sprint 09."

### What I Learned

* Sprint 09 used temporary in-memory arrays.
* Sprint 10 requires persistent cloud storage.
* Data must survive server restarts.
* MongoDB Atlas acts as the database.
* Mongoose acts as the bridge between Express and MongoDB.

### How I Applied It

I replaced the in-memory blogPosts array with MongoDB collections.

---

## Prompt 2: MongoDB Atlas Setup

### Why I Asked

I had never created a cloud database before.

### Prompt

"Walk me through creating a MongoDB Atlas cluster and connecting it to a Node.js application."

### What I Learned

* How Atlas clusters work.
* How to create a database user.
* How to obtain the connection string.
* Why Network Access settings are required.

### How I Applied It

I created a free Atlas cluster and generated a connection URI.

---

## Prompt 3: Securing Credentials

### Why I Asked

The sprint instructions warned against exposing database credentials.

### Prompt

"Why should MongoDB credentials be stored in .env instead of directly inside server.js?"

### What I Learned

* Hardcoded secrets are visible in GitHub.
* Environment variables separate code from configuration.
* .env files should never be committed.

### How I Applied It

I stored MONGO_URI inside .env and added .env to .gitignore.

---

## Prompt 4: Connecting Express to MongoDB

### Why I Asked

I needed to understand how Express communicates with Atlas.

### Prompt

"Explain mongoose.connect() and how database connections are established."

### What I Learned

* Mongoose manages database connections.
* Connection promises can be handled using .then() and .catch().
* Successful connections should be logged.

### How I Applied It

I added mongoose.connect(process.env.MONGO_URI) to server.js.

---

## Prompt 5: Creating a Schema

### Why I Asked

I didn't understand how MongoDB documents are structured.

### Prompt

"Explain Mongoose schemas and models using a blog post example."

### What I Learned

* Schemas define document structure.
* Models provide database methods.
* Collections are automatically created from models.

### How I Applied It

I created a Post schema with title, content, authorId, createdAt, and updatedAt fields.

---

## Prompt 6: Migrating CRUD Operations

### Why I Asked

I previously used JavaScript arrays and needed to move to database queries.

### Prompt

"Show the MongoDB equivalent of array-based CRUD operations."

### What I Learned

* Post.create() inserts records.
* Post.find() retrieves records.
* Post.findById() retrieves one record.
* Post.findByIdAndUpdate() updates records.
* Post.findByIdAndDelete() removes records.

### How I Applied It

I replaced all array logic with Mongoose methods.

---

## Prompt 7: Debugging Atlas Connection Errors

### Why I Asked

My application failed to connect to Atlas.

### Prompt

"I am getting MongooseServerSelectionError. How do I debug Atlas connection issues?"

### What I Learned

* Atlas blocks unknown IP addresses.
* Network Access settings must be configured.
* Incorrect connection strings can cause DNS errors.
* Environment variables must load correctly.

### How I Applied It

I fixed the Atlas whitelist settings and corrected the connection string.

---

## Prompt 8: Understanding ObjectIds

### Why I Asked

I noticed MongoDB generated IDs instead of numeric IDs.

### Prompt

"Explain MongoDB ObjectIds and why they replace manual IDs."

### What I Learned

* MongoDB automatically creates unique identifiers.
* ObjectIds are globally unique.
* Manual counters are unnecessary.

### How I Applied It

I removed numeric ID logic and used MongoDB-generated IDs.

---

## Prompt 9: Relational Modeling

### Why I Asked

The sprint required a User and Post relationship.

### Prompt

"Explain relationships in MongoDB and how references work."

### What I Learned

* MongoDB uses document references instead of SQL joins.
* ObjectIds can reference documents in another collection.
* Relationships are defined using ref.

### How I Applied It

I added authorId to the Post schema and linked it to User documents.

---

## Prompt 10: Understanding populate()

### Why I Asked

I needed to understand how author information appears inside post responses.

### Prompt

"What does populate() do and why is it needed?"

### What I Learned

* populate() replaces ObjectIds with actual documents.
* It allows related data to be returned in a single API response.
* It behaves similarly to a join.

### How I Applied It

I added populate("authorId") to my GET routes.

---

## Prompt 11: Aggregation Requirement

### Why I Asked

The sprint required a Top 3 Most Recent Posts endpoint.

### Prompt

"How can I return the latest three posts using MongoDB queries?"

### What I Learned

* sort() controls document ordering.
* limit() restricts results.
* createdAt timestamps can be used for recency.

### How I Applied It

I created the /posts/recent/top3 endpoint.

---

## Prompt 12: API Testing

### Why I Asked

I wanted to verify database persistence.

### Prompt

"Give me a Postman testing workflow for all endpoints."

### What I Learned

* Test users before posts.
* Verify author references.
* Verify populate() output.
* Verify data appears in Atlas.

### How I Applied It

I tested every route using Postman and checked Atlas after each operation.

---

## Prompt 13: Deployment Preparation

### Why I Asked

I needed to deploy the application safely.

### Prompt

"How should I deploy an Express + MongoDB Atlas application?"

### What I Learned

* Render is suitable for Express servers.
* Environment variables must be configured on the hosting platform.
* Database credentials should never be committed to GitHub.

### How I Applied It

I prepared the project for deployment using environment variables.

---

## Key Learning Outcomes

Through Sprint 10 I learned:

* MongoDB Atlas cloud database setup
* Mongoose schemas and models
* Database CRUD operations
* ObjectIds and references
* Relational modeling in MongoDB
* populate() for data hydration
* Query sorting and limiting
* Environment variable security
* Atlas troubleshooting
* Express deployment workflow

AI was used for learning concepts, debugging issues, understanding errors, and reviewing architecture decisions. All implementation was completed after understanding the concepts and applying them within the project requirements.
