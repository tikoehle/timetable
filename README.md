# Timetable
Solving a school scheduling problem using a SAT-Solver


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


