# Mergington High School Activities API

A super simple FastAPI application that allows students to view and sign up for extracurricular activities.

## Features

- View all available extracurricular activities
- Sign up for activities with authentication
- Role-based access for parent, provider, and admin users

## Getting Started

1. Install the dependencies:

   ```
   pip install fastapi uvicorn
   ```

2. Run the application:

   ```
   python app.py
   ```

3. Open your browser and go to:
   - API documentation: http://localhost:8000/docs
   - Alternative documentation: http://localhost:8000/redoc

## Authentication

This application uses a simple in-memory authentication flow. Users can log in via the `/login` endpoint and receive a Bearer token for subsequent protected requests.

### Sample users

- `parent1` / `parentpass` — role: `parent`
- `provider1` / `providerpass` — role: `provider`
- `admin1` / `adminpass` — role: `admin`

### Login request

POST `/login`

```json
{
  "username": "parent1",
  "password": "parentpass"
}
```

### Login response

```json
{
  "access_token": "...",
  "token_type": "Bearer",
  "role": "parent",
  "email": "parent1@mergington.edu",
  "username": "parent1"
}
```

## API Endpoints

| Method | Endpoint                                                          | Description                                                                 |
| ------ | ----------------------------------------------------------------- | --------------------------------------------------------------------------- |
| GET    | `/activities`                                                     | Get all activities with their details and current participant count         |
| POST   | `/login`                                                          | Authenticate and receive a Bearer token                                     |
| GET    | `/me`                                                             | Get the current authenticated user                                          |
| POST   | `/activities/{activity_name}/signup?email=student@mergington.edu` | Sign up for an activity (requires authentication and role-based access)     |
| DELETE | `/activities/{activity_name}/unregister?email=student@mergington.edu` | Unregister from an activity (requires authentication and role-based access) |

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

All data is stored in memory, which means data will be reset when the server restarts.
