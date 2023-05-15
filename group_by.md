# DAY 3 (exercise query database JOIN and GROUP BY)

## Request GROUP BY:

1. Contare quanti iscritti ci sono stati ogni anno

SELECT COUNT(*) AS `total_enrolment`, YEAR(`enrolment_date`) AS `year`
FROM `students`
GROUP BY `year`;



2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

SELECT COUNT(*) AS `total_teacher`, `office_address`
FROM `teachers`
GROUP BY `office_address`;



3. Calcolare la media dei voti di ogni appello d'esame

SELECT AVG(`exam_student`.`vote`) AS `vote_average`, `exam_student`.`exam_id` AS `session`
FROM `exam_student`
GROUP BY `session`;



4. Contare quanti corsi di laurea ci sono per ogni dipartimento

SELECT COUNT(*) AS `total_degrees`, `departments`.`name` AS `department_name`
FROM `degrees`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
GROUP BY `department_name`;

or

SELECT COUNT(*) AS `total_degrees`, `degrees`.`department_id` AS `department_id`
FROM `degrees`
GROUP BY `department_id`;