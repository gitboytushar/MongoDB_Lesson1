# Aggregation Framework: Question 6

## My query1: Calculate the average age of students in the students collection.

```shell
studentPortal> db.students.aggregate([{$group: {_id: null, averageAge: { $avg: "$age" }}}])

[ { _id: null, averageAge: 23 } ]
```

## My query2: Group students by their graduation year and count the number of students in each group.

```shell
studentPortal> db.students.aggregate([{$group: {_id: "graduationYear", studentCount: {$sum: 1}}}])

[ { _id: 'graduationYear', studentCount: 3 } ]
```

### My query3: Find the maximum and minimum age of students.

```shell
studentPortal> db.students.find({}, {_id: false, name: true, age: true})
[
  { name: 'Alice Smith', age: 23 },
  { name: 'Eve Davis', age: 21 },
  { name: 'Con Davis', age: 25 }
]

# Required Query
studentPortal> db.students.aggregate([{$group: {_id: "null", maxAge: {$max: "$age"}, minAge: {$min: "$age"}}}])

[ { _id: 'null', maxAge: 25, minAge: 21 } ]
```

### My query4: Calculate the average grade for the course "Database Systems".

```shell
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
  },
  {
    name: 'Willy Wonka',
    courses: [
      { courseName: 'Quantum Mechanics', grade: 'B+' },
      { courseName: 'Thermodynamics', grade: 'C' }
    ]
  },
  {
    name: 'Olivia',
    courses: [
      { courseName: 'Database Systems', grade: 'B+' },
      { courseName: 'Algorithms', grade: 'C' }
    ]
  }
]

# Required Query
studentPortal> db.students.aggregate([{$unwind: "$courses"}, {$match: {"courses.courseName": "Database Systems"}}, {$group: {_id: "$courses.courseName", averageGrade: {$avg: "$courses.grade"}}}])

[ { _id: 'Database Systems', averageGrade: null } ]

# It is returning Null because the grade is in alphabetical format instead of numeric
```

## My query5: Group students by their major and calculate the average age for each group.

```shell
studentPortal> db.students.aggregate([
      {
         $group: {
            _id: "$major",
            averageAge: {"$avg": "$age"}
         }
      },
      {
         $project: {
            _id: 0,
            major: "$_id", averageAge: 1
         }
      }
   ])

# Output:
[
  { averageAge: 23, major: 'Information Technology' },
  { averageAge: 26, major: 'Mechanics' },
  { averageAge: 20, major: 'Computer Science' }
]
```
