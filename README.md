# Common-Table-Expressions-CTEs-


WITH student_grades AS (
  SELECT student_id, course_id, grade
  FROM students
  JOIN enrollments ON students.student_id = enrollments.student_id
  JOIN grades ON enrollments.enrollment_id = grades.enrollment_id
)

SELECT student_name, average_grade
FROM student_grades
JOIN students ON student_grades.student_id = students.student_id
GROUP BY student_name;


SELECT student_name, grade, rank() OVER (PARTITION BY student_id ORDER BY grade DESC) AS student_rank
FROM students
JOIN enrollments ON students.student_id = enrollments.student_id
JOIN grades ON enrollments.enrollment_id = grades.enrollment_id;

SELECT student_name, JSON_VALUE(student_data, '$.email') AS email
FROM students;

SELECT student_name, enrollment_date
FROM students
JOIN enrollments ON students.student_id = enrollments.student_id
WHERE enrollment_date BETWEEN '2022-01-01' AND '2022-12-31';
