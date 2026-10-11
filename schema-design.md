Smart Clinic Management System — MySQL Schema Design

 1. Overview

The MySQL database stores information about administrators, doctors, patients, appointments, and prescriptions. Primary keys uniquely identify records, while foreign keys maintain relationships between related records.

 2. Database Tables

 2.1 Admins

Stores administrator account information.

| Column | Data Type | Constraints |
|---|---|---|
| admin_id | BIGINT | Primary key, auto-increment |
| name | VARCHAR(100) | NOT NULL |
| email | VARCHAR(150) | NOT NULL, UNIQUE |
| password_hash | VARCHAR(255) | NOT NULL |

 2.2 Doctors

Stores doctor profiles and login information.

| Column | Data Type | Constraints |
|---|---|---|
| doctor_id | BIGINT | Primary key, auto-increment |
| name | VARCHAR(100) | NOT NULL |
| email | VARCHAR(150) | NOT NULL, UNIQUE |
| password_hash | VARCHAR(255) | NOT NULL |
| speciality | VARCHAR(100) | NOT NULL |
| available_times | JSON | Stores availability information |
 2.3 Patients

Stores registered patient information.

| Column | Data Type | Constraints |
|---|---|---|
| patient_id | BIGINT | Primary key, auto-increment |
| name | VARCHAR(100) | NOT NULL |
| email | VARCHAR(150) | NOT NULL, UNIQUE |
| phone | VARCHAR(20) | UNIQUE |
| password_hash | VARCHAR(255) | NOT NULL |
| date_of_birth | DATE | NULL |

### 2.4 Appointments

Stores appointment bookings between patients and doctors.

| Column | Data Type | Constraints |
|---|---|---|
| appointment_id | BIGINT | Primary key, auto-increment |
| patient_id | BIGINT | Foreign key referencing patients |
| doctor_id | BIGINT | Foreign key referencing doctors |
| appointment_time | DATETIME | NOT NULL |
| status | VARCHAR(30) | NOT NULL |
| created_at | TIMESTAMP | Default current timestamp |

 2.5 Prescriptions

Stores prescriptions associated with appointments.

| Column | Data Type | Constraints |
|---|---|---|
| prescription_id | BIGINT | Primary key, auto-increment |
| appointment_id | BIGINT | Foreign key referencing appointments |
| doctor_id | BIGINT | Foreign key referencing doctors |
| patient_id | BIGINT | Foreign key referencing patients |
| medication | TEXT | NOT NULL |
| instructions | TEXT | NULL |
| created_at | TIMESTAMP | Default current timestamp |

 3. Relationships

- One doctor can have many appointments.
- One patient can book many appointments.
- Each appointment belongs to one doctor and one patient.
- An appointment can have one or more
