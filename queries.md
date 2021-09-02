#####Make sure you download the starter code and run the following:

```sh
  psql < movies.sql
  psql movies_db
```

#####In markdown, you can place a code block inside of three backticks (```) followed by the syntax highlighting you want, for example

\```sql

SELECT \* FROM users;

\```

#####Using the `movies_db` database, write the correct SQL queries for each of these tasks:

1.  The title of every movie.
```sql
SELECT title 
FROM movies;
```
2.  All information on the G-rated movies.
```sql
SELECT * 
FROM movies 
WHERE rating='G';
```
3.  The title and release year of every movie, ordered with the oldest movie first.
```sql
SELECT title, release_year 
FROM movies 
ORDER BY release_year;
```
4.  All information on the 5 longest movies.
```sql
SELECT * 
FROM movies 
ORDER BY runtime DESC 
LIMIT(5);
```
5.  A query that returns the columns of `rating` and `total`, tabulating the total number of G, PG, PG-13, and R-rated movies.
```sql
SELECT rating, count(rating) 
AS total 
FROM movies 
GROUP BY rating;
```
6.  A table with columns of `release_year` and `average_runtime`,tabulating the average runtime by year for every movie in the database. The data should be in reverse chronological order (i.e. the most recent year should be first).
```sql
SELECT release_year, AVG(runtime) 
AS average_runtime 
FROM movies 
GROUP BY release_year 
ORDER BY release_year;
```
7.  The movie title and studio name for every movie in the database.
```sql
SELECT Movies.title, Studios.name  
FROM Movies 
JOIN Studios 
ON Movies.ID=Studios.ID;
```
8.  The star first name, star last name, and movie title for every matching movie and star pair in the database.
```sql
SELECT s.first_name, s.last_name, m.title
FROM movies m
JOIN roles r
ON m.id=r.movie_id
JOIN stars s
ON r.star_id = s.id;
```
9.  The first and last names of every star who has been in a G-rated movie. The first and last name should appear only once for each star, even if they are in several G-rated movies. *IMPORTANT NOTE*: it's possible that there can be two *different* actors with the same name, so make sure your solution accounts for that.
```sql
SELECT s.first_name, s.last_name
FROM Stars s
JOIN Roles r
ON s.id = r.star_id
JOIN Movies m
ON r.movie_id = m.id
WHERE m.rating='G'
GROUP BY s.first_name, s.last_name;
```
10. The first and last names of every star along with the number of movies they have been in, in descending order by the number of movies. (Similar to #9, make sure that two different actors with the same name are considered separately).
```sql
SELECT s.first_name, s.last_name, count(*) AS n_movies
FROM Stars s
JOIN roles r
ON s.id=r.star_id
JOIN Movies m
ON r.movie_id = m.id
GROUP BY s.first_name, s.last_name
ORDER BY n_movies DESC;
```
### The rest of these are bonuses

11. The title of every movie along with the number of stars in that movie, in descending order by the number of stars.
```sql
SELECT m.title, count(r.star_id)
AS stars
FROM movies m
JOIN roles r
ON m.id=r.movie_id
GROUP BY m.title
ORDER BY stars DESC;
```
12.  The first name, last name, and average runtime of the five stars whose movies have the longest average.
```sql
SELECT s.first_name, s.last_name, AVG(m.runtime) 
AS average_runtime
FROM Stars s
JOIN Roles r
ON s.id = r.star_id
JOIN Movies m
ON r.movie_id = m.id
GROUP BY s.first_name, s.last_name
ORDER BY average_runtime DESC
LIMIT(5);
```
13.  The first name, last name, and average runtime of the five stars whose movies have the longest average, among stars who have more than one movie in the database.
```sql
SELECT s.first_name, s.last_name, AVG(m.runtime) 
AS average_runtime
FROM Stars s
JOIN Roles r
ON s.id = r.star_id
JOIN Movies m
ON r.movie_id = m.id
GROUP BY s.first_name, s.last_name
HAVING count(*) > 1
ORDER BY average_runtime DESC
LIMIT(5);
```
14.  The titles of all movies that don't feature any stars in our database.
```sql
SELECT m.title
FROM Movies m
LEFT JOIN roles r
ON m.id=r.movie_id
WHERE r.star_id IS NULL
```
15.  The first and last names of all stars that don't appear in any movies in our database.
```sql
SELECT s.first_name, s.last_name
FROM Stars s
LEFT JOIN roles r
ON s.id = r.star_id
WHERE r.movie_id IS NULL;
```
16.  The first names, last names, and titles corresponding to every role in the database, along with every movie title that doesn't have a star, and the first and last names of every star not in a movie.
```sql
SELECT s.first_name, s.last_name,m.title
FROM Stars s
FULL OUTER JOIN roles r
ON s.id = r.star_id
FULL OUTER JOIN movies m
ON r.movie_id = m.id;
```

