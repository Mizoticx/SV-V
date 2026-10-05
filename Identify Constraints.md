# Task 1 --- Identify Constraints

## Automated Railway Level-Crossing Control System (ARLCCS)

The following constraints describe rules that the Automated Railway
Level-Crossing Control System must always satisfy during normal and
abnormal operation.

  -----------------------------------------------------------------------
  Constraint ID           Constraint in Simple    Why the Constraint Is
                          English                 Necessary
  ----------------------- ----------------------- -----------------------
  **C1**                  The barrier must not    Opening the barrier
                          open while a train is   could allow road
                          present in or           traffic to enter the
                          approaching the         crossing and collide
                          crossing.               with the train.

  **C2**                  The barrier must be     Road traffic must be
                          closed before a train   prevented from entering
                          enters the crossing.    the crossing before the
                                                  train arrives.

  **C3**                  Warning lights must be  Visual warnings alert
                          activated whenever a    drivers and pedestrians
                          train is approaching or that a train is
                          present at the          approaching or passing.
                          crossing.               

  **C4**                  The audible alarm must  An audible warning
                          be active whenever the  provides an additional
                          crossing is in a        safety signal,
                          train-warning state.    especially for people
                                                  who may not see the
                                                  warning lights.

  **C5**                  The barrier must remain The barrier must
                          closed while the train  prevent road traffic
                          is passing through the  from entering the
                          crossing.               crossing during train
                                                  passage.

  **C6**                  The barrier may open    A train may still be
                          only after the system   present even if a
                          has confirmed that the  sensor temporarily
                          train has completely    reports that the
                          cleared the crossing.   crossing is clear.

  **C7**                  If a train-detection    A failed or incorrect
                          sensor fails or gives   sensor could falsely
                          an unreliable reading,  indicate that no train
                          the system must enter a is present. Keeping the
                          safe state and must not barrier closed prevents
                          open the barrier.       unsafe road access.

  **C8**                  If a barrier fails to   A failed barrier
                          close when a train is   creates a direct
                          approaching, the system collision risk and
                          must issue an emergency requires an immediate
                          warning and prevent     safety response.
                          normal road traffic     
                          from being allowed      
                          through.                

  **C9**                  Loss of communication   Communication failure
                          with the control center must not result in the
                          must not cause the      barriers opening while
                          crossing to enter an    a train may be present.
                          unsafe state.           

  **C10**                 The system must not     A false clear
                          report that the         indication could cause
                          crossing is clear       the barriers to open
                          unless train-detection  too early.
                          information confirms    
                          that the train has      
                          completely passed.      

  **C11**                 Emergency conditions    Emergency situations
                          must activate the       require immediate
                          appropriate warning and action to protect road
                          safety response.        users, railway
                                                  personnel, and the
                                                  train.

  **C12**                 The system must not     Conflicting commands
                          allow conflicting       can produce
                          safety commands, such   unpredictable barrier
                          as opening the barrier  behavior and compromise
                          while simultaneously    safety.
                          commanding it to remain 
                          closed.                 
  -----------------------------------------------------------------------

## Summary

These constraints define the safety boundaries of ARLCCS. They specify
what the system is allowed to do and, more importantly, what it must
never do. The constraints can later be converted into formal logical
expressions so that violations can be detected systematically.
