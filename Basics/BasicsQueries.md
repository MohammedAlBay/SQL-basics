# Try to complete the basics exercices by making queries instead of using a DBMS tool:

## Write the queries below for each of the Basics exercice instructions:

## 🌱 Must-have features

### 3) Make the following tables and populate them with some dummy data (have at least two entries for every table)
  - groups: id, name, location, start_date, max_participants
  - learners: id, name, email, active
  - coaches: id, name

```
CREATE TABLE [IF NOT EXISTS] groups(
  group_id int auto_increment,
  name varchar(50) NOT NULL,
  location text NOT NULL,
  start_date date,
  max_participants tinyint(4) NOT NULL
);

insert into groups('name', 'location', 'start_date', 'max_participants')
values
  ('Verou6', 'BRUSSELS', '2022-06-12', '25'),
  ('Verou7', 'LUIK', '2023-01-17', '25');

CREATE TABLE [IF NOT EXISTS] learners(
  learner_id int auto_increment,
  name varchar(50) NOT NULL,
  email varchar(50),
  active BOOLEAN NOT NULL
);

insert into learners('name', 'email', 'active')
values
  ('Mathias', 'mathias@hotmail.com', 'YES'),
  ('Leo', 'leonidas@gmail.com', 'NO');

CREATE TABLE [IF NOT EXISTS] coaches(
  coach_id int auto_increment,
  name varchar(50) NOT NULL,
);

insert into coaches('name')
values
  ('Sarah'),
  ('Erwin');

```

### 4) Try the following selects
  - Get all data from the groups*
  - Get the name and email of the first learner, and alias the name to learner_name*

```
SELECT name, email FROM learners
WHERE learner_id = 1;

UPDATE learners
SET name = 'learner_name'
WHERE learner_id = 1;

```

### 5) 💩 happens - a group needs to be postponed
  - Update the start date of the first_group (make it two months later)*
  - Introduce a new field status which can contain a long text indicating the reason for postponing (bonus points if it's a creative one)

```
SELECT start_date 
FROM groups
ORDER BY group_id
LIMIT 1;

UPDATE groups
SET start_date = DATEADD('2023-10-03', INTERVAL 2 MONTH)
WHERE group_id = 1;

ALTER TABLE groups
add status longtext;





```

### 6) One of the learners changed his/her mind and decided to be an astronaut
  - Delete someone from the learners table*

```
DELETE FROM learners
WHERE learner_id = 1;

```


## 🌼 Nice to have (doable)

### 6) A learner belongs to a group, and a group has a coach
  - Find a technique to make this connection in the database (what of the field is unique to a record, so we can refer to it?)

```
<Your SQL query here>

```

### 7) We want all the data
  - Select a coach and all related groups*
  - Select all the above, but also all learners from this group who are still active*

```
<Your SQL query here>

```