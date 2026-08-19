# Mergington High School Activities API

A super simple FastAPI application that allows students to view and sign up for extracurricular activities.

## Features

- View all available extracurricular activities
- Sign up for activities

## Getting Started

1. Install the dependencies:

   ```
   pip install fastapi uvicorn
   ```

   SQLite is provided by Python's standard library, so no additional database
   package is required.

2. Run the application:

   ```
   uvicorn app:app --reload
   ```

3. Open your browser and go to:
   - API documentation: http://localhost:8000/docs
   - Alternative documentation: http://localhost:8000/redoc

## API Endpoints

| Method | Endpoint                                                          | Description                                                         |
| ------ | ----------------------------------------------------------------- | ------------------------------------------------------------------- |
| GET    | `/activities`                                                     | Get all activities with their details and current participant count |
| POST   | `/activities/{activity_name}/signup?email=student@mergington.edu` | Sign up for an activity                                             |

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

Activities and registrations are stored in SQLite. The database is initialized
with the sample activities the first time the application starts, and existing
data is preserved across restarts. By default the database is created at
`src/activities.db`. Set `ACTIVITY_DB_PATH` to use a different SQLite file:

```bash
ACTIVITY_DB_PATH=/path/to/activities.db uvicorn app:app --reload
```

The database schema is created automatically on startup. The activities and
registrations tables enforce unique activity names and duplicate registrations.
