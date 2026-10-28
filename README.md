[README.md](https://github.com/user-attachments/files/34069035/README.md)
# University Management System: ERD & Relational Mapping

A database design project that models a centralized **University Management System**. It covers the Entity-Relationship Diagram (ERD), the mapping of the ERD to relational schemas, and a presentation of the design.

![Final ERD](images/erd.png)

## Table of Contents
- [Project Overview](#project-overview)
- [Business Requirements](#business-requirements)
- [Entities and Attributes](#entities-and-attributes)
- [Relationships](#relationships)
- [ERD to Relational Mapping](#erd-to-relational-mapping)
- [Repository Structure](#repository-structure)
- [How to View or Edit the ERD](#how-to-view-or-edit-the-erd)
- [Team](#team)

## Project Overview
The university needs one system to manage:
- Students
- Professors
- Courses and enrollment
- Departments
- Student clubs
- Books and borrowing
- Projects and collaboration

This project covers the **conceptual design (ERD)** and the **logical design (relational mapping)** of that system.

**Tools used:** draw.io (diagrams.net) for the ERD, Microsoft Word for the mapping document, PowerPoint for the presentation.

## Business Requirements
- Every main entity (Student, Professor, Course, Department, Book, Club, Project) has a unique ID.
- Students can enroll in multiple courses.
- Each professor belongs to one department and may supervise or advise students.
- Students may join clubs (optional).
- Students can borrow books from the library.
- Projects require collaboration among students, professors, and departments.
- A student has a multi-valued attribute: phone numbers.

## Entities and Attributes

| Entity | Attributes | Notes |
|---|---|---|
| **Student** | **Student ID**, Student Name, Email, Date of Birth, Phone Number, University ID (Card Number, Issue Date) | Phone is multi-valued. Age is derived from Date of Birth. University ID is composite. |
| **Professor** | **Prof. ID**, Prof. Name | |
| **Department** | **Dep. ID**, Dep. Name | |
| **Course** | **Course ID**, Course Name | |
| **Book** | **Book ID**, Book Title, Author, Library | |
| **Club** | **Club ID**, Club Name | |
| **Project** | **Project ID**, Project Name | Weak entity in the ERD. |
| **Academic Advisor** | **ID**, Name | Weak entity in the ERD, identified through the Advice relationship. |

Bold attributes are primary keys.

## Relationships

| Relationship | Entities | Cardinality | Notes |
|---|---|---|---|
| Enroll | Student, Course | M:N | Has the attribute **Grades** (and Semester in the mapping). |
| Borrow | Student, Book | 1:N | A student can borrow many books. |
| Join | Student, Club | M:N | Optional. A club may have zero members. |
| Collaboration | Student, Professor, Department, Project | Ternary or higher | Links students, professors and departments to a project. |
| Assigned | Professor, Department | N:1 | A professor is assigned to one department. |
| Supervise | Professor, Department | 1:1 | Each department is supervised by one professor. |
| Responsible | Professor, Course | N:M | Professors are responsible for courses. |
| Advice | Professor, Academic Advisor | 1:1 | Identifying relationship. |

## ERD to Relational Mapping

PK = Primary Key, FK = Foreign Key. The same mapping is in [`docs/ERD_Mapping.docx`](docs/ERD_Mapping.docx).

| Table | Columns |
|---|---|
| **Student** | Student ID (PK), Student name, Date of Birth, Email, University ID number, University ID Issue date |
| **Student phone** | Student ID (FK), Phone number |
| **Graduation project** | Student ID (FK), Grad project ID (PK), Grad project name, Department ID (FK) |
| **Course** | Course ID (PK), Course name |
| **Club** | Club ID (PK), Club name |
| **Library** | Library ID (PK), Library name |
| **Book** | Book ID (PK), Book author, Book title, Library ID (FK) |
| **Professor** | Professor ID (PK), Professor name, Department ID (FK), Grad project ID (FK) |
| **Academic advisor** | Professor ID (FK), Advisor ID (PK), Advisor name |
| **Department** | Department ID (PK), Department name, Supervisor prof. ID (FK) |
| **Research Project** | Project ID (PK), Project name |
| **Join club** | Student ID (FK), Club ID (FK) |
| **Course enroll** | Student ID (FK), Course ID (FK), Grades, Semester |
| **Course responsible** | Course ID (FK), Professor ID (FK) |
| **Borrow** | Student ID (FK), Book ID (FK), Library ID (FK), Borrowing details |
| **Collaboration** | Student ID (FK), Project ID (FK), Professor ID (FK), Department ID (FK) |

### Mapping rules applied
- **Multi-valued attribute** (Student phone) becomes its own table with a foreign key to Student.
- **M:N relationships** (Enroll, Join, Responsible) become junction tables.
- **1:N relationships** are mapped by placing the FK on the "many" side.
- **Composite attribute** (University ID) is flattened into simple columns.
- **Derived attribute** (Age) is not stored. It is computed from Date of Birth.
- **Weak entities** take the key of their owner entity as part of their key.

## Repository Structure
```
university-management-erd/
├── README.md
├── images/
│   └── erd.png                  # Screenshot of the final ERD
├── diagrams/
│   └── Final_ERD_project.drawio # Editable source file
├── docs/
│   └── ERD_Mapping.docx         # Relational mapping document
└── presentation/
    ├── Presentation.pptx        # Project slides
    └── Presentation.pdf         # PDF version (viewable on GitHub)
```

## How to View or Edit the ERD
1. Go to [app.diagrams.net](https://app.diagrams.net).
2. Choose **Open Existing Diagram** and select `diagrams/Final_ERD_project.drawio`.
3. Edit it and export as PNG or PDF if needed.

You can also open the `.drawio` file directly with the draw.io extension in VS Code.

## Team
- Mahmoud Khaled
- Ashraf Mohamed
- Abdel Rahman Mohamed
- Mohamed AbdEl-Nasser
