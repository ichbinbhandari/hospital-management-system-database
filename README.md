# 🏥 Hospital Management System — Database Design Project

A relational database design project developed as part of the coursework at **TH Aschaffenburg – University of Applied Sciences**. This project demonstrates end-to-end database engineering: from requirements gathering through user stories, to ER modelling, normalization, and SQL implementation.

---

## 👥 Authors

| Name | Role |
|---|---|
| Krishna Raj Bhandari | Doctor User Stories & SQL Queries |
| Suraj Bhatta | Patient User Stories & SQL Queries |
| Vinayak Talawar | Pharmacist User Stories & SQL Queries |
| Anirudh Aggarwal | Nurse User Stories & SQL Queries |
| Vojislav Andelic | Admin User Stories & SQL Queries |

---

## 📌 Project Overview

The Hospital Management System is a normalized relational database solution designed to streamline the operations of a healthcare facility. It manages core hospital entities — **doctors, patients, appointments, diagnoses, prescriptions, medicines, and billing** — through a clean, well-structured schema.

### Key Features
- Centralized data management for all hospital operations
- Appointment scheduling and status tracking
- Full patient medical history: diagnoses, symptoms, and prescriptions
- Medicine inventory management with batch and expiry tracking
- Automated billing with itemized medicine records
- Role-based query support for doctors, patients, nurses, pharmacists, and admins

---

## 📁 Repository Structure

```
hospital-management-system/
│
├── README.md
│
├── docs/
│   ├── user_stories.md          # 25 user stories across 5 roles
│   ├── er_diagram.png           # Entity-Relationship Diagram
│   └── relational_schema.md     # Final normalized relational schema
│
├── sql/
│   ├── schema.sql               # CREATE TABLE statements (DDL)
│   ├── sample_data.sql          # INSERT statements with sample data
│   └── queries.sql              # All 25 user story SQL query implementations
│
└── report/
    └── Project_Report_Hospital_Management_System.pdf
```

---

## 🗂️ Database Schema

The schema is fully normalized to **Boyce-Codd Normal Form (BCNF)** and consists of **12 tables**:

| Table | Description |
|---|---|
| `Doctor` | Healthcare professional details |
| `Doctor_Specialization` | Multi-valued specializations per doctor |
| `Patient` | Patient demographics and medical info |
| `Appointment` | Links doctors and patients with scheduling details |
| `Diagnosis` | Medical findings linked to an appointment |
| `Diagnosis_Symptom` | Individual symptoms per diagnosis |
| `Medicine` | Medicine inventory with pricing and stock |
| `Medicine_Ingredient` | Ingredients per medicine |
| `Medicine_Batch` | Batch-level expiry and quantity tracking |
| `Prescribe` | Medicines prescribed per appointment |
| `Bill` | Patient billing records |
| `Bill_Medicine` | Medicines included in each bill |

---

## 🔄 Normalization Summary

| Normal Form | Status | Key Action |
|---|---|---|
| 1NF | ✅ Achieved | Extracted multi-valued attributes (symptoms, ingredients, specializations) into junction tables |
| 2NF | ✅ Achieved | Redesigned `Prescribe` from `(doctor_id, medicine_id)` to `(appointment_id, medicine_id)` to remove partial dependencies |
| 3NF | ✅ Achieved | Eliminated all transitive dependencies |
| BCNF | ✅ Achieved | Every determinant is a candidate key |

---

## 👤 User Stories

25 user stories were defined across 5 stakeholder roles:

- **Doctor** (5 stories) — appointment preparation, diagnosis history, workload analysis
- **Patient** (5 stories) — appointment overview, treatment details, billing
- **Pharmacist** (5 stories) — prescription dispensing, inventory, expiry management
- **Nurse** (5 stories) — daily appointment flow, patient care summaries
- **Admin** (5 stories) — system-wide reporting, revenue analysis, user management

Each story is implemented as a SQL query using joins, aggregations, subqueries, and date functions.

---

## 🛠️ Technologies Used

- **SQL** (MySQL-compatible syntax)
- **ER Modelling** (Chen notation)
- **Relational Schema Design & Normalization**

---

## 🚀 How to Run

1. Clone this repository:
   ```bash
   git clone https://github.com/<your-username>/hospital-management-system.git
   ```

2. Open your MySQL client (MySQL Workbench, DBeaver, or CLI).

3. Create a new database and select it:
   ```sql
   CREATE DATABASE hospital_db;
   USE hospital_db;
   ```

4. Run the schema file to create all tables:
   ```sql
   SOURCE sql/schema.sql;
   ```

5. Load the sample data:
   ```sql
   SOURCE sql/sample_data.sql;
   ```

6. Run any of the user story queries:
   ```sql
   SOURCE sql/queries.sql;
   ```

---

## 📊 Sample Queries

**Doctor — Upcoming appointments:**
```sql
SELECT a.appointment_id, a.date_time, a.purpose, p.name AS patient_name
FROM Appointment a
JOIN Patient p ON a.patient_id = p.patient_id
WHERE a.doctor_id = 1 AND a.date_time > NOW()
ORDER BY a.date_time;
```

**Admin — Monthly revenue:**
```sql
SELECT YEAR(billing_date) AS year, MONTH(billing_date) AS month, SUM(price) AS total_revenue
FROM Bill
GROUP BY YEAR(billing_date), MONTH(billing_date)
ORDER BY year, month;
```

---

## 📄 License

This project was developed for academic purposes at TH Aschaffenburg. Feel free to reference or adapt it with appropriate attribution.
