# SQL Homework

The local cinema are having a Marvel Movie Marathon! They have asked you to help maintain their database of movies with times and attendees.

## To access the database:

First, create a database called 'marvel'

```
# terminal
createdb marvel
```

Next, run the provided SQL script to populate your database:

```
# terminal
psql -d marvel -f marvel.sql
```

Use the supplied data as the source of data to answer the questions. Copy the SQL command you have used to get the answer, and paste it below the question, along with the result they gave.

## Questions

1.  Return ALL the data in the 'movies' table.

```sql
SELECT * FROM movies;
```

2.  Return ONLY the name column from the 'people' table

```sql
SELECT name FROM people;
```

3.  Oops! Someone at CodeClan spelled Graham's name wrong! Change it to reflect the proper spelling ('Graeme Broose' should be 'Graham Bruce').

```sql
-- check the returned row first and then use id for update
SELECT * from people WHERE name = 'Graeme Broose';
UPDATE people SET name = 'Graham Bruce' WHERE id = 3;
```

4. Insert your name into the 'people' table.

```sql
INSERT INTO people (name) VALUES ('James');
```

5.  Return ONLY your name from the 'people' table.

```sql
SELECT name FROM people WHERE name = 'James';
```

6.  The cinema is showing 'Batman Begins', but Batman is DC, not Marvel! Delete the entry from the 'movies' table.

```sql
-- check the returned row first and then use id for delete
SELECT * FROM movies WHERE title = 'Batman Begins';
DELETE FROM movies WHERE id = 9;
```

7.  Create a new entry in the 'people' table with the name of one of the instructors.

```sql
INSERT INTO people (name) VALUES ('Keith Douglas');
```

8.  Craig has decided to hijack our movie evening, Remove him from the table of people.

```sql
-- check the returned row first and then use id for delete
SELECT * FROM people WHERE name = 'Craig Morton';
DELETE FROM people WHERE id = 16;
```

9.  The cinema has just heard that they will be holding an exclusive midnight showing of 'Avengers: Infinity War'!! Create a new entry in the 'movies' table to reflect this.

```sql
-- check the type for show_time (it's a VARCAHR), google is my friend
SELECT column_name, data_type FROM information_schema.columns WHERE table_name = 'movies';
INSERT INTO movies (title, year, show_time) VALUES ('Avengers: Infinity War', 2018, '00:00');
```

10.  The cinema would also like to make the Guardians movies a back to back feature. Find out the show time of "Guardians of the Galaxy" and set the show time of "Guardians of the Galaxy 2" to start two hours later.

```sql
-- return the show_time for Guardians and then the id for Guardians 2 then update using id
SELECT show_time FROM movies WHERE title = 'Guardians of the Galaxy';
SELECT id FROM movies WHERE title = 'Guardians of the Galaxy 2';
UPDATE movies SET show_time = '20:55' WHERE id = 16;
```

## Extension

1.  Research how to delete multiple entries from your table in a single command.

```sql
-- all movies from 2008 or 2010
DELETE FROM movies WHERE year = 2008 OR year = 2010;
-- all movies not called 'Ant-Man'
DELETE FROM movies WHERE title <> 'Ant-Man';
-- all movies with a title starting with 'Guard'
DELETE FROM movies WHERE title LIKE 'Guard%';
-- all movies with a title not starting with 'Guard'
DELETE FROM movies WHERE title NOT LIKE 'Guard%';
-- all movies before 2017
DELETE FROM movies WHERE year < 2017;
-- all movies with a title ending in a number
DELETE FROM movies WHERE title ~ '[1-9]$';
```
