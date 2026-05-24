# Part 1: Job Shop Scheduling (40 marks)

> **Note for this submission:** I am an AIML320 student, so the AIML420-specific
> tasks (and the AIML420-only marks) are **not required**. Questions are tagged
> below with which course they apply to.

## Objectives

The goal of this assignment is to help you understand the basic concepts of
planning and scheduling, and simple algorithms for them. In particular, the
following topics should be reviewed:

- Investigate a job shop scheduling problem.
- Implement a heuristic to solve a scheduling problem.

## Problem Description

You are required to find solutions (schedules) for a job shop scheduling problem,
with **3 jobs** and **2 machines**, as shown in the table below.

| Job | Arrival Time | Operation | Machine | Proc Time |
|-----|--------------|-----------|---------|-----------|
| J1  | 0            | O11       | M1      | 50        |
|     |              | O12       | M2      | 25        |
| J2  | 10           | O21       | M2      | 30        |
|     |              | O22       | M1      | 35        |
| J3  | 20           | O31       | M1      | 40        |
|     |              | O32       | M2      | 20        |

### Constraints

- **Number of operations:** Each job `Jj` has two operations `Oj1` and `Oj2`.
- **Precedence constraint:** Operations must strictly follow the precedence
  constraint. That is, processing of `Oj2` (j = 1, 2, 3) cannot start before
  `Oj1` has been completely processed.
- **Arrival time:** Each job has an arrival time (`ArrivalTime`). For each job
  `Jj`, processing of the first operation `Oj1` cannot start earlier than the
  job's arrival time.
- **Resource constraint:** Each machine can process at most one operation at a
  time. Each operation can only be processed by a particular machine. For
  example, operation `O11` can only be processed by machine `M1`.

## Solution / Schedule Representation

A solution/schedule for a job shop scheduling problem is a sequence of actions.
Each action is composed of the processed operation, the machine to process the
operation, and the starting time. The finishing time of an action is the
starting time plus the processing time of the processed operation. The actions
are sorted in ascending order of starting time, i.e., the former action starts
no later than the latter one.

In this assignment, the following format is adopted to represent a schedule:

```
Process(O11, M1, 0) → Process(O21, M2, 10) → ...
```

where `Process(o, m, t)` stands for an action that processes operation `o` with
machine `m` starting at time `t`.

> You do not need to write code for the questions in Part 1.

## Questions

### Question 1 — Earliest starting times (10 marks)

Suppose you are given a schedule whose action sequence is as follows:

```
Process(O11, M1, t1) → Process(O21, M2, t2) → Process(O31, M1, t3) →
Process(O12, M2, t4) → Process(O22, M1, t5) → Process(O32, M2, t6)
```

Since the sequence of actions is sorted in non-decreasing order of starting
time, you know that `t1 ≤ t2 ≤ t3 ≤ t4 ≤ t5 ≤ t6`.

Calculate the earliest starting time for each of the six actions, i.e., `t1` to
`t6`. You can draw a Gantt chart to help you think.

> **Hint:** The earliest starting time of an action is the later of two times:
> the earliest ready time of the operation, and the earliest idle time of the
> machine.

### Question 2 — Completion times and makespan (10 marks AIML320 / 5 marks AIML420)

For the solution given in Question 1, find the completion time of each job, which
is the finishing time of its last operation. Then calculate the **makespan** of
the solution, defined as the maximum completion time of all the jobs.

### Question 3 — SPT solution (10 marks AIML320 / 5 marks AIML420)

Write the final solution obtained by the **Shortest Processing Time (SPT)**
dispatching rule. You may draw a figure (Gantt chart) to help you find the
solution.

### Question 4 — Compare SPT vs FCFS (5 marks)

For the solution obtained by the SPT rule, calculate the completion time of each
job and the makespan. Compare the makespan of this solution with that obtained
in Question 1 to find out which solution is better in terms of makespan.

> **Note:** The solution in Question 1 is obtained by the
> First-Come-First-Serve (FCFS) rule.

### Question 5 — Does a better solution mean a better rule? (5 marks)

The two compared solutions are obtained by the SPT and FCFS rules, respectively.
If one solution is better than the other, does it mean that the rule that
generates the better solution is better than the other rule? Why or why not?

### Question 6 — Static and dynamic solution methods (AIML420 mandatory, 10 marks)

> **AIML420 only — not required for this AIML320 submission.**

Often in practice, neither the SPT nor FCFS rules are good enough for solving the
job shop scheduling problem. Suggest two methods to solve the job shop scheduling
problem:

- One method should consider the problem to be **static** (all information is
  known in advance).
- The other method should consider it to be **dynamic** (e.g., unpredicted job
  arrivals can happen in real time).

Clearly describe your methods (e.g., algorithm framework, solution
representation/encoding, search operators).
