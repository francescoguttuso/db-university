-- EX - Query con SELECT

-- 1. Selezionare tutti gli studenti nati nel 1990 (160)

select count(id)
from students
where date_of_birth like '1990%';

-- 2. Selezionare tutti i corsi che valgono più di 10 crediti (479)
select count(id)
from courses
where cfu >10;

-- 3. Selezionare tutti gli studenti che hanno più di 30 anni
select \*
from students
where year(date_of_birth) < 1996;

-- 4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)
select count(id)
from courses
where period = 'I semestre' and year = 1;

-- 5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)
select count(id)
from exams
where date = '2020-06-20' and hour > '14:00:00';

-- 6. Selezionare tutti i corsi di laurea magistrale (38)
select count(id)
from degrees
where name like 'Corso di Laurea Magistrale%';

-- 7. Da quanti dipartimenti è composta l'università? (12)
select count(id)
from departments;

-- 8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)
select count(id)
from teachers
where phone is null;

-- EX - Query con GROUP BY

-- 1. Contare quanti iscritti ci sono stati ogni anno
select year(enrolment_date), count(id)
from students
group by year(enrolment_date);

-- 2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
select office_address, count(id)
from teachers
group by office_address

-- 3. Calcolare la media dei voti di ogni appello d'esame
select exam_id, avg(vote)
from exam_student
group by exam_id;

-- 4. Contare quanti corsi di laurea ci sono per ogni dipartimento
select department_id, count(id)
from degrees
group by department_id;
