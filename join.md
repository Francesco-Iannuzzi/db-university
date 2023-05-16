# DAY 3 (exercise query database JOIN and GROUP BY)

## Request JOIN:

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

SELECT `students`.`name` AS `student_name`, `students`.`surname` AS `student_surname`, `degrees`.`name` AS `degree_name`
FROM `degrees`
JOIN `students` ON `degrees`.`id` = `students`.`degree_id`
WHERE `degrees`.`name` = 'Corso di Laurea in Economia';



2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

SELECT `degrees`.`name` AS `degree_name`, `departments`.`name` AS `department_name`, `degrees`.`level`
FROM `departments`
JOIN `degrees` ON  `departments`.`id` = `degrees`.`department_id`
WHERE `departments`.`name` = 'Dipartimento di Neuroscienze'
AND `degrees`.`level` = 'magistrale';



3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

SELECT `courses`.`name` AS `course_name`, `teachers`.`name` AS `teacher_name`, `teachers`.`surname` AS `teacher_surname`, `teachers`.`id` AS `teacher_id`
FROM `teachers`
JOIN `course_teacher` ON `teachers`.`id` = `course_teacher`.`teacher_id`
JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id`
WHERE `teachers`.`name` = 'Fulvio'
AND `teachers`.`surname` = 'Amato';



4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

SELECT `students`.`name` AS `student_name`, `students`.`surname` AS `student_surname`, `degrees`.`name` AS `degree_name`, `degrees`.`level`, `degrees`.`address`, `degrees`.`email`, `degrees`.`website`, `departments`.`name` AS `department_name`
FROM `departments`
JOIN `degrees` ON `departments`.`id` = `degrees`.`department_id`
JOIN `students` ON `degrees`.`id` = `students`.`degree_id`
ORDER BY `students`.`surname` ASC, `students`.`name` ASC;



5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

SELECT `degrees`.`name` AS `degree_name`, `courses`.`name` AS `course_name`, `teachers`.`name` AS `teacher_name`, `teachers`.`surname` AS `teacher_surname`
FROM `degrees`
JOIN `courses` ON `degrees`.`id` = `courses`.`degree_id`
JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`;



6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

SELECT DISTINCT `teachers`.`name` AS `teacher_name`, `teachers`.`surname` AS `teacher_surname`, `teachers`.`phone`, `teachers`.`email`, `teachers`.`office_address`, `teachers`.`office_number`, `departments`.`name` AS `department_name`
FROM `degrees`
JOIN `courses` ON `degrees`.`id` = `courses`.`degree_id`
JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name` = 'Dipartimento di Matematica';

or

SELECT DISTINCT `teachers`.*, `departments`.`name` AS `department_name`
FROM `degrees`
JOIN `courses` ON `degrees`.`id` = `courses`.`degree_id`
JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name` = 'Dipartimento di Matematica';


7. BONUS: Selezionare per ogni studente quanti tentativi d’esame ha sostenuto per superare ciascuno dei suoi esami, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18

SELECT `students`.`id`, `students`.`name`, `courses`.`id` AS `course_id`, `courses`.`name`,
COUNT(`exam_student`.`vote`) AS `attempts_number`,
MAX(`exam_student`.`vote`) AS `highest_vote`
FROM `students`
JOIN `exam_student` ON `students`.`id` = `exam_student`.`students`.`id`
JOIN `exams` ON `exam_student`.`exam_id` = `exams`.`id`
JOIN `courses` ON `exams`.`course_id` = `courses`.`id`
GROUP BY `students`.`id`, `courses`.`id`
HAVING `highest_vote` >= 18