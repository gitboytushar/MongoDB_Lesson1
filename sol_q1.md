## My query1 - insertOne - command:

```shell
studentPortal> db.students.insertOne({name: "Alice Smith", age: 21, major: "Electrical Engineering", graduationYear: 2024, courses: [{courseName: "Circuit Analysis", grade: "A-"}, {courseName: "Electromagnetics", grade: "B"}], address: {street: "456 Elm St", city: "Gotham", zipCode: 67890}})

{
   acknowledged: true,
   insertedId: ObjectId('666878bd8f70d239fb04a832')
}
```

## My query2 - insertMany - command:

```shell
studentPortal> db.students.insertMany([{name: "Bob Johnson", age: 23, major: "Mathematics", graduationYear: 2022, courses: [{courseName: "Calculus", grade: "A+"}, {courseName: "Statistics", grade: "A"}], address: {street: "789 Pine St", city: "Star City", zipCode: 11223}}, {name: "Eve Davis", age: 20, major: "Physics", graduationYear: 2025, courses: [{courseName: "Quantum Mechanics", grade: "B+"}, {courseName: "Thermodynamics", grade: "B"}], address: {street: "101 Maple St", city: "Central City", zipCode: 33445}}])

{
   acknowledged: true,
   insertedIds: {
      '0': ObjectId('66687ba68f70d239fb04a833'),
      '1': ObjectId('66687ba68f70d239fb04a834')
   }
}

```

## Output - All the documents are created with their data:

```shell
studentPortal> db.students.find()
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
  },
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
  },
  {
    _id: ObjectId('66687ba68f70d239fb04a833'),
    name: 'Bob Johnson',
    age: 23,
    major: 'Mathematics',
    graduationYear: 2022,
    courses: [
      { courseName: 'Calculus', grade: 'A+' },
      { courseName: 'Statistics', grade: 'A' }
    ],
    address: { street: '789 Pine St', city: 'Star City', zipCode: 11223 }
  },
  {
    _id: ObjectId('66687ba68f70d239fb04a834'),
    name: 'Eve Davis',
    age: 20,
    major: 'Physics',
    graduationYear: 2025,
    courses: [
      { courseName: 'Quantum Mechanics', grade: 'B+' },
      { courseName: 'Thermodynamics', grade: 'B' }
    ],
    address: { street: '101 Maple St', city: 'Central City', zipCode: 33445 }
  }
]

```
