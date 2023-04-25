---
title: "Introduction to Educational Timetabling"
last_modified_at: 2023-04-18
author_profile: true
categories:
  - Optimization
tags:
  - Educational Timetabling
---
## Main problems
There are three main problems in the educational timetabling area:

- High-School Timetabling (HTT): The weekly scheduling for all the classes of 
a high-school, avoiding teachers meeting two classes at the same time, and 
vice versa.

- University Course Timetabling (CTT): The weekly scheduling for all the 
lectures of a set of university courses, minimizing the overlaps of lectures of 
courses having common students.

- University Examination Timetabling (ETT): The scheduling for the exams of a 
set of university courses, avoidingoverlap of exams of courses having common 
students, and spreading the exams for the students as much aspossible.

## Factors
- Times: The time horizon is divided into days and each day is split into 
timeslots (in general, the same number of timeslots is given in each day). 
A period is a pair <day, timeslot>.

- Events: An event is a meeting between students and one or more teachers. 
Events can be of different types: lectures or exams of a course, laboratories, 
or seminars.

- Resources: We consider three main kinds of resources: students, teachers, 
and rooms. Events have to be scheduled taking into account resource restrictions, 
such as students’ enrollments, teachers’ requests and rooms’ availabilities.

- Constraints: As customary, constraints are split into hard and soft ones 
(soft constraints are also called objectives). The hard constraints must be 
always satisfied, whereas the soft ones contribute to the objective function,
which is a weighted sum of all soft constraint penalties.

## Constraints
The different sorts of timetabling constraints (of which there many) can be 
categorised into five main classes:

- Unary constraints that involve just one event, such as the constraint “event a
must not take place on a Tuesday”, or the constraint “event a must occur in 
timeslot b”.

- Binary constraints that concern pairs of events, such the constraint “event a
must take place before event b”, or the event clash constraint, which is 
considered in more detail below. (Note that chains of binary constraints can 
also be applied, suchas the constraint “event a must take place before b, which
must take place before c”, etc. . .)

- Capacity constraints that are governed by room capacities, etc. For example “All
events should be assigned to a room which has a sufficient capacity”.

- Event spread constraints that concern requirements such as the “spreading-out” 
or “clumping-together” of events within the timetable in order to ease 
student/teacher workload, and/or to agree with a university’s timetabling policy.

- Agent constraints that are imposed in order to promote therequirements and/or
preferences of the people who will use the timetables, such as the constraint 
“lecturer x likes to teach event a on Mondays”, or “lecturer y must have have n 
free mornings per week”.

## High-School Timetabling (XHSTT) (ITC 2011)
### Factors
- Times and resources
  - Students: Usually a student group is preassigned to each events. Constraints 
  that can be important for students are controlling the number of idle times, 
  the number of lessons per day.
  - Teachers: As mentioned earlier, in some countries teachers are preassigned 
  to events, while in others they are not. In the latter case the choice of 
  assignment will be restricted by teachers’ qualifications and workload limits. 
  Important issues for the teachers are the total number of idle times, the 
  number of assigned times per day, the number of days with events, and 
  unavailable days or times.
  - Rooms: Most events take place in a room. If rooms abound, we can disregard 
  them, if not they can be a bottleneck, especially for rooms.

- Event
  - The duration, which is the number of times that have to be assigned to the 
  event. These times must be consecutive.
  - The course related to an event.
  - The time that the event is scheduled to. If the duration is larger than one, 
  the event will occupy some following times as well. Constructing a timetable 
  involves assigning a time to all events.
  - The workload that the event will contribute to a teacher’s total workload. 
  Often this is the same as the duration. The workload is only needed when 
  teachers are not preassigned, and consequently total workloads must be calculated.
  - The resource groups are preassigned.
  - Any number of resources, either preassigned, or to be assigned. These each 
  have a ‘role’, used to identify them. A role might have value ‘room’, 
  ‘teacher’, ‘senior teacher’, and so on. A resource may be constrained to be 
  from a particular resource group, for example a Science laboratory or an 
  English teacher.

### Constraints
- Basic scheduling constraints
  - AssignTimeConstraint (Cost per event). Assign a time to each of the selected 
  events.
  - AssignResourceConstraint (Cost per event). Assign a resource to the role in 
  each of the selected events.

- Event constraints
  - LinkEventsConstraint (Cost per event group). Schedule the selected event 
  groups at the same (starting) time.
  - SpreadEventsConstraint. (Cost per event group). Schedule the events of the 
  selected event groups to the selected time groups between a minimum and a 
  maximum number of times.
  - AvoidSplitAssignmentsConstraint. (Cost per event group). For each selected 
  event group, schedule the selected role of each event of this group to the 
  same resource.

- Resource constraints: Resource constraints describe the quality of the 
timetable of a single resource; the corresponding cost is attributed to the 
resource.
  - AvoidClashesConstraint. Schedule the selected resources without clashes. 
  This is one of the basic (hard) constraints.
  - AvoidUnavailableTimesConstraint. Avoid that the selected resources are busy 
  in the selected times.
  - LimitWorkloadConstraint. Schedule workload to the selected resources between 
  a minimum and a maximum.
  - LimitIdleTimesConstraint. The number of idle times in the selected time 
  groups should lie between a minimum and a maximum for each of the selected 
  resources. Typically the time groups are a day or all days.
  - LimitBusyTimesConstraint. The number of occupied times for the selected resources
  should lie between a minimum and a maximum for each of the selected time groups.
  Typically the time groups are the days.
  - ClusterBusyTimesConstraint. The number of time groups with an assigned time should
  lie between a minimum and a maximum for the selected resources. Typically the time
  groups are days; for example a teacher requiring at most 3 days with lessons.

## Curriculum-based Course Timetabling (Track 3 ITC 2007)

### The problem consists of the following entities: 
- Days, Timeslots, and Periods.  We are given a number of 
teaching days in the week (typically 5 or 6). Each day is
split in a fixed number of timeslots, which is equal for all
days. A period is a pair composed of a day and a timeslot.
The total number of scheduling periods is the product of
the days times the day timeslots.

- Courses and Teachers. Each course consists of a fixed
number of lectures to be scheduled in distinct periods, it
is attended by given number of students, and is taught by
a teacher. For each course there is a minimum number
of days that the lectures of the course should be spread
in, moreover there are some periods in which the course
cannot be scheduled.

- Rooms. Each room has a capacity, expressed in terms of
number of available seats. All rooms are equally suitable
for all courses (if large enough).

- Curricula. A curriculum is a group of courses such that
any pair of courses in the group have students in common.
Based on curricula, we have the conflicts between courses
and other soft constraints.
The solution of the problem is an assignment of a period
(day and timeslot) and a room to all lectures of each course.

### The hard constraints are the following:
- Lectures: All lectures of a course must be scheduled, and
they must be assigned to distinct periods. A violation occurs 
if a lecture is not scheduled.

- RoomOccupancy: Two lectures cannot take place in the
same room in the same period. Two lectures in the same
room at the same period represent one violation . Any
extra lecture in the same period and room counts as one
more violation.

- Conflicts: Lectures of courses in the same curriculum or
taught by the same teacher must be all scheduled in different 
periods. Two conflicting lectures in the same period
represent one violation. Three conflicting lectures count
as 3 violations: one for each pair.

- Availabilities: If the teacher of the course is not available
to teach that course at a given period, then no lectures of
the course can be scheduled at that period. Each lecture
in a period unavailable for that course is one violation.

- RoomCapacity: For each lecture, the number of students
that attend the course must be less or equal than the number 
of seats of all the rooms that host its lectures.Each
student above the capacity counts as 1 point of penalty.

- MinimumWorkingDays: The lectures of each course must
be spread into the given minimum number of days. Each
day below the minimum counts as 5 points of penalty.

- CurriculumCompactness: Lectures belonging to a curriculum 
should be adjacent to each other (i.e., in consecutive periods). 
For a given curriculum we account for a violation every time there 
is one lecture not adjacent to any other lecture within the same day. 
Each isolated lecture in a curriculum counts as 2 points of penalty.

- RoomStability: All lectures of a course should be given in
the same room. Each distinct room used for the lectures
of a course, but the first, counts as 1 point of penalty.


