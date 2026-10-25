# 🎓 Full Stack Student Management System
### Devixo Solutions Summer Internship — Week 3 (Task 03)
**Domain:** Web Development Internship  
**Intern Name:** Sehar Fatima  
**Submission:** Task 03 – Full Stack Student Management System  

---

## 📋 Project Overview

An enterprise-grade, responsive **Full Stack Student Management System** developed in accordance with the **Devixo Solutions Summer Internship** Week 3 requirements. The system implements robust Role-Based Access Control (Single Admin, Teacher, and Student), automated Gmail OTP two-factor verification for student/teacher registration, permanent MySQL data persistence, interactive statistics dashboards, and complete CRUD functionality across students, instructors, and academic courses.

[![PHP](https://img.shields.io/badge/PHP-8.1+-777BB4?style=for-the-badge&logo=php&logoColor=white)](https://php.net)
[![Laravel](https://img.shields.io/badge/Laravel-10.x-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)](https://laravel.com)
[![MySQL](https://img.shields.io/badge/MySQL-8.0%20%2F%20MariaDB-4479A1?style=for-the-badge&logo=mysql&logoColor=white)](https://mysql.com)
[![JavaScript](https://img.shields.io/badge/JavaScript-ES6+-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](https://developer.mozilla.org)
[![Responsive](https://img.shields.io/badge/Design-Mobile%20%2F%20Tablet%20%2F%20Desktop-10B981?style=for-the-badge)](https://laravel.com)

---

## ✨ Features Breakdown

### 🔐 1. Authentication & Role-Based Access Control (RBAC)
- **Single Administrator Architecture**: Centralized management where only 1 authorized Admin maintains control over the entire institution.
- **Gmail OTP Verification**: When the Admin registers a new student or teacher, an automated 6-digit OTP is generated and dispatched to their Gmail address.
- **Interactive OTP Modal**: Upon initial sign-in, unverified users are prompted with an OTP modal dialog to authenticate their email before accessing portal features.
- **Role-Guarded Dashboards**: Separate middleware-protected dashboard experiences for Admin, Instructors, and Students.
- **Secure Sign Out**: Complete session cleanup and CSRF token invalidation upon logout.

### 👨‍🎓 2. Student Management Module
- **Add Student**: Intuitive modal with validation (Name, Email, Roll No, Password, and Course Enrollment). Auto-generates unique institutional roll numbers (`STU-YYYY-XXX`) if omitted.
- **Edit Student**: Instant updates to student profiles, credentials, and course assignments.
- **Delete Student**: Permanent deletion with relational database cleanup (detaching courses cleanly).
- **Search Student**: Live multi-field search filtering by Student Name, Email, or Roll Number with query string persistence.
- **View Student Details**: AJAX-powered modal displaying complete profile data, registration timestamp, and a list of enrolled courses.
- **Pagination**: Clean, responsive 8-records-per-page pagination with URL search parameter preservation.

### 👩‍🏫 3. Teacher / Instructor Module
- **Add Teacher**: Register faculty members with name, email, credentials, and automatic Gmail OTP.
- **Edit Teacher**: Update instructor details and assign/reassign department roles.
- **Delete Teacher**: Safe deletion with automatic course disassociation.
- **Instructor Directory**: Filterable list with course assignments and active status.

### 📚 4. Course Management Module
- **Add Course**: Create courses with Course Title, Course Code, Description, Active Status, and assigned Instructor.
- **Edit & Update**: Modify catalog data and reallocate teachers on the fly.
- **Delete Course**: Safely remove courses and detach enrolled students without orphaned records.
- **Teacher Assignment**: Quick one-click instructor assignment and removal.
- **Student Enrollment**: Dedicated per-student course enrollment manager.

### 📊 5. Professional Dashboard
- **Dynamic Statistics Cards**: Real-time counter metrics for Total Students, Total Teachers, Total Courses, and System Quizzes.
- **Recent Registrations**: Quick-glance overview of recent student additions with course counts and direct actions (View Details, Edit, Delete).
- **Global Search Bar**: Instant real-time filtering directly from the dashboard home.
- **Responsive Layout**: Designed from the ground up for Mobile (320px–480px), Tablet (768px–1024px), and Desktop/Laptop displays.

---

## 🛠️ Technology Stack (Option 1 Selected)

- **Frontend**: HTML5, Vanilla CSS3 (Custom Design System), JavaScript (ES6+), Font Awesome 6 Icons, Google Fonts (Bricolage Grotesque & DM Sans).
- **Backend**: PHP 8.1+, Laravel 10.x Web Framework.
- **Database**: MySQL / MariaDB (Local permanent database storage with Eloquent ORM).
- **Authentication**: Session-based RBAC with RoleMiddleware and Sanctum API fallback.
- **Email / OTP**: Remote LMS OTP Service Integration with Gmail dispatch.

---

## 🚀 Setup & Installation Guide

### Prerequisites
- PHP >= 8.1 with `pdo_mysql`, `curl`, and `mbstring` extensions enabled.
- Composer installed.
- MySQL / MariaDB (via XAMPP or standalone service).

### Step 1: Clone the Repository
```bash
ithub.com/seharfatima433/fullstack-student-management-system
```

### Step 2: Install PHP Dependencies
```bash
composer install
```

### Step 3: Configure Environment
Copy `.env.example` to `.env`:
```bash
cp .env.example .env
php artisan key:generate
```

Configure your MySQL connection in `.env`:
```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=root
DB_PASSWORD=
```

### Step 4: Run Migrations & Seed Data
```bash
# Start MySQL in XAMPP
# Then run:
php artisan migrate --seed
```

### Step 5: Start Development Server
```bash
php artisan serve --port=8080
```
Open your browser and navigate to: `https://devlura.site/web-cheating-detection-main/public/`

---



## 📁 Project Architecture & Structure

```
├── app/
│   ├── Http/
│   │   ├── Controllers/Web/
│   │   │   ├── AdminController.php    # Student, Teacher, Course CRUD & Dashboard
│   │   │   ├── AuthController.php     # Session Auth & Gmail OTP Verification
│   │   │   ├── TeacherController.php  # Instructor Dashboard & Quizzes
│   │   │   └── StudentController.php  # Student Portal & Enrolled Courses
│   │   └── Middleware/
│   │       └── RoleMiddleware.php     # Role-based route guard
│   └── Models/
│       ├── ExamUser.php               # User model (Admin, Teacher, Student)
│       └── Course.php                 # Academic course model & relations
├── database/
│   ├── migrations/                    # Database schemas for users, courses, relations
│   └── seeders/DatabaseSeeder.php     # Default admin, sample teachers & students
├── resources/views/
│   ├── layouts/app.blade.php          # Main responsive layout with sidebar & drawer
│   ├── auth/login.blade.php           # Secure login with OTP modal dialog
│   └── admin/
│       ├── dashboard.blade.php        # Statistics, search, and recent registrations
│       ├── students.blade.php         # Student management with pagination & search
│       ├── teachers.blade.php         # Teacher management directory
│       ├── courses.blade.php          # Course catalog & instructor assignments
│       └── student-courses.blade.php  # Individual student enrollment editor
└── routes/web.php                     # Route definitions with role middleware guards
```

---

## 👩‍💻 Author & Internship Details

- **Intern Name:** Sehar Fatima  
- **Internship:** Devixo Solutions Summer Internship  
- **Task:** Task 03 – Full Stack Student Management System  
- **GitHub:** [@seharfatima433](https://github.com/seharfatima433)  
- **Repository:** [web-cheating-detection](https://github.com/seharfatima433/web-cheating-detection)  
