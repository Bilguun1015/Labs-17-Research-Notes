**Research list:**
- Azure
- Node js Admin Panel 

**Things I found**

Azure - 

Admin Panel Frameworks for NodeJs - AdminBro, opensource admin panel framework works specially with React/Redux. 
Express Admin - Nodejs tool for easy creation of admin interface
rest-admin-dashboard: https://steelkiwi.com/blog/add-an-admin-panel-to-nodejs-project/


**Searching Through the Database**


tables with student_id column:
- Attendance
- ContactLog
- CourseEnrollment
- InvoiceLineItem
- PlacementExam
- ProgressReport
- ReceiptLineItem
- SectionExam
- Student


tables with course_id column:
- CourseEnrollment
- GeneralCourse
- InvoiceLineItem
- Meeting
- ProgressReport
- ReceiptLineItem
- SectionExam

**All the tables with their properties**


| Table Name       | Columns |
| ---------------  | ---------------------------------------- |
| Attendance       | notes, meeting_id, student_id, attendance|
| Block            | block_id, neighborhood|
| Calendar         | public_school, int_sec_open, calendar_date, lower_primary_open, activity, upper_primary_open|
| ContactLog       | follow-up_required, follow-up_result, person_contacting, contact_id, request_date, request_time, person_requesting, student_id, reason, contact_date, contact_time, telephone_number, person_contacted, Outcome|
| ContactType      | method|
| CourseEnrollment | course_id, student_id, first_day, last_day, result, notes|
| CourseLength     | meetings|
| CourseSchedule   | ID, long_description, sql, short_description|
| CourseType       | type_id, description|
| GeneralCourse    | hourly_rate, course_id, legacy_id, term, course_type, gender, group_type, grade_level, level,   section, subsection, days, room, start_time, end_time, teacher, notes, status|
| GroupType        | type_id, short_description, long_description|
| Invoice          | invoice_number, invoice_date, invoice_note|
| InvoiceLineItem  | invoice_line_item_id, invoice_number, student_id, course_id, item_id, quantity, amount, payment_due, notes Item             | item_id, description, category, price|
| Level            | certificate_text, level_id, textbook, description, cef_equivalent, pacing_guide|
| Meeting          | notes, unpaid, meeting_id, course_id, meeting_date, teacher, material_covered, homework_assigned|
| PacingGuide      | lesson, content, pacing_name, section|
| Paste Errors     | F1, F3, F2, F4, F5, F6|
| PlacementExam    | student_id, placement_id, test_date, test, overall_level, speaking_fluency, spoken_accuracy, listening_comprehension, oral_level, mc_correct, mc_marked, mc_level, writing_level, notes|
| ProgressReport   | student_id, teacher_id, course_id, report_date, interest, participation, submitting_homework, homework_effort, speaking_fluency, speaking_accuracy, pronunciation, vocabulary, grammar, listening, reading, writing, overall, notes|
| Receipt          | receipt_number, receipt_date, total_amount, received_by, notes|
| ReceiptLineItem  | receipt_line_item_id, receipt_number, student_id, course_id, item_id, quantity, amount, notes|
| ResultType       | ID, short_description, long_description|
| Room             | room_id, chairs, availability|
| SchoolGrade      | grade_id, description|
| SectionExam      | exam_id, course_id, student_id, exam_date, overall_score, raw_score, written_score, vocabulary, fluency, accuracy, communication, notes|
| Staff            | staff_id, staff_name, cpr, mobile_number, email, accent, bio, gender, birthdate, admin, active, short_name, teaching_rate|
| Student          | student_id, cpr, registration_date, first_name, additional_names, gender, birthdate, school_grade, school_name, grade_updated, home_telephone, mobile_telephone, block, road, building, flat, email, notes, preferred_contact_method, no_call, delinquent_account, expelled|
| Term             | term_id, term_name, subsection|


**All the queiries and what they accomplish (order by importance - most important first)**


| Query Name | What It Accomplishes | PostgreSQL | What Tables It Affects | Additional Query Affected |
| ---------- | -------------------- | ---------- | ---------------------- | ------------------------- |
| account_balances_net | Takes student id displays their names, mobile_telephone, balance_owed, deliquent_account, no_call and notes. | SELECT s.student_id, s.first_name, s.additional_names, s.mobile_telephone, s.delinquent_account, s.no_call, s.notes, sum(invoice.sum - receipt.sum) as balance_owed FROM "Student" as s LEFT JOIN (select student_id, sum(amount) from "InvoiceLineItem" group by student_id) as invoice ON s.student_id = invoice.student_id LEFT JOIN (select student_id, sum(amount) from "ReceiptLineItem" group by student_id) as receipt ON s.student_id = receipt.student_id GROUP BY s.student_id, invoice.sum, receipt.sum; | Student, ReceiptLineItem | account_balances_receipt -> which uses the student_id to sum all the amount in the ReceiptLineItem group them by student_id |
| active_students | Takes student_id and displays active status of the student | SELECT ce.student_id, gc.status FROM "GeneralCourse" as gc INNER JOIN "CourseEnrollment" as ce ON gc.course_id = ce.course_id WHERE gc.status = 'active'; |  GeneralCourse, CourseEnrollment | none |
| attending_by_term | 


