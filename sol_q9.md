# Bulk Write Operations: Question 9

## Pre-requisites for these queries

```shell
studentPortal> db.students.drop()
true

studentPortal> db.students.find()

studentPortal> show collections

studentPortal> use studentPortal
already on db studentPortal

studentPortal> db.createCollection("students")
{ ok: 1 }

studentPortal> show collections
students
```

### My query1: Insert multiple student documents in a single operation (as previously mentioned).

```shell
studentPortal> db.students.insertMany([{name: "Alice Smith", age: 23, major: "Information Technology", graduationYear: 2023, courses: [{courseName: "Database Systems", grade: "A"}, {courseName: "Java", grade: "B+"}]}, {name: "Bob Johnson", age: 24, major: "Computer Science", graduationYear: 2024, courses: [{courseName: "DSA", grade: "C"}, {courseName: "Theory of Computation", grade: "D"}]}, {name: "Eve Davis", age: 20, major: "Mechanics", graduationYear: 2026, courses: [{courseName: "Calculus", grade: "A-"}, {courseName: "Product Design", grade: "A+"}]}])
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId('666a855d8f70d239fb04a835'),
    '1': ObjectId('666a855d8f70d239fb04a836'),
    '2': ObjectId('666a855d8f70d239fb04a837')
  }
}

studentPortal> db.students.find()
[
  {
    _id: ObjectId('666a855d8f70d239fb04a835'),
    name: 'Alice Smith',
    age: 23,
    major: 'Information Technology',
    graduationYear: 2023,
    courses: [
      { courseName: 'Database Systems', grade: 'A' },
      { courseName: 'Java', grade: 'B+' }
    ]
  },
  {
    _id: ObjectId('666a855d8f70d239fb04a836'),
    name: 'Bob Johnson',
    age: 24,
    major: 'Computer Science',
    graduationYear: 2024,
    courses: [
      { courseName: 'DSA', grade: 'C' },
      { courseName: 'Theory of Computation', grade: 'D' }
    ]
  },
  {
    _id: ObjectId('666a855d8f70d239fb04a837'),
    name: 'Eve Davis',
    age: 20,
    major: 'Physics',
    graduationYear: 2026,
    courses: [
      { courseName: 'Kinetic Energy', grade: 'A-' },
      { courseName: "Newton's laws", grade: 'A+' }
    ]
  }
]
```

### My query2: Perform a bulk update to set the graduationYear to 2024 for all students majoring in "Physics".

```shell
studentPortal> db.students.find({"major": "Physics"},{_id: false})
[
  {
    name: 'Eve Davis',
    age: 20,
    major: 'Physics',
    graduationYear: 2026,
    courses: [
      { courseName: 'Kinetic Energy', grade: 'A-' },
      { courseName: "Newton's laws", grade: 'A+' }
    ]
  }
]

# Required Query
studentPortal> db.students.updateMany({"major": "Physics"}, {$set: {graduationYear: 2024}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}

# check output the graduationYear is changed
studentPortal> db.students.find({"major": "Physics"},{_id: false})
[
  {
    name: 'Eve Davis',
    age: 20,
    major: 'Physics',
    graduationYear: 2024,
    courses: [
      { courseName: 'Kinetic Energy', grade: 'A-' },
      { courseName: "Newton's laws", grade: 'A+' }
    ]
  }
]
```

### My query3: Perform a bulk delete to remove all students who have a grade lower than 'C' in any course.

```shell
studentPortal> db.students.find({},{_id: false, courses: {grade: true}, name: true})
[
  { name: 'Alice Smith', courses: [ { grade: 'A' }, { grade: 'B+' } ] },
  { name: 'Bob Johnson', courses: [ { grade: 'C' }, { grade: 'D' } ] },
  { name: 'Eve Davis', courses: [ { grade: 'A-' }, { grade: 'A+' } ] }
]

# Required Query
studentPortal> db.students.deleteMany({"courses.grade": {$in: ['D', 'F']}}, {})
{ acknowledged: true, deletedCount: 1 }

# The student Bob Johnson is deleted (He has one grade D)
studentPortal> db.students.find({},{_id: false, courses: {grade: true}, name: true})
[
  { name: 'Alice Smith', courses: [ { grade: 'A' }, { grade: 'B+' } ] },
  { name: 'Eve Davis', courses: [ { grade: 'A-' }, { grade: 'A+' } ] }
]
```
