## Instruction

Dopo aver testato le vostre query con phpMyAdmin, riportatele in un file query.md e caricatelo nella vostra repo.
1. Selezionare tutti gli studenti nati nel 1990 (160)
2. Selezionare tutti i corsi che valgono più di 10 crediti (479)
3. Selezionare tutti gli studenti che hanno più di 30 anni
4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)
5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)
6. Selezionare tutti i corsi di laurea magistrale (38)
7. Da quanti dipartimenti è composta l'università? (12)
8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)


## Query

1.  SELECT *
    FROM `students`
    WHERE `date_of_birth` LIKE '1990%';

2.  SELECT * 
    FROM `courses` 
    WHERE `cfu` > 10;

3.  SELECT * 
    FROM `students` 
    WHERE `date_of_birth` < '1993/04/24';

4.  SELECT *
    FROM `courses`
    WHERE `period` = 'I semestre' AND `year` = 1;

5.  SELECT *
    FROM `exams` 
    WHERE `date` = '2020-06-20' AND `hour` > '14:00:00';

6.  SELECT *
    FROM `degrees` 
    WHERE `name` LIKE '%Laurea Magistrale%';

7.  SELECT COUNT(*) 
    as total_departments FROM `departments`;

8.  SELECT COUNT(*)
    as teachers_without_phone 
    FROM `teachers` WHERE `phone` IS NULL;