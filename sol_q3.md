# Update Documents: Question 3

### My query1: Update Alice Smith's age to 22.

```shell
studentPortal> db.students.find({name: "Alice Smith"})
[
  {
    _id: ObjectId('666878bd8f70d239fb04a832'),
    name: 'Alice Smith',
    age: 21,
    major: 'Electrical Engineering',
    graduationYear: 2024,
    courses: [
      { courseName: 'Circuit Analysis', grade: 'A-' },
      { courseName: 'Electromagnetics', grade: 'B' }
    ],
    address: { street: '456 Elm St', city: 'Gotham', zipCode: 67890 }
  }
]

studentPortal> db.students.updateOne({name: "Alice Smith"}, {$set: {age: 22}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}

studentPortal> db.students.find({name: "Alice Smith"})
[
  {
    _id: ObjectId('666878bd8f70d239fb04a832'),
    name: 'Alice Smith',
    age: 22,
    major: 'Electrical Engineering',
    graduationYear: 2024,
    courses: [
      { courseName: 'Circuit Analysis', grade: 'A-' },
      { courseName: 'Electromagnetics', grade: 'B' }
    ],
    address: { street: '456 Elm St', city: 'Gotham', zipCode: 67890 }
  }
]
```

## My query2: Add a new course to John Doe's courses: {"courseName": "Machine Learning", "grade": "A"}.

```shell
studentPortal> db.students.find({name: "John Doe"})
[
  {
    _id: ObjectId('666873fc8f70d239fb04a831'),
    name: 'John Doe',
    age: 22,
    major: 'Computer Science',
    graduationYear: 2023,
    courses: [
      { courseName: 'Database Systems', grade: 'A' },
      { courseName: 'Operating Systems', grade: 'B+' }
    ],
    address: { street: '123 Main St', city: 'Metropolis', zipCode: 54321 }
  }
]

studentPortal> db.students.updateOne({name: "John Doe"},{$push: {courses: {courseName: "Machine Learning", grade: "A"}}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}

studentPortal> db.students.find({name: "John Doe"})
[
  {
    _id: ObjectId('666873fc8f70d239fb04a831'),
    name: 'John Doe',
    age: 22,
    major: 'Computer Science',
    graduationYear: 2023,
    courses: [
      { courseName: 'Database Systems', grade: 'A' },
      { courseName: 'Operating Systems', grade: 'B+' },
      { courseName: 'Machine Learning', grade: 'A' }
    ],
    address: { street: '123 Main St', city: 'Metropolis', zipCode: 54321 }
  }
]
```

### My query3: Change the major of all students graduating in 2023 to "Information Technology".

```shell
studentPortal> db.students.find({}, {major: true})
[
  {
    _id: ObjectId('666878bd8f70d239fb04a832'),
    major: 'Electrical Engineering'
  },
  { _id: ObjectId('66687ba68f70d239fb04a833'),
    major: 'Mathematics'
  },
  { _id: ObjectId('66687ba68f70d239fb04a834'),
    major: 'Physics'
  },
  {
    _id: ObjectId('666873fc8f70d239fb04a831'),
    major: 'Computer Science'
  }
]

studentPortal> // After my updateMany() query all these Major will be changed to Information Technology

studentPortal> db.students.updateMany({}, {$set: {major: "Information Technology"}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 4,
  modifiedCount: 4,
  upsertedCount: 0
}

studentPortal> db.students.find({}, {major: true})
[
  {
    _id: ObjectId('666878bd8f70d239fb04a832'),
    major: 'Information Technology'
  },
  {
    _id: ObjectId('66687ba68f70d239fb04a833'),
    major: 'Information Technology'
  },
  {
    _id: ObjectId('66687ba68f70d239fb04a834'),
    major: 'Information Technology'
  },
  {
    _id: ObjectId('666873fc8f70d239fb04a831'),
    major: 'Information Technology'
  }
]
```

### My query4: Update the address of Bob Johnson to {"street": "890 Pine St", "city": "Star City", "zipCode": "11223"}.

```shell
studentPortal> db.students.find({name: "Bob Johnson"}, {address: true})
[
  {
    _id: ObjectId('66687ba68f70d239fb04a833'),
    address: { street: '789 Pine St', city: 'Star City', zipCode: 11223 }
  }
]

studentPortal> // Changing the Address to new one

studentPortal> db.students.updateOne({name: "Bob Johnson"}, {$set: {address: {"street": "890 Pine St", "city": "Star City", "zipCode": "11223"}}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}

studentPortal> db.students.find({name: "Bob Johnson"}, {address: true})
[
  {
    _id: ObjectId('66687ba68f70d239fb04a833'),
    address: { street: '890 Pine St', city: 'Star City', zipCode: '11223' }
  }
]
```

## My query5: Increment the age of all students by 1.

```shell
studentPortal> db.students.find({}, {age: true})
[
  { _id: ObjectId('666878bd8f70d239fb04a832'), age: 22 },
  { _id: ObjectId('66687ba68f70d239fb04a833'), age: 23 },
  { _id: ObjectId('66687ba68f70d239fb04a834'), age: 20 },
  { _id: ObjectId('666873fc8f70d239fb04a831'), age: 22 }
]
studentPortal> // incrementing all ages by 1

studentPortal> db.students.updateMany({}, {$inc: {age: +1}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 4,
  modifiedCount: 4,
  upsertedCount: 0
}
studentPortal> db.students.find({}, {age: true})
[
  { _id: ObjectId('666878bd8f70d239fb04a832'), age: 23 },
  { _id: ObjectId('66687ba68f70d239fb04a833'), age: 24 },
  { _id: ObjectId('66687ba68f70d239fb04a834'), age: 21 },
  { _id: ObjectId('666873fc8f70d239fb04a831'), age: 23 }
]
```
