# Part 1 — Job Shop Scheduling: Study Worksheet

> **How to use this file.** This is *your* worksheet. The concepts and method are filled in,
> but the answer cells are blank on purpose — you compute them, and I'll check each one before
> we move on. We'll go question by question in chat.

---

## The problem (reference data)

3 jobs, 2 machines. Strict precedence (Oj2 only after Oj1 finishes), each job has an arrival
time, each operation runs on one fixed machine for a fixed time.

| Job | Arrival | Op  | Machine | ProcTime |
|-----|---------|-----|---------|----------|
| J1  | 0       | O11 | M1      | 50       |
|     |         | O12 | M2      | 25       |
| J2  | 10      | O21 | M2      | 30       |
|     |         | O22 | M1      | 35       |
| J3  | 20      | O31 | M1      | 40       |
|     |         | O32 | M2      | 20       |

---

## §0 — Concepts cheat-sheet

1. **Three constraints**
   - *Precedence:* Oj2 cannot start until Oj1 is completely finished.
   - *Arrival:* Oj1 (first op of a job) cannot start before the job's arrival time.
   - *Resource:* a machine does one operation at a time; each op runs on its assigned machine.

2. **Operation ready time** = the earliest an op *could* start if its machine were free:
   - First op `Oj1` → ready at the **job's arrival time**.
   - Second op `Oj2` → ready at the **finish time of `Oj1`**.

3. **Machine free time** = the time the machine finishes whatever it was scheduled to do before.
   (Starts at 0 for both machines.)

4. **The core formula** (this is the assignment's hint):

   ```
   start = max( operation ready time , machine free time )
   finish = start + ProcTime
   ```

   In words: an op waits for *both* its own prerequisites (arrival/precedence) *and* the machine.
   Whichever is later wins.

5. **Completion time of a job** `Cj` = finish time of its **last** operation (`Oj2`).

6. **Makespan** = `max(C1, C2, C3)` — when *everything* is done.

7. **Dispatching rules** decide *which* waiting op a freed-up machine takes next:
   - **FCFS** (First-Come-First-Serve): take the op that became **ready/queued earliest**.
   - **SPT** (Shortest Processing Time): take the ready op with the **smallest ProcTime**.

8. **Gantt chart** = two timelines (M1, M2) on a shared axis. A block = one op. Look for **idle
   gaps** (machine free but nothing ready) and notice when a block is pushed right because a
   constraint, not the machine, was the bottleneck.

---

## §1 — The reusable recipe (apply to any given action sequence)

Process the actions **in the given order**, one at a time. For each action:

1. Find the **operation ready time** (rule 2 above).
2. Find the **machine free time** = when that machine last finished (rule 3).
3. `start = max(ready, machine free)`.
4. `finish = start + ProcTime`.
5. **Update** that machine's free time to `finish` (for later actions), and if this was `Oj1`,
   remember `finish` because it becomes the ready time for `Oj2`.

Keep a running note of each machine's free time and each job's Oj1 finish as you go.

---

## §Q1 — Earliest start times (10 marks)

Given action sequence (this is the FCFS order):
`O11 → O21 → O31 → O12 → O22 → O32`

Fill in the four right-hand columns using the recipe. `op`, `machine`, `ProcTime` are given.

| # | op  | machine | ProcTime | ready time | machine free at | **start (tk)** | finish |
|---|-----|---------|----------|------------|-----------------|----------------|--------|
| 1 | O11 | M1      | 50       |            |                 | t1 =           |        |
| 2 | O21 | M2      | 30       |            |                 | t2 =           |        |
| 3 | O31 | M1      | 40       |            |                 | t3 =           |        |
| 4 | O12 | M2      | 25       |            |                 | t4 =           |        |
| 5 | O22 | M1      | 35       |            |                 | t5 =           |        |
| 6 | O32 | M2      | 20       |            |                 | t6 =           |        |

**Consistency check:** the start times must come out **non-decreasing**: t1 ≤ t2 ≤ t3 ≤ t4 ≤ t5 ≤ t6.

**Gantt (fill in the blocks — one row per machine):**

```
time:  0    10    20    30    40    50    60    70    80    90   100   110   120   130
M1  |
M2  |
```

---

## §Q2 — Completion times & makespan (10 marks)

Read the finish times from your Q1 table.

| Job | last op | completion time Cj |
|-----|---------|--------------------|
| J1  | O12     | C1 =               |
| J2  | O22     | C2 =               |
| J3  | O32     | C3 =               |

**Makespan** = max(C1, C2, C3) = ____

---

## §Q3 — Solution from the SPT rule (10 marks)

Here you **build** the schedule yourself instead of being given the order. Simulate forward in
time. Whenever a machine is free **and** ≥1 of its operations is ready, start the ready op with
the **smallest ProcTime**.

**Decision log** (add a row each time a machine starts an op):

| time | machine free | ready candidates (op : ProcTime) | chosen (smallest) | start | finish |
|------|--------------|----------------------------------|-------------------|-------|--------|
|      |              |                                  |                   |       |        |

**Resulting action sequence** (sorted by start time):

`Process(__, __, __) → Process(__, __, __) → Process(__, __, __) → Process(__, __, __) → Process(__, __, __) → Process(__, __, __)`

**Gantt:**

```
time:  0    10    20    30    40    50    60    70    80    90   100   110   120   130   140
M1  |
M2  |
```

---

## §Q4 — SPT completion times, makespan & comparison (5 marks)

| Job | last op | completion time Cj |
|-----|---------|--------------------|
| J1  | O12     | C1 =               |
| J2  | O22     | C2 =               |
| J3  | O32     | C3 =               |

**SPT makespan** = ____   **FCFS makespan (from Q2)** = ____

**Which is better (smaller makespan) for this instance?** ____

---

## §Q5 — Does the better solution mean the better rule? (5 marks)

Write a short argument. Guiding questions to structure it:

- How many problem instances did we compare the rules on? Is that enough to generalise?
- Could the ranking of FCFS vs SPT flip on a *different* set of jobs/times? Why?
- Should rules be judged on one result, or on average / worst-case behaviour over many problems?

**Your answer:**

---

## §Q6 — (AIML420 only — optional for you)

Not required for AIML320. If you want the extension later: one *static* method (all info known up
front — e.g. a search/metaheuristic over a permutation encoding) and one *dynamic* method
(handles unexpected arrivals in real time — e.g. online dispatching / re-scheduling). Ask me and
we'll flesh it out.
