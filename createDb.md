## Setting up the required database and its collection:

```shell
test> show dbs
admin 48.00 KiB
config 36.00 KiB
local 88.00 KiB

test> use studentPortal
switched to db studentPortal

studentPortal> db.createCollection("students")
{ ok: 1 }

studentPortal> show dbs
admin 48.00 KiB
config 36.00 KiB
local 88.00 KiB
studentPortal 8.00 KiB

studentPortal> show collections
students
```

## My Query

```shell
studentPortal> db.students.insertOne({name: "John Doe", age: 22, major: "Computer Science", graduationYear: 2023, courses: [{courseName: "Database Systems", grade: "A"}, {courseName: "Operating Systems", grade: "B+"}], address: {street: "123 Main St", city: "Metropolis", zipCode: 54321}})

{
   acknowledged: true,
   insertedId: ObjectId('666873fc8f70d239fb04a831')
}
```

## Output: First Document is created ATQ

```shell
studentPortal> db.students.find()
[
   {
      \_id: ObjectId('666873fc8f70d239fb04a831'),
      name: 'John Doe',
      age: 22,
      major: 'Computer Science',
      graduationYear: 2023,
      courses: [
         { courseName: 'Database Systems', grade: 'A' },
         { courseName: 'Operating Systems', grade: 'B+' }
      ],
      address: {
         street: '123 Main St',
         city: 'Metropolis',
         zipCode: 54321
      }
   }
]
```
