# Text Search: Question 8

### My query1: Perform a text search to find students whose names contain the word "John".

```shell
# Need to create name as text index to use following $text operator
studentPortal> db.students.createIndex({name: "text"})
name_text

studentPortal> db.students.getIndexes()
[
  { v: 2, key: { _id: 1 }, name: '_id_' },
  { v: 2, key: { name: 1 }, name: 'name_1' },
  {
    v: 2,
    key: { major: 1, graduationYear: 1 },
    name: 'major_1_graduationYear_1'
  },
  {
    v: 2,
    key: { 'courses.courseName': 1 },
    name: 'courses.courseName_1'
  },
  # here new text index is created
  {
    v: 2,
    key: { _fts: 'text', _ftsx: 1 },
    name: 'name_text',
    weights: { name: 1 },
    default_language: 'english',
    language_override: 'language',
    textIndexVersion: 3
  }
]

# Required Query
studentPortal> db.students.find({$text: {$search: "John"}})
[
  {
    _id: ObjectId('666a751544cdb035c07551d5'),
    name: 'Rock John',
    age: 20,
    major: 'Computer Science',
    graduationYear: 2025,
    courses: [
      { courseName: 'Database Systems', grade: 'B+' },
      { courseName: 'Algorithms', grade: 'C' }
    ],
    address: { street: '101 Maple St', city: 'Central City', zipCode: 33445 }
  }
]
```

### My query2: Enable text search on the address field and find students who live on a street that contains "Elm".

```shell
studentPortal> db.students.getIndexes()
[
  { v: 2, key: { _id: 1 }, name: '_id_' },
  { v: 2, key: { name: 1 }, name: 'name_1' },
  {
    v: 2,
    key: { major: 1, graduationYear: 1 },
    name: 'major_1_graduationYear_1'
  },
  {
    v: 2,
    key: { 'courses.courseName': 1 },
    name: 'courses.courseName_1'
  },
  {
    v: 2,
    key: { _fts: 'text', _ftsx: 1 },
    name: 'name_text',
    weights: { name: 1 },
    default_language: 'english',
    language_override: 'language',
    textIndexVersion: 3
  }
]

# copy <name-text-index> value

# deleting the previous text-index
studentPortal> db.students.dropIndex("name_text")
{ nIndexesWas: 5, ok: 1 }

studentPortal> db.students.getIndexes()
[
  { v: 2, key: { _id: 1 }, name: '_id_' },
  { v: 2, key: { name: 1 }, name: 'name_1' },
  {
    v: 2,
    key: { major: 1, graduationYear: 1 },
    name: 'major_1_graduationYear_1'
  }
]

# create 'New' text-index for <address-street> to search within it
studentPortal> db.students.createIndex({"address.street": "text"})
address.street_text

studentPortal> db.students.getIndexes()
[
  { v: 2, key: { _id: 1 }, name: '_id_' },
  { v: 2, key: { name: 1 }, name: 'name_1' },
  {
    v: 2,
    key: { major: 1, graduationYear: 1 },
    name: 'major_1_graduationYear_1'
  },
  {
    v: 2,
    key: { 'courses.courseName': 1 },
    name: 'courses.courseName_1'
  },
  {
    v: 2,
    key: { _fts: 'text', _ftsx: 1 },
    name: 'address.street_text',
    weights: { 'address.street': 1 },
    default_language: 'english',
    language_override: 'language',
    textIndexVersion: 3
  }
]

# Required Query>
studentPortal> db.students.find({$text: {$search: "Elm"}})
[
  {
    _id: ObjectId('666a5f7144cdb035c07551d2'),
    name: 'Con Davis',
    age: 25,
    major: 'Information Technology',
    graduationYear: 2025,
    courses: [
      { courseName: 'Quantum Mechanics', grade: 'B+' },
      { courseName: 'Thermodynamics', grade: 'C' }
    ],
    address: { street: '115 Elm St', city: 'Gotham', zipCode: 22332 }
  },
  {
    _id: ObjectId('666878bd8f70d239fb04a832'),
    name: 'Alice Smith',
    age: 23,
    major: 'Information Technology',
    graduationYear: 2024,
    courses: [
      { courseName: 'Circuit Analysis', grade: 'A-' },
      { courseName: 'Electromagnetics', grade: 'B' }
    ],
    address: { street: '456 Elm St', city: 'Gotham', zipCode: 67890 }
  }
]
```
