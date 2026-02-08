# Repository Architecture and Functionality

## Overview

This repository is a **GitHub Skills learning exercise** designed to teach developers how to use GitHub Copilot effectively. It provides a hands-on coding environment where learners practice using Copilot's AI-powered code completion and assistance features.

The repository contains a fully functional **High School Management System** web application that serves as the practice project for learners. This application allows students to view and sign up for extracurricular activities at the fictional "Mergington High School."

## Main Functionality

### Purpose
- **Educational Tool**: Interactive exercise for learning GitHub Copilot
- **Practical Application**: Working web application demonstrating real-world development scenarios
- **Skill Development**: Hands-on practice with AI-assisted coding techniques

### Learning Exercise Components
The repository includes automated GitHub Actions workflows that guide learners through different Copilot features:
- Step 0: Starting the exercise
- Step 1: Preparing the environment
- Step 2: First introduction to Copilot
- Step 3: Copilot edits and code modifications
- Step 4: Copilot agent mode
- Step 5: Copilot on GitHub

## Key Components

### 1. Backend API (`src/app.py`)
A FastAPI-based REST API that manages extracurricular activities:

**Core Features:**
- **Activity Management**: In-memory database storing 9 different activities (Chess Club, Programming Class, Gym Class, Basketball Team, Tennis Club, Drama Club, Art Studio, Debate Team, Science Club)
- **Student Registration**: API endpoints for signing up and unregistering from activities
- **Static File Serving**: Hosts the frontend web interface

**API Endpoints:**
- `GET /` - Redirects to the main web interface
- `GET /activities` - Returns all available activities with details
- `POST /activities/{activity_name}/signup?email={email}` - Sign up a student for an activity
- `POST /activities/{activity_name}/unregister?email={email}` - Remove a student from an activity

**Activity Data Structure:**
Each activity includes:
- Description of the activity
- Schedule (days and times)
- Maximum participant capacity
- Current list of registered participants (email addresses)

### 2. Frontend Web Application (`src/static/`)

**Components:**
- `index.html` - Main webpage structure with activity listing and signup form
- `styles.css` - Styling for the web interface
- `app.js` - Client-side JavaScript for API interactions and dynamic content loading

**User Interface Features:**
- Display all available extracurricular activities
- Show activity details (description, schedule, capacity)
- Provide a signup form for students to register
- Real-time feedback on registration status

### 3. Test Suite (`tests/test_app.py`)

Comprehensive test coverage using pytest and FastAPI TestClient:
- **Activity Retrieval Tests**: Verify activities endpoint returns correct data
- **Signup Flow Tests**: Test complete signup and unregister workflows
- **Validation Tests**: Ensure proper error handling for invalid activities
- **Edge Case Tests**: Check duplicate signups and non-existent activities

### 4. Development Environment

**Container Configuration** (`.devcontainer/devcontainer.json`):
- Python 3.13 development environment
- Port forwarding for the FastAPI server (port 8000)
- Pre-configured with GitHub Copilot VS Code extension
- Automatic dependency installation on container creation

**Dependencies** (`requirements.txt`):
- `fastapi` - Modern web framework for building APIs
- `uvicorn` - ASGI server for running FastAPI
- `pytest` - Testing framework
- `requests` - HTTP library for API calls
- `httpx` - Async HTTP client for TestClient

### 5. Automation & Workflows (`.github/workflows/`)

GitHub Actions workflows that automate the learning experience:
- **Exercise Progression**: Automatically updates the exercise as learners complete steps
- **Guided Learning**: Posts instructional content to GitHub Issues
- **Progress Tracking**: Monitors learner progress through the Copilot features

## Technology Stack

| Layer | Technology | Purpose |
|-------|-----------|---------|
| **Backend Framework** | FastAPI | High-performance Python web API |
| **Server** | Uvicorn | ASGI server for async operations |
| **Frontend** | HTML/CSS/JavaScript | Simple, interactive web interface |
| **Testing** | pytest + TestClient | Automated testing and validation |
| **Development** | Dev Containers | Consistent development environment |
| **AI Assistant** | GitHub Copilot | Code completion and assistance |
| **Automation** | GitHub Actions | Exercise workflow automation |

## Application Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    GitHub Skills                        │
│              (Learning Exercise Platform)               │
└─────────────────────────────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────┐
│                  Learner's Browser                      │
│  ┌───────────────────────────────────────────────┐    │
│  │         Frontend (Static Files)                │    │
│  │  - index.html (UI Structure)                  │    │
│  │  - app.js (API Client)                        │    │
│  │  - styles.css (Styling)                       │    │
│  └─────────────────┬─────────────────────────────┘    │
└────────────────────┼──────────────────────────────────┘
                     │ HTTP/JSON
                     ▼
┌─────────────────────────────────────────────────────────┐
│              Backend API (FastAPI)                      │
│  ┌───────────────────────────────────────────────┐    │
│  │  Routes:                                       │    │
│  │  - GET /activities                            │    │
│  │  - POST /activities/{name}/signup             │    │
│  │  - POST /activities/{name}/unregister         │    │
│  └─────────────────┬─────────────────────────────┘    │
│                    │                                    │
│  ┌─────────────────▼─────────────────────────────┐    │
│  │     In-Memory Data Store                      │    │
│  │  (Activities Dictionary)                      │    │
│  └───────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────┘
```

## Data Flow

1. **Page Load**: Browser requests `GET /` → Server redirects to `/static/index.html`
2. **Activity Loading**: JavaScript calls `GET /activities` → Server returns activity data → UI displays activities
3. **Student Signup**: 
   - User fills form with email and activity selection
   - JavaScript sends `POST /activities/{name}/signup?email={email}`
   - Server validates and adds student to activity
   - Response confirms signup or returns error
4. **Activity Unregister**: Similar flow using the unregister endpoint

## Use Cases

### Primary Use Case: Learning GitHub Copilot
Students and developers use this repository to:
1. Set up a development environment with Copilot enabled
2. Practice using Copilot for code completion
3. Learn to write code with AI assistance
4. Understand how to effectively prompt Copilot
5. Complete guided exercises that demonstrate Copilot features

### Secondary Use Case: Activity Management System
The application itself serves as:
- A demo of a real-world REST API
- An example of FastAPI best practices
- A template for similar management systems
- A testing ground for web development skills

## Setup and Running

**Installation:**
```bash
pip install -r requirements.txt
```

**Running the Application:**
```bash
cd src
uvicorn app:app --reload
```

**Running Tests:**
```bash
pytest
```

**Access the Application:**
- Open browser to `http://localhost:8000`
- API documentation available at `http://localhost:8000/docs`

## Security Considerations

- **In-Memory Storage**: Data is not persisted (suitable for learning/demo)
- **No Authentication**: Open API without user authentication (educational context)
- **Input Validation**: Email format validation on frontend only
- **CORS**: Not configured (single-origin application)

## Future Enhancement Opportunities

For learners practicing with Copilot, this codebase offers opportunities to add:
- Capacity checking (prevent over-enrollment)
- Student profile management
- Activity search and filtering
- Email notifications
- Data persistence with a database
- Authentication and authorization
- Admin dashboard for activity management

## Summary

This repository serves a dual purpose: it's both an **interactive learning platform** for GitHub Copilot and a **functional web application** demonstrating modern Python web development. The High School Activity Management System provides realistic coding scenarios where learners can practice AI-assisted development in a safe, guided environment.
