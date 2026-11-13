# Product Brief – ShiftMate

## Project Name

**ShiftMate – Smart Work & Study Schedule Manager**

## Purpose

ShiftMate is a web application designed to help students who work part-time manage their work shifts, school responsibilities, and estimated earnings in one place.

## Target User

The main users are high school and university students who work part-time while studying.

## Problem

Students who work while attending school often struggle to manage work shifts, exams, assignments, and study sessions.

Using separate calendars or notes can lead to scheduling conflicts, missed deadlines, and difficulty keeping track of working hours and earnings.

ShiftMate aims to solve this problem by organizing work and school information in one application.

## Data We Will Use

Unlike our previous Game Discovery project, ShiftMate will not use a predefined dataset.

Users will enter their own information, which will be stored in a SQLite database.

The application will use:

- Work shifts (date, start time, end time)
- Hourly wage
- School events (exams, assignments, and study sessions)
- Event dates and times
- Working hours calculated from shifts
- Estimated gross earnings

## Main User Flow

1. The user opens the ShiftMate website.
2. The user enters their hourly wage.
3. The user adds upcoming work shifts.
4. The user adds school events and deadlines.
5. The application saves the information in the database.
6. The user views their work and school activities together.
7. The system calculates working hours and estimated gross earnings.
8. The system warns the user if a work shift overlaps with a timed school event.
9. The user can update or delete shifts and school events when plans change.

## Minimum Viable Product (MVP)

The first working version of ShiftMate will include five essential features.

### 2. School Event Management
- Add, edit, and delete school events.
- Support three event types: exams, assignments, and study sessions.
- Assignments have a due date and an optional due time.
- Exams and study sessions have a date, start time, and end time.
- Save all school events in the SQLite database.
- Only events with start and end times are used for scheduling conflict detection.

### 3. Combined Schedule
- Display work shifts and school events in a simple weekly list, grouped by date.
- Allow users to view their weekly schedule.
- Clearly distinguish work activities from school activities.

### 1. Work Shift Management
- Add new shifts.
- Edit or delete existing shifts.
- Save shift dates and start/end times.

### 2. School Event Management
- Add exams, assignments, and study sessions.
- Edit or delete school events.
- Save event dates and relevant times.

### 3. Combined Schedule
- Display upcoming work shifts and school events together.
- Allow users to view their weekly schedule.
- Distinguish work activities from school activities.

### 4. Working Hours and Earnings
- Allow users to enter a basic hourly wage.
- Calculate working hours from saved shifts.
- Display estimated gross earnings.

### 5. Conflict Detection
- Detect overlapping work shifts and timed school events.
- Display warnings when conflicts occur.
- Allow users to edit conflicting events.

## Should Have

These features are important but can be added after the MVP works:

- Dashboard with monthly work statistics.
- Monthly calendar navigation.
- Different colors for work and school activities.
- Search and filtering of shifts and school events.
- Helpful messages when no information is available.
- Improved responsive layout for smaller screens.

## Could Have

Optional features that could improve the application:

- Different hourly rates for evenings and weekends.
- Monthly earnings charts.
- Earnings and savings targets.
- Warnings about late shifts before early exams.
- Exporting schedules to PDF.
- Shift status tracking (scheduled, completed, cancelled).

## Out of Scope

The following features will not be included in the first version:

- Multiple user accounts and authentication.
- Connections to employers' scheduling systems.
- Automatic shift swapping between employees.
- Real payroll processing and tax calculations.
- Email or SMS notifications.
- AI-generated work schedules.
- Native mobile applications.

## Technical Approach

The application will use:

- Node.js and Express.js for the backend.
- SQLite for storing information.
- HTML, CSS, and JavaScript for the frontend.
- GitHub for version control and project management.
- GitHub Copilot Agent to assist with development.

The first version will be a local, single-user web application.

## Main Risks

1. **Time calculations:** Shifts that continue past midnight must be handled correctly.
2. **Scheduling conflicts:** The application must correctly identify overlapping timed activities.
3. **Salary accuracy:** Estimated earnings may differ from actual salary because taxes, breaks, and additional pay rates are not included.
4. **Invalid data:** Incorrect or missing information must not cause the application to crash.
5. **Project complexity:** Too many features could make the project difficult to finish.

