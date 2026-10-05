# Task 3 --- Identify Constraint Violations

## Automated Railway Level-Crossing Control System (ARLCCS)

Each scenario below shows a realistic situation in which one of the
formal constraints is violated.

------------------------------------------------------------------------

## Violation V1 --- Barrier opens while train is present

**Constraint:** C1

``` text
Train_Present → ¬Barrier_Open
```

**Observed state:**

``` text
Train_Present = TRUE
Barrier_Open = TRUE
```

**What went wrong?**

The system opened the road barrier even though a train was still present
in the crossing.

**Why is this a violation?**

C1 requires `¬Barrier_Open` whenever `Train_Present` is true. Since the
barrier is open, the required condition is false.

------------------------------------------------------------------------

## Violation V2 --- Barrier is not closed when a train is approaching

**Constraint:** C2

``` text
Train_Approaching → Barrier_Closed
```

**Observed state:**

``` text
Train_Approaching = TRUE
Barrier_Closed = FALSE
```

**What went wrong?**

A train is approaching, but the barrier has not closed.

**Why is this a violation?**

The condition `Train_Approaching` is true, so the barrier must be
closed. The observed state contradicts the constraint.

------------------------------------------------------------------------

## Violation V3 --- Warning lights are off while a train is approaching

**Constraint:** C3

``` text
(Train_Approaching ∨ Train_Present) → Warning_Light_On
```

**Observed state:**

``` text
Train_Approaching = TRUE
Train_Present = FALSE
Warning_Light_On = FALSE
```

**What went wrong?**

A train is approaching but the warning lights are not active.

**Why is this a violation?**

The expression `Train_Approaching ∨ Train_Present` is true, so
`Warning_Light_On` must also be true. It is false, therefore the
constraint is violated.

------------------------------------------------------------------------

## Violation V4 --- Audible alarm is off while a train is present

**Constraint:** C4

``` text
(Train_Approaching ∨ Train_Present) → Alarm_On
```

**Observed state:**

``` text
Train_Approaching = FALSE
Train_Present = TRUE
Alarm_On = FALSE
```

**What went wrong?**

The train is in the crossing, but the audible alarm is not active.

**Why is this a violation?**

Because `Train_Present = TRUE`, the left side of the implication is
true. Therefore `Alarm_On` must be true, but it is false.

------------------------------------------------------------------------

## Violation V5 --- Barrier opens while train is passing

**Constraint:** C5

``` text
Train_Present → Barrier_Closed
```

**Observed state:**

``` text
Train_Present = TRUE
Barrier_Closed = FALSE
```

**What went wrong?**

The train is passing through the crossing while the road barrier is not
closed.

**Why is this a violation?**

C5 requires the barrier to remain closed whenever a train is present.
Since the barrier is not closed, the constraint has been violated.

------------------------------------------------------------------------

## Violation V6 --- Barrier opens before the train is confirmed clear

**Constraint:** C6

``` text
Barrier_Open → Train_Cleared
```

**Observed state:**

``` text
Barrier_Open = TRUE
Train_Cleared = FALSE
```

**What went wrong?**

The system opened the barrier without confirming that the train had
completely cleared the crossing.

**Why is this a violation?**

C6 states that an open barrier implies a confirmed cleared train. Since
`Train_Cleared = FALSE`, the condition required by C6 is not satisfied.

------------------------------------------------------------------------

## Violation V7 --- Sensor failure but barrier opens

**Constraint:** C7

``` text
Sensor_Failed → (Safe_Mode ∧ ¬Barrier_Open)
```

**Observed state:**

``` text
Sensor_Failed = TRUE
Safe_Mode = FALSE
Barrier_Open = TRUE
```

**What went wrong?**

A train-detection sensor has failed, but the system neither entered safe
mode nor kept the barrier closed.

**Why is this a violation?**

C7 requires both `Safe_Mode = TRUE` and `Barrier_Open = FALSE` when a
sensor fails. Both required safety conditions are violated.

------------------------------------------------------------------------

## Violation V8 --- Barrier failure during train approach does not trigger emergency response

**Constraint:** C8

``` text
(Train_Approaching ∧ Barrier_Failed) → Emergency
```

**Observed state:**

``` text
Train_Approaching = TRUE
Barrier_Failed = TRUE
Emergency = FALSE
```

**What went wrong?**

A train is approaching and the barrier has failed, but the system has
not activated an emergency response.

**Why is this a violation?**

Both conditions in the left side of the implication are true, so
`Emergency` must be true. Since it is false, C8 is violated.

------------------------------------------------------------------------

## Violation V9 --- Communication loss does not put the system into safe mode

**Constraint:** C9

``` text
Communication_Lost → Safe_Mode
```

**Observed state:**

``` text
Communication_Lost = TRUE
Safe_Mode = FALSE
```

**What went wrong?**

Communication with the control center has been lost, but the crossing
continues operating without entering safe mode.

**Why is this a violation?**

The constraint requires safe mode whenever communication is lost. The
observed state does not satisfy that requirement.

------------------------------------------------------------------------

## Violation V10 --- Crossing is declared clear without train-clear confirmation

**Constraint:** C10

``` text
Clear_Confirmed → Train_Cleared
```

**Observed state:**

``` text
Clear_Confirmed = TRUE
Train_Cleared = FALSE
```

**What went wrong?**

The system reports that the crossing is clear even though it has not
confirmed that the train has completely cleared it.

**Why is this a violation?**

The implication requires `Train_Cleared = TRUE` whenever
`Clear_Confirmed = TRUE`. Since the train-clear confirmation is false,
the constraint is violated.

------------------------------------------------------------------------

## Violation V11 --- Emergency occurs but the system does not enter safe mode

**Constraint:** C11

``` text
Emergency → Safe_Mode
```

**Observed state:**

``` text
Emergency = TRUE
Safe_Mode = FALSE
```

**What went wrong?**

An emergency condition exists, but the system does not activate its safe
operating mode.

**Why is this a violation?**

C11 requires safe mode whenever an emergency is detected. The system
state contradicts this requirement.

------------------------------------------------------------------------

## Violation V12 --- Road traffic is allowed while a train is present

**Constraint:** C12

``` text
Train_Present → ¬Normal_Road_Traffic_Allowed
```

**Observed state:**

``` text
Train_Present = TRUE
Normal_Road_Traffic_Allowed = TRUE
```

**What went wrong?**

Normal road traffic is permitted to enter the crossing while a train is
present.

**Why is this a violation?**

C12 requires normal road traffic to be disabled whenever a train is
present. Since traffic is allowed, the constraint is violated.

------------------------------------------------------------------------

## Summary Table

  --------------------------------------------------------------------------------------------
  Violation ID      Constraint        Main Fault        Evidence of Violation
  ----------------- ----------------- ----------------- --------------------------------------
  **V1**            C1                Barrier opens     `Train_Present = TRUE`,
                                      while train is    `Barrier_Open = TRUE`
                                      present           

  **V2**            C2                Barrier not       `Train_Approaching = TRUE`,
                                      closed during     `Barrier_Closed = FALSE`
                                      train approach    

  **V3**            C3                Warning lights    Train approaching,
                                      remain off        `Warning_Light_On = FALSE`

  **V4**            C4                Audible alarm     Train present, `Alarm_On = FALSE`
                                      remains off       

  **V5**            C5                Barrier not       `Train_Present = TRUE`,
                                      closed during     `Barrier_Closed = FALSE`
                                      train passage     

  **V6**            C6                Barrier opens     `Barrier_Open = TRUE`,
                                      before train is   `Train_Cleared = FALSE`
                                      confirmed clear   

  **V7**            C7                Sensor failure    `Sensor_Failed = TRUE`,
                                      does not produce  `Safe_Mode = FALSE`,
                                      safe state        `Barrier_Open = TRUE`

  **V8**            C8                Barrier failure   Train approaching + barrier failed,
                                      does not trigger  `Emergency = FALSE`
                                      emergency         

  **V9**            C9                Communication     `Communication_Lost = TRUE`,
                                      loss does not     `Safe_Mode = FALSE`
                                      activate safe     
                                      mode              

  **V10**           C10               Crossing declared `Clear_Confirmed = TRUE`,
                                      clear without     `Train_Cleared = FALSE`
                                      confirmation      

  **V11**           C11               Emergency does    `Emergency = TRUE`,
                                      not activate safe `Safe_Mode = FALSE`
                                      mode              

  **V12**           C12               Road traffic      `Train_Present = TRUE`,
                                      allowed while     `Normal_Road_Traffic_Allowed = TRUE`
                                      train is present  
  --------------------------------------------------------------------------------------------

## Overall Conclusion

A constraint violation occurs when the actual system state contradicts a
rule that must always be satisfied. Formal constraints make this easier
to detect because each rule can be evaluated as true or false.

For ARLCCS, violations involving an open barrier, failed sensors, failed
barriers, communication loss, or incorrect train-clear information
should result in an appropriate fail-safe or emergency response. The
purpose of verification is to ensure that unsafe states are detected and
that the system responds according to its safety requirements.
