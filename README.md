# Basics of Mongodb
1. To start mongodb server type `mongod`
2. mongodb by default port is 27017
3. To connect to server type `mongosh`
4. USe `show dbs` to view database
```
test> show dbs
admin    40.00 KiB
alok      8.00 KiB
config  108.00 KiB
local    40.00 KiB
mydb     24.00 KiB
test      8.00 KiB
test>
```
5. To know we are inside which database type ` db `

6. To create/switch to any db type "use dbName" 
Syntax : `use product`
``` 
test> use product
switched to db mydb
mydb>
```

7. (I) To create db collection type "db.createCollection("dbName")" 
Syntax : ` db.createCollection("prod")`
OR
7. (II) We can directly use "db.colloectionName.insert({name:"alok", age:"20"})"
Syntax : `db.users.insert({name:"alok", age:"20"})`

```
test> show dbs
admin     40.00 KiB
alok       8.00 KiB
config   108.00 KiB
local     40.00 KiB
mydb      24.00 KiB
product   48.00 KiB
test      16.00 KiB
test> use product
switched to db product
product> show collections
prod
users
product>
```

8. To delete db collections type "db.CollectionName.drop()" 
Syntax : `db.users.drop()` and it shows true means collection deleted succesfully.
```
product> db.prod.drop()
true
```

9. To delete that particular db type "db.dropDatabase()" 
Syntax : `db.dropDatabase()`
```
product> db.dropDatabase()
{ ok: 1, dropped: 'product' }
```

10. Now if we type show dbs then it not show product db
```
test> show dbs
admin    40.00 KiB
alok      8.00 KiB
config  108.00 KiB
local    40.00 KiB
mydb     24.00 KiB
test     16.00 KiB
```

# How to use CRUD OPERATIONS in mongodb

## 1. Insert Operation
> Make a bd of name lib

> In mongodb we have three options to insert data.
1. insert : insert one and multiple 

2. insertOne : single-object

3. insertMany : multiple-array

> 1. Using insert
```
lib> db.books.insert({ name:"The Complete Java Book", pages:50
0, price:100})
DeprecationWarning: Collection.insert() is deprecated. Use insertOne, insertMany, or bulkWrite.
{
  acknowledged: true,
  insertedIds: { '0': ObjectId('65e6ef4bbfbb7525c48da9ef') }
}
```
> To view that inserted data type " db.collectionsName.find()" ` db.books.find()`

> We are not using this function because it is deprecation warining and show some warnings.
```
DeprecationWarning: Collection.insert() is deprecated. Use insertOne, insertMany, or bulkWrite.
```

> 2. Using insertOne
```
lib> db.books.insertOne({ name:"Think in Java", pages:600, price:700})
{
  acknowledged: true,
  insertedId: ObjectId('65e6f19fbfbb7525c48da9f0')
}
lib> db.books.insertOne({ name:"Think in Python", pages:450, price:600})
{
  acknowledged: true,
  insertedId: ObjectId('65e6f1d8bfbb7525c48da9f1')
}
```

> 3. using insertMany
```
lib> db.books.insertMany([{ name: "Master Programming", pages: 460, price: 580 }, { name: "Write SQL", pages: 567, pirce: 670 }])
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId('65e6f309bfbb7525c48da9f2'),
    '1': ObjectId('65e6f309bfbb7525c48da9f3')
  }
}
```
> In mongodb there is no limitations of schema, if we want to add some properties in some insert then we add it directly 

> Now we see all inserted books data.
```
lib> db.books.find()
[
  {
    _id: ObjectId('65e6ef4bbfbb7525c48da9ef'),
    name: 'The Complete Java Book',
    pages: 500,
    price: 100
  },
  {
    _id: ObjectId('65e6f19fbfbb7525c48da9f0'),
    name: 'Think in Java',
    pages: 600,
    price: 700
  },
  {
    _id: ObjectId('65e6f1d8bfbb7525c48da9f1'),
    name: 'Think in Python',
    pages: 450,
    price: 600
  },
  {
    _id: ObjectId('65e6f309bfbb7525c48da9f2'),
    name: 'Master Programming',
    pages: 460,
    price: 580
  },
  {
    _id: ObjectId('65e6f309bfbb7525c48da9f3'),
    name: 'Write SQL',
    pages: 567,
    pirce: 670
  },
  {
    _id: ObjectId('65e6f532bfbb7525c48da9f4'),
    name: 'Think in Python',
    pages: 450,
    price: 600,
    author: [ 'John-Wills', 'Ram Sharma' ]
  }
]
```

## 2. Update Operation

We have agian three optios in update same as insert.
So, basically we use updateOne and UpdateMany.

>To use updateOne

db.books.updateOne({ _id: ObjectId('....')}, {$set:{updated object}})

Syntax : 
```
db.books.updateOne({ _id: ObjectI('65e6f309bfbb7525c48da9f3')}, {$set:{name:"The MLCourse", pages:890, price:1400}})
```
> We have various update operators in mongodb, so we can search on google and use them like 

1. For Field name : $currentDate, $inc, $min, $max etc
2. Fro Array name : $, $[], $addToSet, $pop etc, 

## 3. Remove Operation

We have agian three optios in update same as insert.
So, basically we use updateOne and UpdateMany.

1. remove
2. removeOne
3. removeMany

> We use reomve "db.collectionName.remove({_id:ObjectId("3453453343)})"
Syntax : ` db.books.remove(id)`

```
lib> db.books.remove({ _id: ObjectId('65e6f309bfbb7525c48da9f2')})
DeprecationWarning: Collection.remove() is deprecated. Use deleteOne, deleteMany, findOneAndDelete, or bulkWrite.
{ acknowledged: true, deletedCount: 1 }
```
Its shows Waring in using remove so use removeOne and removeMany

## 3. Select Operation

This is use to select and find the data.

1. We can use db.books.find() to view whole data.
`db.books.find()`
2. We can use db.books.find().pretty() to view better
`db.books.find().pretty()`
3. We can use db.books.find().limit() to view that limited data only, if we put (2) in limit then it shows first two data.
`db.books.find().limit()`
4. We can use db.books.find().sort({price:1}) for increasing order
and db.books.find().sort({price:-1}) for decreasing order.
`db.books.find().sort({price:1})`

5. We can use more than one function at one time like `db.books.find().pretty().sort({price:1})`

> We have various select operators in mongodb, so we can search on google and use them like

1. Comparison : $eq, $gt, $gte, $in, $lt, $lte etc
2. Logical : $and, $not, $nor, $or
3. Element : $exists, $type
4. Evaluation : $expr, jsonSchema, $mod
5. Geospatial : $geoIntersects, $geoWithin
6. Array : $all, $elemMatch, $size
7. Bitwise : $bitsAllClear, $bitsAnyClear
> We can use these functional query for better undersatnding off our data.
`db.books.find({price:{$eq:600}})`

```
lib> db.books.find({price:{$eq:600}})
[
  {
    _id: ObjectId('65e6f1d8bfbb7525c48da9f1'),
    name: 'Think in Python',
    pages: 450,
    price: 600
  },
  {
    _id: ObjectId('65e6f532bfbb7525c48da9f4'),
    name: 'Think in Python',
    pages: 450,
    price: 600,
    author: [ 'John-Wills', 'Ram Sharma' ]
  }
]
```

## 4. Complex Select operations with multiple clause and select operators

In this we use more than one query for operation

1. We take $and
Syntax : ``` { $and: [ { <expression1> }, { <expression2> } , ... , { <expressionN> } ] } ```

db.books.find({$and:[{pages:450},{price:600}]})

```
lib> db.books.find({$and:[{pages:450},{price:600}]})
[
  {
    _id: ObjectId('65e6f1d8bfbb7525c48da9f1'),
    name: 'Think in Python',
    pages: 450,
    price: 600
  },
  {
    _id: ObjectId('65e6f532bfbb7525c48da9f4'),
    name: 'Think in Python',
    pages: 450,
    price: 600,
    author: [ 'John-Wills', 'Ram Sharma' ]
  }
]
```

