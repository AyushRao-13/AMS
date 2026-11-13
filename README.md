# Attendance Management System

A web-based attendance management application built with **React**, **Django**, and **MySQL**. It supports attendance and reporting workflows for faculty members, Class Coordinators, and Heads of Department (HODs).

## Features

- Role-specific workflows and report views for faculty, Class Coordinators, and HODs.
- Faculty authentication using Django sessions.
- Record and update student attendance by class, subject, and date.
- Student-wise attendance summaries, including present days, total classes, and attendance percentages.
- Downloadable CSV attendance reports.
- Email-based password generation/reset workflow.
- React frontend communicating with Django through HTTP endpoints.

## Technology Stack

| Layer | Technology |
|---|---|
| Frontend | React 18, React Router |
| Frontend requests/state | Axios, Redux Toolkit (where used) |
| Backend | Python, Django 4.1.7 |
| Database | MySQL |
| Database access | Django ORM |
| Reports | CSV |

## Architecture

```text
React Frontend
      |
      | HTTP requests / JSON responses
      v
Django Backend
      |
      | Django ORM
      v
MySQL Database
```

React handles the user interface. Django processes requests, applies application logic, manages faculty session workflows, and accesses persistent records through the ORM. MySQL stores the application's academic and attendance data.

## Prerequisites

- Python 3.11.x (the project documentation specifies Python 3.11.9).
- Node.js and npm.
- MySQL Server.

Use the existing frontend `package.json` for the exact Node scripts and JavaScript dependencies.

## Setup and Installation

The commands below assume the Django backend contains `manage.py` and the React frontend contains `package.json`. Adjust folder names to match your repository.

### 1. Clone the repository

```bash
git clone <YOUR_REPOSITORY_URL>
cd <PROJECT_FOLDER>
```

### 2. Set up the Django backend

Open a terminal in the folder containing `manage.py`.

**Windows PowerShell:**

```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
```

**Windows Command Prompt:**

```bat
python -m venv venv
venv\Scripts\activate
```

Install backend dependencies:

```bash
pip install -r requirements.txt
```

### 3. Configure MySQL

1. Start the MySQL server.
2. Create the database configured in Django settings. The project documentation previously used the database name `ams`.
3. Open the backend `settings.py`.
4. Confirm the `DATABASES` configuration contains your local database name, username, password, host, and port.
5. Ensure the MySQL Python adapter used by the project is installed.

Example:

```sql
CREATE DATABASE ams;
```

Do not commit database passwords or other credentials to GitHub.

### 4. Apply migrations

From the backend folder:

```bash
python manage.py check
python manage.py migrate
```

If you have intentionally changed Django models, create migrations first:

```bash
python manage.py makemigrations
python manage.py migrate
```

### 5. Create a Django superuser (optional)

```bash
python manage.py createsuperuser
```

A Django superuser is for the Django admin site. It does not necessarily create a faculty account for the application's own login workflow.

### 6. Run the Django backend

```bash
python manage.py runserver
```

Default backend address:

```text
http://127.0.0.1:8000/
```

### 7. Run the React frontend

Open a second terminal and move to the frontend folder containing `package.json`:

```bash
npm install
npm start
```

If the existing `package.json` uses Vite, use its configured script instead:

```bash
npm run dev
```

Use the script already defined in `package.json`. Ensure the frontend API base URL points to the Django backend.

## Running the Application

1. Start MySQL.
2. Start the Django backend.
3. Start the React frontend.
4. Open the frontend URL shown in the terminal.
5. Sign in using an account created through the application's faculty workflow.
6. Use the role-specific screens to manage attendance, view summaries, and download reports.

If enabled, Django admin is generally available at `http://127.0.0.1:8000/admin/`.

## Troubleshooting

- **MySQL connection error:** Check that MySQL is running and verify the database name, username, password, host, and port in Django settings.
- **Missing MySQL driver:** Install the adapter expected by the project's Django database configuration.
- **Migration error:** Confirm that the configured database exists and inspect the migration files.
- **React cannot reach Django:** Check that Django is running and that the frontend API base URL is correct. Review the browser console and Django terminal.
- **CORS or CSRF error:** Check the existing Django CORS/CSRF configuration and frontend origin. Do not permanently disable security protections.
- **Frontend start command fails:** Check the `scripts` section of `package.json` and use the command defined there.

## Notes

- This README describes the documented React + Django + MySQL implementation.
- The project documentation specifies Django 4.1.7 and Python 3.11.9. Verify actual installed versions and dependencies against your source repository before deployment.
- Do not publish secret keys, passwords, or database backups containing personal information.

## License

Add the license applicable to this project before public distribution.
