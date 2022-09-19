1 . Contare quanti iscritti ci sono stati ogni anno (912, 1709, 1645, 734).

SELECT COUNT(*) AS 'enroled_students_per_year', YEAR(enrolment_date) as 'enrolment_year'  
FROM `students`  
GROUP BY (YEAR(enrolment_date));

---

2 . Contare gli insegnanti che hanno l'ufficio nello stesso edificio (professori suddivisi in 29 edifici).

SELECT COUNT(*) AS 'teachers_number', `office_address`  
FROM `teachers`  
GROUP BY `office_address`;

---

3 . Calcolare la media dei voti di ogni appello d'esame (4078 appelli d'esame).

SELECT `exam_id` AS 'individual_exam_id', AVG(`vote`) AS 'average_vote_per_exam'  
FROM `exam_student`  
GROUP BY `exam_id`;

---

4 . Contare quanti corsi di laurea ci sono per ogni dipartimento (12 dipartimenti totali, 75 corsi di laurea totali).

SELECT `department_id`, COUNT(`name`) AS 'courses_number_per_department'  
FROM `degrees`  
GROUP BY `department_id`;