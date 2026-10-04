# Project Overview

HR Hub is a centralized Salesforce application where employees, leave requests, skills, and assets are managed as interconnected records. The system enforces data quality through validation rules, automates repetitive tasks using Flows, and ensures secure data access through a robust sharing model.

# Salesforce Features Used

This project leverages a wide array of declarative Salesforce features:
Data Modeling: Custom & Standard Objects, Custom Fields (Text, Picklist, Multi-select, Formula, Roll-up, Auto-number), Schema Builder.
UI & Navigation: Record Types, Page Layouts, Dependent Picklists, Custom Tabs, Lightning App
Data Quality: 21 Validation Rules, Lookup Filters.
Automation: Record-Triggered Flows (Before-Save & After-Save), Quick Actions, Email Alerts.
Communication: classic Email Templates, Email Alerts.

# Project Structure

The application is built around six core objects to manage the employee lifecycle:
Department: Organizational units (e.g., Engineering, HR, IT).
Employee: The central record for staff members (Full Time & Interns).
Leave Request: Tracks time-off requests and approvals.
HR Asset: Tracks company equipment (Laptops, ID Cards, etc.).
Skill & Employee Skill: Manages employee competencies using a many-to-many junction.
Contact (Standard): Repurposed to store Emergency Contacts.

# Object Realtionships

Relationships were carefully chosen to reflect real-world business logic and data lifecycle requirements:
Object
Relationship Type
Business Justification
Department
Lookup (Parent of Employee)
An employee can exist without a department, and departments are protected from deletion while employees are attached.
Employee
Self-Lookup (Manager)
The manager is also an employee within the same object.
Employee
Lookup (Login User)
Links the physical person to their Salesforce system login.
Leave Request
Master-Detail (to Employee)
A leave request has no meaning without an employee. It is deleted if the employee is deleted, and allows Roll-Up summaries on the Employee record.
HR Asset
Lookup (to Employee)
Assets can sit in stock unassigned and must survive in the system even if the assigned employee leaves.
Employee Skill
Junction (Master-Detail to Employee & Skill)
Resolves the Many-to-Many relationship between employees and skills. Holds extra data like Proficiency and Years of Use.
Contact
Lookup (to Employee)
Reused the standard Contact object for emergency contacts to avoid creating redundant custom objects.

# Validation Rules

Implemented 11 Validation Rules to ensure data quality at the point of entry (UI, API, and Imports):
Employee (7 rules):  enforces 10-digit phone numbers, ensures joining dates are within 90 days, mandates resignation dates for resigned staff, and ensures interns do not have a salary.
Leave Request (4 rules): Blocks past dates, ensures 'To' date is after 'From' date, mandates reasons for Sick leaves and Rejections, and prevents casual leaves from exceeding the remaining balance.

# Page Layouts

Record Types: The Employee object features two Record Types: Full Time and Intern.
Full Time displays Salary, Variable Pay, and Probation End Date.
Intern displays Stipend and Internship End Date, hiding salary fields.
Dependent Picklists: On Leave Requests, the Leave Sub-Type dynamically changes based on the Leave Type (e.g., selecting "Sick" only shows Fever, Surgery, Hospitalization).

# Email Templates

Configured deliverability to "All Email" and created the following Lightning Email Templates:
ET_HR_Welcome: Sent to new hires.
ET_HR_Leave_Approved: Sent to employees when their leave is approved.
ET_HR_Leave_Rejected: Sent to employees when their leave is rejected (includes the rejection reason).
Email Alert: Alert_HR_Welcome_Employee is triggered by the After-Save flow to automate the welcome email.

# Quick Actions

Created contextual Quick Actions to speed up daily HR and IT operations:
On Employee:
Request Leave: Pre-fills the employee lookup.
Issue Asset: Creates an asset with Status = Assigned and today's date.
Mark Resigned: Updates status and triggers the resignation date flow.
On Leave Request:
Approve Leave: Instantly updates status to Approved.
Reject Leave: Prompts for a mandatory Rejection Reason.

# Process Flows

Built 2 Record-Triggered Flows to automate repetitive tasks:
HR_Leave_After_Save (After-Save)
Trigger: Leave Request updated to Approved or Rejected.
Action: Emails the employee the decision. If it is a "Long Leave" (>5 days), it creates a handover task for the employee's manager.
HR_Employee_After_Save (After-Save)
Trigger: Employee created (and not Resigned).
Action: Sends the Welcome Email Alert and creates two onboarding Tasks (Prepare welcome kit, Arrange laptop/ID card).

# What i Learned

Through building the HR Hub, I reinforced several key Salesforce administration principles:
Configuration First: Leveraging declarative tools (Flows, Validation Rules) ensures the system remains agile and easily maintainable without code deployments.
Data Quality at the Source: Using Validation Rules and Lookup Filters prevents bad data from entering the system via the UI, API, or Data Loader.

# Conclusion
The HR Hub successfully transitions the HR department from fragmented spreadsheets to a unified, automated, and secure Salesforce environment. It provides real-time visibility into leave balances, automates onboarding and leave communications, and ensures company assets are tracked securely.
