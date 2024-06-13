# Problem Set: MongoDB Queries To Solve

Database and Collection Setup: Assume you have a MongoDB database named studentPortal and a collection named students. 

The documents in the students collection have the following structure:

```shell
{
   "name": "John Doe",
   "age": 22,
   "major": "Computer Science",
   "graduationYear": 2023,
   "courses": [
      {"courseName": "Database Systems", "grade": "A"},
      {"courseName": "Operating Systems", "grade": "B+"}
   ],
   "address": {
      "street": "123 Main St",
      "city": "Metropolis",
      "zipCode": "54321"
   }
}
```

# Questions:

## 1. Insert a new student document with the following details:
```shell
   {
  "name": "Alice Smith",
  "age": 21,
  "major": "Electrical Engineering",
  "graduationYear": 2024,
  "courses": [
    {"courseName": "Circuit Analysis", "grade": "A-"},
    {"courseName": "Electromagnetics", "grade": "B"}
  ],
  "address": {
    "street": "456 Elm St",
    "city": "Gotham",
    "zipCode": "67890"
  }
}
```
## Insert multiple student documents in a single operation:
[
```shell
  {
    "name": "Bob Johnson",
    "age": 23,
    "major": "Mathematics",
    "graduationYear": 2022,
    "courses": [
      {"courseName": "Calculus", "grade": "A+"},
      {"courseName": "Statistics", "grade": "A"}
    ],
    "address": {
      "street": "789 Pine St",
      "city": "Star City",
      "zipCode": "11223"
    }
  },
  {
    "name": "Eve Davis",
    "age": 20,
    "major": "Physics",
    "graduationYear": 2025,
    "courses": [
      {"courseName": "Quantum Mechanics", "grade": "B+"},
      {"courseName": "Thermodynamics", "grade": "B"}
    ],
    "address": {
      "street": "101 Maple St",
      "city": "Central City",
      "zipCode": "33445"
    }
  }
```
]
## 2. Find Documents
   - Retrieve all student documents from the students collection.
   - Find the student with the name "Alice Smith".
   - Retrieve students who are majoring in "Computer Science".
   - Find students who have a grade of 'A' in any course.
   - Retrieve students who live in "Gotham".
   - Find students who have taken the course "Operating Systems".

## 3. Update Documents
   - Update Alice Smith's age to 22.
   - Add a new course to John Doe's courses: {"courseName": "Machine Learning", "grade": "A"}.
   - Change the major of all students graduating in 2023 to "Information Technology".
   - Update the address of Bob Johnson to {"street": "890 Pine St", "city": "Star City", "zipCode": "11223"}.
   - Increment the age of all students by 1.

## 4. Delete Documents
   - Remove the student document with the name "John Doe".
   - Delete all students who are majoring in "Electrical Engineering".
   - Remove students who have graduated before 2023.

## 5. Advanced Queries
   - Find all students who have scored an 'A' in any course.
   - Retrieve students who live in "Gotham".
   - Find students who have taken the course "Operating Systems".
   - Retrieve students who are older than 21.
   - Find students who have at least one course with a grade lower than 'B'.

## 6. Aggregation Framework
   - Calculate the average age of students in the students collection.
   - Group students by their graduation year and count the number of students in each group.
   - Find the maximum and minimum age of students.
   - Calculate the average grade for the course "Database Systems".
   - Group students by their major and calculate the average age for each group.

## 7. Indexing
   - Create an index on the name field of the students collection.
   - Create a compound index on the major and graduationYear fields.
   - Create an index on the courses.courseName field to improve the performance of queries involving course names.

## 8. Text Search
   - Perform a text search to find students whose names contain the word "John".
   - Enable text search on the address field and find students who live on a street that contains "Elm".

## 9. Bulk Write Operations
   - Insert multiple student documents in a single operation (as previously mentioned).
   - Perform a bulk update to set the graduationYear to 2024 for all students majoring in "Physics".
   - Perform a bulk delete to remove all students who have a grade lower than 'C' in any course.