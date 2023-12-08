# Try to complete the basics exercices by making queries instead of using a DBMS tool:

## Write the queries below for each of the Basics exercice instructions:

## 🌱 Must-have features

### 3) Make the following tables and populate them with some dummy data (have at least two entries for every table)
  - groups: id, name, location, start_date, max_participants
  - learners: id, name, email, active
  - coaches: id, name

```
<Your SQL query here>

```

### 4) Try the following selects
  - Get all data from the groups*
  - Get the name and email of the first learner, and alias the name to learner_name*

```
<Your SQL query here>

```

### 5) 💩 happens - a group needs to be postponed
  - Update the start date of the first_group (make it two months later)*
  - Introduce a new field status which can contain a long text indicating the reason for postponing (bonus points if it's a creative one)

```
<Your SQL query here>

```

### 6) One of the learners changed his/her mind and decided to be an astronaut
  - Delete someone from the learners table*

```
<Your SQL query here>

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