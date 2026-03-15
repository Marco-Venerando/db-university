# DB University – Query SQL

## 1. Selezionare tutti gli studenti nati nel 1990

```sql
SELECT *
FROM students
WHERE YEAR(date_of_birth) = 1990;
```

## 2. Selezionare tutti i corsi che valgono più di 10 crediti

```sql
SELECT *
FROM courses
WHERE cfu > 10;
```

## 3. Selezionare tutti gli studenti che hanno più di 30 anni

```sql
SELECT *
FROM students
WHERE TIMESTAMPDIFF(YEAR, date_of_birth, CURDATE()) > 30;
```

## 4. Selezionare tutti i corsi del primo semestre del primo anno

```sql
SELECT *
FROM courses
WHERE year = 1
AND period = 'I semestre';
```

## 5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio del 20/06/2020

```sql
SELECT *
FROM exams
WHERE date = '2020-06-20'
AND hour > '14:00:00';
```

## 6. Selezionare tutti i corsi di laurea magistrale

```sql
SELECT *
FROM degrees
WHERE level = 'magistrale';
```

## 7. Da quanti dipartimenti è composta l'università?

```sql
SELECT COUNT(*)
FROM departments;
```

## 8. Quanti sono gli insegnanti che non hanno un numero di telefono?

```sql
SELECT COUNT(*)
FROM teachers
WHERE phone IS NULL;
```
