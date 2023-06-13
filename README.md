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
There are 4375 variable assignments.
Solving
Solution #0, objective: 0.0

Results:
Status:  OPTIMAL


---------------------------------------------------------------------------
Teachers
---------------------------------------------------------------------------

Teacher: T1
Total teaching hours: 14
Unallocated teaching hours: 0
+-----------------------+---------+-----------+
|                       | class   | subject   |
|-----------------------+---------+-----------|
| Monday:07:10-07:55    | 2-A     | Math      |
| Monday:08:00-08:45    | 2-A     | Math      |
| Monday:09:00-09:45    | 3-A     | Math      |
| Monday:10:30-11:15    | 3-A     | Math      |
| Monday:11:25-12:10    | 3-A     | Math      |
| Tuesday:07:10-07:55   | 3-A     | Math      |
| Tuesday:08:00-08:45   | 2-B     | Math      |
| Tuesday:09:00-09:45   | 2-B     | Math      |
| Wednesday:09:00-09:45 | 1-B     | Math      |
| Wednesday:10:30-11:15 | 1-B     | Math      |
| Thursday:07:10-07:55  | 1-B     | Math      |
| Friday:07:10-07:55    | 1-A     | Math      |
| Friday:08:00-08:45    | 1-A     | Math      |
| Friday:09:00-09:45    | 1-A     | Math      |
+-----------------------+---------+-----------+

Teacher: T2
Total teaching hours: 12
Unallocated teaching hours: 0
+-----------------------+---------+-----------+
|                       | class   | subject   |
|-----------------------+---------+-----------|
| Monday:09:00-09:45    | 2-B     | English   |
| Monday:10:30-11:15    | 2-B     | English   |
| Monday:11:25-12:10    | 2-B     | English   |
| Tuesday:07:10-07:55   | 2-B     | English   |
| Tuesday:08:00-08:45   | 3-A     | English   |
| Tuesday:09:00-09:45   | 1-A     | English   |
| Wednesday:10:30-11:15 | 1-A     | English   |
| Thursday:07:10-07:55  | 2-A     | English   |
| Thursday:08:00-08:45  | 2-A     | English   |
| Thursday:11:25-12:10  | 2-A     | English   |
| Friday:07:10-07:55    | 2-A     | English   |
| Friday:10:30-11:15    | 1-A     | English   |
+-----------------------+---------+-----------+

Teacher: T3
Total teaching hours: 6
Unallocated teaching hours: 6
+-----------------------+---------+-----------+
|                       | class   | subject   |
|-----------------------+---------+-----------|
| Monday:07:10-07:55    | 2-B     | History   |
| Monday:08:00-08:45    | 2-B     | History   |
| Monday:09:00-09:45    | 2-A     | History   |
| Monday:10:30-11:15    | 2-A     | History   |
| Monday:11:25-12:10    | 1-A     | History   |
| Wednesday:11:25-12:10 | 1-A     | History   |
+-----------------------+---------+-----------+

Teacher: T4
Total teaching hours: 6
Unallocated teaching hours: 8
+-----------------------+---------+-----------+
|                       | class   | subject   |
|-----------------------+---------+-----------|
| Monday:07:10-07:55    | 3-A     | English   |
| Monday:08:00-08:45    | 1-B     | English   |
| Monday:09:00-09:45    | 1-B     | English   |
| Wednesday:07:10-07:55 | 1-B     | English   |
| Friday:09:00-09:45    | 1-B     | History   |
| Friday:11:25-12:10    | 1-B     | History   |
+-----------------------+---------+-----------+

Teacher: T5
Total teaching hours: 2
Unallocated teaching hours: 0
+-----------------------+---------+-----------+
|                       | class   | subject   |
|-----------------------+---------+-----------|
| Monday:08:00-08:45    | 3-A     | Science   |
| Wednesday:08:00-08:45 | 3-A     | Science   |
+-----------------------+---------+-----------+

Teacher: T6
Total teaching hours: 2
Unallocated teaching hours: 0
+--------------------+---------+-----------+
|                    | class   | subject   |
|--------------------+---------+-----------|
| Monday:07:10-07:55 | 1-A     | Sport     |
| Monday:08:00-08:45 | 1-A     | Sport     |
+--------------------+---------+-----------+

Teacher: T7
Total teaching hours: 2
Unallocated teaching hours: 0
+---------------------+---------+-----------+
|                     | class   | subject   |
|---------------------+---------+-----------|
| Monday:07:10-07:55  | 1-B     | Sport     |
| Tuesday:07:10-07:55 | 1-B     | Sport     |
+---------------------+---------+-----------+


---------------------------------------------------------------------------
Classes
---------------------------------------------------------------------------

Class: 1-A
Total teaching hours for English: 3
Total teaching hours for Math: 3
Total teaching hours for History: 2
Total teaching hours for Sport: 2
+-----------------------+-----------+-----------+
|                       | subject   | teacher   |
|-----------------------+-----------+-----------|
| Monday:07:10-07:55    | Sport     | T6        |
| Monday:08:00-08:45    | Sport     | T6        |
| Monday:11:25-12:10    | History   | T3        |
| Tuesday:09:00-09:45   | English   | T2        |
| Wednesday:10:30-11:15 | English   | T2        |
| Wednesday:11:25-12:10 | History   | T3        |
| Friday:07:10-07:55    | Math      | T1        |
| Friday:08:00-08:45    | Math      | T1        |
| Friday:09:00-09:45    | Math      | T1        |
| Friday:10:30-11:15    | English   | T2        |
+-----------------------+-----------+-----------+

Class: 1-B
Total teaching hours for English: 3
Total teaching hours for Math: 3
Total teaching hours for History: 2
Total teaching hours for Sport: 2
+-----------------------+-----------+-----------+
|                       | subject   | teacher   |
|-----------------------+-----------+-----------|
| Monday:07:10-07:55    | Sport     | T7        |
| Monday:08:00-08:45    | English   | T4        |
| Monday:09:00-09:45    | English   | T4        |
| Tuesday:07:10-07:55   | Sport     | T7        |
| Wednesday:07:10-07:55 | English   | T4        |
| Wednesday:09:00-09:45 | Math      | T1        |
| Wednesday:10:30-11:15 | Math      | T1        |
| Thursday:07:10-07:55  | Math      | T1        |
| Friday:09:00-09:45    | History   | T4        |
| Friday:11:25-12:10    | History   | T4        |
+-----------------------+-----------+-----------+

Class: 2-A
Total teaching hours for English: 4
Total teaching hours for Math: 2
Total teaching hours for History: 2
+----------------------+-----------+-----------+
|                      | subject   | teacher   |
|----------------------+-----------+-----------|
| Monday:07:10-07:55   | Math      | T1        |
| Monday:08:00-08:45   | Math      | T1        |
| Monday:09:00-09:45   | History   | T3        |
| Monday:10:30-11:15   | History   | T3        |
| Thursday:07:10-07:55 | English   | T2        |
| Thursday:08:00-08:45 | English   | T2        |
| Thursday:11:25-12:10 | English   | T2        |
| Friday:07:10-07:55   | English   | T2        |
+----------------------+-----------+-----------+

Class: 2-B
Total teaching hours for English: 4
Total teaching hours for Math: 2
Total teaching hours for History: 2
+---------------------+-----------+-----------+
|                     | subject   | teacher   |
|---------------------+-----------+-----------|
| Monday:07:10-07:55  | History   | T3        |
| Monday:08:00-08:45  | History   | T3        |
| Monday:09:00-09:45  | English   | T2        |
| Monday:10:30-11:15  | English   | T2        |
| Monday:11:25-12:10  | English   | T2        |
| Tuesday:07:10-07:55 | English   | T2        |
| Tuesday:08:00-08:45 | Math      | T1        |
| Tuesday:09:00-09:45 | Math      | T1        |
+---------------------+-----------+-----------+

Class: 3-A
Total teaching hours for English: 2
Total teaching hours for Math: 4
Total teaching hours for Science: 2
+-----------------------+-----------+-----------+
|                       | subject   | teacher   |
|-----------------------+-----------+-----------|
| Monday:07:10-07:55    | English   | T4        |
| Monday:08:00-08:45    | Science   | T5        |
| Monday:09:00-09:45    | Math      | T1        |
| Monday:10:30-11:15    | Math      | T1        |
| Monday:11:25-12:10    | Math      | T1        |
| Tuesday:07:10-07:55   | Math      | T1        |
| Tuesday:08:00-08:45   | English   | T2        |
| Wednesday:08:00-08:45 | Science   | T5        |
+-----------------------+-----------+-----------+

School:
+-----------------------+---------------------------------------------------------------------------------+
|                       | class:(subject, teacher)                                                        |
|-----------------------+---------------------------------------------------------------------------------|
| Monday:07:10-07:55    | 1-A:(Sport,T6) 1-B:(Sport,T7) 2-A:(Math,T1) 2-B:(History,T3) 3-A:(English,T4)   |
| Monday:08:00-08:45    | 1-A:(Sport,T6) 1-B:(English,T4) 2-A:(Math,T1) 2-B:(History,T3) 3-A:(Science,T5) |
| Monday:09:00-09:45    | 1-B:(English,T4) 2-A:(History,T3) 2-B:(English,T2) 3-A:(Math,T1)                |
| Monday:10:30-11:15    | 2-A:(History,T3) 2-B:(English,T2) 3-A:(Math,T1)                                 |
| Monday:11:25-12:10    | 1-A:(History,T3) 2-B:(English,T2) 3-A:(Math,T1)                                 |
| Tuesday:07:10-07:55   | 1-B:(Sport,T7) 2-B:(English,T2) 3-A:(Math,T1)                                   |
| Tuesday:08:00-08:45   | 2-B:(Math,T1) 3-A:(English,T2)                                                  |
| Tuesday:09:00-09:45   | 1-A:(English,T2) 2-B:(Math,T1)                                                  |
| Tuesday:10:30-11:15   |                                                                                 |
| Tuesday:11:25-12:10   |                                                                                 |
| Wednesday:07:10-07:55 | 1-B:(English,T4)                                                                |
| Wednesday:08:00-08:45 | 3-A:(Science,T5)                                                                |
| Wednesday:09:00-09:45 | 1-B:(Math,T1)                                                                   |
| Wednesday:10:30-11:15 | 1-A:(English,T2) 1-B:(Math,T1)                                                  |
| Wednesday:11:25-12:10 | 1-A:(History,T3)                                                                |
| Thursday:07:10-07:55  | 1-B:(Math,T1) 2-A:(English,T2)                                                  |
| Thursday:08:00-08:45  | 2-A:(English,T2)                                                                |
| Thursday:09:00-09:45  |                                                                                 |
| Thursday:10:30-11:15  |                                                                                 |
| Thursday:11:25-12:10  | 2-A:(English,T2)                                                                |
| Friday:07:10-07:55    | 1-A:(Math,T1) 2-A:(English,T2)                                                  |
| Friday:08:00-08:45    | 1-A:(Math,T1)                                                                   |
| Friday:09:00-09:45    | 1-A:(Math,T1) 1-B:(History,T4)                                                  |
| Friday:10:30-11:15    | 1-A:(English,T2)                                                                |
| Friday:11:25-12:10    | 1-B:(History,T4)                                                                |
+-----------------------+---------------------------------------------------------------------------------+

Statistics:
Branches: 1314.000000
Conflicts: 0.000000
Problem solved in 0.098500 seconds
```
