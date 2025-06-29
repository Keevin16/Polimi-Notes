``` json
db.nameOfTheDatabase.insertOne(
{
  "_id": ObjectId("5ea64532a7678a3b27d34e00"),
  "name": {
    "first": "Mark",
    "last": "Johnson"
  },
  "age": 37,
  "birth_date": {
    "$date": "1986-03-01T00:00:00.000Z"
  },
  "address": {
    "street": "Giuseppe Ponzio",
    "city": "Milan",
    "postal_code": "20133"
  },
  "mobile_phone_numbers": [
    {
      "phone_number": "+39 XXX 3456 778",
      "service_provider": "Wind"
    },
    {
      "phone_number": "+39 YYY 9874 123",
      "service_provider": "TIM"
    }
  ]
}
)
```
#### ObjectID
It's a unique identifier of 12 Byte, like a **Primary Key** automatically generated.
These 12 bytes are divided in three parts:
- **4-byte timestamp value**, representing the value creation 
- **5-byte random value**, which is unique to the machine 
- **3-byte increasing counter**, initialized to a random value
``` json
  "_id": ObjectId("5ea64532a7678a3b27d34e00"),
```
#### Complex Structure -_> Sub-document
``` json
"name": {
    "first": "Mark",
    "last": "Johnson"
  }
  ```
   
#### Complex Structure -_> Collection
The collection is precisely a collection of sub-document!
``` json
  "mobile_phone_numbers": [
    {
      "phone_number": "+39 XXX 3456 778",
      "service_provider": "Wind"
    },
    {
      "phone_number": "+39 YYY 9874 123",
      "service_provider": "TIM"
    }
  ]
```

#### Simple Field
``` json
  "first": "Mark",
```

#### Complex field
``` json
  "$date": "1986-03-01T00:00:00.000Z"
```

## Create a document/s
It's possible to insert a document inside a collection using the method ` InsertOne(...)`.
Multiple documents instead can be added using `InsertMany(...)`.

## Create Index/es
**Indexes** are **data structures** that **store** a small portion of the collection's data set in an **easy to traverse form**.
Indexes are created with the method `createIndex(...)`, which accepts a list of the fields.
To sort the ordering of the elements : **ascending** (1), **descending** (-1)

``` json
  db.nameOfTheDatabase.createIndex(
	  {
	  "name.last": -1,
	  "name.first": 1,
	  "age": 1
	  }
  )
```

## Collect Document & Filtering
A document can be collected using the `findOne(...)` method, it collects the first document that satisfies **one or more condition** defined in a filter.

Instead to collect more document is possible to use the command `find(...)` method.
``` json
  db.nameOfTheDatabase.find(
	  {
		 "name.first": "Mark"
	  }
  )
```

Rather to count it's used the command `countDocuments(...)`.

## Filtering when are involved the array
If you'd like to retrieve document/s with array is useful to use `$unwind`.
Instead to find(..) as method is important to call aggregate(...)! 
``` json
  db.nameOfTheDatabase.aggregate([
	  {
		 "$unwind": {"path": "$mobile_phone_numbers"}
	  },
	  {
	  $group:{
		  "_id":{"provider":"$mobile_phone_numbers.service_provider"},
		  "phone_number_per_provider":{"$sum" : 1}
		  }
	  }
])
```

## Update Document/s
A document can be updated using the `updateOne(...)` method, it collects the first document that satisfies **one or more condition** defined in a filter.

Instead to update more document in a row is possible to use the command `updateMany(...)` method.

``` json
  db.nameOfTheDatabase.updateOne(
	  { "age": 23},
	  { "$set": {"age": 70} }
  )
```

## $match
**$match** is used to filter documents based on the query, the documents that passed the matching are passed to the next pipeline stage.
``` json
db.articles.aggregate( [
  { $match: { $or: [ { score: { $gt: 70, $lt: 90 } }, { views: { $gte: 1000 } } ] } },
  { $group: { _id: null, count: { $sum: 1 } } }
] );
``` 
## Delete Document/s
Delete a single document that satisfies one or more condition -_> `deleteOne(...)`.
As before but to delete multiple documents in a row: `deleteMany(...)`.

## Projection
Projection are list of **key-value pairs** made by **field name** and a  **boolean value** representing whether the field will be return.
Setting the value to:
- 1 the value'll be showed
- 0 the value won't be returned

>These Projections are done with the object to **restrict, explicit or expand the fields**.

``` json
  db.nameOfTheDatabase.find(
  { "age": 23},
  { "birth_date": 1, "isAccepted": 0 }
  )
```

## Crazy Commands
- .sort()
- .limit(number)
``` json
  db.nameOfTheDatabase.find(
	 {"name.first": "mark", "name.last": "Giudice" }
	 ).sort(
		 {"name.first":1, "name.last":-1}
	 ).limit(5)
```
note: While sorting id 1 is ascending, otherwise (-1) descending.
## Crazy Operators

>**Logical** query operator
- $and
- $not
- $nor
- $or
``` json
db.name.find(
{
	"$or":[
		{"name.first": "Mark", "name.last": "TONI"},
		{"age": 20}
	]
}
)
```

>**Comparison** query operator
- $eq
- $lt (lte)
- $in
- $ne, which stands for **not equal** 
- $nin, which stands for **not contained in a specified array**

``` json
db.name.find(
{
	"$or":[
		"$and":[
			{"age": {"$gt": 19} },
			{"age": {"$lte": 40} }
		],
	{ "age": {"$nin"}: [20,21,22,23] }
	]
}
)
```

>**Element** query operator
- $exists
- $type
``` json
db.name.find(
{
	"$and":[
		{"birth_date": {"$exists": true}},
		{"birth_date": {"$type": "date"}}
	]
}
)
```

>**Evaluation** query operator
- **$text** matches documents based on text search on indexed fields
- **$regex** matches documents based on a specified regular expression 
- **$where** matches documents based on a Javascript expression



#### Examples
In this case we want to compute the total number of bedrooms available across the housing dataset
``` json
db.name.aggregate(
	[
	"$group"; {
		"_id": null,
		"bedroom_count": { "$sum": "$bedroom"}
	}
	]
)
```
What I want to remark is:
- remember to use the [ ] because we are talking about more sub document 
- Cause we want to take all the values of the dataset --> set the "_ id": true
- bedroom_count is the name of the output, it's not a real variable
- cause we want to take the numerical value of bedroom we use the $!!!!!, otherwise we are taking the string!

Note:
in the $group, if we set **"_ id": null** we group everything together into one group. 
>It's like saying: “I don’t care about grouping by a specific field, just give me a total.”

ex:
``` json
{ $group: { _id: null, total: { $sum: 1 } } }
```
INSTEAD "_ id ": true doesn't have sense! He used it on the slides with this meaning but it's garbage.