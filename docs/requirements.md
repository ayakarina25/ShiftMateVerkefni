# Requirements – ShiftMate

## 1. Purpose

The purpose of ShiftMate is to help students who work part-time manage their time between school, studying, and work.

The application will help students organize their schedules, create personalized study plans based on their available time, subject difficulty, and upcoming exams, and track their working hours and estimated earnings.

The main goal is to make time management easier, reduce scheduling conflicts, and help students balance their responsibilities without feeling overwhelmed.

## 2. Primary User

The primary users of ShiftMate are high school and university students who work part-time while studying.

These students need to manage multiple subjects, exams, assignments, study sessions, and work shifts.

ShiftMate is designed to help them organize their schedules, plan their study time based on their availability, and balance their academic and work responsibilities.

## 3. Problem

Students who work part-time often struggle to balance their school responsibilities, study time, and work schedules.

They may find it difficult to identify available time for studying and decide how to divide that time between different subjects, especially when exams and deadlines are approaching.

Managing school and work schedules separately can also lead to scheduling conflicts and make it difficult to track working hours.

ShiftMate aims to solve these problems by bringing everything together in one application and helping students create realistic, flexible study plans.

## 4. Out of Scope

The following features will not be included in the final ShiftMate project:

- User registration and login systems.
- Multiple user accounts.
- Connections to external school or employer systems.
- Automatic shift swapping between employees.
- Advanced payroll calculations, including taxes and deductions.
- Email and SMS notifications.
- AI chatbots or machine-learning-based scheduling.
- Native mobile applications.

These features are excluded to keep the project manageable and focus on the main goal: helping working students organize their schedules, create personalized study plans, and track estimated earnings.

## 5. Functional Requirements

### FR-01 – Add Work Shifts

The user can add work shifts by entering a date, start time, end time, and an optional workplace.

The system saves the shifts in the SQLite database and supports overnight shifts.

### FR-02 – Edit and Delete Work Shifts

The user can edit or delete existing work shifts when their schedule changes or incorrect information has been entered.

### FR-03 – Subject Management

The user can add, edit, and save their school subjects throughout the semester.

The user can assign a difficulty level to each subject, select which subjects they want to study each day, and change their selection later.

Subjects remain saved until the user manually deletes them when they are no longer needed.

### FR-04 – Flexible Study Hours

The user can set their maximum daily study hours and adjust how that time is divided between selected subjects.

The user can save study sessions, mark them as completed or skipped, and reschedule them when needed.

The system ensures that planned study time does not exceed the user's chosen daily limit.

Skipped sessions display a reminder the following day without automatically adding extra study hours.

### FR-05 – Personalized Study Recommendations

The system can suggest how to distribute study time between the user's selected subjects based on subject difficulty, upcoming exams, and available study time.

The user can accept or modify the suggested plan.

### FR-06 – School Schedule and Event Management

The user can add, edit, and delete school hours, exams, and assignments.

Exams and study sessions can have specific times, while assignments can be recorded with deadlines without requiring a start time.

### FR-07 – Weekly Schedule Overview

The system displays work shifts, school hours, exams, assignment deadlines, and planned study sessions in a weekly schedule grouped by date.

### FR-08 – Scheduling Conflict Detection

The system detects overlapping timed activities, such as work shifts, classes, exams, and planned study sessions, and displays a warning when a conflict is found.

Assignment deadlines without scheduled time intervals are not treated as conflicts.

### FR-09 – Working Hours and Earnings Calculator

The user can enter their hourly wage.

The system calculates total scheduled working hours and estimated gross earnings based on saved shifts.

Advanced payroll calculations, such as taxes and deductions, are excluded.

### FR-10 – Input Validation

The system validates user input when adding or editing shifts, subjects, school events, and study plans.

It prevents invalid or missing required information from being saved and displays clear error messages.

## 6. Non-Functional Requirements

### NFR-01 – Usability

ShiftMate must have a simple, clear, and user-friendly interface.

Students should be able to manage their schedules and study plans without needing technical knowledge.

### NFR-02 – Responsive Design

The application must work on both desktop and mobile browsers.

The layout should adapt to different screen sizes while keeping the main features easy to access.

### NFR-03 – Performance

The application should respond quickly to user actions.

On the local development setup, the weekly schedule should load within 3 seconds when displaying up to 100 saved activities.

### NFR-04 – Data Persistence

The application must store user information in a SQLite database.

Saved shifts, subjects, school events, and study plans must remain available after the application is restarted, unless the user deletes them.

### NFR-05 – Privacy and Data Protection

ShiftMate must be designed as a local, single-user application.

Student information must not be shared with external services, and the application must not require user registration or login.

## 7. User Stories

### US-01 – Manage Work Shifts

As a student who works part-time, I want to add, edit, and delete my work shifts so that I can keep my schedule accurate when my working hours change.

### US-02 – Manage School Subjects

As a student, I want to save my subjects for the semester and choose which ones to study each day so that I can focus on the subjects I need without entering them repeatedly.

### US-03 – Manage School Events

As a student, I want to record my classes, exams, and assignment deadlines so that I can keep track of my academic responsibilities in one place.

### US-04 – Create Personalized Study Plans

As a student, I want to choose my daily study subjects, set my maximum study hours, receive personalized study recommendations, and manage my study sessions so that I can follow a realistic and flexible study plan.

### US-05 – View My Schedule and Conflicts

As a working student, I want to see my school activities, work shifts, and study sessions in one weekly schedule so that I can identify conflicts and organize my time more easily.

### US-06 – Track Working Hours and Earnings

As a working student, I want to calculate my working hours and estimated earnings so that I can keep track of how much I am working and approximately how much money I will earn.

## 8. Acceptance Criteria

### US-01 – Manage Work Shifts

- **AC-01:** PASS if the student can add a shift with a date, start time, end time, and optional workplace, and it is saved successfully.
- **AC-02:** PASS if the student can edit or delete a saved shift.
- **AC-03:** PASS if an overnight shift, such as 17:00–00:00, is saved and calculated correctly.

### US-02 – Manage School Subjects

- **AC-01:** PASS if the student can add, edit, and save subjects, including a difficulty level for each subject.
- **AC-02:** PASS if the student can select specific subjects for a study day and change that selection later.
- **AC-03:** PASS if subjects remain saved until the student manually deletes them.

### US-03 – Manage School Events

- **AC-01:** PASS if the student can add, edit, and delete classes, exams, and assignment deadlines.
- **AC-02:** PASS if an assignment can be saved with a deadline without requiring a start time.
- **AC-03:** PASS if saved school events appear on their correct dates in the weekly schedule.

### US-04 – Create Personalized Study Plans

- **AC-01:** PASS if the student can select subjects and set a maximum daily study duration.
- **AC-02:** PASS if the system suggests study-time allocations based on selected subjects, difficulty levels, upcoming exams, and available study time.
- **AC-03:** PASS if the student can manually adjust the suggested durations without exceeding their chosen daily study limit.
- **AC-04:** PASS if the student can save a study plan, mark sessions as completed or skipped, and reschedule them. Skipped sessions must display a reminder the following day without automatically adding extra study hours.

### US-05 – View My Schedule and Conflicts

- **AC-01:** PASS if the weekly schedule displays saved work shifts, school events, and planned study sessions grouped by date.
- **AC-02:** PASS if the system warns the student when two timed activities overlap.
- **AC-03:** PASS if an assignment deadline without a time interval does not trigger an overlap warning.

### US-06 – Track Working Hours and Earnings

- **AC-01:** PASS if the student can enter and save their hourly wage.
- **AC-02:** PASS if the system correctly calculates scheduled working hours, including overnight shifts.
- **AC-03:** PASS if the system displays estimated gross earnings calculated from working hours and hourly wage.

## 9. Open Questions

The following questions will be resolved before or during the design stage:

1. **Study Availability:** How should students specify their preferred study hours, and should they be able to change those hours for individual days?

2. **Study Recommendations:** What simple rules should the system use to prioritize subjects based on difficulty and upcoming exam dates?

3. **Skipped Session Reminders:** Where should the reminder for skipped study sessions appear in the application, such as on the dashboard or in the weekly schedule?