<!--
Modellizzare la struttura di un database per memorizzare tutti i dati riguardanti una università:
- sono presenti diversi Dipartimenti (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);
- ogni Dipartimento offre più Corsi di Laurea (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)
- ogni Corso di Laurea prevede diversi Corsi (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);
- ogni Corso può essere tenuto da diversi Insegnanti;
- ogni Corso prevede più appelli d'Esame;
- ogni Studente è iscritto ad un solo Corso di Laurea;
- ogni Studente può iscriversi a più appelli di Esame;
- per ogni appello d'Esame a cui lo Studente ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente.
-->

# Database University

## Entity name:
- Department
- Course
- Degree
- Teacher
- Exam
- Student

## Tables name: 
- departments
- courses
- deegres
- teachers
- exams
- students

## Relationship
- oneToMany: Departmens -> Courses / Courses -> deegres / Degree -> Exams
- manyToMany: Students -> Exams / deegres -> Teachers

## Table Columns: 


### Courses
- id| AUTO_INCREMENT, NOTNULL, PRIMARY_KEY, UNIQUE, INDEX, BIGINT
- departments_id| NOTNULL, FOREIGN_KEY, UNIQUE, INDEX, BIGINT
- name| VARCHAR(97), NOTNULL
- type| VARCHAR(48), NULL
- level| VARCHAR(10), NULL


### deegres
- id| AUTO_INCREMENT, NOTNULL, PRIMARY_KEY, UNIQUE, INDEX, BIGINT
- courses_id | NOTNULL, FOREIGN_KEY, UNIQUE, INDEX, BIGINT
- name| VARCHAR(50), NOTNULL
- credits| TINYINT, NOTNULL


### teachers
- id| AUTO_INCREMENT, NOTNULL, PRIMARY_KEY, UNIQUE, INDEX, BIGINT
- deegres_id|  NOTNULL, FOREIGN_KEY, UNIQUE, INDEX, BIGINT
- name| VARCHAR(22), NOTNULL
- lastname| VARCHAR(23), NOTNULL
- email| VARCHAR(40), NULL
- phone_number| CHAR(10) NULL
- note| TEXT, NULL


### exam
- id| AUTO_INCREMENT, NOTNULL, PRIMARY_KEY, UNIQUE, INDEX, BIGINT
- degree| NOTNULL, FOREIGN_KEY, INDEX, BIGINT
- student_id| NOTNULL, FOREIGN_KEY, INDEX, BIGINT
- date| DATETIME
- outcome| VARCHAR(10), NOTNULL
- vote| TINYINT, NOTNULL


### students
- id| AUTO_INCREMENT, NOTNULL, PRIMARY_KEY, UNIQUE, INDEX, BIGINT
- badge_number: VARCHAR(10), NOTNULL
- name| VARCHAR(22), NOTNULL
- lastname| VARCHAR(23), NOTNULL
- email| VARCHAR(40), NULL
- phone_number| CHAR(10) NULL


### vote table pivot
- exam_id| FOREIGN KEY, NULL
- student_id | NOTNULL, FOREIGN_KEY, INDEX, BIGINT