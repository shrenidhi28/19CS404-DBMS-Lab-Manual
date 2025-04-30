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

# ER Diagram Submission - Shrenidhi.C

## Scenario Chosen:
University

## ER Diagram:
<img width="944" alt="image" src="https://github.com/user-attachments/assets/6eb2a604-5304-4b26-a6da-69cc49be27a0" />


## Entities and Attributes:
- Program: program_no,program name
- Department: dept_id,dept_name
- students: add_no,full_name,mobile no,dob
- course: course_id,course_name
- teacher: teacher_id,teacher name
...

## Relationships and Constraints:
-has (program–students) (1:N, Total–Partial)
-has (department–program) (1:N, Partial–Total)
-enrolls (students–courses) (M:N, Partial–Partial)
-taught by (courses–teacher) (N:1, Total–Partial)

## Extension (Prerequisite / Billing):
1. Prerequisites are modeled using a recursive relationship on the `course` entity.  
2. The relationship is named prerequisite, connecting a course to its required course(s).  
3. It has M:N cardinality since one course can have multiple prerequisites and vice versa.  
4. Billing is modeled by adding a new entity called billing.  
5. A student is connected to billing via a 1:N relationship (`student` to `billing`).  
6. The `billing` entity stores attributes like amount, due date, and status.

## Design Choices:
Brief explanation of why you chose certain entities, relationships, and assumptions:

```

Entities like student, course, program, department, and teacher represent core real-world objects in an academic system.

Relationships such as enrolls, has, and taught by reflect key interactions (e.g., students enroll in courses, teachers teach them).

A recursive relationship for prerequisite allows modeling course dependencies naturally.

A separate billing entity captures financial data without overloading the student entity.

Cardinalities and participation were assumed based on typical university rules (e.g., every course must have a teacher).

These design choices aim for clarity, normalization, and scalability in a real-world database.

```

## RESULT

Therfore the ER diagram is created and implemented.
