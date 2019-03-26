# MongoDB

###### Get file from Internet using curl
```$ curl https://github.com/mistertandon/node-express-hbs/blob/master/movies_collection.json -o movies_collection.json```

###### Import to MongoDB
```$ mongoimport -v --file=movies_collection.json -h localhost -p 27717 -d sample -c movies```

###### Note:
The following site contains many MongoDB JSON Datasets
```https://github.com/ozlerhakan/mongodb-json-files```

## MongoDB CRUD Operations
### Create
#### Create/Insert Documents to Collections
##### insertOne
##### insertMany

### Read
#### Query Documents
##### Select All documents in a Collection
Selects all documents in the collection
```$ db.getCollection('movies').find({})```
```$ db.movies.find()```

Select first document in the collection
```$ db.movies.findOne()```

```> db.movies.findOne()```

```javascript
{
    "_id": ObjectId("589cbda9c0b9fec62febf274"),
    "title": "Deadpool",
    "year": 2016,
    "rated": "R",
    "released": ISODate("2016-06-18T04:00:00Z"),
    "runtime": 108,
    "countries": [
        "USA"
    ],
    "genres": [
        "Comics character",
        "Adventure",
        "Action"
    ],
    "director": "Tim Miller",
    "writers": [
        "Rhett Reese",
        "Paul Wernick"
    ],
    "actors": [
        "Ryan Reynolds",
        "Morena Baccarin",
        "Ed Skrein",
        "T.J. Miller",
        "Gina Carano",
        "Leslie Uggams",
        "Stefan Kapičić",
        "Brianna Hildebrand"
    ],
    "plot": "Deadpool is a 2016 American superhero film directed by Tim Miller and written by Rhett Reese and Paul Wernick, based on the Marvel Comics character of the same name.",
    "poster": "http://ia.media-imdb.com/images/M/MV5BMTgxOTY4Mjc0MF5BMl5BanBnXkFtZTcwNTA4MDQyMw@@._V1_SX300.jpg",
    "imdb": {
        "id": "tt1431045",
        "rating": 8.1,
        "votes": 585141
    },
    "tomato": {
        "meter": 99,
        "image": "certified",
        "rating": 6.9,
        "reviews": 287,
        "fresh": 241,
        "consensus": "Fast, funny, and gleefully profane, the fourth-wall-busting Deadpool.",
        "userMeter": 90,
        "userRating": 4.3,
        "userReviews": 181719
    },
    "metacritic": 92,
    "awards": {
        "wins": 5,
        "nominations": 12,
        "text": "wo Golden Globe Award nominations for Best Motion Picture – Musical or Comedy and Best Actor – Motion Picture Musical or Comedy."
    },
    "type": "movie"
} 
```


##### Select using conditions
* Equality 

``` db.movies.find({year: 2016})```

``` SELECT * FROM movies WHERE year = 2016;```

* Comparison Operators - ```$eq```, ```$gt```, ```$gte```, ```$lt```, ```$lte```, ```$ne``` 

```> db.movies.find({"imdb.rating": {$gt: 8}}, {title:1, "imdb.rating":1, _id:0})```

```json
{ "title" : "Deadpool", "imdb" : { "rating" : 8.1 } }
{ "title" : "Toy Story 4", "imdb" : { "rating" : 8.4 } }
{ "title" : "zootopia", "imdb" : { "rating" : 8.1 } }
```



* Contained - ```$in```, ```$nin```

```> db.movies.find({genres: {$in: ["Adventure","Action"]}})```

* Logical Operators - $and, $not, $nor, $or
```db.movies.find(
		{"imdb.rating": {$gte: 8}, "tomato.rating": {$gte: 8}},
		{title: 1, "imdb.rating": 1, "tomato.rating": 1, _id: 0}
	);```

```json
{ "title" : "Toy Story 4", "imdb" : { "rating" : 8.4 }, "tomato" : { "rating" : 8.9 } }
{ "title" : "zootopia", "imdb" : { "rating" : 8.1 }, "tomato" : { "rating" : 8.1 } }
```

```> db.movies.find({$or:[{year: {$eq:2011}},{genres:{$in:['Comedy']}}]},{_id:0, title:1, year:1, genres:1})```

```json
{ "title" : "Toy Story 4", "year" : 2011, "genres" : [ "Animation", "Adventure", "Comedy" ] }
{ "title" : "kung fu panda 3", "year" : 2016, "genres" : [ " Animation", "Action", "Adventure", "Comedy", "Family" ] }
{ "title" : "zootopia", "year" : 2016, "genres" : [ "Animation", "Adventure", "Comedy", "Crime", "Family", "Mystery" ] }
```

* Element - $exists, $type


* Evaluation - $expr, $jsonschema, $mod, $regex, $text, $where
* Array - $all, $elemMatch, $size
* Geospatial - $near, $nearSphere, $geoWithin, $geoIntersects
* Bitwise - $bitsAllClear, $bitsAllSet, $bitsAnyClear, $bitsAnySet

##### Query on Embedded/Nested Documents
##### Query on Array
##### Query on Array of Embedded Documents

#### Projection


### Update
#### updateOne
#### updateMany
#### replaceOne
### Delete
#### deleteOne
#### deleteMany
### Bulk Write
