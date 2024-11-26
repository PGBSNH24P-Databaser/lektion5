# Lösningar på övningar (lektion-4-till-6)

- recept och ingredienser
- streaming (video - tittare)
- ordrar och produkter

## 1.

1. One-to-Many: authors -> books
2. --
3. --
4. `SELECT * FROM books`
5. `SELECT * FROM authors`
6. `INSERT INTO books (book_id, title, author_id, published_year) VALUES (1, 'Lord of thr Rings', 999, 2020)`
7. `SELECT * FROM books WHERE author_id = 1`

## 2.

1. One-to-Many: classes -> students
2. --
3. --
4. `DELETE FROM classes WHERE class_id = 1`
5. -||-
6. `SELECT * FROM students WHERE class_id = 1`

## 3.

1. One-to-Many: genres -> games
2. --
3. --
4. `UPDATE genres SET genre_id = 4 WHERE game_id = 1`
5. `DELETE FROM genres WHERE genre_id = 1`

## 4.

1. Many-to-Many: teams -> team_players <- players
2. För att det är en many-to-many relation; då krävs en junction tabell
3. --
4. --
5. `INSERT INTO team_players (team_id, player_id, jersey_number, join_date) VALUES (3, 2, 40, current_date)`
6. -||-

## 5.

1. Many-to-Many: students -> student_hobbies <- hobbies
2. För att det är en many-to-many relation; då krävs en junction tabell
3. --
4. --
5. `INSERT INTO student_hobbies (student_id, hobby_id, years_experience, skill_level) VALUES (2, 4, 10, 'medel')`
6. `DELETE FROM student_hobbies WHERE student_id = 1 AND hobby_id = 3`
