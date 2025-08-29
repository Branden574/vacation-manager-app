# 📱 Vacation Manager (Android)

## Author
- **Name:** Branden Vincent
- **Student ID:** 011601357

---

## 📌 Overview
Vacation Manager is an Android application that allows users to plan vacations, manage associated excursions, and generate reports.  
This project is the **Capstone (D424) upgrade** of the earlier **D308 Mobile App Development** submission.

> **Capstone highlights:** Migrated repo, hardened architecture (MVVM + Repository + Room), fixed threading issues, implemented secure login/session, improved reporting and search UX, and cleaned up DAOs/packages for maintainability.

---

## 🚀 Key Changes (Capstone vs. earlier D308 version)

- **Repository Migration**
  - Project moved to: https://github.com/Branden574/vacation-manager/releases/tag/v1.0.1
  - Work completed on branch: **`app`** (working feature branch also available).

- **Architecture & Threading**
  - Centralized `Repository` mediates between ViewModels and Room DAOs.
  - Writes use `ExecutorService` off the main thread.
  - Queries exposed via **LiveData** → reactive UI.

- **DAO & Package Cleanup**
  - Lowercase `dao/` and `database/` packages.
  - Removed duplicate/misnamed files (`* 2.java`).
  - `VacationDatabaseBuilder` returns consistent DAO references.

- **Authentication & Security**
  - Hashed password storage (SHA-256).
  - `SessionManager` persists user session across restarts.
  - Login, Create Account, Logout, and Splash routing flows.
  - Support for **EncryptedSharedPreferences** (optional).

- **Reporting**
  - Report shows **title + timestamp**, multi-row vacation + excursion details.
  - Built off main thread for performance.

- **Search & UX**
  - `SearchView` filters vacations in real-time.
  - **Empty states**, **SwipeRefresh**, **DatePickers**, and guarded deletes for vacations with excursions.

- **Excursion/Vacation Flow Fixes**
  - Excursion linked with correct vacation ID.
  - Date validation ensures excursions fall inside vacation window.

- **Build & Release**
  - Debug and release APK generation tested and documented.

---

## 🎯 Rubric B Mapping

- **B1 – OOP Principles**
  - Inheritance: Activities extend `AppCompatActivity`; ViewModels extend `AndroidViewModel`.
  - Polymorphism: Adapter `bind/notify` overrides; listener interfaces.
  - Encapsulation: Entities use private fields + getters/setters; DAOs hidden behind Repository.

- **B2 – Search**
  - `SearchView` in Vacation List filters displayed vacations in real time.

- **B3 – Database CRUD**
  - `VacationDao` and `ExcursionDao` support add/edit/delete.
  - Repository wraps DAO calls and ensures async writes.

- **B4 – Reports**
  - Generated reports include title, timestamp, and tabular vacation + excursion details.

- **B5 – Validation**
  - Non-empty field checks, numeric parsing, and **date-range validation**.

- **B6 – Security**
  - Passwords hashed with SHA-256.
  - Session persistence with sign-out support.

- **B7 – Scalable Design**
  - MVVM + Repository pattern.
  - Room handles persistence.
  - LiveData ensures reactive UI.

- **B8 – GUI / UX**
  - Material Design: Card lists, FABs, DatePickers, toasts, confirmation dialogs.
  - Empty states + SwipeRefresh for improved usability.

---

## 🏗️ Architecture

- **UI (Activities)**  
  `VacationListActivity`, `VacationDetailsActivity`, `ExcursionDetailsActivity`, `ReportActivity`, `LoginActivity`, `SplashActivity`

- **ViewModels**  
  `VacationListViewModel`, `VacationDetailsViewModel`, `ExcursionViewModel`

- **Data Models (Entities)**  
  `Vacation`, `Excursion`

- **Persistence**  
  `database/VacationDatabaseBuilder`, `dao/VacationDao`, `dao/ExcursionDao`

- **Repository Layer**  
  `repositories/Repository`

- **Adapters**  
  `adapters/VacationAdapter`, `adapters/ExcursionAdapter`

---

## 📲 Installation & Running

### Option 1: Install APK
1. Download the signed APK (Android 8.0+).
2. Install on your device/emulator.  
   *(Enable “Install from Unknown Sources” if needed.)*

### Option 2: Run from Source
```bash
git clone https://gitlab.com/wgu-gitlab-environment/student-repos/bvinc38/d424-software-engineering-capstone.git
cd d424-software-engineering-capstone
git checkout app   # or 'working' branch if testing features
