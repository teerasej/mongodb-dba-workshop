
# Challenging MongoDB Performance Scenarios and Cases

You can use [chatGPT](https://chatgpt.com/) for working with this!

### Scenario 1: **Role: Database Administrator for a Streaming Service**

- **Scenario:** You are responsible for managing the performance of a MongoDB database that stores movie information and viewer comments. Your goal is to ensure that the database can handle complex queries efficiently, particularly as the number of viewers and the amount of data grows.

#### Real-World Cases (Query Creation):
1.  Retrieve all comments for a specific movie by its title.

2.  List all movies released between 2010 and 2020, sorted by the number of comments.
   

3. Find all movies where the comments include specific keywords, and the movie’s rating is above 'G'.
   

#### MongoDB Queries (Index Creation):
1.  Create an index to improve the performance of queries that retrieve movies by their title.
   
2.  Create an index to speed up the query that sorts movies by the number of comments.
   
3. Create an index to optimize the query that searches for specific keywords in comments and filters movies by rating.
   
---

### Scenario 2: **Role: Data Analyst for a Film Industry Report**
- **Scenario:** As a data analyst, you are tasked with generating reports that involve querying large amounts of data from a MongoDB database. You need to create efficient queries to generate insights and indexes to improve the speed of these queries.

#### Real-World Cases (Query Creation):
1.  Generate a list of all movies released in 2020.
2.  Count the number of comments for movies directed by a specific director.
3. Identify movies with an average rating above 9 that have more than 100 comments.
  
#### MongoDB Queries (Index Creation):
1.  Create an index to improve the performance of retrieving movies by their release year.
  
2.  Create an index to optimize counting comments by a specific director.
   
3. Create an index to speed up queries that find movies with high ratings and many comments.
   
---

### Scenario 3: **Role: Backend Developer for a Movie Review Platform**
- **Scenario:** You are a backend developer working on a platform where users can browse movies and read or leave comments. Your responsibility includes optimizing the database to ensure a smooth user experience, especially when loading lists of movies or comments.

#### Real-World Cases (Query Creation):
1.  Retrieve a list of comments left by a specific user.
   
2.  List movies along with the first 10 comments sorted by the date they were posted.
   
3. Find movies that have been commented on in the last week and are rated PG-13.
   
#### MongoDB Queries (Index Creation):
1.  Create an index to improve performance when retrieving comments by user email.
   
2.  Create an index to optimize sorting comments by the date they were posted.
   
3. Create an index to improve querying for movies with recent comments and a specific rating.
   
---

These scenarios and cases should help learners understand the importance of creating efficient queries and indexes to optimize the performance of MongoDB databases. Each scenario is tied to a specific role, making the exercises relevant and applicable to real-world situations.
