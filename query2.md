## Group by

1. Contare quanti iscritti ci sono stati ogni anno
2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
3. Calcolare la media dei voti di ogni appello d'esame
4. Contare quanti corsi di laurea ci sono per ogni dipartimento

## Joins

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)


## BONUS

Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.


// Group by //

1.  SELECT COUNT(id), YEAR(`students`.`enrolment_date`) AS 'year_enrolment'
    FROM `students` 
    GROUP BY YEAR(`enrolment_date`);

2.  SELECT COUNT(id) , `teachers`.`office_address`
    FROM `teachers`
    GROUP BY `office_address`;   

3.  SELECT AVG(`exam_student`.`vote`) AS 'media_vote', `exam_student`.`exam_id`
    FROM `exam_student`
    GROUP BY exam_id;    

4.  SELECT COUNT(id), `degrees`.`department_id`
    FROM `degrees`
    GROUP BY `department_id`;  


// JOIN //

1.  SELECT `students`.`name`,`students`.`surname`, `degrees`.`name` AS 'name_of_course'
    FROM `students`
    JOIN `degrees`
    ON `degrees`.`id` = `students`.`degree_id`
    WHERE `degrees`.`name` = "Corso di Laurea in Economia";
 
    (68 results)


2.  SELECT `degrees`.`name`, `degrees`.`level`, `departments`.`name` AS 'name_of_departement'
    FROM `degrees`
    JOIN `departments`
    ON `departments`.`id` = `degrees`.`department_id`
    WHERE `departments`.`name`= "Dipartimento di Neuroscienze" AND `degrees`.`level` = "magistrale";

    (1 results)


3.  SELECT `courses`.`name`, `teachers`. `name`, `teachers`. `surname`
    FROM `course_teacher`
    JOIN `teachers`
    ON `teachers`.`id` = `course_teacher`.`teacher_id`
    JOIN `courses`
    ON `courses`.`id` = `course_teacher`.`course_id`
    WHERE `course_teacher`.`teacher_id` = 44;

    (11 results)

4.  SELECT `students`.`*`, `degrees`.`name` AS 'name_of_course', `departments`.`name`  AS 'name_department'
    FROM `students`
    JOIN `degrees`
    ON `degrees`.`id` = `students`.`degree_id`
    JOIN `departments`
    ON `departments`.`id`= `degrees`.`department_id`
    ORDER BY `students`.`surname` , `students`.`name` ASC;

    (11 results)

5.  SELECT `degrees`.`name`, `teachers`.`name` AS 'name_of_teacher', `teachers`.`surname`, `courses`.`name` AS 'name_of_course'
    FROM `degrees`
    JOIN `courses`
    ON `degrees`.`id` = `courses`.`degree_id`
    JOIN `course_teacher`
    ON `courses`.`id` = `course_teacher`.`course_id`
    JOIN `teachers`
    ON `teachers`.`id` = `course_teacher`.`teacher_id`;

6.  SELECT `departments`.`name` AS 'name_of_department', `teachers`.`*`
    FROM `course_teacher`
    JOIN `teachers`
    ON `teachers`.`id` = `course_teacher`.`teacher_id`
    JOIN `courses`
    ON `courses`.`id` = `course_teacher`.`course_id`
    JOIN `degrees`
    ON `degrees`.`id` = `courses`.`degree_id`
    JOIN `departments`
    ON `departments`.`id`= `degrees`.`department_id`
    WHERE `departments`.`name` = "Dipartimento di Matematica";

