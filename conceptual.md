### Conceptual Exercise

Answer the following questions below:

- What is PostgreSQL?
>Is a database software that allow us to create tables to manage data.

- What is the difference between SQL and PostgreSQL?
>Psql is an open-source ORDM that uses query language, while SQL is a RDBM from microsoft.

- In `psql`, how do you connect to a database?
> $ psql database or inside psql \c database;

- What is the difference between `HAVING` and `WHERE`?
> WHERE statement filters from a table, while HAVING filters from groups (GROUP BY)

- What is the difference between an `INNER` and `OUTER` join?
> Inner Join only shows the overlap of the tables, while outer joins shows more than the overlap.

- What is the difference between a `LEFT OUTER` and `RIGHT OUTER` join?
> Left will return all rows from table on left side, right outer will return all rows from right side of the join.

- What is an ORM? What do they do?
> Object-relational mapping, is a way to convert data to objects we can use in our code. So it's possible to store more types of data, like booleans and dates.

- What are some differences between making HTTP requests using AJAX 
  and from the server side using a library like `requests`?
> AJAX will make the request from the client while 'requests' will make the request from the server therefore we will manipulate the data differently
- What is CSRF? What is the purpose of the CSRF token?
> Cross Site Request Forgery is an attack that can change the requests made by the user to alter the data. We implement a CSRF token into a form to make sure it's the form from our server that is making the request.

- What is the purpose of `form.hidden_tag()`?
> It creates a CSRF token in the form.b