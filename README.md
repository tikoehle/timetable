# Timetable
Solving a school scheduling problem using a SAT-Solver

State: Work in progress, 12 June 2023


This combinatorial optimization problem is solved using the SAT-Solver from Googles OR-Tools. The implementation is based on the ```school_scheduling_sat.py``` example from ortools: <a href="https://github.com/google/or-tools/blob/main/examples/contrib/school_scheduling_sat.py">View source on GitHub</a>. All the constraints are of course school specific and have been modeled in close cooperation with the school.

## Objective
[TBD]


## Hard constraints

C1: Each Level must have the quantity of classes per Subject specified in the Curriculum.

C2: Each Level can do at most one class at a time.

C3: Teacher can do at most one class at a time.

C4: Maximum work hours for each teacher.

C5: Assign your preferred teacher and let the solver choose the time slot.

C6: Assign your preferred teacher for a fixed assignment of [level, subject, teacher, timeslot].


## Harte Randbedingungen

C1: Jede Stufe muss die im Lehrplan angegebene Anzahl an Unterrichtsstunden pro Fach haben.

C2: Jede Klassenstufe kann höchstens eine Klasse gleichzeitig absolvieren.

C3: Der Lehrer kann höchstens eine Unterrichtsstunde gleichzeitig absolvieren.

C4: Maximale Arbeitszeit für jeden Lehrer.

C5: Weisen Sie Ihren bevorzugten Lehrer zu und lassen Sie das Programm das Zeitfenster auswählen.

C6: Weisen Sie Ihren bevorzugten Lehrer für eine feste Aufgabe in Kombination von [Klasse, Fach, Lehrer, Zeitfenster] zu.


## Soft constraints
[TBD]


## Example results with example input data
There are three different views: 
- Teachers tables
- Class tables
- School schedule table

### Exampel output

```
There are 4025 variable assignments.
Solving
Solution #0, objective: 0.0

Results:
Status:  OPTIMAL


---------------------------------------------------------------------------
Teachers
---------------------------------------------------------------------------

Teacher: T1
Total teaching hours: 11.0h
Unallocated hours: 3.0h
+-----------------------+---------+-----------+
|                       | class   | subject   |
|-----------------------+---------+-----------|
| Monday:08:00-09:30    | 1-B     | Math      |
| Monday:09:45-11:15    | 1-B     | Math      |
| Monday:11:30-12:30    | 3-A     | Math      |
| Monday:13:30-15:30    | 2-A     | Math      |
| Tuesday:11:30-12:30   | 3-A     | Math      |
| Tuesday:13:30-15:30   | 3-A     | Math      |
| Wednesday:11:30-12:30 | 2-B     | Math      |
| Thursday:11:30-12:30  | 2-B     | Math      |
+-----------------------+---------+-----------+

Teacher: T2
Total teaching hours: 6h
Unallocated hours: 6h
+-----------------------+---------+-----------+
|                       | class   | subject   |
|-----------------------+---------+-----------|
| Monday:11:30-12:30    | 2-B     | English   |
| Tuesday:11:30-12:30   | 1-A     | English   |
| Wednesday:11:30-12:30 | 1-A     | English   |
| Thursday:13:30-15:30  | 3-A     | English   |
| Friday:11:30-12:30    | 1-A     | English   |
+-----------------------+---------+-----------+

Teacher: T3
Total teaching hours: 8h
Unallocated hours: 4h
+----------------------+---------+-----------+
|                      | class   | subject   |
|----------------------+---------+-----------|
| Monday:11:30-12:30   | 2-A     | History   |
| Monday:13:30-15:30   | 2-B     | History   |
| Tuesday:11:30-12:30  | 2-A     | History   |
| Tuesday:13:30-15:30  | 1-B     | History   |
| Thursday:13:30-15:30 | 1-A     | History   |
+----------------------+---------+-----------+

Teacher: T4
Total teaching hours: 13.0h
Unallocated hours: 1.0h
+----------------------+---------+-----------+
|                      | class   | subject   |
|----------------------+---------+-----------|
| Monday:08:00-09:30   | 1-A     | Math      |
| Monday:09:45-11:15   | 1-A     | Math      |
| Monday:11:30-12:30   | 1-B     | English   |
| Tuesday:11:30-12:30  | 1-B     | English   |
| Tuesday:13:30-15:30  | 2-A     | English   |
| Tuesday:15:45-17:15  | 2-B     | English   |
| Thursday:08:00-09:30 | 2-B     | English   |
| Friday:11:30-12:30   | 1-B     | English   |
| Friday:13:30-15:30   | 2-A     | English   |
+----------------------+---------+-----------+

Teacher: T5
Total teaching hours: 2h
Unallocated hours: 0h
+--------------------+---------+-----------+
|                    | class   | subject   |
|--------------------+---------+-----------|
| Monday:13:30-15:30 | 3-A     | Science   |
+--------------------+---------+-----------+

Teacher: T6
Total teaching hours: 1h
Unallocated hours: 1h
+--------------------+---------+-----------+
|                    | class   | subject   |
|--------------------+---------+-----------|
| Monday:11:30-12:30 | 1-A     | Sport     |
+--------------------+---------+-----------+

Teacher: T7
Total teaching hours: 2h
Unallocated hours: 0h
+--------------------+---------+-----------+
|                    | class   | subject   |
|--------------------+---------+-----------|
| Monday:13:30-15:30 | 1-B     | Sport     |
+--------------------+---------+-----------+


---------------------------------------------------------------------------
Classes
---------------------------------------------------------------------------

Class: 1-A
Total teaching hours for English: 3h
Total teaching hours for Math: 3.0h
Total teaching hours for History: 2h
Total teaching hours for Sport: 1h
+-----------------------+-----------+-----------+
|                       | subject   | teacher   |
|-----------------------+-----------+-----------|
| Monday:08:00-09:30    | Math      | T4        |
| Monday:09:45-11:15    | Math      | T4        |
| Monday:11:30-12:30    | Sport     | T6        |
| Tuesday:11:30-12:30   | English   | T2        |
| Wednesday:11:30-12:30 | English   | T2        |
| Thursday:13:30-15:30  | History   | T3        |
| Friday:11:30-12:30    | English   | T2        |
+-----------------------+-----------+-----------+

Class: 1-B
Total teaching hours for English: 3h
Total teaching hours for Math: 3.0h
Total teaching hours for History: 2h
Total teaching hours for Sport: 2h
+---------------------+-----------+-----------+
|                     | subject   | teacher   |
|---------------------+-----------+-----------|
| Monday:08:00-09:30  | Math      | T1        |
| Monday:09:45-11:15  | Math      | T1        |
| Monday:11:30-12:30  | English   | T4        |
| Monday:13:30-15:30  | Sport     | T7        |
| Tuesday:11:30-12:30 | English   | T4        |
| Tuesday:13:30-15:30 | History   | T3        |
| Friday:11:30-12:30  | English   | T4        |
+---------------------+-----------+-----------+

Class: 2-A
Total teaching hours for English: 4h
Total teaching hours for Math: 2h
Total teaching hours for History: 2h
+---------------------+-----------+-----------+
|                     | subject   | teacher   |
|---------------------+-----------+-----------|
| Monday:11:30-12:30  | History   | T3        |
| Monday:13:30-15:30  | Math      | T1        |
| Tuesday:11:30-12:30 | History   | T3        |
| Tuesday:13:30-15:30 | English   | T4        |
| Friday:13:30-15:30  | English   | T4        |
+---------------------+-----------+-----------+

Class: 2-B
Total teaching hours for English: 4.0h
Total teaching hours for Math: 2h
Total teaching hours for History: 2h
+-----------------------+-----------+-----------+
|                       | subject   | teacher   |
|-----------------------+-----------+-----------|
| Monday:11:30-12:30    | English   | T2        |
| Monday:13:30-15:30    | History   | T3        |
| Tuesday:15:45-17:15   | English   | T4        |
| Wednesday:11:30-12:30 | Math      | T1        |
| Thursday:08:00-09:30  | English   | T4        |
| Thursday:11:30-12:30  | Math      | T1        |
+-----------------------+-----------+-----------+

Class: 3-A
Total teaching hours for English: 2h
Total teaching hours for Math: 4h
Total teaching hours for Science: 2h
+----------------------+-----------+-----------+
|                      | subject   | teacher   |
|----------------------+-----------+-----------|
| Monday:11:30-12:30   | Math      | T1        |
| Monday:13:30-15:30   | Science   | T5        |
| Tuesday:11:30-12:30  | Math      | T1        |
| Tuesday:13:30-15:30  | Math      | T1        |
| Thursday:13:30-15:30 | English   | T2        |
+----------------------+-----------+-----------+

School:
+-----------------------+---------------------------------------------------------------------------------+
|                       | class:(subject, teacher)                                                        |
|-----------------------+---------------------------------------------------------------------------------|
| Monday:08:00-09:30    | 1-A:(Math,T4) 1-B:(Math,T1)                                                     |
| Monday:09:45-11:15    | 1-A:(Math,T4) 1-B:(Math,T1)                                                     |
| Monday:11:30-12:30    | 1-A:(Sport,T6) 1-B:(English,T4) 2-A:(History,T3) 2-B:(English,T2) 3-A:(Math,T1) |
| Monday:13:30-15:30    | 1-B:(Sport,T7) 2-A:(Math,T1) 2-B:(History,T3) 3-A:(Science,T5)                  |
| Monday:15:45-17:15    |                                                                                 |
| Tuesday:08:00-09:30   |                                                                                 |
| Tuesday:09:45-11:15   |                                                                                 |
| Tuesday:11:30-12:30   | 1-A:(English,T2) 1-B:(English,T4) 2-A:(History,T3) 3-A:(Math,T1)                |
| Tuesday:13:30-15:30   | 1-B:(History,T3) 2-A:(English,T4) 3-A:(Math,T1)                                 |
| Tuesday:15:45-17:15   | 2-B:(English,T4)                                                                |
| Wednesday:08:00-09:30 |                                                                                 |
| Wednesday:09:45-11:15 |                                                                                 |
| Wednesday:11:30-12:30 | 1-A:(English,T2) 2-B:(Math,T1)                                                  |
| Thursday:08:00-09:30  | 2-B:(English,T4)                                                                |
| Thursday:09:45-11:15  |                                                                                 |
| Thursday:11:30-12:30  | 2-B:(Math,T1)                                                                   |
| Thursday:13:30-15:30  | 1-A:(History,T3) 3-A:(English,T2)                                               |
| Thursday:15:45-17:15  |                                                                                 |
| Friday:08:00-09:30    |                                                                                 |
| Friday:09:45-11:15    |                                                                                 |
| Friday:11:30-12:30    | 1-A:(English,T2) 1-B:(English,T4)                                               |
| Friday:13:30-15:30    | 2-A:(English,T4)                                                                |
| Friday:15:45-17:15    |                                                                                 |
+-----------------------+---------------------------------------------------------------------------------+

Statistics:
Branches: 330.000000
Conflicts: 0.000000
Problem solved in 0.051507 milliseconds
```
