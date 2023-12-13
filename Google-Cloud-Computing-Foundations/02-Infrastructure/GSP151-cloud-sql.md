# GSP151 - Cloud SQL for MySQL: Qwik Start

[GSP151 - Cloud SQL for MySQL: Qwik Start](https://www.cloudskillsboost.google/course_sessions/6846186/labs/377260)

## Task 1. Create a Cloud SQL instance

* SQL > Create Instance > MySQL
* `myinstance`, `MySQL 8`
* generate password: `MhMp;yS75l;b1NZu`
* Edition: `Enterprise`, Preset: `Development`
* Region: `us-west1`, Multi zones (Highly available) > Primary Zone: `us-west1-c`

## Task 2. Connect to your instance using the mysql client in Cloud Shell

```sh
gcloud sql connect myinstance --user=root
```

## Task 3. Create a database and upload data

```sql
CREATE DATABASE guestbook;

USE guestbook;
CREATE TABLE entries (guestName VARCHAR(255), content VARCHAR(255),
    entryID INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(entryID));
    INSERT INTO entries (guestName, content) values ("first guest", "I got here!");
INSERT INTO entries (guestName, content) values ("second guest", "Me too!");

SELECT * FROM entries;
```

```text
+--------------+-------------------+---------+
| guestName    | content           | entryID |
+--------------+-------------------+---------+
| first guest  | I got here!       |       1 |
| second guest | Me too!           |       2 |
+--------------+-------------------+---------+
2 rows in set (0.00 sec)
mysql>
```
