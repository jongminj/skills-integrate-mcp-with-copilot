# Mergington High School Activities API

A super simple FastAPI application that allows students to view and sign up for extracurricular activities.

## Features

- View all available extracurricular activities
- View participant lists without signing in
- Sign up or unregister students as a teacher

## Getting Started

1. Install the dependencies:

   ```
   pip install fastapi uvicorn
   ```

2. Configure a teacher account and run the application:

   ```
   export TEACHER_USERNAME=your-teacher-username
   export TEACHER_PASSWORD='replace-with-a-long-random-password'
   uvicorn src.app:app --reload
   ```

3. Open your browser and go to:
   - API documentation: http://localhost:8000/docs
   - Alternative documentation: http://localhost:8000/redoc

## API Endpoints

| Method | Endpoint                                                          | Description                                                         |
| ------ | ----------------------------------------------------------------- | ------------------------------------------------------------------- |
| GET    | `/activities`                                                     | Get all activities with their details and current participant count |
| GET    | `/teacher/session`                                                | Validate teacher credentials (HTTP Basic authentication)           |
| POST   | `/activities/{activity_name}/signup?email=student@mergington.edu` | Sign up a student (teacher authentication required)                 |
| DELETE | `/activities/{activity_name}/unregister?email=student@mergington.edu` | Unregister a student (teacher authentication required)           |

## Data Model

The application uses a simple data model with meaningful identifiers:

1. **Activities** - Uses activity name as identifier:

   - Description
   - Schedule
   - Maximum number of participants allowed
   - List of student emails who are signed up

2. **Students** - Uses email as identifier:
   - Name
   - Grade level

All data is stored in memory, which means data will be reset when the server restarts. Configure teacher credentials through environment variables; there are no default credentials. Use HTTPS when deploying because HTTP Basic authentication sends credentials with each request.
