# Group by:

## Query n-1 Contare quanti iscritti ci sono stati ogni anno
```sql
SELECT COUNT(*) AS `enrolment_year`, YEAR(`enrolment_date`) AS `year` 
FROM `students` 
GROUP BY `year`;
```

## Query n-2 Contare gli insegnanti che hanno l'ufficio nello stesso edificio
```sql
SELECT COUNT(*) AS `teachers_number`, `office_address` 
FROM `teachers` 
GROUP BY `office_address`;
```

## Query n-3 Calcolare la media dei voti di ogni appello d'esame
```sql
SELECT AVG(`vote`) AS `avarage_vote`, `student_id` 
FROM `exam_student` 
GROUP BY `student_id`;
```

## Query n-4 Contare quanti corsi di laurea ci sono per ogni dipartimento
```sql
SELECT COUNT(*) AS `courses_number`, `department_id` 
FROM `degrees` 
GROUP BY `department_id`;
```



# Joins:

## Query n-5 Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

```sql
SELECT `students`.* , `degrees`.`name` AS `degree_name` 
FROM `students` 
JOIN `degrees` ON `degrees`.`id` = `students`.`degree_id` 
WHERE `degrees`.`name` = 'Corso di Laurea in Economia';
```

## Query n-6 Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
```sql
SELECT `degrees`.* , `departments`.`name` AS `department_name` 
FROM `degrees` 
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id` 
WHERE `degrees`.`name` LIKE 'Corso di Laurea Magistrale%' 
AND `departments`.`name` = 'Dipartimento di Neuroscienze';
```

## Query n-7 Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
```sql
SELECT `courses`.* , `course_teacher`.`teacher_id` 
FROM `courses` 
JOIN `course_teacher` ON `course_teacher`.`course_id` = `courses`.`id` 
WHERE `course_teacher`.`teacher_id` = 44;
```

## Query n-8 Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
```sql
SELECT `students`.*, `degrees`.`name` AS `degree_name`, `degrees`.`level` AS `degree_level`, `degrees`.`address` AS `degree_address`, `degrees`.`email` AS `degree_email`, `degrees`.`website` AS `degree_website`, `departments`.`name` AS `department_name`
FROM `students` 
JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id` 
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id` 
ORDER BY `students`.`surname`, `students`.`name`;
```


## Query n-9 Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
```sql
SELECT `degrees`.`id` AS `degree_id` ,`degrees`.`department_id` ,`degrees`.`name` AS `degree_name`, `degrees`.`level` AS `degree_level`, `degrees`.`address` AS `degree_address`, `degrees`.`email` AS `degree_email`, `degrees`.`website` AS `degree_website`, `courses`.`id` AS `course_id`, `courses`.`name` AS `course_name`, `courses`.`description` AS `course_description`, `courses`.`period` AS `course_period`, `courses`.`year` AS `course_year`, `courses`.`cfu` AS `course_cfu`, `courses`.`website` AS `website`, `teachers`.`id` AS `teacher_id`, `teachers`.`name` AS `teacher_name`, `teachers`.`surname` AS `teacher_surname`, `teachers`.`phone` AS `teacher_phone`, `teachers`.`email` AS `teacher_email`, `teachers`.`office_address` AS `teacher_office_address`, `teachers`.`office_number` AS `teacher_office_number`
FROM `degrees` 
JOIN `courses` ON `courses`.`degree_id` = `degrees`.`id` 
JOIN `course_teacher` ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`;
```

## Query n-10 Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
```sql
SELECT DISTINCT `teachers`.* , `departments`.`name`
FROM `teachers`
JOIN `course_teacher` ON `course_teacher`.`teacher_id` = `teachers`.`id`
JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id` 
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name` = 'Dipartimento di Matematica';
```