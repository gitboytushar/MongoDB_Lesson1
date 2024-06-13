# Indexing: Question 7

### My query1: Create an index on the name field of the students collection.

```shell
studentPortal> db.students.getIndexes()
[ { v: 2, key: { _id: 1 }, name: '_id_' } ]

# Required Query
studentPortal> db.students.createIndex({name: 1})
name_1

studentPortal> db.students.getIndexes()
[
  { v: 2, key: { _id: 1 }, name: '_id_' },
  { v: 2, key: { name: 1 }, name: 'name_1' }
]
```

### My query2: Create a compound index on the major and graduationYear fields.

```shell
studentPortal> db.students.getIndexes()
[
  { v: 2, key: { _id: 1 }, name: '_id_' },
  { v: 2, key: { name: 1 }, name: 'name_1' }
]

# Required Query
studentPortal> db.students.createIndex({major: 1, graduationYear: 1})
major_1_graduationYear_1

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
```

### My query3: Create an index on the courses.courseName field to improve the performance of queries involving course names.

```shell
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

# Required Query
studentPortal> db.students.createIndex({"courses.courseName": 1})
courses.courseName_1

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
  }
]
```
