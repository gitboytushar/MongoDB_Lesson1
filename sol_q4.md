# Delete Documents: Question 4

### My query1: Remove the student document with the name "John Doe".

```shell
studentPortal> db.students.find({}, {_id: false, name: true})
[
  { name: 'John Doe' }
  { name: 'Alice Smith' },
  { name: 'Bob Johnson' },
  { name: 'Eve Davis' },
]

studentPortal> db.students.deleteOne({name: "John Doe"})
{ acknowledged: true, deletedCount: 1 }

studentPortal> db.students.find({}, {_id: false, name: true})
[
  { name: 'Alice Smith' },
  { name: 'Bob Johnson' },
  { name: 'Eve Davis' }
]
```

## My query2. Delete all students who are majoring in "Electrical Engineering".

```shell
studentPortal> db.students.find({}, {_id: false, name: true,  major: true})
[
  { name: 'Alice Smith', major: 'Information Technology' },
  { name: 'Bob Johnson', major: 'Information Technology' },
  { name: 'Eve Davis', major: 'Information Technology' }
]

studentPortal> db.students.deleteMany({major: "Electrical Engineering"})
{ acknowledged: true, deletedCount: 0 }
```

### My query3. Remove students who have graduated before 2023.

```shell
studentPortal> db.students.find({}, {_id: false, name: true,  graduationYear: true})
[
  { name: 'Alice Smith', graduationYear: 2024 },
  { name: 'Bob Johnson', graduationYear: 2022 },
  { name: 'Eve Davis', graduationYear: 2025 }
]

studentPortal> db.students.deleteMany({graduationYear: {$lt: 2023}})
{ acknowledged: true, deletedCount: 1 }

studentPortal> db.students.find({}, {_id: false, name: true,  graduationYear: true})
[
  { name: 'Alice Smith', graduationYear: 2024 },
  { name: 'Eve Davis', graduationYear: 2025 }
]
```
