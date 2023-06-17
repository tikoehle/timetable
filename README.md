# Timetable
## Solving the High School timetable problem using a SAT-Solver
#### State: Work in progress, 12 June 2023
#### Author: Timo Koehler

The process of timetable construction is a common and repetitive task for schools worldwide.
In the world of algorithms this problem is called "high school timetable problem", other variants exist for course and student-based educational institutions, and they are all referring to the task of creating an optimal schedule, subject to various constraints and objectives. The goal is to assign subjects, teachers, and classrooms to specific time slots while satisfying all the necessary requirements and optimizing certain criteria. This problem involves numerous constraints that must be considered when constructing the timetable. Some common constraints include:

1. Teacher availability
2. Classroom availability
3. Subject prerequisites
4. Student course requests
5. Teacher and student preferences
6. Time slot constraints
7. Class size limitations
8. Time slots for specific locations, like Sporthalle oder Fachkabinett
9. Reoptimization because of teacher sick days

... and many more, depending on the concrete school and project.
This project implements the hard and soft boundary conditions for a German Gymnasium and optimizes the result based on the objectives formulated below.

Timetabling problems in their general form belong to the class of NP-complete problems giving little hope of finding an generic algorithm that produces an optimal result for any problem size and in polynomial bounded time. Nevertheless, specific timetabling problems with great practical relevancy can be solved using constraint integer programming approaches to model and solve the problem. Integer programming is a mathematical optimization technique that seeks to find the best assignment of variables subject to linear constraints. The binary nature of the variables in integer programming allows for the representation of binary decisions, such as whether a subject is assigned to a particular time slot. It becomes possible to find an optimal or near-optimal solution that meets the various constraints and objectives, resulting in an efficient and effective schedule.

This project solves the problem using a SAT-Solver from Googles OR-Tools. The implementation is based on the ```school_scheduling_sat.py``` example from ortools: <a href="https://github.com/google/or-tools/blob/main/examples/contrib/school_scheduling_sat.py">View source on GitHub</a>. All the constraints are of course school specific and have been modeled in close cooperation with the school.

## Objective
[TBD]


## Hard constraints

C1: Each Level must have the quantity of classes per Subject specified in the Curriculum.

C2: Each Level can do at most one class at a time.

C3: Each class must be assigned to only one location/room.

C4: Teacher can do at most one class at a time.

C5: Maximum work hours for each teacher.

C6: Assign your preferred teacher and let the solver choose the time slot and select a random location/room.

C7: Assign your preferred teacher for a fixed assignment of [level, subject, teacher, timeslot] and select a random location/room.


## Harte Randbedingungen

C1: Jede Stufe muss die im Lehrplan angegebene Anzahl an Unterrichtsstunden pro Fach haben.

C2: Jede Klassenstufe kann höchstens eine Klasse gleichzeitig absolvieren.

C3: Jede Klasse darf nur einem Ort/Raum zugeordnet sein.

C4: Der Lehrer kann höchstens eine Unterrichtsstunde gleichzeitig absolvieren.

C5: Maximale Arbeitszeit für jeden Lehrer.

C6: Weisen Sie Ihren bevorzugten Lehrer zu und lassen Sie das Programm das Zeitfenster und einen zufälligen Ort/Raum auswählen.

C7: Weisen Sie Ihren bevorzugten Lehrer für eine feste Aufgabe in Kombination von [Klasse, Fach, Lehrer, Zeitfenster] zu und wählen Sie einen zufälligen Ort/Raum aus.


## Soft constraints
[TBD]


## Example results with example input data
There are three different views: 
- Teachers tables
- Class tables
- School schedule table

### Example output

```
Search space is: 49000
Solving
Solution #0, objective: 0.0

Results:
Status:  OPTIMAL


---------------------------------------------------------------------------
Teachers
---------------------------------------------------------------------------

Teacher: T1
Total teaching hours: 9
Unallocated teaching hours: 5
+-----------------------+---------+-----------+--------+--------+
|                       | class   | subject   | bldg   |   room |
|-----------------------+---------+-----------+--------+--------|
| Monday:07:10-07:55    | 3-A     | Math      | B      |      4 |
| Monday:11:25-12:10    | 3-A     | Math      | A      |      2 |
| Tuesday:09:00-09:45   | 3-A     | Math      | B      |      2 |
| Wednesday:08:00-08:45 | 2-B     | Math      | A      |      4 |
| Thursday:08:00-08:45  | 1-B     | Math      | B      |      4 |
| Thursday:11:25-12:10  | 1-B     | Math      | B      |      5 |
| Thursday:13:30-14:15  | 1-A     | Math      | B      |      6 |
| Friday:09:00-09:45    | 2-B     | Math      | B      |      3 |
| Friday:10:30-11:15    | 3-A     | Math      | A      |      1 |
+-----------------------+---------+-----------+--------+--------+
+-----------+--------------------------------+-----------+
|           | slot_sequence(location)        |   max_seq |
|-----------+--------------------------------+-----------|
| Monday    | ['B', '0', '0', '0', 'A', '0'] |         1 |
| Tuesday   | ['0', '0', 'B', '0', '0']      |         1 |
| Wednesday | ['0', 'A', '0', '0', '0', '0'] |         1 |
| Thursday  | ['0', 'B', '0', '0', 'B', 'B'] |         2 |
| Friday    | ['0', '0', 'B', 'A', '0']      |         2 |
+-----------+--------------------------------+-----------+

Teacher: T2
Total teaching hours: 10
Unallocated teaching hours: 2
+----------------------+---------+-----------+--------+--------+
|                      | class   | subject   | bldg   |   room |
|----------------------+---------+-----------+--------+--------|
| Monday:07:10-07:55   | 2-A     | English   | B      |      6 |
| Monday:08:00-08:45   | 2-B     | English   | A      |      4 |
| Monday:09:00-09:45   | 2-A     | English   | A      |      2 |
| Tuesday:08:00-08:45  | 2-B     | English   | B      |      3 |
| Thursday:07:10-07:55 | 2-B     | English   | A      |      4 |
| Thursday:11:25-12:10 | 1-A     | English   | B      |      6 |
| Thursday:13:30-14:15 | 2-A     | English   | A      |      4 |
| Friday:08:00-08:45   | 2-A     | English   | B      |      3 |
| Friday:09:00-09:45   | 1-A     | English   | A      |      4 |
| Friday:10:30-11:15   | 1-A     | English   | A      |      4 |
+----------------------+---------+-----------+--------+--------+
+-----------+--------------------------------+-----------+
|           | slot_sequence(location)        |   max_seq |
|-----------+--------------------------------+-----------|
| Monday    | ['B', 'A', 'A', '0', '0', '0'] |         3 |
| Tuesday   | ['0', 'B', '0', '0', '0']      |         1 |
| Wednesday | ['0', '0', '0', '0', '0', '0'] |         0 |
| Thursday  | ['A', '0', '0', '0', 'B', 'A'] |         2 |
| Friday    | ['0', 'B', 'A', 'A', '0']      |         3 |
+-----------+--------------------------------+-----------+

Teacher: T3
Total teaching hours: 5
Unallocated teaching hours: 7
+----------------------+---------+-----------+--------+--------+
|                      | class   | subject   | bldg   |   room |
|----------------------+---------+-----------+--------+--------|
| Monday:11:25-12:10   | 2-B     | History   | B      |      5 |
| Tuesday:07:10-07:55  | 1-A     | History   | B      |      1 |
| Tuesday:09:00-09:45  | 1-B     | History   | A      |      2 |
| Thursday:07:10-07:55 | 1-A     | History   | B      |      5 |
| Friday:09:00-09:45   | 1-B     | History   | B      |      5 |
+----------------------+---------+-----------+--------+--------+
+-----------+--------------------------------+-----------+
|           | slot_sequence(location)        |   max_seq |
|-----------+--------------------------------+-----------|
| Monday    | ['0', '0', '0', '0', 'B', '0'] |         1 |
| Tuesday   | ['B', '0', 'A', '0', '0']      |         1 |
| Wednesday | ['0', '0', '0', '0', '0', '0'] |         0 |
| Thursday  | ['B', '0', '0', '0', '0', '0'] |         1 |
| Friday    | ['0', '0', 'B', '0', '0']      |         1 |
+-----------+--------------------------------+-----------+

Teacher: T4
Total teaching hours: 14
Unallocated teaching hours: 0
+-----------------------+---------+-----------+--------+--------+
|                       | class   | subject   | bldg   |   room |
|-----------------------+---------+-----------+--------+--------|
| Monday:10:30-11:15    | 1-A     | Math      | A      |      1 |
| Monday:11:25-12:10    | 2-A     | Math      | A      |      3 |
| Monday:13:30-14:15    | 1-B     | Math      | B      |      2 |
| Tuesday:08:00-08:45   | 1-B     | English   | B      |      1 |
| Tuesday:10:30-11:15   | 2-B     | English   | B      |      1 |
| Tuesday:11:25-12:10   | 3-A     | English   | A      |      3 |
| Wednesday:08:00-08:45 | 1-B     | English   | B      |      5 |
| Wednesday:09:00-09:45 | 2-B     | History   | B      |      1 |
| Wednesday:10:30-11:15 | 1-A     | Math      | B      |      6 |
| Wednesday:13:30-14:15 | 2-A     | Math      | A      |      4 |
| Thursday:07:10-07:55  | 2-A     | History   | A      |      3 |
| Thursday:08:00-08:45  | 2-A     | History   | B      |      3 |
| Thursday:11:25-12:10  | 3-A     | English   | B      |      3 |
| Friday:07:10-07:55    | 1-B     | English   | A      |      2 |
+-----------------------+---------+-----------+--------+--------+
+-----------+--------------------------------+-----------+
|           | slot_sequence(location)        |   max_seq |
|-----------+--------------------------------+-----------|
| Monday    | ['0', '0', '0', 'A', 'A', 'B'] |         3 |
| Tuesday   | ['0', 'B', '0', 'B', 'A']      |         2 |
| Wednesday | ['0', 'B', 'B', 'B', '0', 'A'] |         3 |
| Thursday  | ['A', 'B', '0', '0', 'B', '0'] |         2 |
| Friday    | ['A', '0', '0', '0', '0']      |         1 |
+-----------+--------------------------------+-----------+

Teacher: T5
Total teaching hours: 2
Unallocated teaching hours: 0
+-----------------------+---------+-----------+--------+--------+
|                       | class   | subject   | bldg   |   room |
|-----------------------+---------+-----------+--------+--------|
| Tuesday:07:10-07:55   | 3-A     | Science   | B      |      6 |
| Wednesday:07:10-07:55 | 3-A     | Science   | B      |      4 |
+-----------------------+---------+-----------+--------+--------+
+-----------+--------------------------------+-----------+
|           | slot_sequence(location)        |   max_seq |
|-----------+--------------------------------+-----------|
| Monday    | ['0', '0', '0', '0', '0', '0'] |         0 |
| Tuesday   | ['B', '0', '0', '0', '0']      |         1 |
| Wednesday | ['B', '0', '0', '0', '0', '0'] |         1 |
| Thursday  | ['0', '0', '0', '0', '0', '0'] |         0 |
| Friday    | ['0', '0', '0', '0', '0']      |         0 |
+-----------+--------------------------------+-----------+

Teacher: T6
Total teaching hours: 2
Unallocated teaching hours: 0
+--------------------+---------+-----------+--------+--------+
|                    | class   | subject   | bldg   |   room |
|--------------------+---------+-----------+--------+--------|
| Monday:07:10-07:55 | 1-A     | Sport     | A      |      2 |
| Monday:08:00-08:45 | 1-A     | Sport     | A      |      1 |
+--------------------+---------+-----------+--------+--------+
+-----------+--------------------------------+-----------+
|           | slot_sequence(location)        |   max_seq |
|-----------+--------------------------------+-----------|
| Monday    | ['A', 'A', '0', '0', '0', '0'] |         2 |
| Tuesday   | ['0', '0', '0', '0', '0']      |         0 |
| Wednesday | ['0', '0', '0', '0', '0', '0'] |         0 |
| Thursday  | ['0', '0', '0', '0', '0', '0'] |         0 |
| Friday    | ['0', '0', '0', '0', '0']      |         0 |
+-----------+--------------------------------+-----------+

Teacher: T7
Total teaching hours: 2
Unallocated teaching hours: 0
+---------------------+---------+-----------+--------+--------+
|                     | class   | subject   | bldg   |   room |
|---------------------+---------+-----------+--------+--------|
| Monday:07:10-07:55  | 1-B     | Sport     | A      |      1 |
| Tuesday:07:10-07:55 | 1-B     | Sport     | A      |      1 |
+---------------------+---------+-----------+--------+--------+
+-----------+--------------------------------+-----------+
|           | slot_sequence(location)        |   max_seq |
|-----------+--------------------------------+-----------|
| Monday    | ['A', '0', '0', '0', '0', '0'] |         1 |
| Tuesday   | ['A', '0', '0', '0', '0']      |         1 |
| Wednesday | ['0', '0', '0', '0', '0', '0'] |         0 |
| Thursday  | ['0', '0', '0', '0', '0', '0'] |         0 |
| Friday    | ['0', '0', '0', '0', '0']      |         0 |
+-----------+--------------------------------+-----------+


---------------------------------------------------------------------------
Classes
---------------------------------------------------------------------------

Class: 1-A
Total teaching hours for English: 3
Total teaching hours for Math: 3
Total teaching hours for History: 2
Total teaching hours for Sport: 2
+-----------------------+-----------+-----------+--------+--------+
|                       | subject   | teacher   | bldg   |   room |
|-----------------------+-----------+-----------+--------+--------|
| Monday:07:10-07:55    | Sport     | T6        | A      |      2 |
| Monday:08:00-08:45    | Sport     | T6        | A      |      1 |
| Monday:10:30-11:15    | Math      | T4        | A      |      1 |
| Tuesday:07:10-07:55   | History   | T3        | B      |      1 |
| Wednesday:10:30-11:15 | Math      | T4        | B      |      6 |
| Thursday:07:10-07:55  | History   | T3        | B      |      5 |
| Thursday:11:25-12:10  | English   | T2        | B      |      6 |
| Thursday:13:30-14:15  | Math      | T1        | B      |      6 |
| Friday:09:00-09:45    | English   | T2        | A      |      4 |
| Friday:10:30-11:15    | English   | T2        | A      |      4 |
+-----------------------+-----------+-----------+--------+--------+

Class: 1-B
Total teaching hours for English: 3
Total teaching hours for Math: 3
Total teaching hours for History: 2
Total teaching hours for Sport: 2
+-----------------------+-----------+-----------+--------+--------+
|                       | subject   | teacher   | bldg   |   room |
|-----------------------+-----------+-----------+--------+--------|
| Monday:07:10-07:55    | Sport     | T7        | A      |      1 |
| Monday:13:30-14:15    | Math      | T4        | B      |      2 |
| Tuesday:07:10-07:55   | Sport     | T7        | A      |      1 |
| Tuesday:08:00-08:45   | English   | T4        | B      |      1 |
| Tuesday:09:00-09:45   | History   | T3        | A      |      2 |
| Wednesday:08:00-08:45 | English   | T4        | B      |      5 |
| Thursday:08:00-08:45  | Math      | T1        | B      |      4 |
| Thursday:11:25-12:10  | Math      | T1        | B      |      5 |
| Friday:07:10-07:55    | English   | T4        | A      |      2 |
| Friday:09:00-09:45    | History   | T3        | B      |      5 |
+-----------------------+-----------+-----------+--------+--------+

Class: 2-A
Total teaching hours for English: 4
Total teaching hours for Math: 2
Total teaching hours for History: 2
+-----------------------+-----------+-----------+--------+--------+
|                       | subject   | teacher   | bldg   |   room |
|-----------------------+-----------+-----------+--------+--------|
| Monday:07:10-07:55    | English   | T2        | B      |      6 |
| Monday:09:00-09:45    | English   | T2        | A      |      2 |
| Monday:11:25-12:10    | Math      | T4        | A      |      3 |
| Wednesday:13:30-14:15 | Math      | T4        | A      |      4 |
| Thursday:07:10-07:55  | History   | T4        | A      |      3 |
| Thursday:08:00-08:45  | History   | T4        | B      |      3 |
| Thursday:13:30-14:15  | English   | T2        | A      |      4 |
| Friday:08:00-08:45    | English   | T2        | B      |      3 |
+-----------------------+-----------+-----------+--------+--------+

Class: 2-B
Total teaching hours for English: 4
Total teaching hours for Math: 2
Total teaching hours for History: 2
+-----------------------+-----------+-----------+--------+--------+
|                       | subject   | teacher   | bldg   |   room |
|-----------------------+-----------+-----------+--------+--------|
| Monday:08:00-08:45    | English   | T2        | A      |      4 |
| Monday:11:25-12:10    | History   | T3        | B      |      5 |
| Tuesday:08:00-08:45   | English   | T2        | B      |      3 |
| Tuesday:10:30-11:15   | English   | T4        | B      |      1 |
| Wednesday:08:00-08:45 | Math      | T1        | A      |      4 |
| Wednesday:09:00-09:45 | History   | T4        | B      |      1 |
| Thursday:07:10-07:55  | English   | T2        | A      |      4 |
| Friday:09:00-09:45    | Math      | T1        | B      |      3 |
+-----------------------+-----------+-----------+--------+--------+

Class: 3-A
Total teaching hours for English: 2
Total teaching hours for Math: 4
Total teaching hours for Science: 2
+-----------------------+-----------+-----------+--------+--------+
|                       | subject   | teacher   | bldg   |   room |
|-----------------------+-----------+-----------+--------+--------|
| Monday:07:10-07:55    | Math      | T1        | B      |      4 |
| Monday:11:25-12:10    | Math      | T1        | A      |      2 |
| Tuesday:07:10-07:55   | Science   | T5        | B      |      6 |
| Tuesday:09:00-09:45   | Math      | T1        | B      |      2 |
| Tuesday:11:25-12:10   | English   | T4        | A      |      3 |
| Wednesday:07:10-07:55 | Science   | T5        | B      |      4 |
| Thursday:11:25-12:10  | English   | T4        | B      |      3 |
| Friday:10:30-11:15    | Math      | T1        | A      |      1 |
+-----------------------+-----------+-----------+--------+--------+

School:
+-----------------------+------------------------------------------------------------------------------+
|                       | class:(subject, teacher, bldg, room)                                         |
|-----------------------+------------------------------------------------------------------------------|
| Monday:07:10-07:55    | 1-B:(Sport,T7,A,1) 1-A:(Sport,T6,A,2) 3-A:(Math,T1,B,4) 2-A:(English,T2,B,6) |
| Monday:08:00-08:45    | 1-A:(Sport,T6,A,1) 2-B:(English,T2,A,4)                                      |
| Monday:09:00-09:45    | 2-A:(English,T2,A,2)                                                         |
| Monday:10:30-11:15    | 1-A:(Math,T4,A,1)                                                            |
| Monday:11:25-12:10    | 3-A:(Math,T1,A,2) 2-A:(Math,T4,A,3) 2-B:(History,T3,B,5)                     |
| Monday:13:30-14:15    | 1-B:(Math,T4,B,2)                                                            |
| Tuesday:07:10-07:55   | 1-B:(Sport,T7,A,1) 1-A:(History,T3,B,1) 3-A:(Science,T5,B,6)                 |
| Tuesday:08:00-08:45   | 1-B:(English,T4,B,1) 2-B:(English,T2,B,3)                                    |
| Tuesday:09:00-09:45   | 1-B:(History,T3,A,2) 3-A:(Math,T1,B,2)                                       |
| Tuesday:10:30-11:15   | 2-B:(English,T4,B,1)                                                         |
| Tuesday:11:25-12:10   | 3-A:(English,T4,A,3)                                                         |
| Wednesday:07:10-07:55 | 3-A:(Science,T5,B,4)                                                         |
| Wednesday:08:00-08:45 | 2-B:(Math,T1,A,4) 1-B:(English,T4,B,5)                                       |
| Wednesday:09:00-09:45 | 2-B:(History,T4,B,1)                                                         |
| Wednesday:10:30-11:15 | 1-A:(Math,T4,B,6)                                                            |
| Wednesday:11:25-12:10 |                                                                              |
| Wednesday:13:30-14:15 | 2-A:(Math,T4,A,4)                                                            |
| Thursday:07:10-07:55  | 2-A:(History,T4,A,3) 2-B:(English,T2,A,4) 1-A:(History,T3,B,5)               |
| Thursday:08:00-08:45  | 2-A:(History,T4,B,3) 1-B:(Math,T1,B,4)                                       |
| Thursday:09:00-09:45  |                                                                              |
| Thursday:10:30-11:15  |                                                                              |
| Thursday:11:25-12:10  | 3-A:(English,T4,B,3) 1-B:(Math,T1,B,5) 1-A:(English,T2,B,6)                  |
| Thursday:13:30-14:15  | 2-A:(English,T2,A,4) 1-A:(Math,T1,B,6)                                       |
| Friday:07:10-07:55    | 1-B:(English,T4,A,2)                                                         |
| Friday:08:00-08:45    | 2-A:(English,T2,B,3)                                                         |
| Friday:09:00-09:45    | 1-A:(English,T2,A,4) 2-B:(Math,T1,B,3) 1-B:(History,T3,B,5)                  |
| Friday:10:30-11:15    | 3-A:(Math,T1,A,1) 1-A:(English,T2,A,4)                                       |
| Friday:11:25-12:10    |                                                                              |
+-----------------------+------------------------------------------------------------------------------+

Statistics:
Branches: 18200.000000
Conflicts: 0.000000
Problem solved in 2.153500 seconds
```
