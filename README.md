# MongoDB

Zen_class_Programme> db.users.insertMany([{ _id: 1, name: "John Doe", email: "john@example.com", codekata_solved: 50 },])
{ acknowledged: true, insertedIds: { '0': 1 } }
Zen_class_Programme>   { _id: 2, name: "Jane Smith", email: "jane@example.com", codekata_solved: 75 },
...   { _id: 3, name: "Sam Wilson", email: "sam@example.com", codekata_solved: 30 }
... ;

Zen_class_Programme> db.users.insertMany([
...   { _id: 1, name: "John Doe", email: "john@example.com", codekata_solved: 50 },
...   { _id: 2, name: "Jane Smith", email: "jane@example.com", codekata_solved: 75 },
...   { _id: 3, name: "Sam Wilson", email: "sam@example.com", codekata_solved: 30 }
... ]);

Zen_class_Programme> db.codekata.insertMany([
...   { user_id: 1, problems_solved: 50 },
...   { user_id: 2, problems_solved: 75 },
...   { user_id: 3, problems_solved: 30 }
... ])
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId('6718c68bc7f95c700d86b01d'),
    '1': ObjectId('6718c68bc7f95c700d86b01e'),
    '2': ObjectId('6718c68bc7f95c700d86b01f')
  }
}

Zen_class_Programme> db.attendance.insertMany([
...   { user_id: 1, date: ISODate("2020-10-16"), status: "present" },
...   { user_id: 2, date: ISODate("2020-10-17"), status: "absent" },
...   { user_id: 3, date: ISODate("2020-10-18"), status: "present" },
...   { user_id: 1, date: ISODate("2020-10-19"), status: "absent" }
... ])
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId('6718c6aac7f95c700d86b020'),
    '1': ObjectId('6718c6aac7f95c700d86b021'),
    '2': ObjectId('6718c6aac7f95c700d86b022'),
    '3': ObjectId('6718c6aac7f95c700d86b023')
  }
}

Zen_class_Programme> db.topics.insertMany([
...   { _id: 1, name: "JavaScript Basics", date: ISODate("2023-10-05") },
...   { _id: 2, name: "MongoDB Introduction", date: ISODate("2023-10-10") }
... ])
{ acknowledged: true, insertedIds: { '0': 1, '1': 2 } }
Zen_class_Programme> db.tasks.insertMany([
...   { user_id: 1, task_name: "JavaScript Assignment", submission_status: "submitted", date: ISODate("2023-10-07") },
...   { user_id: 2, task_name: "MongoDB Task", submission_status: "not_submitted", date: ISODate("2023-10-12") }
... ])
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId('6718c76cc7f95c700d86b024'),
    '1': ObjectId('6718c76cc7f95c700d86b025')
  }
}
Zen_class_Programme> db.company_drives.insertMany([
...   { drive_name: "Google", date: ISODate("2020-10-16"), user_ids: [1, 2] },
...   { drive_name: "Amazon", date: ISODate("2020-10-20"), user_ids: [2, 3] }
... ])
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId('6718c77ac7f95c700d86b026'),
    '1': ObjectId('6718c77ac7f95c700d86b027')
  }
}
Zen_class_Programme> db.mentors.insertMany([
...   { _id: 1, name: "Mentor A", mentee_count: 20 },
...   { _id: 2, name: "Mentor B", mentee_count: 10 }
... ])
{ acknowledged: true, insertedIds: { '0': 1, '1': 2 } }
Zen_class_Programme> db.topics.find({date:{$gte:ISODate("2023-10-01"),$lt:ISODate("2023-11-01")}});
[
  {
    _id: 1,
    name: 'JavaScript Basics',
    date: ISODate('2023-10-05T00:00:00.000Z')
  },
  {
    _id: 2,
    name: 'MongoDB Introduction',
    date: ISODate('2023-10-10T00:00:00.000Z')
  }
]
Zen_class_Programme> db.tasks.find({date:{$gte:ISODate("2023-10-01"),$lt:ISODate("2023-11-01")}});
[
  {
    _id: ObjectId('6718c76cc7f95c700d86b024'),
    user_id: 1,
    task_name: 'JavaScript Assignment',
    submission_status: 'submitted',
    date: ISODate('2023-10-07T00:00:00.000Z')
  },
  {
    _id: ObjectId('6718c76cc7f95c700d86b025'),
    user_id: 2,
    task_name: 'MongoDB Task',
    submission_status: 'not_submitted',
    date: ISODate('2023-10-12T00:00:00.000Z')
  }
]

Zen_class_Programme> db.company_drives.find({date:{$gte:ISODate("2020-10-15"),$lt:ISODate("2020-11-01")}});
[
  {
    _id: ObjectId('6718c77ac7f95c700d86b026'),
    drive_name: 'Google',
    date: ISODate('2020-10-16T00:00:00.000Z'),
    user_ids: [ 1, 2 ]
  },
  {
    _id: ObjectId('6718c77ac7f95c700d86b027'),
    drive_name: 'Amazon',
    date: ISODate('2020-10-20T00:00:00.000Z'),
    user_ids: [ 2, 3 ]
  }
]

Zen_class_Programme> db.company_drives.aggregate([ { $lookup: { from: "users", localField: "user_ids", foreignField: "_id", as: "students" } }]);
[
  {
    _id: ObjectId('6718c77ac7f95c700d86b026'),
    drive_name: 'Google',
    date: ISODate('2020-10-16T00:00:00.000Z'),
    user_ids: [ 1, 2 ],
    students: [
      {
        _id: 1,
        name: 'John Doe',
        email: 'john@example.com',
        codekata_solved: 50
      }
    ]
  },
  {
    _id: ObjectId('6718c77ac7f95c700d86b027'),
    drive_name: 'Amazon',
    date: ISODate('2020-10-20T00:00:00.000Z'),
    user_ids: [ 2, 3 ],
    students: []
  }
]
Zen_class_Programme> db.codekata.aggregate([
... {
... $lookup:{
... from:"users",
... localField:"user_id",
... foreignField:"_id",
... as:"userDetails"}},{
... $project:{
... "userDetails.name":1,
... "problems_solved":1}}])
[
  {
    _id: ObjectId('6718c68bc7f95c700d86b01d'),
    problems_solved: 50,
    userDetails: [ { name: 'John Doe' } ]
  },
  {
    _id: ObjectId('6718c68bc7f95c700d86b01e'),
    problems_solved: 75,
    userDetails: []
  },
  {
    _id: ObjectId('6718c68bc7f95c700d86b01f'),
    problems_solved: 30,
    userDetails: []
  }
]
Zen_class_Programme> db.mentors.find({
... mentee_count:{$gt:15}})
[ { _id: 1, name: 'Mentor A', mentee_count: 20 } ]
Zen_class_Programme> db.attendance.aggregate([
... {$match:{
... date:{
... $gte: ISODate("2020-10-15"),
... $lt:ISODate("2020-11-01")},status:"absent"}},
... {$lookup:{
... from:"tasks",
... localField:"user_id",
... foreignField:"user_id",
... as:"taskDetails"}},
... {$match:{"taskDetails.submission_status":"not_submitted"}},
... {$count:"absent_and_not_submitted_users"}]);
[ { absent_and_not_submitted_users: 1 } ]






