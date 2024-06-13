# Advanced Queries: Question 5

### My query1: Find all students who have scored an 'A' in any course.

```shell
studentPortal> db.students.find({}, {_id: false, name: true, courses: {grade: true}})
[
  { name: 'Alice Smith', courses: [ { grade: 'A-' }, { grade: 'B' } ] },
  { name: 'Eve Davis', courses: [ { grade: 'B+' }, { grade: 'B' } ] }
]

studentPortal> db.students.find({"courses.grade": "A"})

# empty output! (shows that there is no-one with grade 'A' in collection)
```

### My query2: Retrieve students who live in "Gotham".

```shell
studentPortal> db.students.find({"address.city": "Gotham"})
[
  {
    _id: ObjectId('666878bd8f70d239fb04a832'),
    name: 'Alice Smith',
    age: 1,
    major: 'Information Technology',
    graduationYear: 2024,
    courses: [
      { courseName: 'Circuit Analysis', grade: 'A-' },
      { courseName: 'Electromagnetics', grade: 'B' }
    ],
    address: { street: '456 Elm St', city: 'Gotham', zipCode: 67890 }
  }
]

# -------------------------------------- or ---------------------------------------

studentPortal> db.students.find({"address.city": "Gotham"}, {_id: false, name: true, address: true})
[
  {
    name: 'Alice Smith',
    address: { street: '456 Elm St', city: 'Gotham', zipCode: 67890 }
  }
]
```

### My query3: Find students who have taken the course "Operating Systems".

```shell
studentPortal> db.students.find({"courses.courseName": "Operating Systems"}, {_id: false, name: true, courses: true})

# empty output! (because there is no one with courseName: Operating systems)
```

### My query4: Retrieve students who are older than 21.

```shell
studentPortal> db.students.find({}, {_id: false, name: true, age: true})
[ { name: 'Alice Smith', age: 23 }, { name: 'Eve Davis', age: 21 } ]

# Required Query
studentPortal> db.students.find({age: {$gt: 21}}, {_id: false, name: true, age: true})
[ { name: 'Alice Smith', age: 23 } ]
```

## My query5: Find students who have at least one course with a grade lower than 'B'.

```shell
# Note: Added extra document with lower grade than B to show an output with the query
studentPortal> db.students.find({}, {_id: false, name: true, courses: true})
[
  {
    name: 'Alice Smith',
    courses: [
      { courseName: 'Circuit Analysis', grade: 'A-' },
      { courseName: 'Electromagnetics', grade: 'B' }
    ]
  },
  {
    name: 'Eve Davis',
    courses: [
      { courseName: 'Quantum Mechanics', grade: 'B+' },
      { courseName: 'Thermodynamics', grade: 'B' }
    ]
  },
  {
    name: 'Con Davis',
    courses: [
      { courseName: 'Quantum Mechanics', grade: 'B+' },
      { courseName: 'Thermodynamics', grade: 'C' }
    ]
  }
]

# Required Query
studentPortal> db.students.find({"courses.grade": {$in: ["B-", "C", "D"]}}, {_id: false, name: true, courses: true})
[
  {
    name: 'Con Davis',
    courses: [
      { courseName: 'Quantum Mechanics', grade: 'B+' },
      { courseName: 'Thermodynamics', grade: 'C' }
    ]
  }
]
```
