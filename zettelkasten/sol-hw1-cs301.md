---
title: Homework 1
author: Muhammad Talha Adnan Khan
date: 2025-02-09
course: CS301 - Languages and Automata
email: mkhan387@uic.edu
---
---
# Home work 1: Finite Automata (and the like)
---
## Part $II$: Proofs

## 3. NFA Complement Closure:
***Problem statement:***
If $M$ is a DFA that recognizes a regular language $L$, by swapping the accepting and non-accepting states yields a new DFA that recognizes the complement of $L$. Show, by giving a counter example, that this construction may not work if $M$ is an NFA instead of a DFA. That is, show that this $M$ is an NFA that recognizes a regular language $L$, swapping the accepting and non-accepting states doesn't necessarily yield a new NFA that recognizes the complement of $L$.

### Solution:

**Claim** 
Swapping accepting and non-accepting states in an NFA $M$ yields an NFA $M'$ such that $L(M') = \overline{L(M)}$ 

---
#### Counterexample  
Define the NFA $M = (Q, \Sigma, \delta, q_0, F)$:  
- **States:** $Q = \{q_0, q_1\}$  
- **Alphabet:** $\Sigma = \{a\}$  
- **Start State:** $q_0$  
- **Accepting States:** $F = \{q_1\}$  
- **Transitions:**  
  $$
  \delta(q_0, a) = \{q_0, q_1\}, \quad \delta(q_1, a) = \{q_1\}.
  $$
---
## Language of $M$  
$L(M) = \{w \mid w \text{ contains at least one } a\}$.  
- **Accepted Strings:** $a, aa, aaa, \dots$  
- **Rejected String:** $\varepsilon$ (empty string).
## Complement Language  
$\overline{L(M)} = \{\varepsilon\}$.  
- **Only Accepted String:** $\varepsilon$.
## Swapped NFA $M'$  
Swap accepting/non-accepting states:  
- **New Accepting States:** $F' = \{q_0\}$.  
- All transitions remain the same.
## Language of $M'$  
$L(M') = \{\varepsilon, a, aa, \dots\}$.  
- **Accepted Strings:** $\varepsilon, a, aa, \dots$.  
- **Rejected Strings:** None (since $q_0$ is always accepting).
## Why the Claim Fails  
In NFAs, a string is accepted if **any path** leads to an accepting state. After swapping:  
1. $\varepsilon$ is accepted (valid for $\overline{L(M)}$).  
2. $a$ is accepted via the path $q_0 \rightarrow q_0$ (invalid for $\overline{L(M)}$).  

$$
\boxed{Thus, L(M') \neq \overline{L(M)}.}  
$$
## Conclusion  
Swapping accepting/non-accepting states in an NFA does **not** guarantee recognition of the complement language.  


## Kleene Star Closure
**Problem Statement**
Let $M = (Q, \Sigma, \delta, q_0, F)$ be a DFA that recognizes a regular language $L$. Construct a new NFA $N = (Q, \Sigma, \delta', q_0, F')$ to recognize the Kleene star of $L$ (i.e., $L^*$ ) such that:
- The states of $N$ (i.e., $Q$) are the same as the states of $M$.
- the start state of $N$ (i.e., $q_0$) is the same as the start state of $M$. 
- $F' = F \cup \{q_0\}$. That is, the accepting states of $N$ (i.e., $F'$) are the accepting states of $M$ and the start state.
- $\delta'$ is defined as follows for any $q \in Q$ and any $c \in \Sigma \cup \{\varepsilon\}$:
$$
$$
$$
\delta'(q, c) = 
\begin{cases} 
\delta(q, c) & \text{if } q \notin F \text{ or } c \neq \varepsilon \\
\delta(q, c) \cup \{q_0\} & \text{if } q \in F \text{ and } c = \varepsilon
\end{cases}
$$ 
That is, the transitions of $N$ (i.e., $\delta'$) are the transitions of $M$ and $\varepsilon$ - transitions from accepting states of $M$ to the start state.
**Show by giving counter example, that this construction doesn't necessarily yield a new NFA that recognizes the Kleene star $L$. Additionally explain how to fix this construction so that the new NFA does recognize the Kleene star of $L$.

### Solution
#### The Counterexample

We now show that this construction may fail to recognize $L^*$.

### Define a Specific Language $L$ and Its DFA $M$

Let
$$
L = \{a^2,\, a^3\},
$$
i.e., 
$$
L = \{ aa,\; aaa\}.
$$
Then,
$$
L^* = \{ \varepsilon,\, a^2,\, a^3,\, a^4,\, a^5,\, a^6,\, \dots \},
$$
so, for example, the string
$$
a^5 \quad (\text{i.e., } aaaaa)
$$
should be accepted because
$$
a^5 = a^2 \cdot a^3.
$$

We construct a DFA $M$ for $L$ as follows:
- **Alphabet:** $\Sigma = \{a\}$.
- **States:** $Q = \{q_0, q_1, q_2, q_3\}$.
- **Start state:** $q_0$.
- **Transitions:**
  - $\delta(q_0, a) = q_1$,
  - $\delta(q_1, a) = q_2$,
  - $\delta(q_2, a) = q_3$.
- **Accepting states:**  
  Let
  $$
  F = \{q_2, q_3\}.
  $$
  Here, $q_2$ represents having read exactly two $a$’s (i.e., $aa$) and $q_3$ represents having read three $a$’s (i.e., $aaa$).

Thus, $L(M) = \{aa,\, aaa\}$.

### Applying the Flawed Construction

According to the naive construction, we build an NFA 
$$
N = (Q, \Sigma, \delta', q_0, F')
$$ 
with:
- **Accepting states:**  
  $$
  F' = F \cup \{q_0\} = \{q_0, q_2, q_3\}.
  $$
- **Additional $\varepsilon$–transitions:**  
  For each $q \in F$ (i.e., for $q_2$ and $q_3$), add
  $$
  \delta'(q, \varepsilon) \supseteq \{q_0\}.
  $$

#### Examining the String $a^5$ (i.e., $aaaaa$)

A correct segmentation for $a^5$ would be:
1. **First copy:**  
   $q_0 \xrightarrow{a} q_1 \xrightarrow{a} q_2$ (accepting, corresponding to $aa$).
2. **Reset via $\varepsilon$:**  
   $q_2 \xrightarrow{\varepsilon} q_0$.
3. **Second copy:**  
   $q_0 \xrightarrow{a} q_1 \xrightarrow{a} q_2 \xrightarrow{a} q_3$ (accepting, corresponding to $aaa$).

Thus, there is an accepting run along this branch.

However, due to nondeterminism the NFA might choose a **faulty branch**. For example, suppose that after reaching $q_2$ (after two $a$’s) the NFA *does not* immediately take the $\varepsilon$–transition. Instead, it continues:
- From $q_2$, it reads another $a$ to go to $q_3$ (thus “committing” to a copy of length 3 rather than ending a copy at $q_2$).
- Then, if it takes the $\varepsilon$–transition from $q_3$ to $q_0$, the remaining input (only one $a$) is insufficient to form either $aa$ or $aaa$.

In such a branch the computation ends in a nonaccepting state. Because the construction relies on nondeterministic choices to “cut” the input at exactly the right moment, it does not *guarantee* that every string in $L^*$ (i.e., every valid segmentation) has an accepting run.

In other words, **by reusing the original start state $q_0$ in the middle of processing a copy of a word from $L$, the construction creates an ambiguity that can cause valid strings in $L^*$ to be rejected.**

---

## Construction

To eliminate this ambiguity, we introduce a **new start state** that is separate from the states of $M$. The corrected NFA is defined as follows:

Define
$$
N' = \Big(Q \cup \{q_{\text{new}}\},\, \Sigma,\, \delta',\, q_{\text{new}},\, F \cup \{q_{\text{new}}\}\Big),
$$
with the following adjustments:
4. **New Start State:**  
   $q_{\text{new}}$ is the new start state and is also accepting (ensuring $\varepsilon$ is accepted).
5. **$\varepsilon$–Transition from New Start:**  
   Add an $\varepsilon$–transition from $q_{\text{new}}$ to the original start state $q_0$:
   $$
   \delta'(q_{\text{new}}, \varepsilon) = \{q_0\}.
   $$
6. **Restarting Copies:**  
   For every accepting state $q \in F$ of the original DFA $M$, add an $\varepsilon$–transition from $q$ back to $q_0$:
   $$
   \delta'(q, \varepsilon) \supseteq \{q_0\}.
   $$

This construction guarantees that every new copy of a word in $L$ is initiated only by leaving the new start state, thus eliminating the ambiguity in segmentation.

---

## Conclusion

- **Flawed Construction:**  
  Using 
  $$
  F' = F \cup \{q_0\}
  $$
  and adding $\varepsilon$–transitions from accepting states to $q_0$ may force the NFA to “reset” in the middle of processing a copy of a word from $L$, causing some strings in $L^*$ to be rejected.

- **Correct Construction:**  
  Introducing a new start state $q_{\text{new}}$ (which is also accepting) and adding an $\varepsilon$–transition from $q_{\text{new}}$ to $q_0$ ensures that every copy of a word in $L$ begins in a controlled manner. This construction correctly recognizes $L^*$.



### Reverse Closure
5 Tuple that describes the NFA

$$
\boxed{

M^R \;=\;\bigl(Q \cup \{q_0{\prime}\},\;\Sigma,\;\delta^R,\;q_0{\prime},\;\{\,q_0\}\bigr).

}
$$
where:

1. **States**: $Q^R = Q \cup \{q_0{\prime}\}.$

2. **Alphabet**: The same input alphabet $\Sigma$.

3. **Start state**: $q_0{\prime}$ is a new state, not in Q.

4. **Set of final states**: $\{\,q_0\}$, i.e. the old start state becomes the _only_ final state.

5. **Transition function** $\delta^R$ is defined by:

• For each transition $\delta(q,a)\ni r$ in M, add $\delta^R(r,a)\ni q$ in $M^R$.

• Also, for every final state $f \in F$, add $\delta^R(q_0{\prime},\varepsilon)\ni f$.

This $M^R$ recognizes exactly $L^R$.


[[cs301_languages_and_automata]]