2025-02-22 12:07

Status: #baby 

Tags: [[cs301_languages_and_automata]]
# 301_chap1_notes

### Finite Automaton:
It is like a very rudimentary and simple robot.
1. What it does it that it reads a string of symbols (like letters or numbers) one by one.
2. Moves between different states based on the symbol it reads.
3. Ends in a state that tells you whether the string is to be accepted or rejected.
#### Example
- Like a ticket-checking machine at a train station
- It scans your ticket letter by letter.
- It changes states for like for this example checking date, destination, seat number
- If everything matches the rules, it **accepts** the ticket. If not, it **rejects**.

Now this is useful as it helps us to under stand patterns, like checking if a password is valid or processing search queries.

In easy words these are the *key points*:
- It has states (like *waiting*, *processing*, *error*).
- It reads symbols one by one.
- It moves between states based on *fixed rules*.
- It *accepts* or *rejects* the string at the end.
---

Figure depicting a finite Automaton called $M_1$ 
**State Diagram:**
![[fig1.4-chap1.jpg]]
This is an example on how a state machine looks.
This is known as a ***State Diagram***. For this course we are going to be using **JFLAP** software to create this type of diagrams.
*Description $M_1$:*
So this is how you look at a state diagram and work through it.
- The circles are known as **states** which are labeled $\mathbf{{q_{1}, q_{2}, q_{3} }}$  
- The **Start State**, $q_1$, which is indicated by the arrow pointing at it from nowhere.
- The **Accept State**, $q_2$, is the one with the double circle.
- The *arrows* are known as the **Transitions**.
When this receives an input string such as 1101, it processes the string and produces an output. The output is what ever state the last char of the string makes us land and and depending on that the output is either **Accepted** or **Rejected**.

#### Example
Input: 1101
##### $M_1$'s processing procedure:
1. Start in state $q_1$.
2. Read 1, follow transition from $q_1$ to $q_2$.
3. Read 1, follow transition from $q_2$ to $q_2$.
4. Read 0, follow transition from $q_2$ to $q_3$.
5. Read 1, follow transition from $q_3$ to $q_2$.
6. **Accept** $\because$ $M_1$ is in an accept state $q_2$ at the end of the input.

The formal definition is precise and resolves any uncertainties about what is allowed in a finite automaton. Is is arcane and hard so just remember it.

##### Finite Automaton's parts:
1. Set of **States**
2. Input **Alphabet** that indicates all of the allowed input symbols.
3. **Start State**
4. List of **Accept States**
5. Rules for moving

###### ***Note:*** 
If a finite automaton has an arrow from a state $x$ to state $y$ labled with input symbol $1$, that means that if the automation is in state $x$ when it reads $1$, it then moves to state $y$. We can indicate that same transition by saying that $\delta(x, 1) = y$. This notation is a math shorthand.

### Formal Definition:
A **finite automaton** is a $5 \text{ tuple}$ $(Q, \Sigma, \delta, q_0, F)$ where:
1. $Q$ is a finite set called the **States**,
2. $\Sigma$ is a finite set called the **Alphabet**,
3. $\delta: Q \times E \longrightarrow Q$ is the **Transition function** [Syntax-Explanation](#Note)
4. $q_0 \in Q$ is the **Start State**, and
5. $F \subseteq Q$ is the **Set of accept states**.

We can describe $M_1$ formally by writing $M_1 = (Q, \Sigma, \delta, q_1, F)$, where:
1. $Q = \{ q_1, q_2, q_3 \}$
2. $\Sigma = \{ 0, 1 \}$
3. $\delta$ is described as:

| Current State |  0  |  1  |
|:-------------:|:---:|:---:|
|    **q1**     | q1  | q2  |
|    **q2**     | q3  | q2  |
|    **q3**     | q2  | q2  |
1. $q_1$ is the start state
2. $F = \{ q_2 \}$

If $A$ is a set of all strings that machine $M$ accepts we say that $A$ is **language of machine** $M$ and write $L(M) = A$. We say **M recognizes A** or **M accepts A**.

$$
A = \{\, w \mid w \text{ contains at least one 1 and an even number of 0s follow the last 1}\}
$$

*Then $L(M_1) = A$, or equivalently, $M_1$ recognizes $A$.*





















## Reference
[[Introduction-to-the-theory-of-computation]]