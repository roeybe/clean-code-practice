# Gym user records

API server that allows Gym staff to get information on gym members.

## Requirements

* users can to be added, along with membership type, and provided a unique User ID
* we can query users by User ID and the following info should be provided
  * name
  * membership type
  * enrolled classes
* get all classes info which provides classes available along with
  * their start times
  * spaces available
  * instructor name
  * location
* enroll a user in a class

## Design

1. API server that has the following endpoints:

* `POST` addUser with payload:

```json
{
   "name": "xyz",
   "membershipType": "premium"

}
```

returning:

```json
{
  "name": "xyz", 
  "userID": "123", 
  "membershipType": "premium"
}
```

* `GET` user?id=123  
  returning:
  
```json
{
 "name": "xyz",
 "membershipType": "premium",
 "enrolledClasses": [
    "spinning",
    "vinyasa Yoga"
 ]
}
```

* `GET` classes returning:
  
```json
{
  "classes": [
    {
      "className": "spinning",
      "startTime": "7:00",
      "spacesAvailable": "10",
      "instructorName": "Sonic",
      "location": "velodrome"
    }
  ]
}
```

* `POST` enrollUser

```json
{ 
    "userID": 123, 
    "className": "spinning", 
    "startTime": "7:00" 
}

```

 returning:

```json
{
  "enrollmentStatus": "success",
  "className": "spinning",
  "startTime": "7am",
  "spacesAvailable": 10,
  "instructorName": "Sonic",
  "location": "velodrome"
}

```

2. RelationalDB to store state, tables: users, classes

3. represent entities in code ideally linking schema with database schema: user, class