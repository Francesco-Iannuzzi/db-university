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

# DAY 1 (create a diagram Database)

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
- oneToMany: Departmens -> Courses / Courses -> Deegres / Degree -> Exams
- manyToMany: Students -> Exams / Deegres -> Teachers

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

<!-- 

DAY 2

Dopo aver creato un nuovo database nel vostro phpMyAdmin e aver importato lo schema allegato, eseguite le query del file allegato.

Cosa consegnare?
Dopo aver testato le vostre query con phpMyAdmin, riportatele in un file .md e caricatelo nella vostra repo.

NOTA:
- importate il database usando il file che vi ho passato qui sotto esattamente cosí come é.
- NON decomprimete il file prima di importarlo.

STEPS:
- Avvia MAMP
- Vai alla pagine di PHPMYADMIN visitando la webstart page di mamp > tools > phpmyadmin
- Nella sidebar di PHPMYADMIN clicca su new per creare un nuovo database, dagli il nome e clicca su create
- Clicca sulla sidebar sul nome del db appena creato
- nel menu in alto cerca la voce import
- clicca su choose file e seleziona il file db_university.sql.gz
- clicca su go in fondo alla pagina

-->

# DAY 2 (exercise query database)

## Request:

- 1 Selezionare tutti gli studenti nati nel 1990 (160)

SELECT *
FROM `students`
WHERE `date_of_birth`
LIKE '1990-%';


- 2 Selezionare tutti i corsi che valgono più di 10 crediti (479)

SELECT *
FROM `courses`
WHERE `cfu` > 10;


- 3 Selezionare tutti gli studenti che hanno più di 30 anni

SELECT *
FROM `students`
WHERE DATEDIFF(CURDATE(), `date_of_birth`) > 30*365;


- 4 Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)

SELECT *
FROM `courses`
WHERE `period` = 'I semestre' AND `year` = 1;


- 5 Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)

SELECT *
FROM `exams`
WHERE `hour` > '14:%' AND `date` = '2020-06-20';


- 6 Selezionare tutti i corsi di laurea magistrale(38)

SELECT *
FROM `degrees`
WHERE `level` = 'magistrale';


- 7 Da quanti dipartimenti è composta l'università? (12)

SELECT COUNT(id)
FROM `departments`;


- 8 Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

SELECT COUNT(id)
FROM `teachers`
WHERE `phone` is NULL;