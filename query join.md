-- 1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

select \* from students
join degrees
on degrees.id = students.degree_id
where degrees.id = 53;

-- 2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

select \* from degrees
join departments
on departments.id=degrees.department_id
where departments.id=7
and degrees.level="magistrale";

-- 3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

select \* from teachers
join course_teacher
on teachers.id=course_teacher.teacher_id
join courses
on courses.id=course_teacher.course_id
where teachers.id=44;

-- 4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

select \* from students
join degrees
on degrees.id= students.degree_id
join departments
on departments.id=degrees.department_id
order by students.surname;

-- 5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
select \* from teachers
join course_teacher
on teachers.id=course_teacher.teacher_id
join courses
on courses.id=course_teacher.course_id
join degrees
on degrees.id = courses.degree_id;

-- 6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

select \* from degrees
join departments
on departments.id= degrees.department_id
join courses
on degrees.id=courses.degree_id
join course_teacher
on courses.id=course_teacher.course_id
join teachers
on teachers.id=course_teacher.teacher_id
where departments.name = "Dipartimento di Matematica";

-- 7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18 --

select count(exam_student.exam_id), students.surname, students.name, max(exam_student.vote) from students
join exam_student
on students.id=exam_student.student_id
join exams
on exams.id=exam_student.exam_id
join courses
on courses.id = exams.course_id
where exam_student.vote >= 18
group by students.id, courses.id;
