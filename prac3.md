
test> show dbs
admin   40.00 KiB
config  60.00 KiB
local   40.00 KiB
test> use mscds
switched to db mscds
mscds> db.createCollection("users")
{ ok: 1 }
mscds> show dbs
admin    40.00 KiB
config  108.00 KiB
local    40.00 KiB
mscds     8.00 KiB
mscds> show dbs
admin    40.00 KiB
config  108.00 KiB
local    40.00 KiB
mscds     8.00 KiB
mscds> show collections
users
mscds> db.users.insertOne({'name':'mscds'})
{
  acknowledged: true,
  insertedId: ObjectId('65d08296cdc7293dd028ae56')
}
mscds> db.users.insertMany({})
MongoInvalidArgumentError: Argument "docs" must be an array of documents
mscds> db.users.insertMany({
...
... }]
Uncaught:
SyntaxError: Unexpected token, expected "," (3:1)

  1 | db.users.insertMany({
  2 |
> 3 | }]
    |  ^
  4 |

mscds>

mscds>

mscds> db.users.insertMany([{"name":"Deep","age":22},{"name":"hecker","age":32},{"name":"mrX","age":22}])
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId('65d0841ecdc7293dd028ae57'),
    '1': ObjectId('65d0841ecdc7293dd028ae58'),
    '2': ObjectId('65d0841ecdc7293dd028ae59')
  }
}
mscds> show Collections
MongoshInvalidInputError: [COMMON-10001] 'Collections' is not a valid argument for "show".
mscds> show collections
users
mscds> db.users.find()
[
  { _id: ObjectId('65d08296cdc7293dd028ae56'), name: 'mscds' },
  { _id: ObjectId('65d0841ecdc7293dd028ae57'), name: 'Deep', age: 22 },
  {
    _id: ObjectId('65d0841ecdc7293dd028ae58'),
    name: 'hecker',
    age: 32
  },
  { _id: ObjectId('65d0841ecdc7293dd028ae59'), name: 'mrX', age: 22 }
]
mscds> db.usersfindOne({'name':'mrX'})
TypeError: db.usersfindOne is not a function
mscds> db.users.findOne({'name':'mrX'})
{ _id: ObjectId('65d0841ecdc7293dd028ae59'), name: 'mrX', age: 22 }
mscds> db.users.find({"age":{$gt:23}})
[
  {
    _id: ObjectId('65d0841ecdc7293dd028ae58'),
    name: 'hecker',
    age: 32
  }
]
mscds> db.users.find({"age":{$gt:22}})
[
  {
    _id: ObjectId('65d0841ecdc7293dd028ae58'),
    name: 'hecker',
    age: 32
  }
]
mscds> db.users.find({"age":{$gt:21}})
[
  { _id: ObjectId('65d0841ecdc7293dd028ae57'), name: 'Deep', age: 22 },
  {
    _id: ObjectId('65d0841ecdc7293dd028ae58'),
    name: 'hecker',
    age: 32
  },
  { _id: ObjectId('65d0841ecdc7293dd028ae59'), name: 'mrX', age: 22 },
  { _id: ObjectId('65d08485eac2c5695e33d270'), name: 'asad', age: 22 }
]
mscds> db.users.updateOne({"name":"mrX"},{$set:{age:12}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
mscds> db.users.find()
[
  { _id: ObjectId('65d08296cdc7293dd028ae56'), name: 'mscds' },
  { _id: ObjectId('65d0841ecdc7293dd028ae57'), name: 'Deep', age: 22 },
  {
    _id: ObjectId('65d0841ecdc7293dd028ae58'),
    name: 'hecker',
    age: 32
  },
  { _id: ObjectId('65d0841ecdc7293dd028ae59'), name: 'mrX', age: 12 },
  { _id: ObjectId('65d08485eac2c5695e33d270'), name: 'asad', age: 22 }
]
mscds> db.users.updateMany({ age: { $lt: 23 } }, { $set: { status: "active" } })
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 3,
  modifiedCount: 3,
  upsertedCount: 0
}
mscds> db.users.deleteOne({ name: "mrX" })
{ acknowledged: true, deletedCount: 1 }
mscds> db.users.find()
[
  { _id: ObjectId('65d08296cdc7293dd028ae56'), name: 'mscds' },
  {
    _id: ObjectId('65d0841ecdc7293dd028ae57'),
    name: 'Deep',
    age: 22,
    status: 'active'
  },
  {
    _id: ObjectId('65d0841ecdc7293dd028ae58'),
    name: 'hecker',
    age: 32
  },
  {
    _id: ObjectId('65d08485eac2c5695e33d270'),
    name: 'asad',
    age: 22,
    status: 'active'
  }
]
mscds> db.users.deleteMany({ age: { $lt: 22 } })
{ acknowledged: true, deletedCount: 1 }
mscds> db.users.find()
[
  { _id: ObjectId('65d08296cdc7293dd028ae56'), name: 'mscds' },
  {
    _id: ObjectId('65d0841ecdc7293dd028ae57'),
    name: 'Deep',
    age: 22,
    status: 'active'
  },
  {
    _id: ObjectId('65d0841ecdc7293dd028ae58'),
    name: 'hecker',
    age: 32
  }
]
mscds> db.users.drop()
true
mscds> db.users.find()

mscds>
