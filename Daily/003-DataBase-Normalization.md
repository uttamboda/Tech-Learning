# Today i have learning about Database Normalization :

---
## First Normal Form (1NF) :
**Points:**
* Each column must contain atomic (single) values.
* No repeating groups or multi-valued attributes are allowed.

**Example:**

| StudentID | PhoneNumbers |
|-----------|--------------|
| 1         | 9876,1234    |


 Not in 1NF → phone numbers are not atomic

----

## Second Normal Form (2NF)
**Points:**
* Table must be in 1NF.
* No partial dependency on a composite primary key.

**Example1:**
Primary Key: (StudentID, CourseID)

| StudentID | CourseID | StudentName |
|-----------|----------|-------------|

 Not in 2NF → StudentName depends only on StudentID

**Example2:**

**Table: Student_Course**  
**Primary Key:** (StudentID, CourseID)

| StudentID | CourseID | StudentName | CourseFee |
|----------|----------|-------------|-----------|
| 1        | C1       | Rahul       | 5000      |
| 1        | C2       | Rahul       | 6000      |
| 2        | C1       | Amit        | 5000      |

**Functional Dependencies:**
* StudentID → StudentName
* CourseID → CourseFee

**Problem:**
* StudentName depends only on StudentID.
* CourseFee depends only on CourseID.
* This is called partial dependency, so the table is not in 2NF.

**Solution (Convert to 2NF) :**

**Student Table**

| StudentID | StudentName |
|----------|-------------|
| 1        | Rahul       |
| 2        | Amit        |

**Course Table**

| CourseID | CourseFee |
|----------|-----------|
| C1       | 5000      |
| C2       | 6000      |

**Enrollment Table**

| StudentID | CourseID |
|----------|----------|

**Result:**
* All non-prime attributes now depend on the whole primary key.
* The database is now in Second Normal Form (2NF).


---


## Third Normal Form (3NF)
**Points:**
* Table must be in 2NF.
* No transitive dependency is allowed.

**Example:**

| EmpID | DeptID | DeptName |
|------|--------|----------|

 Not in 3NF → DeptName depends on DeptID, not directly on EmpID

**Example (Table NOT in 3NF)** 

**Table: Employee**  
**Primary Key:** EmpID

| EmpID | EmpName | DeptID | DeptName | DeptLocation |
|------|---------|--------|----------|--------------|
| 101  | Rahul   | D1     | HR       | Delhi        |
| 102  | Amit    | D2     | IT       | Mumbai       |
| 103  | Neha    | D1     | HR       | Delhi        |

**Functional Dependencies:**
* EmpID → EmpName
* EmpID → DeptID
* DeptID → DeptName
* DeptID → DeptLocation

**Problem:**
* DeptName and DeptLocation depend on DeptID.
* DeptID depends on EmpID.
* This creates a transitive dependency.
* Therefore, the table is not in 3NF.

---

### Solution (Convert to 3NF)

**Employee Table**

| EmpID | EmpName | DeptID |
|------|---------|--------|
| 101  | Rahul   | D1     |
| 102  | Amit    | D2     |
| 103  | Neha    | D1     |

**Department Table**

| DeptID | DeptName | DeptLocation |
|--------|----------|--------------|
| D1     | HR       | Delhi        |
| D2     | IT       | Mumbai       |


**Result:**
* Transitive dependency is removed.
* All non-key attributes depend only on the primary key.
* The database is now in Third Normal Form (3NF).
---


## Boyce–Codd Normal Form (BCNF)
**Points:**
* Table must be in 3NF.
* For every functional dependency (X → Y), X must be a superkey.

**Example (Table NOT in BCNF):**

| EmpID | Dept | Manager |
|------|------|---------|
| 1    | IT   | Rahul   |
| 2    | IT   | Rahul   |
| 3    | HR   | Neha    |

**Functional Dependencies:**
* EmpID → Dept, Manager
* Dept → Manager

**Problem:**
* Dept determines Manager.
* Dept is not a superkey.
* This violates BCNF.

### Solution (Convert to BCNF)

**Department Table**

| Dept | Manager |
|------|---------|

**Employee Table**

| EmpID | Dept |
|------|------|

**Result:**
* Every determinant is now a superkey.
* The table is in BCNF.

----

## Fourth Normal Form (4NF)
**Points:**
* Table must be in BCNF.
* No multi-valued dependency is allowed.

**Example (Table NOT in 4NF):**

| Student | Skill  | Hobby  |
|---------|--------|--------|
| Rahul   | Java   | Music  |
| Rahul   | Python | Music  |
| Rahul   | Java   | Sports |

**Problem:**
* A student can have multiple skills and multiple hobbies.
* Skills and hobbies are independent of each other.
* This causes redundancy.


### Solution (Convert to 4NF)

**Student_Skill Table**

| Student | Skill  |
|---------|--------|
| Rahul   | Java   |
| Rahul   | Python |

**Student_Hobby Table**

| Student | Hobby  |
|---------|--------|
| Rahul   | Music  |
| Rahul   | Sports |

**Result:**
* Multi-valued dependency is removed.
* The table is in 4NF.

---

## Fifth Normal Form (5NF)
**Points:**
* Table must be in 4NF.
* No join dependency should exist except those implied by candidate keys.

**Example (Conceptual):**

| Supplier | Product | Project |
|----------|---------|---------|

**Problem:**
* Data can be reconstructed only by joining multiple tables.
* Redundancy appears due to complex join dependencies.



### Solution (Convert to 5NF)

**Supplier_Product Table**  
**Supplier_Project Table**  
**Product_Project Table**

**Result:**
* Data cannot be further decomposed without losing information.
* The table is in 5NF.

---

## Summary of Normal Forms

* **1NF:** Atomic values only
* **2NF:** No partial dependency
* **3NF:** No transitive dependency
* **BCNF:** Every determinant is a superkey
* **4NF:** No multi-valued dependency
* **5NF:** No join dependency