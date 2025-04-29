# Experiment 1: Entity-Relationship (ER) Diagram

## 🎯 Objective:
To understand and apply the concepts of ER modeling by creating an ER diagram for a real-world application.

## 📚 Purpose:
The purpose of this workshop is to gain hands-on experience in designing ER diagrams that visually represent the structure of a database including entities, relationships, attributes, and constraints.

---

## 🧪 Choose One Scenario:

### 🔹 Scenario 1: University Database
Design a database to manage students, instructors, programs, courses, and student enrollments. Include prerequisites for courses.

**User Requirements:**
- Academic programs grouped under departments.
- Students have admission number, name, DOB, contact info.
- Instructors with staff number, contact info, etc.
- Courses have number, name, credits.
- Track course enrollments by students and enrollment date.
- Add support for prerequisites (some courses require others).

---

### 🔹 Scenario 2: Hospital Database
Design a database for patient management, appointments, medical records, and billing.

**User Requirements:**
- Patient details including contact and insurance.
- Doctors and their departments, contact info, specialization.
- Appointments with reason, time, patient-doctor link.
- Medical records with treatments, diagnosis, test results.
- Billing and payment details for each appointment.

---

## 📝 Tasks:
1. Identify entities, relationships, and attributes.
2. Draw the ER diagram using any tool (draw.io, dbdiagram.io, hand-drawn and scanned).
3. Include:
   - Cardinality & participation constraints
   - Prerequisites for University OR Billing for Hospital
4. Explain:
   - Why you chose the entities and relationships.
   - How you modeled prerequisites or billing.

# ER Diagram Submission - Shrenidhi C

## Scenario Chosen:
University

## ER Diagram:
<img width="869" alt="image" src="https://github.com/user-attachments/assets/a07256d1-5498-4b44-85d3-0495d6ce7b70" />


## Entities and Attributes:
- Program: program_no,program name
- Department: dept_id , dept_name
- Students: addno,fullname,mobile_no,dob
- courses: course_id, course_name
- teacher: teacher_id,teacher_name


## Relationships and Constraints:
-has (Program–Student) (One-to-Many, Total Participation on Student side)

-has (Program–Department) (Many-to-One, Total Participation on Program side)

-enrolls (Student–Course) (Many-to-Many, Partial Participation on both sides)

-taught by (Course–Teacher) (Many-to-One, Total Participation on Course side)

## Extension (Prerequisite / Billing):
- Students, Programs, and Courses:
   Students belong to a program.
   Programs belong to a department.
   Students enroll in courses.
   Courses are taught by teachers.
-Entities and Attributes:
Student: admission number, full name, mobile number, date of birth.
Program: program number, name.
Department: department ID, name.
Course: course ID, name.
Teacher: teacher ID, name.

## Design Choices:
```

Student 
Central to the academic system—represents individuals enrolled in programs and courses.
Attributes: admission no, full name, mobile no, dob to uniquely identify and describe each student.

Program
Represents a structured collection of courses that students enroll in (e.g., BSc CS, BBA).
Attributes like program no, program name distinguish each program.

Department
Logical grouping of programs and staff (e.g., Department of Science).
Attributes: dept id, dept name.

Course
Core academic content that students enroll in.
Attributes: course id, course name.

Teacher
Responsible for teaching courses.
Attributes like teacher id, teacher name identify and describe them.

```

## RESULT

The experiment resulted in a structured ER model capturing relationships between students, programs, departments, courses, and teachers; therefore, it provides a clear foundation for building an academic management database.
