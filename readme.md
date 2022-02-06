
# show dbs
admin     41 kB
config  36.9 kB
local   73.7 kB
masai     41 kB

# use a database
- use masai
test> use masai
switched to db masai
masai>

# show collections
- show collections
users

# querry all documents in a collections

where users is a collection name
db.users.find()

# masai> db.users.find()
[ { _id: ObjectId("61fc05022892133ef299d89b"), field_name: 'Satya' } ]

# Or masai> db.users.find({})
[ { _id: ObjectId("61fc05022892133ef299d89b"), field_name: 'Satya' } ]

# count of results
- db.users.find({}).count()

# querry by a field name
- db.users.find({field_name: value})

# insert One
- db.users.insertOne({ field_name: value})

masai> db.users.insert({name: "Satya", code:"pw1_125", active: true})
DeprecationWarning: Collection.insert() is deprecated. Use insertOne, insertMany, or bulkWrite.
{
  acknowledged: true,
  insertedIds: { '0': ObjectId("61ff5d6c3d9a802a987f3ca4") }
}

# insert Many
- db.users.insertMany([{ field_name: value},{field_name: value}])

masai> db.users.insertMany([{ name: "Jaswant", code: "pw1_009", active: false},{name: "Pawan", code: "pw1_91", actice: true}])
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId("61ff679f84fad959b1793a34"),
    '1': ObjectId("61ff679f84fad959b1793a35")
  }
}

# Object ID
-ObjectId(0x12)
ObjectId("000000123d9a802a987f3ca5")

-Object(0x12)
[Number: 18]

- typeof ObjectId(0x12)
object

-x = ObjectId()
ObjectId("61ff5fe83d9a802a987f3ca7")

- x.valueOf()
ObjectId("61ff5fe83d9a802a987f3ca7")

- x.toString()
61ff5fe83d9a802a987f3ca7

# Below picture clear above commands
![Screenshot (174)](https://user-images.githubusercontent.com/80479635/152673620-2a1b9623-90bf-4892-a62c-a68e717a3c5d.png)
![Screenshot (175)](https://user-images.githubusercontent.com/80479635/152673636-aa53afb4-45ef-43fa-8153-95444864b32b.png)

# Data types

BSON => Binary JSON

-Dates
-binary format, easier / better for storage
-querying / traversable
-timestamp
-ObjectId
-Integers
-Decimal

# CRUD (Create, Read, Update, Delete)

-create (insertOne, insertMany)
-find
-find by field name


# update one
-updateOne
-updateMany
-$set
-$inc
-use $set and $inc together

updateOne([querry {name,value},{$set: {}}])
db.users.updateOne({ _id: ObjectId("61ff679f84fad959b1793a35") },{$set: {name: "SatyaBrata"}})

masai> db.users.updateOne({ _id: ObjectId("61ff679f84fad959b1793a35") },{$set: {name: "SatyaBrata"}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
masai> db.users.find()
[
  { _id: ObjectId("61fc05022892133ef299d89b"), field_name: 'Satya' },
  {
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  { _id: ObjectId("61fc05022892133ef299d89b"), field_name: 'Satya' },
  {
    _id: ObjectId("61ff5d6c3d9a802a987f3ca4"),
    name: 'Satya',
    code: 'pw1_125',
    active: true
  },
  {
    _id: ObjectId("61ff679f84fad959b1793a34"),
    name: 'Jaswant',
    code: 'pw1_009',
    active: false
  },
  {
    _id: ObjectId("61ff679f84fad959b1793a35"),
    name: 'SatyaBrata',
    code: 'pw1_135',
    actice: true,
    active: true
  }
]

# Below picture for above
![Screenshot (176)](https://user-images.githubusercontent.com/80479635/152673674-d66c73c1-b152-4ac4-b384-da3cce526f17.png)

# replace one (like put or patch)
-db.users.replaceOne({ _id: ObjectId("61fc05022892133ef299d89b") },{name: "SatyaBrata",code: "pw1_135",active: true})
masai> db.users.find()
[
  {
    _id: ObjectId("61fc05022892133ef299d89b"),
    name: 'SatyaBrata',
    code: 'pw1_135',
    active: true
  },
  {
    _id: ObjectId("61ff5d6c3d9a802a987f3ca4"),
    name: 'Satya',
    code: 'pw1_125',
    active: true
  },
  {
    _id: ObjectId("61ff679f84fad959b1793a34"),
    name: 'Jaswant',
    code: 'pw1_009',
    active: false
  },
  {
    _id: ObjectId("61ff679f84fad959b1793a35"),
    name: 'SatyaBrata',
    code: 'pw1_135',
    actice: true,
    active: true
  }
]

# Below picture for above
![Screenshot (177)](https://user-images.githubusercontent.com/80479635/152673704-f2b22c9a-36d1-485a-950a-6be258e412e1.png)

# updateMany
masai> db.users.updateMany({ active: true },{$set: {active: false}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 0,
  modifiedCount: 0,
}
masai> db.users.find()
[
  {
    _id: ObjectId("61fc05022892133ef299d89b"),
    name: 'SatyaBrata',
    code: 'pw1_135',
    active: false
  },
  {
    _id: ObjectId("61ff5d6c3d9a802a987f3ca4"),
    name: 'Satya',
    code: 'pw1_125',
    active: false
  },
  {
    _id: ObjectId("61ff679f84fad959b1793a34"),
    name: 'Jaswant',
    code: 'pw1_009',
    active: false
  },
  {
    _id: ObjectId("61ff679f84fad959b1793a35"),
    name: 'SatyaBrata',
    code: 'pw1_135',
    actice: true,
    active: false
  }
]
# Below picture for above
![Screenshot (178)](https://user-images.githubusercontent.com/80479635/152673719-5ad3bfe5-afdf-4629-89f4-14a5874545b4.png)

# updateMany by $set operator
masai> db.users.updateMany({ active: false },{$set: {followers: 0}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 4,
  modifiedCount: 4,
  upsertedCount: 0
}
masai> db.users.find()
[
  {
    _id: ObjectId("61fc05022892133ef299d89b"),
    name: 'SatyaBrata',
    code: 'pw1_135',
    active: false,
    followers: 0
  },
  {
    _id: ObjectId("61ff5d6c3d9a802a987f3ca4"),
    name: 'Satya',
    code: 'pw1_125',
    active: false,
    followers: 0
  },
  {
    _id: ObjectId("61ff679f84fad959b1793a34"),
    name: 'Jaswant',
    code: 'pw1_009',
    active: false,
    followers: 0
  },
  {
    _id: ObjectId("61ff679f84fad959b1793a35"),
    name: 'SatyaBrata',
    code: 'pw1_135',
    actice: true,
    active: false,
    followers: 0
  }
]
  {
    _id: ObjectId("61fc05022892133ef299d89b"),
    name: 'SatyaBrata',
    code: 'pw1_135',
    active: false,
    followers: 0
  },
  {
    _id: ObjectId("61ff5d6c3d9a802a987f3ca4"),
    name: 'Satya',
    code: 'pw1_125',
    active: false,
    followers: 1
  },
  {
    _id: ObjectId("61ff679f84fad959b1793a34"),
    name: 'Jaswant',
    code: 'pw1_009',
    active: false,
    followers: 0
  },
  {
    _id: ObjectId("61ff679f84fad959b1793a35"),
    name: 'SatyaBrata',
    code: 'pw1_135',
    actice: true,
    active: false,
    followers: 0
  }
]
# Below picture for above
![Screenshot (179)](https://user-images.githubusercontent.com/80479635/152673748-eb354bfb-4c9a-4913-b164-c8be263a78eb.png)
![Screenshot (180)](https://user-images.githubusercontent.com/80479635/152673782-5dd339c6-0400-43d7-a621-699846391d82.png)

# updateMany By $inc operator
masai> db.users.updateMany({ name: "Satya" },{$inc: {followers: 1}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
masai> db.users.find()
[
  {
    _id: ObjectId("61fc05022892133ef299d89b"),
    name: 'SatyaBrata',
    code: 'pw1_135',
    active: false,
    followers: 0
  },
    _id: ObjectId("61ff5d6c3d9a802a987f3ca4"),
    name: 'Satya',
    code: 'pw1_125',
    active: false,
    followers: 1
  },
  {
    _id: ObjectId("61ff679f84fad959b1793a34"),
    name: 'Jaswant',
    code: 'pw1_009',
    active: false,
    followers: 0
  },
  {
    _id: ObjectId("61ff679f84fad959b1793a35"),
    name: 'SatyaBrata',
    code: 'pw1_135',
    actice: true,
    active: false,
    followers: 0
  }
]
# Below picture for above
![Screenshot (181)](https://user-images.githubusercontent.com/80479635/152673806-9440ce8f-0fe9-475a-9442-1af8a6c2eda2.png)
![Screenshot (182)](https://user-images.githubusercontent.com/80479635/152673827-88268b89-1d7c-415d-9c20-c819077b3af3.png)

# delete
-deleteOne
-deleteMany

-db.users.deleteOne({name: "SatyaBrata"})
{ acknowledged: true, deletedCount: 1 }

masai> db.users.find()
[
  {
    _id: ObjectId("61ff5d6c3d9a802a987f3ca4"),
    name: 'Satya',
    code: 'pw1_125',
    active: false,
    followers: 2
  },
  {
    _id: ObjectId("61ff679f84fad959b1793a34"),
    name: 'Jaswant',
    code: 'pw1_009',
    active: false,
    followers: 0
  }
]

-db.temp.deleteMany({})

masai> db.temp.insert({name: "Satya"})
DeprecationWarning: Collection.insert() is deprecated. Use insertOne, insertMany, or bulkWrite.
{
  acknowledged: true,
  insertedIds: { '0': ObjectId("61ff74d984fad959b1793a36") }
}
masai> show collections
temp
users
masai> db.temp.find()
[ { _id: ObjectId("61ff74d984fad959b1793a36"), name: 'Satya' } ]
masai> db.temp.insertOne({name: "Albert"})
{
  acknowledged: true,
  insertedId: ObjectId("61ff751384fad959b1793a37")
}
masai> db.temp.find()
[
  { _id: ObjectId("61ff74d984fad959b1793a36"), name: 'Satya' },
  { _id: ObjectId("61ff751384fad959b1793a37"), name: 'Albert' }
]
masai> db.temp.deleteMany({})
{ acknowledged: true, deletedCount: 2 }
masai> db.temp.find()

masai>
# Below picture for above
![Screenshot (183)](https://user-images.githubusercontent.com/80479635/152673860-70d17358-b189-4680-85cc-4139bff3c9dc.png)

# use of different db
masai> use temporarydb
switched to db temporarydb
temporarydb> show dbs
admin     41 kB
config   111 kB
local   73.7 kB
masai    123 kB
temporarydb> use masai
switched to db masai
masai> show dbs
admin     41 kB
config   111 kB
local   73.7 kB
masai    123 kB

# insertMany in companies(db) like 1000

-db.companies.insertMany([MOCK_DATA.json file data])
# Below picture for above
![Screenshot (184)](https://user-images.githubusercontent.com/80479635/152673873-aafe3bbe-6f1f-46cf-ba58-58add721bd95.png)
![Screenshot (185)](https://user-images.githubusercontent.com/80479635/152673898-a7058b84-e726-43f4-8d7a-74f1908be30f.png)

# Comparison operators

-db.companies.find({}) // gt, gte, lt, lte
-$gte(greater than equal to)
-$gt(greater than)
-$lt(less than)
-$lte(less than equal to)
-$ne(not equal to)
-$in(equal to the values)
-$eq(equal to)
-$nin(not equals to values)

-db.companies.find({rating: {$gte: 80}})
-db.companies.find({rating: {$gte: 80}}).count()
207

-db.companies.find({rating: {$lt: 5}}).count()
40

-db.companies.find({rating: {$lte: 2}}).count()
19

-db.companies.find({rating: {$lte: 2, $gte: 1}}).count()
19

-db.companies.find({rating: {$lte: 5,}}).count()
52

- db.companies.find({rating: {$ne: 100}}).count()
996

-db.companies.find({rating: {$in: [3,5]}}).count()
25

-db.companies.find({rating: {$eq: 3}}).count()
13
-db.companies.find({rating: {$eq: 5}}).count()
12
13+12 = db.companies.find({rating: {$in: [3,5]}}).count()

-db.companies.find({rating: {$in: [3,4,5]}}).count()
33
# Below picture for above
![Screenshot (186)](https://user-images.githubusercontent.com/80479635/152673922-7d6f4266-91ba-4ae0-94bb-83816750e75c.png)

-db.companies.find({rating: {$nin: [3,4,5]}}).count()
971

# Projection

find(querry, projection)

read only data that you need

projection
{field_name: 1 or 0}

-db.companies.find({rating: {$in: [3,4,5]}},{company_name: 1})
[
  {
    _id: ObjectId("61ff7cbb84fad959b1793a85"),
    company_name: 'Jabbersphere'
  },
  { _id: ObjectId("61ff7cbb84fad959b1793abb"), company_name: 'Avamba' },
  { _id: ObjectId("61ff7cbb84fad959b1793ae1"), company_name: 'Mydo' },

-db.companies.find({rating: {$in: [3,4,5]}},{company_name: 1, _id: 0})
[
  { company_name: 'Jabbersphere' },
  { company_name: 'Avamba' },
  { company_name: 'Mydo' },
  { company_name: 'Realblab' },
  { company_name: 'Eazzy' },
  { company_name: 'Cogidoo' },
  { company_name: 'Buzzster' },

-it
[
  { company_name: 'Gabcube' },
  { company_name: 'Mydeo' },
  { company_name: 'Bluejam' },
  { company_name: 'Oyoloo' },
  { company_name: 'Dynabox' },
  { company_name: 'Eadel' },
  { company_name: 'Skinix' },
  { company_name: 'Kazio' },
  { company_name: 'Yambee' },
  { company_name: 'Jatri' },
  { company_name: 'Twimm' },
  { company_name: 'Dablist' },
  { company_name: 'Rhynyx' }
]

-db.companies.find({rating: {$in: [3,4,5]}},{company_name: 1, _id: 0, origin_country: 1})
[
  { company_name: 'Jabbersphere', origin_country: 'JP' },
  { company_name: 'Avamba', origin_country: 'CN' },
  { company_name: 'Mydo', origin_country: 'ID' },
  { company_name: 'Realblab', origin_country: 'GB' },
  { company_name: 'Eazzy', origin_country: 'CN' },
  { company_name: 'Cogidoo', origin_country: 'BR' },
  { company_name: 'Buzzster', origin_country: 'FR' },
  { company_name: 'Browseblab', origin_country: 'CN' },
  { company_name: 'Photofeed', origin_country: 'KW' },

-db.companies.find({rating: {$gte: 80},origin_country: "US"},{company_name: 1, _id: 0, origin_country: 1})
[
  { company_name: 'Tekfly', origin_country: 'US' },
  { company_name: 'Tanoodle', origin_country: 'US' },
  { company_name: 'Digitube', origin_country: 'US' },
  { company_name: 'Photobug', origin_country: 'US' },
  { company_name: 'Twimm', origin_country: 'US' }
]

-db.companies.find({origin_country: "US"}).count()
12

-db.companies.find({origin_country: "US"}).limit(5)
first five country

-db.companies.find({origin_country: "US"},{_id:0, company_name: 1}).limit(5)
[
  { company_name: 'Youbridge' },
  { company_name: 'Wordify' },
  { company_name: 'Yotz' },
  { company_name: 'Tekfly' },
  { company_name: 'Tanoodle' }
]

-db.companies.find({origin_country: "US"},{_id:0, company_name: 1,rating: 1}).limit(5)
[
  { company_name: 'Youbridge', rating: 79 },
  { company_name: 'Wordify', rating: 44 },
  { company_name: 'Yotz', rating: 15 },
  { company_name: 'Tekfly', rating: 82 },
  { company_name: 'Tanoodle', rating: 84 }
]

# descending order sorting by using rating: -1
-db.companies.find({origin_country: "US"},{_id:0, company_name: 1,rating: 1}).sort({rating: -1}).limit(5)
[
  { company_name: 'Twimm', rating: 97 },
  { company_name: 'Digitube', rating: 93 },
  { company_name: 'Tanoodle', rating: 84 },
  { company_name: 'Photobug', rating: 83 },
  { company_name: 'Tekfly', rating: 82 }
]

# Ascending order sorting by using rating: 1
-db.companies.find({origin_country: "US"},{_id:0, company_name: 1,rating: 1}).sort({rating: 1}).limit(5)

[
  { company_name: 'Yotz', rating: 15 },
  { company_name: 'Skyba', rating: 39 },
  { company_name: 'Oyondu', rating: 41 },
  { company_name: 'Wordify', rating: 44 },
  { company_name: 'Jabbertype', rating: 64 }
]

# Descending order sorting by using rating: -1 and company_name: 1 
-db.companies.find({origin_country: "US"},{_id:0, company_name: 1,rating: 1}).sort({rating: -1, company_name: 1}).limit(10)
[
  { company_name: 'Twimm', rating: 97 },
  { company_name: 'Digitube', rating: 93 },
  { company_name: 'Tanoodle', rating: 84 },
  { company_name: 'Photobug', rating: 83 },
  { company_name: 'Tekfly', rating: 82 },
  { company_name: 'Youbridge', rating: 79 },
  { company_name: 'Feedspan', rating: 76 },
  { company_name: 'Jabbertype', rating: 64 },
  { company_name: 'Wordify', rating: 44 },
  { company_name: 'Oyondu', rating: 41 }
]

# Ascending order sorting by company_name
-db.companies.find({origin_country: "US"},{_id:0, company_name: 1,rating: 1}).sort({company_name: 1}).limit(10)
[
  { company_name: 'Digitube', rating: 93 },
  { company_name: 'Feedspan', rating: 76 },
  { company_name: 'Jabbertype', rating: 64 },
  { company_name: 'Oyondu', rating: 41 },
  { company_name: 'Photobug', rating: 83 },
  { company_name: 'Skyba', rating: 39 },
  { company_name: 'Tanoodle', rating: 84 },
  { company_name: 'Tekfly', rating: 82 },
  { company_name: 'Twimm', rating: 97 },
  { company_name: 'Wordify', rating: 44 }
]

-db.companies.find({},{_id:0, company_name: 1,rating: 1}).sort({company_name: 1}).limit(10)
[
  { company_name: 'Abatz', rating: 49 },
  { company_name: 'Abatz', rating: 94 },
  { company_name: 'Agivu', rating: 15 },
  { company_name: 'Agivu', rating: 33 },
  { company_name: 'Aibox', rating: 81 },
  { company_name: 'Aibox', rating: 50 },
  { company_name: 'Ailane', rating: 2 },
  { company_name: 'Aimbo', rating: 75 },
  { company_name: 'Aimbo', rating: 15 },
  { company_name: 'Aimbo', rating: 43 }
]

-db.companies.find({},{_id:0, company_name: 1,rating: 1}).sort({company_name: 1, rating: -1}).limit(10) 
[
  { company_name: 'Abatz', rating: 94 },
  { company_name: 'Abatz', rating: 49 },
  { company_name: 'Agivu', rating: 33 },
  { company_name: 'Agivu', rating: 15 },
  { company_name: 'Aibox', rating: 81 },
  { company_name: 'Aibox', rating: 50 },
  { company_name: 'Ailane', rating: 2 },
  { company_name: 'Aimbo', rating: 75 },
  { company_name: 'Aimbo', rating: 43 },
  { company_name: 'Aimbo', rating: 15 }
]

# Explain()

db.companies.find({},{_id:0, company_name: 1,rating: 1}).sort({company_name: 1, rating: -1}).limit(10).
explain()
{
  explainVersion: '1',
  queryPlanner: {
    namespace: 'masai.companies',
    indexFilterSet: false,
    parsedQuery: {},
    maxIndexedOrSolutionsReached: false,
    maxIndexedAndSolutionsReached: false,
    maxScansToExplodeReached: false,
    winningPlan: {
      stage: 'PROJECTION_SIMPLE',
      transformBy: { _id: 0, company_name: 1, rating: 1 },
      inputStage: {
        stage: 'SORT',
        sortPattern: { company_name: 1, rating: -1 },
        memLimit: 104857600,
        limitAmount: 10,
        type: 'simple',
        inputStage: { stage: 'COLLSCAN', direction: 'forward' }
      }
    },
    rejectedPlans: []
  },
  command: {
    find: 'companies',
    filter: {},
    sort: { company_name: 1, rating: -1 },
    projection: { _id: 0, company_name: 1, rating: 1 },
    limit: 10,
    '$db': 'masai'
  },
  serverInfo: {
    host: 'LAPTOP-0RDA0M4E',
    port: 27017,
    version: '5.0.6',
    gitVersion: '212a8dbb47f07427dae194a9c75baec1d81d9259'
  },
  serverParameters: {
    internalQueryFacetBufferSizeBytes: 104857600,
    internalQueryFacetMaxOutputDocSizeBytes: 104857600,
    internalLookupStageIntermediateDocumentMaxSizeBytes: 104857600,
    internalDocumentSourceGroupMaxMemoryBytes: 104857600,
    internalQueryMaxBlockingSortMemoryUsageBytes: 104857600,
    internalQueryProhibitBlockingMergeOnMongoS: 0,
    internalQueryMaxAddToSetBytes: 104857600,
    internalDocumentSourceSetWindowFieldsMaxMemoryBytes: 104857600
  },
  ok: 1
}

-db.companies.find({}).explain()
{
  explainVersion: '1',
  queryPlanner: {
    namespace: 'masai.companies',
    indexFilterSet: false,
    parsedQuery: {},
    maxIndexedOrSolutionsReached: false,
    maxIndexedAndSolutionsReached: false,
    maxScansToExplodeReached: false,
    winningPlan: { stage: 'COLLSCAN', direction: 'forward' },
    rejectedPlans: []
  },
  command: { find: 'companies', filter: {}, '$db': 'masai' },
  serverInfo: {
    host: 'LAPTOP-0RDA0M4E',
    port: 27017,
    version: '5.0.6',
    gitVersion: '212a8dbb47f07427dae194a9c75baec1d81d9259'
  },
  serverParameters: {
    internalQueryFacetBufferSizeBytes: 104857600,
    internalQueryFacetMaxOutputDocSizeBytes: 104857600,
    internalLookupStageIntermediateDocumentMaxSizeBytes: 104857600,
    internalDocumentSourceGroupMaxMemoryBytes: 104857600,
    internalQueryMaxBlockingSortMemoryUsageBytes: 104857600,
    internalQueryProhibitBlockingMergeOnMongoS: 0,
    internalQueryMaxAddToSetBytes: 104857600,
    internalDocumentSourceSetWindowFieldsMaxMemoryBytes: 104857600
  },
  ok: 1
}

# top 10 in descending order

-db.companies.find({},{_id:0, company_name: 1,rating: 1}).sort({rating: -1}).limit(10)
[
  { company_name: 'Livetube', rating: 100 },
  { company_name: 'Edgeclub', rating: 100 },
  { company_name: 'Edgepulse', rating: 100 },
  { company_name: 'Thoughtbeat', rating: 100 },
  { company_name: 'Quimba', rating: 100 },
  { company_name: 'Topiclounge', rating: 100 },
  { company_name: 'Eadel', rating: 100 },
  { company_name: 'Flipbug', rating: 100 },
  { company_name: 'Flashspan', rating: 99 },
  { company_name: 'Browsetype', rating: 99 }
]

# second top ten
-db.companies.find({},{_id:0, company_name: 1,rating: 1}).sort({rating: -1}).limit(10).skip(10)
[
  { company_name: 'Browsetype', rating: 99 },
  { company_name: 'Chatterpoint', rating: 99 },
  { company_name: 'Twitterwire', rating: 99 },
  { company_name: 'Brightdog', rating: 99 },
  { company_name: 'Feedfire', rating: 99 },
  { company_name: 'Skibox', rating: 99 },
  { company_name: 'Browsecat', rating: 99 },
  { company_name: 'Vinder', rating: 99 },
  { company_name: 'Photojam', rating: 99 },
  { company_name: 'Flashspan', rating: 99 }
]
