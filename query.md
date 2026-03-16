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

## query con join

## 1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

```sql
SELECT students.*
FROM students
JOIN degrees
ON students.degree_id = degrees.id
WHERE degrees.name = 'Corso di Laurea in Economia';
```

---

## 2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

```sql
SELECT degrees.*
FROM degrees
JOIN departments
ON degrees.department_id = departments.id
WHERE degrees.level = 'magistrale'
AND departments.name = 'Dipartimento di Neuroscienze';
```

---

## 3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id = 44)

```sql
SELECT courses.*
FROM courses
JOIN course_teacher
ON courses.id = course_teacher.course_id
WHERE course_teacher.teacher_id = 44;
```

---

## 4. Selezionare tutti gli studenti con il corso di laurea e il dipartimento

```sql
SELECT students.name,
students.surname,
degrees.name AS degree,
departments.name AS department
FROM students
JOIN degrees
ON students.degree_id = degrees.id
JOIN departments
ON degrees.department_id = departments.id
ORDER BY students.surname, students.name;
```

---

## 5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

```sql
SELECT degrees.name AS degree,
courses.name AS course,
teachers.name,
teachers.surname
FROM degrees
JOIN courses
ON degrees.id = courses.degree_id
JOIN course_teacher
ON courses.id = course_teacher.course_id
JOIN teachers
ON course_teacher.teacher_id = teachers.id;
```

---

## 6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica

```sql
SELECT DISTINCT teachers.*
FROM teachers
JOIN course_teacher
ON teachers.id = course_teacher.teacher_id
JOIN courses
ON course_teacher.course_id = courses.id
JOIN degrees
ON courses.degree_id = degrees.id
JOIN departments
ON degrees.department_id = departments.id
WHERE departments.name = 'Dipartimento di Matematica';
```

---

## 7. BONUS: Numero di tentativi e voto massimo per ogni studente e esame

```sql
SELECT
student_id,
exam_id,
COUNT(*) AS attempts,
MAX(vote) AS max_vote
FROM exam_student
GROUP BY student_id, exam_id;
```

### Solo tentativi con voto minimo 18

```sql
SELECT
student_id,
exam_id,
COUNT(*) AS attempts,
MAX(vote) AS max_vote
FROM exam_student
WHERE vote >= 18
GROUP BY student_id, exam_id;
```

## query group by

## 1. Contare quanti iscritti ci sono stati ogni anno

```sql
SELECT YEAR(enrolment_date) AS year,
COUNT(*) AS total_students
FROM students
GROUP BY YEAR(enrolment_date);
```

---

## 2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

```sql
SELECT office_address,
COUNT(*) AS total_teachers
FROM teachers
GROUP BY office_address;
```

---

## 3. Calcolare la media dei voti di ogni appello d'esame

```sql
SELECT exam_id,
AVG(vote) AS average_vote
FROM exam_student
GROUP BY exam_id;
```

---

## 4. Contare quanti corsi di laurea ci sono per ogni dipartimento

```sql
SELECT departments.name,
COUNT(degrees.id) AS total_degrees
FROM departments
JOIN degrees
ON departments.id = degrees.department_id
GROUP BY departments.name;
```
