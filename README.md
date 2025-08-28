# Python FastAPI SQLAlchemy Relationships Solution

## About

This repo contains the solution code for the [Python FastAPI SQLAlchemy Relationships](https://pages.git.generalassemb.ly/modular-curriculum-all-courses/python-fastapi-sqlalchemy-relationships/canvas-landing-pages/fallback.html) Lesson.

## Getting Started

1. Fork and clone this repo.

2. Navigate into the project directory:

```sh
 cd python-fastapi-sqlalchemy-relationships-solution
```

3. Install dependencies (this also creates the virtual environment if it doesn’t exist):

```sh
 pipenv install
```

4. Activate the virtual environment:

```sh
 pipenv shell
```

### Set up the database

1. Set up your PostgreSQL database:

   - Ensure PostgreSQL is installed and running on your machine.
   - Create a database named `teas_db` if it does not already exist:

```bash
createdb teas_db
```

### Connect to database

Open the application in Visual Studio Code:

```bash
code .
```

The database connection string is defined in the `config/environment.py` file:

```python
db_URI = "postgresql://<username>@localhost:5432/teas_db"
```

- Ensure your PostgreSQL instance is configured to allow connections with the provided credentials.
- **_Modify your database connection string to use your username as the `<username>`._**

### Seed the database

Seed the database with initial data:

- Run the `seed.py` file to reset the database by dropping existing tables and repopulating it with starter data:

```bash
pipenv run python seed.py
```

> You should see output indicating the database was successfully seeded. If there are any errors, check the `db_URI` in the `config/environment.py` file.

### Verifying the Data

To confirm that the data has been inserted correctly, use the `psql` tool to query the database.

```sh
psql -d teas_db -U <username>
```

### Query the Tables

```sql
-- View all teas
SELECT * FROM teas;

-- View all comments
SELECT * FROM comments;
```

You should see the following results:

1. The `teas` table contains the teas from `teas_list`.

```text
 id |    name    | in_stock | rating |         created_at         |         updated_at
----+------------+----------+--------+----------------------------+----------------------------
  1 | chai       | t        |      4 | 2025-02-14 14:45:55.261833 | 2025-02-14 14:45:55.261833
  2 | earl grey  | f        |      3 | 2025-02-14 14:45:55.261833 | 2025-02-14 14:45:55.261833
  3 | matcha     | t        |      3 | 2025-02-14 14:45:55.261833 | 2025-02-14 14:45:55.261833
  4 | green tea  | t        |      5 | 2025-02-14 14:45:55.261833 | 2025-02-14 14:45:55.261833
  5 | black tea  | t        |      4 | 2025-02-14 14:45:55.261833 | 2025-02-14 14:45:55.261833
  6 | oolong     | f        |      4 | 2025-02-14 14:45:55.261833 | 2025-02-14 14:45:55.261833
  7 | hibiscus   | t        |      4 | 2025-02-14 14:45:55.261833 | 2025-02-14 14:45:55.261833
  8 | peppermint | t        |      5 | 2025-02-14 14:45:55.261833 | 2025-02-14 14:45:55.261833
  9 | jasmine    | t        |      3 | 2025-02-14 14:45:55.261833 | 2025-02-14 14:45:55.261833
(9 rows)
```

2. The `comments` table contains the comments from `comments_list`, with the correct `tea_id` linking them to their respective teas.

```text
 id |               content                | tea_id |         created_at         |         updated_at
----+--------------------------------------+--------+----------------------------+----------------------------
  1 | This is a great tea                  |      1 | 2025-02-14 14:45:55.264234 | 2025-02-14 14:45:55.264234
  2 | Perfect for relaxing evenings        |      2 | 2025-02-14 14:45:55.264234 | 2025-02-14 14:45:55.264234
  3 | I love the vibrant green color!      |      3 | 2025-02-14 14:45:55.264234 | 2025-02-14 14:45:55.264234
  4 | So refreshing and healthy!           |      4 | 2025-02-14 14:45:55.264234 | 2025-02-14 14:45:55.264234
  5 | A classic choice for any time of day |      5 | 2025-02-14 14:45:55.264234 | 2025-02-14 14:45:55.264234
(5 rows)
```
