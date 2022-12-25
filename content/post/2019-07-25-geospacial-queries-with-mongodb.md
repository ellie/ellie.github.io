+++
author = "Ellie Huxtable"
date = 2019-07-25T19:45:00Z
description = ""
draft = false
image = "/images/photo-1562504208-03d85cc8c23e?ixlib=rb-1.2.1&q=80&fm=jpg&crop=entropy&cs=tinysrgb&w=2000&fit=max&ixid=eyJhcHBfaWQiOjExNzczfQ.jpg"
slug = "geospacial-queries-with-mongodb"
title = "Geospatial queries with MongoDB"

+++


I'm currently playing with MongoDB and its [geospatial queries](https://docs.mongodb.com/manual/geospatial-queries/). It’s pretty interesting so far, so I just thought I'd write something up to show how I'm using it with PyMongo!

Firstly, the obvious `pip install pymongo` is needed. We will need a mongo client first, which is easy enough

```python
from pymongo import MongoClient

client = MongoClient()
```

It’s pretty neat - by default, MongoClient will connect to `mongodb://localhost:27017`.

You might want to do something like this instead though

```python
url = os.environ.get("MONGO_URL", "mongodb://localhost:27017")
client = MongoClient(url)

```

We're going to want to create a MongoDB index on a document field to allow the geospatial magic to work. We will be creating a [`2dsphere`](https://docs.mongodb.com/manual/core/2dsphere/) index.

```python
from pymongo import MongoClient, GEOSPHERE, DESCENDING

client = MongoClient()
db = client.foo
db.bar.create_index([("location", GEOSPHERE)])

```

Now all that is needed is to insert a document and run a query :) We'll insert a document that just has a `location` field

```python
db.bar.insert_one({
	“location”: {
		"coordinates" : [ 
			51.4982563, 
			-0.0861183
    		],
    		"type" : "Point"
	}
})

```

The `location` field needs to be [GeoJSON](https://en.wikipedia.org/wiki/GeoJSON), which is a JSON standard for representing geographic features. It makes querying for documents super easy!

```python
db.bar.find({
	"location": {
		"$near": {
			"$geometry": {"type": "Point", "coordinates": [LAT, LONG]},
			"$maxDistance": range,
		}
	}
})

```

