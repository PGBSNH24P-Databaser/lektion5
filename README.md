---
author: Lektion 5
date: MMMM dd, YYYY
paging: "%d / %d"
---

# Lektion 5

Hej och välkommen!

## Agenda

1. Frågor, quiz och repetition
2. Genomgång av övningar (1-5)
3. Repetition av many-to-many relationer
4. Exempel med relationer
5. Constraints för relationer
6. Introduktion till joins
7. Övning med handledning
8. Quiz frågor

---

# Fråga

När är det aktuellt att använda en `CROSS JOIN`?

# Svar

De används väldigt sällan, men i så fall för att hämta alla möjliga kombinationer av något, som exempelvis kunder och priser.

---

# Fråga

I ett exempel finns denna definition (vid skapandet av tabell):

```sql
FOREIGN KEY (author_id) REFERENCES authors(author_id)
```

Det ser annorlunda ut från vanlig syntax, vad betyder det?

# Svar

Det är helt enkel ett annat sätt att skapa foreign keys, ekvivalent med:

```sql
column type REFERENCES authors(author_id)
```

---

# Quiz frågor

- Vad är en connection string?
- Varför skall man inte lägga in query-argument genom string concatenation?
- Vilka argument tar `NpgsqlCommand` klass-constructorn in?
- Kan en primary key vara av datatypen `int`?
- Om man vill spara en lista med saker i PostgreSQL, vad gör man?
- Varför är det ovanligt att ha One-to-One relationer?
- Vad är det för skillnad på Many-to-One och One-to-Many relationer?
- Hur implementeras Many-to-Many relationer med tabeller?

---

# Typer av relationer

## One-to-One

En rad refererar till exakt en rad. Förekommer sällan.

## One-to-Many och Many-to-One

En rad refererar till flera (0-n) rader. One-to-Many och Many-to-One är samma sak från olika perspektiv.

## Many-to-Many

Flera rader refererar till flera rader. Om One-to-Many går åt båda hållen så är det Many-to-Many. Skapas med "junction" tabeller.

Exempel: användare <-> git repos, spelare <-> spel

---

# Exempel med relationer

- E-commerce: produkter och ordrar
- Social media plattform: användare, inlägg, kommentarer
- GitHub: användare, repositories, inställningar

---

# Constraints

- `ON DELETE`
  - `RESTRICT` - Förhindra radering när relationer finns
  - `CASCADE` - Radera alla rader med matchande foreign key
  - `SET NULL` - Radera matchande foreign keys (sätt till NULL)
  - `NO ACTION` - Lik `RESTRICT` men kan bli defered
- `ON UPDATE`
  - `RESTRICT` - Förhindra ändring av primary key
  - `CASCADE` - Uppdaterar foreign key om primary key ändras
  - `SET NULL` - Radera matchande foreign keys (sätt till NULL)

---

# Constraints exempel

```sql
CREATE TABLE departments (
    id INT PRIMARY KEY,
    name VARCHAR(50)
);

CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(50),
    dept_id INT,
    FOREIGN KEY (dept_id) REFERENCES departments(id)
        ON DELETE CASCADE
        ON UPDATE SET NULL
);
```

---

# Introduktion till joins

En join är en slags query som kan hämta data från två eller fler tabeller samtidigt. De används i samband med relationer.

Joins kan användas för att hämta data i en tabell om man endast har information om en annan tabell.

Exempel: du har namnet på en person men vill veta vad namnen på husdjuren är.

---

# Typer av joins

- `INNER JOIN` - Hämtar alla rader med matchande värden
- `LEFT JOIN` - Hämtar alla rader från vänster, och de rader från höger som matchar
- `RIGHT JOIN` - Hämtar alla rader från höger, och de rader från vänster som matchar
- `FULL OUTER JOIN` - Hämtar alla rader och matchar de som går
- `CROSS JOIN` - Matchar alla rader och kolumner från båda tabeller

---

# Joins exempel

```sql
SELECT 
    employees.name,
    departments.dept_name
FROM employees
INNER JOIN departments ON employees.dept_id = departments.dept_id;

SELECT 
    employees.name,
    departments.dept_name
FROM employees
LEFT JOIN departments ON employees.dept_id = departments.dept_id;

SELECT 
    employees.name,
    departments.dept_name
FROM employees
FULL OUTER JOIN departments ON employees.dept_id = departments.dept_id;
```

---

# Quiz frågor

- Ge ett exempel på en Many-to-Many relation.
- Hur implementeras Many-to-Many relationer med tabeller?
- Vad är det för skillnad på `LEFT JOIN` och `RIGHT JOIN?`
- Vad gör `INNER JOIN`?
- Vad gör `ON DELETE CASCADE`?
- Nämn ett exempel då `ON DELETE SET NULL` är passande.
- Kan en query innehålla flera joins?
