---
# title: "Constraints for Vietnam University Course Timetabling"
# last_modified_at: 2023-04-26
# author_profile: true
# categories:
#   - Optimization
# tags:
#   - Educational Timetabling
---
- Unary constraints
    - All lectures of a course must be scheduled. (Hard)

- Binary constraints (chains of binary constraints)
    - All lectures must be assigned to distinct periods. (Hard)
    - Lectures of courses must be all scheduled in different periods. (Hard)
    - Lectures of courses in the same curriculum must be all scheduled in different periods. (Hard)
    - Two lectures cannot take place in the
    same room in the same period. (Hard)
    - All lectures of a course should be given in
    the same room. (Soft)

- Capacity constraints
    - For each lecture, the number of students
    that attend the course must be less or equal than the number  of seats of all the rooms that host its lectures. (Soft)

- Event spread constraints
    - The lectures of each course must
    be spread into the given minimum number of days. (Soft)

- Agent constraints
    - If the teacher of the course is not available
    to teach that course at a given period, then no lectures of the course can be scheduled at that period. (Hard)