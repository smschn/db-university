1 . Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia. (68)

SELECT *  
FROM `students`  
JOIN `degrees`  
ON `degrees`.`id` = `students`.`degree_id`  
WHERE `degrees`.`name` = "Corso di Laurea in Economia";

---

2 . Selezionare tutti i Corsi di Laurea del Dipartimento di Neuroscienze. (7)

SELECT *  
FROM `departments`  
JOIN `degrees`  
ON `degrees`.`department_id` = `departments`.`id`  
WHERE `departments`.`name` = "Dipartimento di Neuroscienze";

---

3 . Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44). (11)

SELECT *  
FROM `courses`  
JOIN `course_teacher`  
ON `course_teacher`.`course_id` = `courses`.`id`  
JOIN `teachers`  
ON `teachers`.`id` = `course_teacher`.`teacher_id`  
WHERE `teachers`.`name` = "Fulvio"  
AND `teachers`.`surname` = "Amato";

---

4 . Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome. (5000)

SELECT `students`.`name`, `students`.`surname`, `departments`.`name` AS `department_name`, `degrees`.`name` AS `degree_name`, `degrees`.`level`, `degrees`.`address`, `degrees`.`email`  
FROM `students`  
JOIN `degrees`  
ON `degrees`.`id` = `students`.`degree_id`  
JOIN `departments`  
ON `departments`.`id` = `degrees`.`department_id`  
ORDER BY `students`.`surname` ASC, `students`.`name` ASC;

---

5 . Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti. (1317)

SELECT `degrees`.`name` AS `degree_name`, `courses`.`name` AS `course_name`, `teachers`.`name` AS `teacher_name`, `teachers`.`surname` AS `teacher_surname`  
FROM `degrees`  
JOIN `courses`  
ON `courses`.`degree_id` = `degrees`.`id`  
JOIN `course_teacher`  
ON `course_teacher`.`course_id` = `courses`.`id`  
JOIN `teachers`  
ON `teachers`.`id` = `course_teacher`.`teacher_id`  
ORDER BY `degrees`.`name` ASC, `courses`.`name` ASC;

---

6 . Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica. (54)

SELECT DISTINCT `departments`.`name` AS `department_name`, `teachers`.`name` AS `teacher_name`, `teachers`.`surname` AS `teacher_surname`  
FROM `departments`  
JOIN `degrees`  
ON `degrees`.`department_id` = `departments`.`id`  
JOIN `courses`  
ON `courses`.`degree_id` = `degrees`.`id`  
JOIN `course_teacher`  
ON `course_teacher`.`course_id` = `courses`.`id`  
JOIN `teachers`  
ON `teachers`.`id` = `course_teacher`.`teacher_id`  
WHERE `departments`.`name` = "Dipartimento di Matematica"

---

7 . BONUS: Selezionare per ogni studente quanti tentativi d’esame ha sostenuto per superare ciascuno dei suoi esami.

SELECT `students`.`id` AS `student_id`, `courses`.`name` AS `course_name`, COUNT(`exam_student`.`vote`) AS `number_of_tries`  
FROM `students`  
JOIN `exam_student`  
ON `exam_student`.`student_id` = `students`.`id`  
JOIN `exams`  
ON `exams`.`id` = `exam_student`.`exam_id`  
JOIN `courses`  
ON `courses`.`id` = `exams`.`course_id`  
GROUP BY `student_id`, `course_name`  
ORDER BY `student_id` ASC;