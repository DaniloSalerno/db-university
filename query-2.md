<!-- 
Group by:
1) Contare quanti iscritti ci sono stati ogni anno

2) Contare gli insegnanti che hanno l'ufficio nello stesso edificio

3) Calcolare la media dei voti di ogni appello d'esame

4) Contare quanti corsi di laurea ci sono per ogni dipartimento

Joins:
5) Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

6) Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

7) Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

8) Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

9) Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

10) Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18. -->



## Query n-1
```sql
SELECT COUNT(*) AS `enrolment_year`, YEAR(`enrolment_date`) AS `year` 
FROM `students` 
GROUP BY `year`;
```

## Query n-2
```sql
SELECT COUNT(*) AS `teachers_number`, `office_address` 
FROM `teachers` 
GROUP BY `office_address`;
```

## Query n-3
```sql
SELECT AVG(`vote`) AS `avarage_vote`, `student_id` 
FROM `exam_student` 
GROUP BY `student_id`;
```

## Query n-4
```sql
SELECT COUNT(*) AS `courses_number`, `department_id` 
FROM `degrees` 
GROUP BY `department_id`;
```

## Query n-5
```sql
SELECT `students`.* , `degrees`.`name` AS `degree_name` 
FROM `students` 
JOIN `degrees` ON `degrees`.`id` = `students`.`degree_id` 
WHERE `degrees`.`name` = 'Corso di Laurea in Economia';
```

## Query n-6
```sql
SELECT `degrees`.* , `departments`.`name` AS `department_name` 
FROM `degrees` 
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id` 
WHERE `degrees`.`name` LIKE 'Corso di Laurea Magistrale%' 
AND `departments`.`name` = 'Dipartimento di Neuroscienze';
```

## Query n-7
```sql
SELECT `courses`.* , `course_teacher`.`teacher_id` 
FROM `courses` 
JOIN `course_teacher` ON `course_teacher`.`course_id` = `courses`.`id` 
WHERE `course_teacher`.`teacher_id` = 44;
```

## Query n-8
```sql
SELECT `students`.*, `degrees`.`name` AS `degree_name`, `degrees`.`level` AS `degree_level`, `degrees`.`address` AS `degree_address`, `degrees`.`email` AS `degree_email`, `degrees`.`website` AS `degree_website`, `departments`.`name` AS `department_name`
FROM `students` 
JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id` 
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id` 
ORDER BY `students`.`surname`, `students`.`name`;
```


