# SchoolBridge — Screen & Flow Inventory

**Status:** Working document — next product deliverable.

The purpose of this inventory is to translate approved business requirements into explicit screens, user actions, rules, outcomes, and notifications before any production coding begins.

## Parent Mobile App

| ID | Screen | Purpose | Priority | Status |
|---|---|---|---|---|
| P01 | Login / OTP | Authenticate registered parent | Must | To detail |
| P02 | Home Dashboard | Daily overview of each child | Must | To detail |
| P03 | Child Switcher | Switch between linked children | Must | To detail |
| P04 | Attendance | View daily / monthly / term attendance | Must | To detail |
| P05 | Homework | View subject-wise assignments and attachments | Must | To detail |
| P06 | Notices | View school / class announcements | Must | To detail |
| P07 | Fees | View dues, history, and payment state | Must | To detail |
| P08 | Payment | Initiate supported fee payment | Must/Phase 1B | To detail |
| P09 | Leave Request | Submit leave request | Must | To detail |
| P10 | Leave History | Track approved / rejected / pending requests | Must | To detail |
| P11 | Notifications | Consolidated alert timeline | Must | To detail |
| P12 | Calendar | View important school dates | Should | To detail |
| P13 | More / Settings | Profile, receipts, downloads, support | Should | To detail |

## Teacher Web Experience

| ID | Screen | Purpose | Priority | Status |
|---|---|---|---|---|
| T01 | Teacher Home | Daily work summary | Must | To detail |
| T02 | My Classes | Select assigned class / section | Must | To detail |
| T03 | Mark Attendance | Record daily attendance quickly | Must | To detail |
| T04 | Homework | Create / edit homework | Must | To detail |
| T05 | Class Notices | Publish targeted class communication | Must | To detail |
| T06 | Leave Review | Approve / reject assigned leave requests | Must | To detail |
| T07 | Student List | View students in assigned classes | Must | To detail |

## School Admin Web Portal

| ID | Screen | Purpose | Priority | Status |
|---|---|---|---|---|
| A01 | Admin Dashboard | School operational overview | Must | To detail |
| A02 | Student Management | Add / edit / import students | Must | To detail |
| A03 | Parent Management | Manage parent accounts / relationships | Must | To detail |
| A04 | Teacher Management | Manage teachers and class assignments | Must | To detail |
| A05 | Classes / Sections | Configure academic structure | Must | To detail |
| A06 | Attendance Admin | View / correct / report attendance | Must | To detail |
| A07 | Homework Oversight | View posted homework | Should | To detail |
| A08 | Notices | Create targeted school communication | Must | To detail |
| A09 | Leave Administration | Review and report leave workflow | Must | To detail |
| A10 | Fee Setup | Configure fees / dues / discounts | Must | To detail |
| A11 | Fee Dashboard | View collections / pending dues | Must | To detail |
| A12 | Imports / Exports | Bulk onboarding and controlled exports | Must | To detail |
| A13 | Roles & Access | Configure authorized users and roles | Must | To detail |
| A14 | School Settings | School-level configuration | Must | To detail |

## Screen Definition Template

For every screen above, complete the following before implementation:

- User / role
- Purpose
- Entry point
- Data displayed
- Inputs
- Available actions
- Business rules
- Validation rules
- Result / output
- Notifications / events generated
- Permissions
- Error / empty states
- Audit requirements
- Dependencies
- Acceptance criteria

## First End-to-End Flow to Define

**Attendance Alert Flow**

Teacher selects class → marks attendance → submits → system validates → attendance saved → absent student's parent identified → parent notification generated → parent opens SchoolBridge → sees child's attendance status and attendance history.
