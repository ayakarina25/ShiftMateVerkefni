# Requirements – ShiftMate

## 1. Purpose

ShiftMate helps students who work part-time organize school, study time, and work in one application. It lets students manage schedules, create flexible study plans, identify conflicts, and estimate working hours and gross earnings.

Its main goal is to make time management easier without expecting students to study during every free hour.

## 2. Primary User

The primary user is a high school or university student who works part-time. The student may have multiple subjects, classes, exams, assignment deadlines, and work shifts, and needs a practical way to balance them.

ShiftMate is designed as a local, single-user web application rather than a general-purpose calendar or a multi-user service.

## 3. Problem

Working students often struggle with two connected problems: **finding time to study** and **deciding how to divide that time between subjects**. Separate school and work schedules can also cause conflicts and make working hours difficult to track.

ShiftMate brings these responsibilities together and offers **rule-based study-time recommendations** that the student can adjust to fit their energy and priorities.

## 4. Scope and Out of Scope

### Included in the MVP

- Work-shift management and simple earnings estimates.
- Subject, class, exam, and assignment management.
- A weekly schedule grouped by date, with overlap warnings.
- Student-entered daily study limits and rule-based time recommendations.
- Study sessions that can be completed, skipped, or manually rescheduled, with an in-app reminder for skipped sessions.

### Out of Scope

- Registration, login, or multiple user accounts.
- Connections to school or employer systems; automatic shift swapping.
- Tax, overtime, allowance, or unpaid-break calculations.
- Automatic detection of free study periods or automatic placement of study sessions into calendar gaps.
- AI chatbots, machine learning, or claims of an optimal study schedule.
- Email, SMS, or push notifications; a native mobile app.
- A full drag-and-drop calendar or complex recurring-event system.

The application will use **Node.js, Express, JavaScript, and SQLite**. The weekly view will be a straightforward date-grouped list that works in desktop and mobile browsers.

## 5. Functional Requirements

### FR-01 – Add Work Shifts

The student can add a shift with a date, start time, end time, and optional workplace. Shifts are saved in SQLite. A shift with an end time earlier than its start time continues into the next day (for example, 17:00–00:00).

### FR-02 – Edit and Delete Work Shifts

The student can edit or delete a saved shift if the details change or were entered incorrectly. Only saved shifts count toward work-hour and earnings estimates; shift cancellation statuses are not part of the MVP.

### FR-03 – Manage Subjects

The student can add, edit, and save subjects for the semester, assign each an **Easy, Medium, or Difficult** level, and choose which saved subjects to study on a particular day.

Subjects stay saved until manually deleted. Deleting a subject requires confirmation and also deletes its linked study sessions.

### FR-04 – Flexible Study Sessions

The student enters a **maximum study duration for each day**, selects subjects, and can save individual study sessions.

Each session has a subject, date, duration, an optional start time, and a status of **Planned, Completed, or Skipped**. A daily plan is the collection of sessions for that date.

The student can edit durations, mark sessions completed or skipped, and manually move a session to another date or time.

The total duration of **Planned and Completed** sessions cannot exceed that day's limit. Skipped sessions do not count toward the active total.

A session skipped yesterday appears in a simple dashboard reminder today, but ShiftMate does **not** add extra study hours automatically.

### FR-05 – Rule-Based Study Recommendations

The student selects subjects and enters a daily study limit.

ShiftMate suggests how to divide that time **between selected subjects only**, using subject difficulty and the date of the nearest upcoming exam for each subject.

More difficult subjects and subjects with nearer exams receive higher priority.

The recommendations must not exceed the student's chosen daily limit and can be accepted, edited, or ignored.

Recommendations are **time allocations**, not automatically chosen clock times. The student can optionally add a start time to a session afterward.

### FR-06 – Manage School Events

The student can add, edit, and delete **classes, exams, and assignments**.

- A class has a date, start time, and end time.
- An exam has a date and may have a start/end time pair.
- An assignment has a deadline date and may have a due time, but does not have a start/end interval.

Study sessions are managed separately under FR-04, not duplicated as school-event records.

### FR-07 – Weekly Schedule

ShiftMate shows work shifts, classes, exams, assignment deadlines, and study sessions in a weekly list grouped by date.

The week starts on **Monday**. Students can view previous and future weeks.

Sessions without a start time appear under their date as **Time not set**. Overnight shifts show that they end the next day.

### FR-08 – Conflict Warnings

ShiftMate warns when two **timed intervals** overlap, including overnight shifts that overlap an event the next day.

An event ending exactly when another begins is **not** a conflict.

Untimed exams, assignment deadlines, and study sessions without a start time do not create interval conflicts.

A warning does not automatically delete or move an activity.

### FR-09 – Work Hours and Estimated Earnings

The student saves **one hourly wage**.

ShiftMate calculates the total duration of shifts whose **start dates fall within the selected week**, and estimates gross earnings as:

**Estimated gross earnings = Shift hours × Hourly wage**

All saved shifts in that week count, whether in the past or future.

No breaks, taxes, premiums, or deductions are included. Results are estimates, not payslips.

### FR-10 – Validation and Feedback

ShiftMate checks required fields, allowed values, valid dates and times, daily study limits, and non-negative wages before saving.

It displays clear messages for invalid input, empty schedules, unavailable study recommendations, conflicts, and failed database operations.

Invalid input must not create or overwrite a database record.

## 6. Shared Rules and Validation

These rules make the functional requirements consistent and testable.

| Area | Rule |
|---|---|
| Date and Time | Use local device time, YYYY-MM-DD dates, and 24-hour HH:MM times. One local time zone is assumed. |
| Week | Monday through Sunday. Past and future activities remain visible. |
| Overnight Shifts | If the shift end time is earlier than its start time, it is next day. Equal start and end times are invalid. A shift must be shorter than 24 hours. |
| Classes and Timed Exams | Start and end must both be present. End must be later than start on the same day. An exam may instead have neither time. |
| Assignment Deadlines | Require a due date. A due time is optional. Deadlines are not timed intervals and never trigger overlap warnings on their own. |
| Subject Difficulty | Exactly Easy, Medium, or Difficult. Subject names cannot be blank. |
| Study Sessions | Require a saved subject, date, and positive duration in 15-minute increments. Start time is optional. When present, the calculated end must remain on the same day. |
| Daily Study Limit | Entered manually for each study day. Planned plus Completed session durations must fit the limit. Skipped sessions are excluded. |
| Wage | One non-negative hourly wage. The same wage and currency unit apply to all saved shifts. |
| Delete Subject | Require confirmation. Linked study sessions are also deleted. |

### Recommendation Rules for the MVP

The recommendation feature is a simple calculation, **not AI**.

1. Give subjects base weights:
   - Easy = 1
   - Medium = 2
   - Difficult = 3

2. Add priority based on upcoming exams:
   - Exam within 0–7 days: +2
   - Exam within 8–14 days: +1
   - No upcoming exam within 14 days: +0
   - Ignore past exams.

3. Split the student's daily study limit proportionally between selected subjects according to their weights. Use **15-minute blocks**, assigning remaining blocks to the highest-priority subject.

4. Never exceed the daily study limit.

5. If there is not enough time to assign at least one 15-minute block per selected subject, display a message asking the student to choose fewer subjects or increase the limit.

6. If no subjects are selected, display a helpful message.

7. Allow the student to change or reject all suggested allocations.

**Example:**

A student has 120 minutes available for studying.

- Mathematics: Difficult, no upcoming exam, weight 3.
- English: Easy, no upcoming exam, weight 1.

ShiftMate suggests:

- Mathematics: 90 minutes.
- English: 30 minutes.

If English has an exam within seven days, its weight becomes 3.

The new recommendation becomes:

- Mathematics: 60 minutes.
- English: 60 minutes.

### Additional Implementation Rules

**Skipped Session Reminders**

Skipped-session reminders will appear in a small section on the weekly schedule page. A separate dashboard is not required. The reminder will appear the following day without automatically adding new study hours.

**Subject Selection**

Selecting subjects for a day is used to generate study recommendations. It does not automatically create or save study sessions. The student must accept a recommendation or manually create a session.

**Daily Study Limits**

Daily study limits must be non-negative whole numbers of minutes. A limit of zero is allowed, but no study sessions can be planned or recommended for that day.

Individual study sessions must have positive durations in 15-minute increments.

**Recommendation Rounding**

Recommendations use complete 15-minute blocks. If a daily limit is not divisible by 15, the remaining minutes are left unused.

Recommended durations must never exceed the daily limit.

**Equal Recommendation Priorities**

If subjects have equal priority during the distribution of remaining study blocks, the system uses the following order:

1. Earlier upcoming exam date.
2. Higher subject difficulty.
3. Alphabetical subject name.

For proportional allocation, initial shares are rounded down to complete 15-minute blocks, and remaining blocks are assigned by largest fractional remainder, using the above tie-breakers when needed.

**Exam Time Validation**

An exam may have both a start and end time or neither. Providing only one time is invalid. When both times are provided, the end time must be later than the start time.

## 7. Non-Functional Requirements

### NFR-01 – Usability

The interface must have clear labels, navigation, buttons, and helpful empty/error states so that a student can use the main features without technical knowledge.

### NFR-02 – Responsive Design

The application must remain readable and usable in a desktop browser at **1280 px** width and a mobile browser at **375 px** width, without horizontal scrolling for the main schedule and forms.

### NFR-03 – Performance

On the developer's computer using a local SQLite database and a current desktop Chrome browser, the weekly schedule should finish loading and rendering within **3 seconds** after navigating to the page, with **100 saved activities** (shifts, school events, and study sessions) in the database.

### NFR-04 – Data Persistence and Reliability

SQLite must retain saved information after restarting the application.

Failed save operations must display an error instead of falsely reporting success.

### NFR-05 – Privacy

ShiftMate is a local, single-user application with no login or external sharing of schedules.

The project must not expose students' schedule data through public sample deployments or third-party services.

## 8. User Stories

### US-01 – Manage Work Shifts

As a student who works part-time, I want to add, edit, and delete work shifts so that my schedule stays accurate when my working hours change.

### US-02 – Manage School Subjects

As a student, I want to save subjects for the semester and choose which ones to study each day so that I can focus on what I need without re-entering subject names.

### US-03 – Manage School Events

As a student, I want to record classes, exams, and assignment deadlines so that I can keep my academic responsibilities in one place.

### US-04 – Create Flexible Study Plans

As a student, I want to choose subjects, set a daily study limit, receive simple recommendations, and complete, skip, or reschedule sessions so that my study plan matches my actual day.

### US-05 – View My Weekly Schedule and Conflicts

As a working student, I want to see work, school, and study activities in one weekly view so that I can notice overlapping commitments.

### US-06 – Estimate Work Hours and Earnings

As a working student, I want to see scheduled work hours and approximate earnings so that I can understand how much I expect to work and earn.

## 9. Acceptance Criteria

Each user story has **2–4 acceptance criteria**, with unique IDs for easier test tracking.

### US-01 – Manage Work Shifts

- **US-01-AC-01:** PASS if a shift with date, start time, end time, and optional workplace is saved and appears in the schedule.
- **US-01-AC-02:** PASS if the student can edit or delete a saved shift and the schedule reflects the change.
- **US-01-AC-03:** PASS if a shift from 17:00 to 00:00 is stored as 7 hours, ending the next day.
- **US-01-AC-04:** PASS if a shift with missing required fields or equal start/end times is rejected with a clear message and is not saved.

### US-02 – Manage School Subjects

- **US-02-AC-01:** PASS if a subject can be added or edited with a name and one of the three defined difficulty levels.
- **US-02-AC-02:** PASS if the student can select saved subjects for a day and change the selection later.
- **US-02-AC-03:** PASS if subjects remain saved after the application restarts.
- **US-02-AC-04:** PASS if deleting a subject requires confirmation and also removes its related study sessions.

### US-03 – Manage School Events

- **US-03-AC-01:** PASS if the student can add, edit, and delete classes, exams, and assignment deadlines.
- **US-03-AC-02:** PASS if an assignment with a deadline date but no time is saved and appears once on the correct day.
- **US-03-AC-03:** PASS if a saved class or timed exam appears under its date in the weekly schedule.
- **US-03-AC-04:** PASS if a class with missing start/end time or an invalid time range is rejected without saving.

### US-04 – Create Flexible Study Plans

- **US-04-AC-01:** PASS if the student can select subjects, set a daily study limit, and save sessions whose total active duration fits that limit.
- **US-04-AC-02:** PASS if a 120-minute recommendation for Difficult Mathematics and Easy English with no upcoming exams suggests 90 and 30 minutes, and nearer exams increase priority as defined in Section 6.
- **US-04-AC-03:** PASS if the student can edit or reject recommendations, but cannot save Planned plus Completed sessions that exceed the daily limit.
- **US-04-AC-04:** PASS if the student can mark a session Completed or Skipped or manually reschedule it. A session skipped yesterday produces an in-app reminder today without automatically adding study time.

### US-05 – View My Weekly Schedule and Conflicts

- **US-05-AC-01:** PASS if the selected Monday–Sunday week displays saved shifts, classes, exams, deadlines, and study sessions once under the correct dates.
- **US-05-AC-02:** PASS if two timed activities that overlap (for example, 09:00–10:30 and 10:00–11:00) produce a conflict warning.
- **US-05-AC-03:** PASS if activities that only touch at a boundary (09:00–10:00 and 10:00–11:00) do not produce a warning.
- **US-05-AC-04:** PASS if an overnight shift conflicts with a next-day timed activity when appropriate, while an assignment deadline without a time interval does not create a conflict.

### US-06 – Estimate Work Hours and Earnings

- **US-06-AC-01:** PASS if the student can save one hourly wage and a negative wage is rejected.
- **US-06-AC-02:** PASS if an overnight 17:00–00:00 shift counts as 7 hours.
- **US-06-AC-03:** PASS if a 7-hour shift and an hourly wage of 2,000 yield estimated gross earnings of 14,000 in the same currency unit.
- **US-06-AC-04:** PASS if the weekly total includes all saved shifts starting in the selected week, with no tax or break deductions.

## 10. Representative Test Cases

These checks can be manual tests or automated tests during implementation.

- **Persistence:** Restart the app and verify saved shifts, subjects, events, and study sessions remain.
- **Empty State:** Open a new database and verify the schedule explains that no activities have been added.
- **Invalid Data:** Attempt to save a negative wage, empty subject name, equal shift times, or study sessions over the daily limit. Verify no invalid record is saved.
- **Overnight Shift:** Save Monday 22:00–Tuesday 02:00 and verify a Tuesday 01:00–02:00 class conflicts, while a Tuesday 02:00–03:00 class does not.
- **Study Planner:** Verify the 90/30 and 60/60 examples from Section 6, including 15-minute increments and the daily cap.
- **Skipped Sessions:** Mark a session skipped, open the dashboard the following day, and verify a reminder appears without modifying that day's planned hours.
- **Database Error:** Simulate a failed save and verify the user sees an error, not a success message.

## 11. Open Questions

These are optional design decisions, not blockers for the MVP.

1. Should the student be able to save a **default daily study limit**, rather than entering it separately for each day?
2. Would a preferred study window (for example, 15:00–21:00) be useful as a future enhancement? For the MVP, the student sets durations and any start times **manually**.
3. Should the skipped-session dashboard reminder include a quick **Reschedule** button, or only a link to the session?

## 12. Decisions from Copilot Agent Review

**Accepted:**

Clarify time/date rules, validation, subject difficulty, study-session records, conflict boundaries, earnings, error states, and concrete tests.

Define recommendations as a small rule-based calculation.

**Adapted:**

Use a student-entered daily study limit rather than automatically calculating free time.

Keep a date-grouped weekly list instead of a full calendar.

**Kept in Scope:**

Completing, skipping, and manually rescheduling study sessions, plus a simple dashboard reminder.

These are important to ShiftMate's flexibility and do not need advanced automation.

**Deferred:**

Automatic free-slot scheduling, advanced rescheduling suggestions, and external notifications.