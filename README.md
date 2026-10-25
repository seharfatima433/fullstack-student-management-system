# Full Stack Student Management System (SMS)
## Devixo Solutions — Summer Internship 2026
### Web Development Internship — Week 3 (Task 03)

---

## 📌 Project Overview
The **Full Stack Student Management System (SMS)** is an enterprise-standard educational management platform engineered to resolve the administrative, security, and accessibility bottlenecks of legacy academic portals.

Developed using **Option 1 (PHP, Laravel 10, MySQL, JavaScript ES6+, HTML5, CSS3)**, the platform replaces uncontrolled public self-registration with **Single Administrator Governance** and enforces **Two-Factor Authentication (2FA) via 6-digit Gmail OTP verification** for all faculty and student accounts.

---

## 👤 Intern & Submission Information
- **Intern Name:** Sehar Fatima
- **Internship Domain:** Web Development Internship
- **Task Designation:** Task 03 – Full Stack Student Management System
- **Host Organization:** Devixo Solutions
- **Submission Date:** October 2026
- **Repository:** [https://github.com/seharfatima/fullstack-student-management-system](https://github.com/seharfatima/fullstack-student-management-system)

---

## 🚀 Key Features

### 1. Single Administrator Governance
- Public registration routes are completely removed to protect institutional integrity.
- Only the authenticated sovereign Admin (`admin@devixo.com`) can provision and manage Student and Teacher profiles.

### 2. Two-Factor Authentication (Gmail OTP 2FA)
- Automated 6-digit OTP code dispatch directly to Gmail inboxes upon account creation.
- Centrally floating frosted-glass modal intercepts unverified sign-in attempts, mandating OTP verification before access is granted.

### 3. Comprehensive CRUD Modules
- **Student Management:** Add new students with roll number indexing, edit profiles, view details, search dynamically, and delete records with confirmation safeguards.
- **Teacher & Faculty Management:** Onboard instructors, view qualifications, and link assigned courses.
- **Course & Quota Management:** Create course catalog entries, assign instructors, and dynamically allocate student enrollment quotas via pivot relations.

### 4. Interactive Metric Dashboard
- Real-time gradient counter cards displaying Total Students, Teachers, Courses, and AI Grading status.
- Recent registrations ledger with avatar badges and quick-action modals.

### 5. Multi-Device Responsive UI/UX
- Mobile drawer navigation with backdrop blur and touch targets.
- Responsive table wrappers (`.table-wrap`) preventing horizontal overflow on smartphone screens.
- Asynchronous form submissions with loading spinners and alert banners (no full page reload required).

---

## 🛠️ Technology Stack (Option 1)

| Layer | Technology | Version | Purpose / Architectural Role |
| :--- | :--- | :--- | :--- |
| **Backend Framework** | Laravel (PHP) | 10.x / PHP 8.1+ | MVC architecture, Eloquent ORM, CSRF protection, and Dependency Injection. |
| **Database** | MySQL / MariaDB | 8.0+ / 10.4+ | Permanent relational persistence, indexing, foreign keys, and ACID compliance. |
| **Frontend Views** | Blade Templates | Laravel 10 Engine | Master layout inheritance (`layouts/app.blade.php`), components, and XSS filtering. |
| **Client Scripting** | JavaScript (ES6+) | Modern Vanilla JS | Asynchronous Fetch API for OTP verification, search filters, and modal handling. |
| **Design & Styling** | CSS3 Custom Tokens | Modern Standards | CSS variables (`--deep`, `--mid`, `--snow`), Flexbox/Grid layouts, Font Awesome 6. |
| **Environment** | XAMPP & Composer | Apache 2.4, PHP 8 | Local development server virtualization, Artisan CLI, and package management. |

---

## 🗄️ Database Architecture & Schema

The system utilizes a relational schema in MySQL:
- `exam_users`: Stores user credentials (`id`, `name`, `email`, `password`, `role`, `rollno`, `email_verified_at`, `timestamps`).
- `courses`: Defines courses (`id`, `name`, `code`, `description`, `teacher_id` foreign key).
- `course_user`: Many-to-many pivot table managing student course enrollments (`user_id`, `course_id`, `assign_count`).
- `quizzes` & `quiz_attempts`: Tracks assessments, student submissions, and proctored records.

---

## ⚙️ Setup & Installation Instructions

Follow these steps to run the application locally on Windows (XAMPP environment):

### Prerequisites
1. **PHP >= 8.1** with PDO, cURL, OpenSSL, and Mbstring extensions enabled.
2. **Composer** installed globally.
3. **MySQL Server** (via XAMPP or standalone).

### Step 1: Clone the Repository
```bash
git clone https://github.com/seharfatima/fullstack-student-management-system.git
cd fullstack-student-management-system
```

### Step 2: Install Dependencies
```bash
composer install
```

### Step 3: Configure Environment Variables
Copy `.env.example` to `.env`:
```bash
cp .env.example .env
```
Open `.env` and verify your database credentials:
```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=student_management_db
DB_USERNAME=root
DB_PASSWORD=
```

### Step 4: Generate Application Key
```bash
php artisan key:generate
```

### Step 5: Run Database Migrations & Seeders
Create the database in MySQL (`student_management_db`), then execute:
```bash
php artisan migrate
php artisan db:seed
```

### Step 6: Start Local Development Server
```bash
php artisan serve
```
The application will be live at: **`http://localhost:8000`**

---

## 🔑 Default Credentials

| Portal / Role | Email | Password | Access Level |
| :--- | :--- | :--- | :--- |
| **Administrator** | `admin@devixo.com` | `admin123` | Full CRUD, user provisioning, course allocations, analytics. |
| **Faculty / Teacher** | `teacher@devixo.com` | `teacher123` | Course quizzes, grading, student performance monitoring. |
| **Student** | `student@devixo.com` | `student123` | Enrolled courses, quiz attempts, real-time results. |

*Note: For new accounts, enter the 6-digit OTP code dispatched to the registered Gmail to complete verification.*

---

## 📁 Project Architecture & Key Files

```text
├── app/
│   ├── Http/
│   │   ├── Controllers/Web/
│   │   │   ├── AdminController.php      # Student, Teacher, Course CRUD & OTP dispatch
│   │   │   ├── AuthController.php       # Login session & asynchronous OTP verification
│   │   │   ├── TeacherController.php    # Instructor dashboard & course quizzes
│   │   │   └── StudentController.php    # Student portal & course view
│   │   └── Middleware/
│   │       └── RoleMiddleware.php       # Role-Based Access Control (Admin/Teacher/Student)
│   └── Models/
│       ├── ExamUser.php                 # User model with course relationships
│       └── Course.php                   # Course model
├── database/
│   ├── migrations/                      # Relational schema migrations
│   └── seeders/DatabaseSeeder.php       # Admin account seeder
├── resources/
│   └── views/
│       ├── layouts/app.blade.php        # Master layout (sidebar drawer, color variables)
│       ├── auth/login.blade.php         # Split login screen & Gmail OTP modal
│       ├── admin/
│       │   ├── dashboard.blade.php      # Stats counters & recent registrations
│       │   ├── students.blade.php       # Student directory & CRUD modals
│       │   └── courses.blade.php        # Course management & assignments
│       └── student/ & teacher/          # Role portals
└── routes/web.php                       # Role-prefixed route definitions
```

---

## 🌟 Bonus Evaluation Criteria Compliance

- ✅ **Permanent MySQL Persistence:** All records preserved across sessions via Eloquent relational models.
- ✅ **Role-Based Access Control (RBAC):** Distinct route prefixes (`/admin`, `/teacher`, `/student`) protected by `RoleMiddleware`.
- ✅ **Dynamic Filtering & Pagination:** Instant table search and badge counts for institutional data.
- ✅ **Form Validation & Loading Spinners:** Real-time feedback, button disabled states, and toast notifications.

---

## 📄 Submission Deliverables
- **PDF Technical Report:** `Devixo_Task03_FullStack_SMS_Report.pdf` (Formatted 6-page comprehensive report).
- **DOCX Word Report:** `Devixo_Task03_FullStack_SMS_Report.docx` (Fully editable Microsoft Word report).
- **Source Code Repository:** Complete Laravel 10 codebase.
- **Documentation:** `README.md` (Setup guide, architectural breakdown, credentials).
#   f u l l s t a c k - s t u d e n t - m a n a g e m e n t - s y s t e m  
 