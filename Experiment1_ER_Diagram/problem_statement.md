# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

**Business Context:**  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

**Requirements:**  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:
<img width="1266" height="518" alt="image" src="https://github.com/user-attachments/assets/d3360a82-0fa1-44d6-83a5-9ac92e959f7a" />



### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
| Member | Member_ID (PK), Name, Membership_Type, Start_Date|Tracks all gym members|
|Program |Program_ID (PK), Program_Name, Type|Yoga, Zumba, Weight Training|
|Trainer |Trainer_ID (PK), Name, Specialization|A trainer may take multiple programs|
|Session |Session_ID (PK), Member_ID (FK), Trainer_ID (FK), Date, Time|For personal training sessions|
|Attendance|Attendance_ID (PK), Session_ID (FK), Status (Present/Absent)|Records session attendance|

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
|Member–Program (Joins)|M:N|Partial|A member can join many programs|
|Program–Trainer (Assigned)|M:N|Total|Programs can have multiple trainers|
|Session–Attendance|1:M|Partial|Each session must have attendance record|


### Assumptions
- Membership type determines allowed programs but not restricted in ER model.
- Personal training sessions are optional.
- Payments cover both membership fees and session fees.

---

# Scenario B: City Library Event & Book Lending System

**Business Context:**  
The Central Library wants to manage book lending and cultural events.

**Requirements:**  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:
<img width="775" height="479" alt="image" src="https://github.com/user-attachments/assets/0e1a5155-452f-4507-98d1-d2186d2e22e2" />


### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
|Member|Member_ID (PK), Name, Email, Phone|Library members|
|Book|Book_ID (PK), Title, Author, Category|Each book has category (Fiction, etc.)|
|Loan|Loan_ID (PK), Book_ID (FK), Member_ID (FK), Loan_Date, Return_Date|Tracks borrowing details|
|Event|Event_ID (PK), Title, Date, Time|Cultural events organized by library|
|Speaker|Speaker_ID (PK), Name, Expertise|Authors or guest speakers|  
### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
|Member–Loan (Borrows)|1:M|Total|Each member can borrow many books|
|Book–Loan|1:M|Total|A book can appear in many loan records|
|Member–Event (Registers)|M:N|Partial|Members can register for events|
|Event–Speaker|M:N|Total|Each event must have at least one speaker|

### Assumptions
- Each event must take place in one room.

- Multiple speakers can be assigned to one event.

- Fine is applied only if return date > due date.

---

# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:
<img width="1009" height="603" alt="image" src="https://github.com/user-attachments/assets/08929740-8551-46a1-a958-06f0d74551b3" />


### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
|CHEF        | Chef_id (PK), Chef_name, Chef_salary                   | Each chef is uniquely identified by Chef_id. Prepares meals.      |
|MEAL        | meal_name (PK), meal_price                   | A meal is prepared by chefs, ordered by customers, and consists of ingredients.      |
| INGREDIENTS       | ing_name (PK), description                   |  Each ingredient has a unique name and is linked to meals.     |
| CUSTOMERS       | cust_phone (PK), cust_name, cust_address                   |  Customers place orders for meals.     |
| SUPPLIER       |  S_id (PK), S_name, S_city                  | Suppliers attend to customers.      |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
|prepares (CHEF–MEAL)              | 1:N           | CHEF (total), MEAL (partial)|One chef can prepare many meals, but a meal is prepared by one chef.|
| orders (CUSTOMERS–MEAL)             | M:N           | Both partial| A customer can order many meals, and a meal can be ordered by many customers|
|  consists of (MEAL–INGREDIENTS)| M:N | Both total|Each meal consists of multiple ingredients, and each ingredient can be part of many meals.       |
| attends (SUPPLIER–CUSTOMERS)          |M:N   |Both partial|A supplier can attend to many customers, and a customer can be attended by many suppliers.
### Assumptions
- Each chef can prepare multiple meals, but a meal is prepared by only one chef.
- A customer can place multiple orders, and each order may include one or more meals. 
- Each meal consists of one or more ingredients, and an ingredient may be used in multiple meals.

---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
