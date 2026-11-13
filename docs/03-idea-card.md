### Project Ideas – ShiftMate

### Project Ideas

We explored three different ideas for our final software project. Our goal was to choose an application that would be useful, interesting to develop, and possible to complete using Node.js, Express, SQLite, HTML, CSS, and JavaScript.

### Potential Users

1. High school students who work part-time.
2. University students who need to manage their schedules.
3. People who want to track their monthly spending.
4. Students who need help organizing assignments and exams.
5. Part-time workers who want to track working hours and earnings.

### Data Opportunities

Unlike our previous project, which used an existing game dataset, these ideas would mainly use information entered by users.

We identified five possible opportunities:

1. Store user-created information in a database.
2. Organize records by dates and categories.
3. Calculate useful statistics from saved information.
4. Allow users to add, edit, and delete records.
5. Display the information in calendars, lists, or dashboards.

### Idea 1 – MoneyWise

## User

People who want to manage their personal finances, especially students and young adults.

## Problem

Many people find it difficult to keep track of their income, expenses, and savings. Without a clear overview, they may spend more than expected or struggle to reach savings goals.

## Data

• The application would use:
• Income and expense amounts
• Transaction dates
• Expense categories
• Monthly budgets
• Savings goals

## Main Flow

1. The user opens the website.
2. The user adds their income and expenses.
3. The system saves the transactions.
4. The dashboard displays income, spending, and remaining money.
5. The user views charts and tracks savings progress.

## Why could this be a good project?

MoneyWise would be useful in everyday life. It would allow us to work with databases, calculations, charts, and interactive dashboards.

## Main Risks

• Financial calculations must be accurate.
• Users could enter incorrect amounts.
• The interface could become confusing if too many features are included.
• Financial information must be handled carefully.

### Idea 2 – ShiftMate

## User

Students who work part-time while attending school or university.

## Problem

Working students often struggle to organize work shifts, exams, assignments, and study time.

Managing these activities separately can lead to scheduling conflicts, missed deadlines, and confusion about working hours and estimated earnings.

## Data

• The application would use:
• Work shift dates and times
• Hourly wage
• School events and deadlines
• Exam dates
• Study sessions
• Calculated working hours and estimated earnings

## Main Flow

1. The user opens the ShiftMate website.
2. The user adds upcoming work shifts.
3. The user adds school events, exams, and deadlines.
4. The system saves the information in a SQLite database.
5. The user views work and school activities in one calendar.
6. The system calculates working hours and estimated gross earnings.
7. The system warns the user when timed work and school activities overlap.

## Why could this be a good project?

ShiftMate solves a real problem for working students.

It combines several interesting programming features, including database management, time calculations, scheduling, conflict detection, and interactive dashboards.

It also has opportunities for future improvements.

## Main Risks

• Shifts that continue past midnight may be difficult to calculate.
• Overlapping schedules must be detected correctly.
• Salary estimates may differ from actual pay.
• The application must remain simple and easy to navigate.

### Idea 3 – StudyFlow

## User

Students who want to organize their schoolwork and prepare for exams.

## Problem

Students may struggle to keep track of assignments, deadlines, and study sessions, especially when they have several subjects.

They need one place to organize tasks and see their progress.

## Data

The application would use:

• School subjects
• Assignments and deadlines
• Exam dates
• Task priorities
• Task completion status
• Study sessions

## Main Flow

1. The user opens the website.
2. The user adds subjects and assignments.
3. The user sets deadlines and priorities.
4. The dashboard displays upcoming tasks.
5. The user marks completed assignments.
6. The system updates the progress overview.

## Why could this be a good project?

StudyFlow would be relatively straightforward to develop and test. It would demonstrate database operations, task management, and progress tracking.

## Main Risks

It may be too similar to existing task management applications.

The project could become too simple.

Managing many tasks and deadlines could make the interface crowded.

### Selected Idea

I chose ShiftMate – Smart Work & Study Schedule Manager.

### Reason

I selected ShiftMate because it solves a real problem for students who balance school and part-time work.

The application is more than a simple task list. It combines work scheduling, school planning, salary calculations, and conflict detection in one system.

I believe the project is interesting, useful, and challenging enough for our final software project while still being realistic to develop step by step.

### Project Statement

I am building a web application for students who work part-time that helps them manage their work shifts and school responsibilities by combining schedules, calculating estimated earnings, and detecting scheduling conflicts.
