#  대학교 학생 인적사항 SQL

## Students
```sql
CREATE TABLE Students (
  stdent_id INT PRIMARY KEY,
  name VARCHAR(100),
  birth_date DATE,
  gender VARCHAR(10),
  department_id INT,
  email VARCHAR(100),
  phone VARCHAR(100),
  address VARCHAR(255),
  FOREIGN KEY (department_id) REFERENCES Departments(department_id)
)
```

## Courses
```sql
CREATE TABLE Courses (
  course_id INT PRIMARY KEY,
  name VARCHAR(100),
  credits INT,
  department_id INT,
  FOREIGH KEY (department_id) REFERENCES Department(department_id)
)
```

## Enrollments
```sql
CREATE TABLE Enrollments (
  enrollments_id INT PRIMARY KEY,
  student_id INT,
  course_id INT,
  semester VARCHAR(20),
  year INT,
  grade CHAR(2),
  FOREIGN KEY (student_id) REFERENCES Students(studnet_id),
  FOREIGH KEY (student_id) REFERENCES Courses(courses_id)
)
```

## Departments
```sql
CREATE TABLE Departments (
  department_id INT PRIMARY KEY,
  name VARCHAR(100),
  head VARCHAR(100)
)
```

## Instructors
```sql
CREATE TABLE Instructors (
  instructor_id INT PRIMARY KEY,
  name VARCHAR(100),
  department_id INT,
  email VARCHAR(100),
  phone VARCHAR(20),
  office_address VARCHAR(255),
  FOREIGH KEY (department_id) REFERENCES Departments(department_id)
)
```













