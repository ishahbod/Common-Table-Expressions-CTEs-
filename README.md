# Common-Table-Expressions-CTEs-
This query first defines a CTE named student_grades. The CTE is a subquery that selects the student ID, course ID, and grade from the students, enrollments, and grades tables. The CTE is then used in the main query to calculate the average grade for each student

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


This query calculates the student rank for each student. The student rank is calculated by partitioning the results by student ID and then ordering the results by grade in descending order. The rank() function is then used to calculate the rank for each student

SELECT student_name, grade, rank() OVER (PARTITION BY student_id ORDER BY grade DESC) AS student_rank
FROM students
JOIN enrollments ON students.student_id = enrollments.student_id
JOIN grades ON enrollments.enrollment_id = grades.enrollment_id;
