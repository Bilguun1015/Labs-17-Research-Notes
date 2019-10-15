**1st Meeting**

Victoria database usage workflow: 
    A student who is coming into get reciepts
    - Go to student table (many names are repeats) search by name
    - Get the student id 

    note by Ann
- go to student table, so many name is repeat
- search for whatever they need in student table
- get the student ID
- take a student ID to student enrollment table
- in student enrollment table they can see total balance, student info, placement test, group ID
- go to course enrollment, enter group ID
- and then you see all the student classmate
    - if unconfirm means interested but do not show up
- q_reenrollment_eligible table is also important
- q_course_infomation table show how many classes are open and completed


**2nd Meeting**

Questions: enrolled student

- If the student is enrolled already and if the parents don't know their student id, find student id -->  go to student table find by firstname and then by family name to locate the student id
- go to student enrollment form with the student id -- which shows the courses the student has taken, shows pass/dropped/confirmed/no exam(right at the end of a section didnt show up for the exam)/failed/transferredOut(same level different day)/cancelEnrollment(before the class started changed their mind)/noShow/unconfirmed(before putting the student into the group)
- go to course information(query) shows the courses -> with the id of the course add the student into the course with parents acceptance, in excel shows the detail info on the course, how many students/inspection/teacher/level/startdate/enddate/roomnumber/
- excel  also autopopulates the attendance sheet - teachers will be filling the attendance by hand on a printed form
- for the parents also print out of what they have to pay, dates of the classes for their kids
- calendar has to filled out with correct information to say what dates are the school open

new student
- student enrollment form fill out the form 
- go to course information and they can pick one of the courses 
- take the course id to course enrollment(table) auto populates the info and fill out what the first day
 
billing
- first day -> pay for first course/registration/dictionary if they dont have enough registration must paid
- go to receipt (query) and print out the receipt

invoice the balance
- go to invoice(query)

display account balance
- account_balances_net(query)

what information should be one place?
reenrollment_eligible -> send them sms
student_reciepts(form) -> shows the balance and what paid, can ensure the parents for their childrens unpaid balance

