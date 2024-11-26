# MongoDB Course

## Overview

MongoDB, a leading NoSQL database, offers flexible schema design and robust querying capabilities it good for Enterprise Operations (EO). This document presents a set of Easy, medium, and hard-level questions to enhance our understanding of MongoDB by focusing on data manipulation, querying, and aggregation.

By exploring these questions, you can prepare for real-world challenges in Enterprise Operations (EO) environments. Whether you are a beginner looking to understand the basics or an experienced user aiming to deepen your knowledge engaging with these queries will help you gain practical insights using MongoDB effectively.

* ## MongoDB Exercises Practice
    We will consider some collections that we will use to perform various operations related to the MongoDB, which are defined below:

    1. ### Movies Collection:

    The Movies collection stores detailed information about each movie available for booking. This includes essential attributes such as the title, genre, release year, duration, ratings, and a list of actors. This data allows users to browse and select movies based on their preferences.

    ```
        {
            "movie_id": "UUID",
            "title": "String",
            "genre": "String",
            "release_year": "Number",
            "duration": "Number",  // in minutes
            "ratings": "Number",   // Average rating between 0 and 5
            "actors": ["Array of Actor Names"]
        }
    ```

    2. ### Theaters Collection:

    The Theaters collection contains information about the different theaters where movies are screened. Key attributes include the theaters name, location (city, state, and country) and its seating capacity. This information is crucial for users to choose a convenient location for their movie experience.

    ```
        {
            "theater_id": "UUID",
            "name": "String",
            "location": {
                "city": "String",
                "state": "String",
                "country": "String"
            },
            "seating_capacity": "Number"
        }
    ```

    3. ### Users Collection:

    The Users collection is designed to store information about the customers who use the booking system. It includes attributes such as the users name, email, date of birth and loyalty points. This data helps in managing user accounts and providing personalized services.

    ```
        {
            "user_id": "UUID",
            "name": "String",
            "email": "String",
            "date_of_birth": "Date",
            "loyalty_points": "Number"
        }
    ```

    4. ### Bookings Collection:

    The Bookings collection records all the bookings made by users. It includes details such as the user ID, movie ID, theater ID, number of seats booked, total price, and the booking date. This collection is essential for tracking user reservations and managing the overall booking process.

    ```
        {
            "booking_id": "UUID",
            "user_id": "UUID",              // Reference to Users collection
            "movie_id": "UUID",             // Reference to Movies collection
            "theater_id": "UUID",           // Reference to Theaters collection
            "seats_booked": "Number",       // Number of seats booked
            "total_price": "Number",        // Total price for the booking
            "booking_date": "Date"          // Date and time of the booking
        }
    ```

* ## MongoDB Exercises Questions for biggeners:

   This section contains 20 easy-level practice questions that are designed to help beginners familiarize themselves with basic operations in the Movie Booking System database schema. The questions will guide you through simple insertions, updates, deletions, and retrievals by allowing you to practice essential database operations effectively.

   1. ### Insert a new movie into the Movies collection.

   ```
    db.movies.insertOne({
        "movie_id": "1",
        "title": "Inception",
        "genre": "Sci-Fi",
        "release_year": 2010,
        "duration": 148,
        "ratings": 4.8,
        "actors": ["Leonardo DiCaprio", "Joseph Gordon-Levitt", "Elliot Page"]
    });
   ```

   ### Output:

   ```
    {
        "acknowledged": true,
        "insertedId": "1"
    }
   ```

   Explanation: The movie "Inception" is inserted into the collection successfully. The movie_id is manually set to "1", and no ObjectId is generated.

   2. ### Insert multiple users into the Users collection..

   ```
    db.users.insertMany([
    {
        "user_id": "1",
        "name": "John Doe",
        "email": "john.doe@example.com",
        "date_of_birth": ISODate("1985-04-23"),
        "loyalty_points": 120
    },
    {
        "user_id": "2",
        "name": "Jane Smith",
        "email": "jane.smith@example.com",
        "date_of_birth": ISODate("1990-07-12"),
        "loyalty_points": 50
    }
    ]);
   ```

   ### Output:

   ```
    {
        "acknowledged": true,
        "insertedIds": {
            "0": "1",
            "1": "2"
        }
    }
   ```

   Explanation: Two users are successfully inserted into the collection. The user_id values "1" and "2" are assigned to John Doe and Jane Smith, respectively.

   3. ### Find all movies in the "Action" genre.

   ```
    db.movies.find({ "genre": "Action" });
   ```

   ### Output:

   ```
    []
   ```

   Explanation: Since no "Action" genre movies have been inserted yet, the query returns an empty array.

   4. ### Find all theaters in the city "New York".

   ```
    db.theaters.find({ "location.city": "New York" });
   ```

   ### Output:

   ```
    []
   ```

   Explanation: No theaters located in New York have been inserted into the collection yet, so the result is an empty array..

   5. ### Update the seating capacity of a theater with ID "1".

   ```
    db.theaters.updateOne(
        { "theater_id": "1" },
        { $set: { "seating_capacity": 300 } }
    );
   ```

   ### Output:

   ```
    {
        "acknowledged": true,
        "matchedCount": 0,
        "modifiedCount": 0
    }
   ```

   Explanation: Since there is no theater with theater_id: "1" in the collection, no matching document is found, and no update is made. matchedCount and modifiedCount remain 0.

   6. ### Delete a movie by its title.

   ```
    db.movies.deleteOne({ "title": "Inception" });
   ```

   ### Output:

   ```
    {
        "acknowledged": true,
        "deletedCount": 1
    }
   ```

   Explanation: The movie "Inception" is successfully deleted from the collection, and deletedCount confirms that one document was removed.

   7. ### Retrieve all bookings made by the user with ID "2".

   ```
    db.bookings.find({ "user_id": "2" });
   ```

   ### Output:

   ```
    []
   ```

   Explanation: Since there are no bookings made by the user with ID "2" in the collection, the query returns an empty array.

   8. ### Find a movie by its title and display only the title and genre fields.

   ```
    db.movies.find(
        { "title": "Inception" },
        { "title": 1, "genre": 1, "_id": 0 }
    );
   ```

   ### Output:

   ```
    []
   ```

   Explanation: Since the movie "Inception" was deleted in query 6, there are no results to return for this query.

   9. ### Find users who have more than 100 loyalty points.

   ```
    db.users.find({ "loyalty_points": { $gt: 100 } });
   ```

   ### Output:

   ```
    [
        {
            "user_id": "1",
            "name": "John Doe",
            "email": "john.doe@example.com",
            "date_of_birth": ISODate("1985-04-23"),
            "loyalty_points": 120
        }
    ]
   ```

   Explanation: John Doe has 120 loyalty points, which is greater than 100, so his record is returned.

   10. ### Find all users born after 1990.

   ```
    db.users.find({ "date_of_birth": { $gt: ISODate("1990-01-01") } });
   ```

   ### Output:

   ```
    [
        {
            "user_id": "2",
            "name": "Jane Smith",
            "email": "jane.smith@example.com",
            "date_of_birth": ISODate("1990-07-12"),
            "loyalty_points": 50
        }
    ]
   ```

   Explanation: Jane Smith was born after January 1, 1990, so her record is returned.

   11. ### Update the ratings of the movie "Inception" to 4.9.

   ```
    db.movies.updateOne(
        { "title": "Inception" },
        { $set: { "ratings": 4.9 } }
    );
   ```

   ### Output:

   ```
    {
        "acknowledged": true,
        "matchedCount": 0,
        "modifiedCount": 0
    }
   ```

   Explanation: Since "Inception" was deleted in query 6, no document is matched or updated.

   12. ### Find all movies released in or after 2015.

   ```
    db.movies.find({ "release_year": { $gte: 2015 } });
   ```

   ### Output:

   ```
    []
   ```

   Explanation: No movies released in or after 2015 have been inserted into the collection yet, so the query returns an empty array.

   13. ### Find all theaters in the state of "California".

   ```
    db.theaters.find({ "location.state": "California" });
   ```

   ### Output:

   ```
    []
   ```

   Explanation: No theaters located in California have been inserted yet, so the result is an empty array.

   14. ### Delete all bookings for the movie "Inception".

   ```
    db.bookings.deleteMany({ "movie_id": "1" });
   ```

   ### Output:

   ```
    {
        "acknowledged": true,
        "deletedCount": 1
    }
   ```

   Explanation: Since one booking for the movie "Inception" exists (inserted in query 10), it is deleted.

   15. ### Insert a new theater into the Theaters collection.

   ```
    db.theaters.insertOne({
        "theater_id": "2",
        "name": "Regal Cinemas",
        "location": { "city": "San Francisco", "state": "California", "country": "USA" },
        "seating_capacity": 400
    });
   ```

   ### Output:

   ```
    {
        "acknowledged": true,
        "insertedId": "2"
    }
   ```

   Explanation: A new theater is inserted successfully into the collection with theater_id: "2".

   16. ### Find the first 5 movies sorted by release year in descending order.

   ```
    db.movies.find().sort({ "release_year": -1 }).limit(5);
   ```

   ### Output:

   ```
    []
   ```

   Explanation: Since only one movie (which was deleted) was inserted, no results are returned.

   17. ### Count how many movies are in the "Sci-Fi" genre.

   ```
    db.movies.countDocuments({ "genre": "Sci-Fi" });
   ```

   ### Output:

   ```
    0
   ```

   Explanation: The movie "Inception" was deleted, so there are no movies in the "Sci-Fi" genre.

   18. ### Find all users who have exactly 50 loyalty points.

   ```
    db.users.find({ "loyalty_points": 50 });
   ```

   ### Output:

   ```
    [
        {
            "user_id": "2",
            "name": "Jane Smith",
            "email": "jane.smith@example.com",
            "date_of_birth": ISODate("1990-07-12"),
            "loyalty_points": 50
        }
    ]
   ```

   Explanation: Jane Smith has exactly 50 loyalty points, so her record is returned.

   19. ### Update the name of the user with ID "1" to "Johnny Doe".

   ```
    db.users.updateOne(
        { "user_id": "1" },
        { $set: { "name": "Johnny Doe" } }
    );
   ```

   ### Output:

   ```
    {
        "acknowledged": true,
        "insertedId": "1"
    }
   ```

   Explanation: A new review is inserted successfully into the collection with review_id: "1".

* ## MongoDB Exercises Questions for Intermediate:

   Medium-level MongoDB questions typically focus on applying core MongoDB concepts to solve more advanced use cases. These questions explore a deeper understanding of MongoDBs querying capabilities, data manipulation, and aggregation framework.

   They require practical experience with MongoDB collections, operations like find(), updateOne(), deleteMany() and the aggregation pipeline for tasks such as grouping, filtering and transforming data.

   1. ### Find all movies where "Leonardo DiCaprio" is one of the actors.

   ```
    db.movies.find({ "actors": "Leonardo DiCaprio" });
   ```

   ### Output:

   ```
    [
        {
            "movie_id": "1",
            "title": "Inception",
            "genre": "Sci-Fi",
            "release_year": 2010,
            "duration": 148,
            "ratings": 4.9,
            "actors": ["Leonardo DiCaprio", "Joseph Gordon-Levitt", "Elliot Page", "Tom Hardy"]
        }
    ]
   ```

   Explanation: The query finds the movie "Inception" where "Leonardo DiCaprio" is listed in the actors array.

   2. ### Add a new actor to the "Inception" movie.

   ```
    db.movies.updateOne(
        { "title": "Inception" },
        { $push: { "actors": "Tom Hardy" } }
    );
   ```

   ### Output:

   ```
    {
        "acknowledged": true,
        "matchedCount": 1,
        "modifiedCount": 1
    }
   ```

   Explanation: This shows that one document was matched (i.e., the movie "Inception") and one was modified (i.e., "Tom Hardy" was added to the actors array).

   3. ### Retrieve all bookings made in September 2023.

   ```
    db.bookings.find({
        "booking_date": {
            $gte: ISODate("2023-09-01"),
            $lt: ISODate("2023-10-01")
        }
    });
   ```

   ### Output:

   ```
    [
        {
            "booking_id": "1",
            "user_id": "1",
            "movie_id": "1",
            "theater_id": "1",
            "seats_booked": 2,
            "total_price": 30,
            "booking_date": ISODate("2023-09-10")
        },
        {
            "booking_id": "2",
            "user_id": "2",
            "movie_id": "3",
            "theater_id": "2",
            "seats_booked": 4,
            "total_price": 60,
            "booking_date": ISODate("2023-09-11")
        },
        {
            "booking_id": "3",
            "user_id": "3",
            "movie_id": "1",
            "theater_id": "1",
            "seats_booked": 1,
            "total_price": 15,
            "booking_date": ISODate("2023-09-12")
        }
    ]
   ```

   Explanation: This query retrieves all bookings made in September 2023, showing three bookings during that time period.

   4. ### Calculate the total price for all bookings made by the user with ID "1".

   ```
    db.bookings.aggregate([
        { $match: { "user_id": "1" } },
        { $group: { _id: null, total: { $sum: "$total_price" } } }
    ]);
   ```

   ### Output:

   ```
    [
        {
            "_id": null,
            "total": 30
        }
    ]
   ```

   Explanation: The aggregation query calculates the sum of the total_price for all bookings made by the user with user_id "1", which amounts to 30.

   5. ### Delete all users who have less than 10 loyalty points.

   ```
    db.users.deleteMany({ "loyalty_points": { $lt: 10 } });
   ```

   ### Output:

   ```
    {
        "acknowledged": true,
        "deletedCount": 0
    }
   ```

   Explanation: No users had less than 10 loyalty points in the dataset, so no documents were deleted.

   6. ### Find all movies that are either in the "Action" or "Adventure" genres.

   ```
    db.movies.find({ "genre": { $in: ["Action", "Adventure"] } });
   ```

   ### Output:

   ```
    []
   ```

   Explanation: No movies in the collection match the genres "Action" or "Adventure" based on the available dataset.

   7. ### Insert multiple bookings into the Bookings collection.

   ```
    db.bookings.insertMany([
        {
            "booking_id": "2",
            "user_id": "2",
            "movie_id": "3",
            "theater_id": "2",
            "seats_booked": 4,
            "total_price": 60,
            "booking_date": ISODate("2023-09-11")
        },
        {
            "booking_id": "3",
            "user_id": "3",
            "movie_id": "1",
            "theater_id": "1",
            "seats_booked": 1,
            "total_price": 15,
            "booking_date": ISODate("2023-09-12")
        }
    ]);
   ```

   ### Output:

   ```
    {
        "acknowledged": true,
        "insertedIds": {
            "0": "2",
            "1": "3"
        }
    }
   ```

   Explanation: Two new booking documents were successfully inserted into the bookings collection.

   8. ### Find the total number of bookings made for the movie with ID "1".

   ```
    db.bookings.countDocuments({ "movie_id": "1" });
   ```

   ### Output:

   ```
    3
   ```

   Explanation: There are 3 bookings associated with the movie that has movie_id "1".

   9. ### Find all theaters in the USA with a seating capacity greater than 300.

   ```
    db.theaters.find({
        "location.country": "USA",
        "seating_capacity": { $gt: 300 }
    });
   ```

   ### Output:

   ```
    [
        {
            "theater_id": "2",
            "name": "Regal Cinemas",
            "location": {
            "city": "San Francisco",
            "state": "California",
            "country": "USA"
            },
            "seating_capacity": 400
        }
    ]
   ```

   Explanation: This query finds all theaters in the USA where the seating_capacity exceeds 300. The "Regal Cinemas" theater in San Francisco is retrieved.

   10. ### Update the loyalty points of all users who have booked more than 3 seats to give them an extra 10 points.

   ```
    db.bookings.aggregate([
        { $group: { _id: "$user_id", total_seats: { $sum: "$seats_booked" } } },
        { $match: { total_seats: { $gt: 3 } } }
        ]).forEach(function(user) {
        db.users.updateOne(
            { "user_id": user._id },
            { $inc: { "loyalty_points": 10 } }
        );
    });
   ```

   ### Output:

   ```
    [
        {
            "acknowledged": true,
            "matchedCount": 1,
            "modifiedCount": 1
        },
        {
            "acknowledged": true,
            "matchedCount": 1,
            "modifiedCount": 1
        }
    ]
   ```

   Explanation: The users with user_id "2" and "3" each booked more than 3 seats, so their loyalty points were incremented by 10.

   11. ### Find all movies where the genre is not "Comedy".

   ```
    db.movies.find({ "genre": { $ne: "Comedy" } });
   ```

   ### Output:

   ```
    [
        {
            "movie_id": "1",
            "title": "Inception",
            "genre": "Sci-Fi",
            "release_year": 2010,
            "duration": 148,
            "ratings": 4.9,
            "actors": ["Leonardo DiCaprio", "Joseph Gordon-Levitt", "Elliot Page", "Tom Hardy"]
        }
    ]
   ```

   Explanation: This query retrieves all movies whose genre is not "Comedy". The movie "Inception" is returned.

   12. ### Find the number of seats booked for each movie.

   ```
    db.bookings.aggregate([
        { $group: { _id: "$movie_id", total_seats: { $sum: "$seats_booked" } } }
    ]);

   ```

   ### Output:

   ```
    [
        { "_id": "1", "total_seats": 3 },
        { "_id": "3", "total_seats": 4 }
    ]
   ```

   Explanation: This query groups bookings by movie_id and sums up the seats_booked for each movie.

   13. ### Find all users who booked seats in "California" theaters.

   ```
    db.bookings.aggregate([
        { $lookup: { from: "theaters", localField: "theater_id", foreignField: "theater_id", as: "theater_info" } },
        { $unwind: "$theater_info" },
        { $match: { "theater_info.location.state": "California" } },
        { $group: { _id: "$user_id" } }
    ]);
   ```

   ### Output:

   ```
    [
        { "_id": "1" },
        { "_id": "2" }
    ]
   ```

   Explanation: This query retrieves the users who booked seats in theaters located in California by performing a lookup from the theaters collection.

   14. ### Increase the ticket price for all bookings made after 2023-09-10 by 5%.

   ```
    db.theaters.updateMany(
        { "location.state": "California" },
        { $set: { "seating_capacity": 500 } }
    );
   ```

   ### Output:

   ```
    {
        "acknowledged": true,
        "matchedCount": 2,
        "modifiedCount": 2
    }
   ```

   Explanation: This query updates the ticket price of bookings made after September 10, 2023, by increasing the total_price by 5%.

   15. ### Find the average rating of all movies in the "Sci-Fi" genre.

   ```
    db.movies.aggregate([
        { $match: { "genre": "Sci-Fi" } },
        { $group: { _id: null, avg_rating: { $avg: "$ratings" } } }
    ]);
   ```

   ### Output:

   ```
    [
        { "_id": null, "avg_rating": 4.9 }
    ]
   ```

   Explanation: This query calculates the average rating of all movies in the "Sci-Fi" genre.

   16. ### Find the movie with the longest duration.

   ```
    db.movies.aggregate([
        { $match: { "genre": "Sci-Fi" } },
        { $group: { _id: null, avg_duration: { $avg: "$duration" } } }
    ]);
   ```

   ### Output:

   ```
    [
        {
            "movie_id": "1",
            "title": "Inception",
            "genre": "Sci-Fi",
            "release_year": 2010,
            "duration": 148,
            "ratings": 4.9,
            "actors": ["Leonardo DiCaprio", "Joseph Gordon-Levitt", "Elliot Page", "Tom Hardy"]
        }
    ]
   ```

   Explanation: This query sorts the movies by duration in descending order and returns the one with the longest duration, which is "Inception" with 148 minutes.

   17. ### Find all bookings where the user booked more than 2 seats.

   ```
    db.bookings.find({ "seats_booked": { $gt: 2 } });
   ```

   ### Output:

   ```
    [
        {
            "booking_id": "2",
            "user_id": "2",
            "movie_id": "3",
            "theater_id": "2",
            "seats_booked": 4,
            "total_price": 60,
            "booking_date": ISODate("2023-09-11")
        }
    ]
   ```

   Explanation: This query retrieves bookings where more than 2 seats were booked. The booking with seats_booked equal to 4 is returned.

   18. ### Find all movies that have both "Tom Hardy" and "Leonardo DiCaprio" in their cast.

   ```
    db.movies.find({  "actors": { $all: ["Tom Hardy", "Leonardo DiCaprio"] }});
   ```

   ### Output:

   ```
    [
        {
            "movie_id": "1",
            "title": "Inception",
            "genre": "Sci-Fi",
            "release_year": 2010,
            "duration": 148,
            "ratings": 4.9,
            "actors": ["Leonardo DiCaprio", "Joseph Gordon-Levitt", "Elliot Page", "Tom Hardy"]
        }
    ]
   ```

   Explanation: This query finds the movie "Inception" where both "Tom Hardy" and "Leonardo DiCaprio" are part of the cast.

   19. ### Find all users who have not made any bookings.

   ```
    db.users.find({  "user_id": { $nin: db.bookings.distinct("user_id") }});
   ```

   ### Output:

   ```
    [
        {
            "user_id": "4",
            "name": "Eve",
            "loyalty_points": 15
        }
    ]
   ```

   Explanation: This query retrieves users who have not made any bookings by excluding user IDs present in the bookings collection.

   20. ### Delete all movies that have less than 3 stars in ratings.

   ```
    db.movies.deleteMany({ "ratings": { $lt: 3 } });
   ```

   ### Output:

   ```
    {
        "acknowledged": true,
        "deletedCount": 0
    }
   ```

   Explanation: No movies in the collection have less than 3 stars, so no documents were deleted.

* ## Advanced MongoDB Exercises Questions:

   Hard-level MongoDB queries involve advanced data operations using the b for tasks like grouping, sorting, and calculating totals. They often include joins across collections using $lookup and creating indexes to optimize query performance.

   These queries are designed for complex scenarios such as identifying top users, analyzing data across multiple criteria or filtering based on specific conditions.

   1. ### Find the top 3 users who have spent the most on bookings (total_price).

   ```
    db.bookings.aggregate([
        { $group: { _id: "$user_id", total_spent: { $sum: "$total_price" } } },
        { $sort: { total_spent: -1 } },
        { $limit: 3 }
    ]);
   ```

   ### Output:

   ```
    [
        { "_id": "2", "total_spent": 150 },
        { "_id": "1", "total_spent": 90 },
        { "_id": "3", "total_spent": 80 }
    ]
   ```

   Explanation: This query groups bookings by user_id and calculates the total amount spent. It then sorts the result in descending order and limits it to the top 3 users.

   2. ### Find all movies that have been booked in more than 2 different theaters.

   ```
    db.bookings.aggregate([
        { $group: { _id: { movie_id: "$movie_id", theater_id: "$theater_id" } } },
        { $group: { _id: "$_id.movie_id", theater_count: { $sum: 1 } } },
        { $match: { theater_count: { $gt: 2 } } }
    ]);
   ```

   ### Output:

   ```
    [
        { "_id": "3", "theater_count": 3 }
    ]
   ```

   Explanation: This query finds movies that have been shown in more than 2 different theaters by counting the distinct theater IDs for each movie.

   3. ### Find the theater with the most seats booked across all movies.

   ```
    db.bookings.aggregate([
        { $group: { _id: "$theater_id", total_seats: { $sum: "$seats_booked" } } },
        { $sort: { total_seats: -1 } },
        { $limit: 1 }
    ]);
   ```

   ### Output:

   ```
    [
        { "_id": "1", "total_seats": 8 }
    ]
   ```

   Explanation: This query sums up the number of seats booked for each theater and returns the theater with the most seats booked.

   4. ### Find the average number of loyalty points for users who have booked seats in "California".

   ```
    db.bookings.aggregate([
        { $lookup: { from: "theaters", localField: "theater_id", foreignField: "theater_id", as: "theater_info" } },
        { $unwind: "$theater_info" },
        { $match: { "theater_info.location.state": "California" } },
        { $lookup: { from: "users", localField: "user_id", foreignField: "user_id", as: "user_info" } },
        { $unwind: "$user_info" },
        { $group: { _id: null, avg_loyalty_points: { $avg: "$user_info.loyalty_points" } } }
    ]);
   ```

   ### Output:

   ```
    [
        { "_id": null, "avg_loyalty_points": 25 }
    ]
   ```

   Explanation: This query calculates the average number of loyalty points for users who have made bookings in theaters located in California.

   5. ### Create an index on the booking_date field in the Bookings collection to optimize queries by date.

   ```
    db.bookings.createIndex({ "booking_date": 1 });
   ```

   ### Output:

   ```
    {
        "createdCollectionAutomatically": false,
        "numIndexesBefore": 1,
        "numIndexesAfter": 2,
        "ok": 1
    }
   ```

   Explanation: This query creates an index on the booking_date field to improve the performance of queries based on booking dates.

   6. ### Find the top 5 most popular actors by counting the number of movies they appear in.

   ```
    db.movies.aggregate([
        { $unwind: "$actors" },
        { $group: { _id: "$actors", movie_count: { $sum: 1 } } },
        { $sort: { movie_count: -1 } },
        { $limit: 5 }
    ]);
   ```

   ### Output:

   ```
    [
        { "_id": "Leonardo DiCaprio", "movie_count": 3 },
        { "_id": "Tom Hardy", "movie_count": 2 },
        { "_id": "Joseph Gordon-Levitt", "movie_count": 2 }
    ]
   ```

   Explanation: This query counts the number of movies each actor appears in and returns the top 5 actors by the number of movie appearances.

   7. ### Find the user who booked the most seats in the month of September 2023.

   ```
    db.bookings.aggregate([
        { $match: { "booking_date": { $gte: ISODate("2023-09-01"), $lt: ISODate("2023-10-01") } } },
        { $group: { _id: "$user_id", total_seats: { $sum: "$seats_booked" } } },
        { $sort: { total_seats: -1 } },
        { $limit: 1 }
    ]);
   ```

   ### Output:

   ```
    [
        { "_id": "2", "total_seats": 8 }
    ]
   ```

   Explanation: This query calculates the total number of seats booked by each user in September 2023 and returns the user with the highest seat booking count.

   8. ### Find all movies that have not been booked by any user.

   ```
    db.movies.find({
        "movie_id": { $nin: db.bookings.distinct("movie_id") }
    });
   ```

   ### Output:

   ```
    [
        {
            "movie_id": "5",
            "title": "Uncharted",
            "genre": "Adventure",
            "release_year": 2022
        }
    ]
   ```

   Explanation: This query finds all movies that do not appear in any bookings.

   9. ### Create a compound index on genre and release_year in the Movies collection to improve filtering by genre and release year.

   ```
    db.movies.createIndex({ "genre": 1, "release_year": -1 });
   ```

   ### Output:

   ```
    {
        "createdCollectionAutomatically": false,
        "numIndexesBefore": 2,
        "numIndexesAfter": 3,
        "ok": 1
    }
   ```

   Explanation: This query creates a compound index on the genre and release_year fields to optimize queries filtering by both fields.

   10. ### Find the user who made the first booking ever in the system and display their name and email.

   ```
    db.bookings.aggregate([
        { $sort: { "booking_date": 1 } },
        { $limit: 1 },
        { $lookup: { from: "users", localField: "user_id", foreignField: "user_id", as: "user_info" } },
        { $unwind: "$user_info" },
        { $project: { name: "$user_info.name", email: "$user_info.email" } }
    ]);
   ```

   ### Output:

   ```
    [
        { "name": "Alice", "email": "alice@example.com" }
    ]
   ```

   Explanation: This query finds the first booking by sorting the bookings collection by booking_date in ascending order and retrieves the corresponding user's name and email using a lookup from the users collection.
