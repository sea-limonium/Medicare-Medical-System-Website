# MediCare - Medical Appointment & Information System

A client-side web application for a doctor's surgery that enables patients to book appointments, doctors to manage consultations and prescriptions, and administrators to handle user management; all built with vanilla HTML, CSS, and JavaScript using IndexedDB for persistent storage and CryptoJS for password encryption.

## Overview

MediCare is a role-based medical system with three distinct portals, each with its own permissions and functionality. The app runs entirely in the browser with no backend server required; data is fetched from hosted JSON endpoints on first load and stored locally in IndexedDB, simulating a full-stack medical records system.

**Patient Portal**: Book appointments with specific doctors, view upcoming appointments, view personal profile information, and access prescribed treatments and medical notes.

**Doctor Portal**: View daily appointments, search patients by name or NHS number, review full patient history (medical notes, treatments, prescriptions), add consultation notes (Chief Complaint, Diagnosis, Assessment), and prescribe medicines.

**Admin Portal**: Full CRUD management of all user accounts (patients, doctors, admins) including adding, updating, and deleting records with fields like name, address, telephone, DOB, and NHS number.

## Features

- **IndexedDB Database**: 7 object stores (patients, doctors, admin, medicines, appointments, treatments, medical_notes) with indexed fields for efficient querying
- **Role-Based Access Control**: Authentication is role-specific; patients cannot access doctor/admin portals and vice versa, enforced via session state
- **Password Encryption**: Passwords are encrypted with AES (CryptoJS) before storage and decrypted only during authentication — never stored in plain text
- **External Data Loading**: Initial data (doctors, patients, admin, medicines) fetched from hosted JSON endpoints and processed into IndexedDB on first run
- **Input Validation**: Email format validation, password strength enforcement, and input sanitisation across all forms
- **GDPR Considerations**: Data minimisation, transparent processing, role-based data segregation, and encrypted credential storage
- **Offline Capable**: Runs entirely client-side with locally cached assets (PWA-style)

## Project Structure

```
MediCare/
├── main/                   # Landing page, login, shared layouts
├── patient/                # Patient portal pages (appointments, profile, treatments)
├── doctor/                 # Doctor portal pages (patient search, notes, prescriptions)
├── admin/                  # Admin portal pages (user management, CRUD operations)
├── js/
│   └── dbmanager.js        # Core logic — IndexedDB init, CRUD ops, auth, encryption
├── images/                 # UI assets
└── css/                    # Stylesheets (if separate from HTML)
```

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | HTML, CSS, JavaScript |
| Database | IndexedDB (client-side, via `dbmanager.js`) |
| Encryption | CryptoJS (AES-256) |
| Data Source | External JSON endpoints (doctors, patients, admin, medicines) |

### Installation & Setup

No dependencies, no build step — just a browser.

1. Clone the repository or download and unzip the project folder.

```bash
git clone https://github.com/sea-limonium/medicare-medical-system-website.git
cd medicare-medical-system-website
```

2. Open `main/index.html` in your web browser.

> The app fetches initial data from external JSON endpoints on first load, so an internet connection is needed for the initial setup. After that, it works offline.

## Data Sources

On first launch, the app pulls seed data from these hosted JSON files and populates IndexedDB:

- `https://jsethi-mdx.github.io/cst2572.github.io/doctors.json`
- `https://jsethi-mdx.github.io/cst2572.github.io/patients.json`
- `https://jsethi-mdx.github.io/cst2572.github.io/admin.json`
- `https://jsethi-mdx.github.io/cst2572.github.io/medicines.json`

## Database Schema

| Object Store | Key Path | Key Indexes | Purpose |
|-------------|----------|-------------|---------|
| `patients` | id | NHS, Email, First, Last | Patient demographics and login |
| `doctors` | id | Email, first_name, last_name | Doctor information and login |
| `admin` | id | Email, first_name, last_name | Administrator accounts |
| `medicines` | id | Drug | Available medications for prescriptions |
| `appointments` | id | Patient_ID, Doctor_ID, Date, Status | Scheduled appointments |
| `treatments` | id | Patient_ID, Doctor_ID, Medicine_ID | Prescription records |
| `medical_notes` | id | Patient_ID, Doctor_ID, Date | Consultation notes (complaint, diagnosis, assessment) |

---

Built as a group coursework project for CST2572 - Secure Web Technologies at Middlesex University Dubai (Spring 2025).
