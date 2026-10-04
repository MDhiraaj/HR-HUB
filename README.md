Project Overview

HR Hub is a Salesforce application built to manage core HR
information in one place. It manages departments, employees, skills,
leave requests, employee skills, emergency contacts, and HR assets
through declarative Salesforce configuration.

Business Requirement

An HR team needs a structured system to:

Maintain employee information

Organize departments

Track leave requests

Record employee skills

Maintain emergency contacts

Manage assets issued to employees

Connect all HR records in Salesforce

Project Outcomes

Maintain accurate employee and department records.

Ensure data quality using required fields, formulas, dependent
picklists, and validation rules.

Provide a simple HR interface using record types, page layouts,
tabs, and list views.

Project Flow

The project was built in the following sequence:

Step                    Configuration           Purpose

1                       Profile shells          Created HR Manager and
HR Employee profiles as
the base setup for HR
Hub users.

2                       Custom objects          Created Department,
Employee, Skill, Leave
Request, HR Asset, and
Employee Skill objects.

3                       Custom fields           Added HR-specific
fields such as Employee
Code, Status, Joining
Date, Leave Balance,
Asset Type, and
Proficiency.

4                       Relationships           Connected objects using
Lookup, Self-Lookup,
Master-Detail, and
Junction relationships.

5                       Standard-object         Extended Contact to
customization           store employee
emergency-contact
details.

6                       Dependent picklist      Configured Leave Type
as the controlling
field for Leave
Sub-Type.

7                       Record types and        Created Full Time and
layouts                 Intern employee
experiences with
separate layouts and
picklist values.

8                       Validation rules        Added business rules to
prevent invalid
employee, leave, skill,
and contact records.

9                       HR Hub app              Created object tabs and
added them to the HR
Hub Lightning app.

10                      List views and data     Created focused list
views and entered
realistic HR test data.

Data Model

The Employee object is the central object. Other objects either
support employee information or are related to employees.

Object                              Purpose

Department                      Stores department details such as
HR, Engineering, Finance, and IT
Support.

Employee                        Stores employee identity,
employment, manager, department,
leave, and related information.

Skill                           Stores a reusable list of
professional and technical skills.

Leave Request                   Stores employee leave type, dates,
reason, status, and calculated
number of days.

HR Asset                        Stores company assets such as
laptops, mobiles, ID cards, and
headsets.

Employee Skill                  Connects employees and skills and
stores proficiency, years of use,
and certification status.

Contact                         Standard Salesforce object extended
to store emergency contacts for
employees.

Relationship Design

Relationship            Implementation          Explanation

Employee → Department   Lookup                  An employee belongs to
a department, while
Department and Employee
remain independent
records.

Employee → Manager      Self-Lookup             A manager is also an
employee, so Employee
looks up to Employee.

Leave Request →         Master-Detail           A leave request belongs
Employee                                        to one employee and
supports roll-up
summaries on Employee.

HR Asset → Employee     Lookup                  An asset can remain in
stock even when it is
not assigned to an
employee.

Employee ↔ Skill        Junction Object         Employee Skill supports
the many-to-many
relationship between
employees and skills.

Employee → Login User   Lookup                  Links an employee
record to the
Salesforce user who
logs in.

Relationship Design Explanation

Master-Detail for Leave Request: A leave request has no
independent business value without its employee and supports roll-up
summaries.

Lookup for HR Asset: An asset can exist in inventory before it
is issued to an employee.

Employee Skill as a Junction Object: Employees and skills have a
many-to-many relationship.

Custom Fields

The application uses multiple Salesforce field types:

Text

Email

Phone

Number

Currency

Percent

Date

Date/Time

Checkbox

URL

Picklist

Multi-Select Picklist

Formula

Roll-Up Summary

Auto Number

Field Examples

Area                                Examples

Employee                            Employee Code, Joining Date,
Status, Designation, Languages
Known, Leave Balance, Years of
Service, Remaining Leave, Status
Flag

Leave Request                       Leave Type, Leave Sub-Type, From
Date, To Date, Reason, Status,
Days, Long Leave

HR Asset                            Asset Type, Serial Number, Status,
Assigned Date, Purchase Cost,
Warranty Expiry, Warranty Active

Employee Skill                      Proficiency, Years of Use,
Certified

Formulas and Roll-Up Summaries

Feature                             Purpose

Years of Service                Calculates employee service length
from Joining Date.

Days                            Calculates leave days using To Date
minus From Date plus one.

Long Leave                      Identifies leave requests longer
than five days.

Warranty Active                 Checks whether Warranty Expiry is
today or later.

Total Approved Leave Days       Sums approved leave days on
Employee.

Total Leave Requests            Counts leave requests related to an
Employee.

Skill Count                     Counts Employee Skill records for
an Employee.

Employee Count                  Counts Employee Skill records for a
Skill.

Record Types and Page Layouts

The Employee object uses two record types:

1. Full Time

The Full Time layout shows:

Employment information

Compensation fields

Probation information

Leave balance

Exit information

Full-time designation values include:

Associate

Consultant

Senior Consultant

Manager

2. Intern

The Intern layout shows:

Internship End Date

Stipend

Internship-related information

Intern designation values include:

Trainee Intern

Project Intern

Employee Record Page

The Employee compact layout displays:

Employee Name

Department

Status

Manager

Related lists provide access to:

Leave Requests

Assets

Employee Skills

Emergency Contacts

Direct Reports

Dependent Picklist

Leave Type is the controlling field and Leave Sub-Type is the
dependent field.

Leave Type   Leave Sub-Types

Sick         Fever, Surgery, Hospitalization
Casual       Personal, Family Event
Earned       Vacation, Travel
Unpaid       Personal

This configuration guides users to select valid leave sub-types based on
the selected leave category.

Validation Rules

Validation rules protect data quality by blocking a record when a
business condition is invalid.

Employee

Employee cannot be their own manager.

Joining Date cannot be too far in the future.

Resignation Date is required when Status is Resigned.

Experience must be within a valid range.

Intern

Internship End Date is mandatory for an Intern.

Internship End Date must be after Joining Date.

Leave Request

To Date cannot be before From Date.

Sick leave requires a reason.

Leave Sub-Type is required.

Rejected leave requires a rejection reason.

Leave cannot exceed 30 days.

Employee Skill

Years of Use must be within the permitted range.

Department

An active department requires a Department Head.

Emergency Contact

An emergency contact requires a phone or mobile number.

HR Hub Lightning App and List Views

The HR Hub Lightning app provides a single navigation area for:

Departments

Employees

Leave Requests

Skills

HR Assets

Contacts

List Views

Object                              List Views

Employee                            All Employees, Active Employees,
Onboarding Employees, Interns,
Full-Time Employees, Joined This
Year, On Leave Today

Leave Request                       All Leave Requests, Pending Leaves,
Approved Leaves, Long Leaves,
Leaves This Month

HR Asset                            All Assets, Available Assets,
Assigned Laptops, Out of Warranty

Department                          Active Departments

Skill                               Salesforce Skills

Test Data

Departments

Engineering

HR

Finance

Sales

IT Support

Skills

Apex

Flows

LWC

Agentforce

Communication

Project Management

Employees

Type        Employee       Code     Department    Status       Manager

Full Time   Anita Sharma   EMP001   HR            Active       ---
Full Time   Ravi Kumar     EMP002   Engineering   Active       ---
Full Time   Priya Reddy    EMP003   Engineering   Active       Ravi Kumar
Full Time   Arjun Nair     EMP004   Engineering   Active       Ravi Kumar
Full Time   Suresh Iyer    EMP005   IT Support    Active       ---
Full Time   Meena Das      EMP006   Finance       Active       ---
Intern      Rohit Verma    EMP007   HR            Onboarding   Anita Sharma
Intern      Sneha Rao      EMP008   Engineering   Onboarding   Ravi Kumar

Leave Requests

Employee   Type       Sub-Type   From         To           Status     Reason

Priya      Casual     Personal   2026-10-12   2026-10-14   Pending    Family
Reddy                                                                 event

Arjun Nair Sick       Fever      2026-10-20   2026-10-21   Approved   Viral
fever

Meena Das  Earned     Vacation   2026-11-02   2026-11-08   Approved   Family
vacation

Rohit      Casual     Personal   2026-10-19   2026-10-20   Rejected   Project
Verma                                                                 release

Sneha Rao  Unpaid     Personal   2026-10-26   2026-10-27   Pending    Personal
work

HR Assets

Asset Type    Serial Number   Status      Assigned To

Laptop        LAP-DELL-001    Assigned    Priya Reddy
Laptop        LAP-HP-002      Available   ---
Mobile        MOB-SAM-003     Assigned    Ravi Kumar
ID Card       ID-EMP-004      Assigned    Arjun Nair
Headset       HST-005         Available   ---
Access Card   AC-007          Assigned    Suresh Iyer

Employee Skills

Employee       Skill           Proficiency      Years

Ravi Kumar     Apex            Advanced             6
Priya Reddy    Flows           Intermediate         2
Arjun Nair     LWC             Intermediate         3
Anita Sharma   Communication   Expert               8
Suresh Iyer    Communication   Advanced             7
Meena Das      Agentforce      Beginner             1

Demo Flow

The following sequence can be used for a project demonstration:

Time                    Demo                    Explanation

0:00--0:45              HR Hub App              Introduce the
application and explain
how it centralizes HR
records.

0:45--2:00              Schema Builder          Explain Employee as the
central object and its
relationships with
other objects.

2:00--3:15              Employee Record Types   Demonstrate Full Time
and Intern record types
with different layouts
and picklist values.

3:15--4:30              Employee Record         Show employee
information,
department, manager,
leaves, assets, and
skills.

4:30--5:45              Leave Request           Demonstrate dependent
picklists and
formula-driven Days and
Long Leave fields.

5:45--6:45              Validation Test         Show how validation
rules prevent invalid
data.

6:45--7:45              Employee Skill          Explain the junction
object and many-to-many
relationship.

7:45--8:45              HR Asset                Explain why Lookup is
used for assets.

8:45--9:30              List Views              Demonstrate operational
views such as Active
Employees, Pending
Leaves, and Available
Assets.

Demo Tests

Test                    Action                  Expected Result

Record Type             Click New on Employees  Full Time and Intern
choices appear.

Intern Layout           Create an Intern        Internship fields and
intern designation
values appear.

Dependent Picklist      Set Leave Type = Sick   Only Fever, Surgery,
and Hospitalization
appear.

Formula                 Create leave from 12    Days becomes 3.
Oct to 14 Oct

Long Leave              Create a 7-day leave    Long Leave becomes
checked.

Validation              Set To Date before From Salesforce prevents
Date                    save and displays an
error.

Validation              Set Status = Resigned   Salesforce prevents
without Resignation     save and displays an
Date                    error.

Relationship            Open Ravi Kumar         Priya Reddy and Arjun
Nair appear as direct
reports when manager
values are set.

Junction Object         Open Apex Skill         Related list shows
employees connected to
Apex.

Common Project Questions and Answers

Why did you use Master-Detail for Leave Request?

Leave is dependent on Employee, and the relationship supports roll-up
summaries on Employee.

Why is HR Asset a Lookup?

An asset can exist independently in stock and can be assigned to an
employee later.

Why do you need Employee Skill?

Employee Skill is the junction object that resolves the many-to-many
relationship between Employee and Skill.

What is the difference between Formula and Roll-Up Summary?

A Formula calculates a value from fields on the record or parent.

A Roll-Up Summary aggregates values from related child records.

Why use Record Types?

Record Types provide different layouts and picklist options for Full
Time and Intern employees.

What is a Dependent Picklist?

A dependent picklist restricts valid dependent values based on a
controlling picklist. In HR Hub, Leave Sub-Type depends on Leave Type.

What does a Validation Rule do?

A validation rule blocks a record from being saved when a defined
business condition is invalid, helping maintain data quality.

Why customize Contact?

Contact is a standard Salesforce object. It was extended to capture
employee emergency-contact information.

Key Salesforce Admin Concepts Demonstrated

This project demonstrates:

Salesforce data modelling

Custom objects and fields

Standard-object customization

Lookup relationships

Self-Lookup relationships

Master-Detail relationships

Junction objects

Formula fields

Roll-Up Summary fields

Dependent picklists

Record Types

Page Layouts

Validation Rules

Lightning App configuration

Tabs

List Views

Schema Builder

Sample/test data

Final Project Summary

HR Hub is a Salesforce Admin project for HR operations management.
It provides a structured way to manage departments, employees, skills,
leaves, assets, and emergency contacts.

The project connects these records using Lookup, Self-Lookup,
Master-Detail, and Junction relationships. It also uses formulas,
roll-up summaries, dependent picklists, record types, page layouts,
validation rules, tabs, list views, and sample data.

The result is a structured and user-friendly HR application that
improves data consistency and gives HR a single place to manage employee
operations.

Project Architecture at a Glance

                         ┌──────────────┐
                         │  Department  │
                         └──────┬───────┘
                                │ Lookup
                                ▼
┌────────────┐          ┌──────────────┐          ┌──────────────┐
│   Contact  │◄─────────│   Employee   │─────────►│  HR Asset    │
└────────────┘  Lookup  └──────┬───────┘  Lookup  └──────────────┘
                                │
                    ┌───────────┼───────────┐
                    │           │           │
              Master-Detail  Self-Lookup  Lookup
                    │           │           │
                    ▼           ▼           ▼
              ┌──────────┐ ┌──────────┐ ┌──────────┐
              │  Leave   │ │ Manager  │ │   User   │
              │ Request  │ │ Employee │ │  Login   │
              └──────────┘ └──────────┘ └──────────┘

                         Employee
                            │
                         Junction
                            ▼
                     ┌──────────────┐
                     │Employee Skill│
                     └──────┬───────┘
                            │
                         Lookup
                            ▼
                       ┌─────────┐
                       │  Skill  │
                       └─────────┘

Author

Mandala Sai Dhiraj

Project: HR Hub -- Salesforce Admin Project
