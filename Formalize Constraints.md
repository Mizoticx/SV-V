# Task 2 --- Formalize Constraints

## Automated Railway Level-Crossing Control System (ARLCCS)

The following eight constraints from Task 1 are expressed using simple
logical notation.

### Notation

-   `Train_Approaching` = a train is approaching the crossing.
-   `Train_Present` = a train is currently in the crossing.
-   `Train_Cleared` = the system has confirmed that the train has
    completely cleared the crossing.
-   `Barrier_Open` = the road barrier is open.
-   `Barrier_Closed` = the road barrier is closed.
-   `Warning_Light_On` = warning lights are active.
-   `Alarm_On` = audible alarm is active.
-   `Sensor_Failed` = a train-detection sensor has failed or is
    unreliable.
-   `Barrier_Failed` = the barrier has failed to close when required.
-   `Communication_Lost` = communication with the control center has
    been lost.
-   `Emergency` = an emergency condition exists.
-   `Safe_Mode` = the crossing is operating in a safe/fail-safe mode.
-   `Clear_Confirmed` = the system has confirmed that the crossing is
    clear.
-   `Normal_Road_Traffic_Allowed` = normal road traffic is allowed to
    pass.

------------------------------------------------------------------------

## C1 --- Barrier must not open while a train is present

**Formal expression:**

``` text
Train_Present → ¬Barrier_Open
```

**Meaning:** If a train is present, the barrier must not be open.

------------------------------------------------------------------------

## C2 --- Barrier must be closed before a train enters

**Formal expression:**

``` text
Train_Approaching → Barrier_Closed
```

**Meaning:** If a train is approaching, the barrier must be closed
before the train enters the crossing.

------------------------------------------------------------------------

## C3 --- Warning lights must be active when a train is approaching or present

**Formal expression:**

``` text
(Train_Approaching ∨ Train_Present) → Warning_Light_On
```

**Meaning:** If either a train is approaching or a train is already
present, the warning lights must be on.

------------------------------------------------------------------------

## C4 --- Audible alarm must be active during the warning state

**Formal expression:**

``` text
(Train_Approaching ∨ Train_Present) → Alarm_On
```

**Meaning:** Whenever a train is approaching or present, the audible
alarm must be active.

------------------------------------------------------------------------

## C5 --- Barrier must remain closed while the train is passing

**Formal expression:**

``` text
Train_Present → Barrier_Closed
```

**Meaning:** A train being present requires the road barrier to remain
closed.

------------------------------------------------------------------------

## C6 --- Barrier may open only after the train has completely cleared the crossing

**Formal expression:**

``` text
Barrier_Open → Train_Cleared
```

**Meaning:** Opening the barrier is permitted only when the system has
confirmed that the train has completely cleared the crossing.

------------------------------------------------------------------------

## C7 --- Sensor failure must result in a safe state and prevent opening

**Formal expression:**

``` text
Sensor_Failed → (Safe_Mode ∧ ¬Barrier_Open)
```

**Meaning:** If a train-detection sensor fails or becomes unreliable,
the system must enter safe mode and must not open the barrier.

------------------------------------------------------------------------

## C8 --- Barrier failure during train approach must trigger an emergency response

**Formal expression:**

``` text
(Train_Approaching ∧ Barrier_Failed) → Emergency
```

**Meaning:** If a train is approaching and the barrier has failed to
close, the system must enter an emergency condition.

------------------------------------------------------------------------

## Additional Useful Formal Constraints

The following expressions further describe the system's safety behavior.

### C9 --- Communication loss must not permit an unsafe open barrier

``` text
Communication_Lost → Safe_Mode
```

### C10 --- Crossing must not be declared clear without confirmation

``` text
Clear_Confirmed → Train_Cleared
```

### C11 --- Emergency condition must activate a safety response

``` text
Emergency → Safe_Mode
```

### C12 --- Normal road traffic must not be allowed when a train is present

``` text
Train_Present → ¬Normal_Road_Traffic_Allowed
```

## Summary

Formalization converts natural-language requirements into logical rules.
This makes the requirements easier to verify because the system can
compare its actual state with the expected logical condition and
identify when a constraint is violated.
