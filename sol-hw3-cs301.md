# Homework 3

## Written
### Chomskey Normal Form 1
Consider the following grammar:
$S \longrightarrow ABA \mid B$
$A \longrightarrow 0A \mid 1B1$
$B \longrightarrow 1 \mid 1B \mid \varepsilon$
In this problem, we will go through the process of converting to Chomskey Normal Form:
(a) Give the resulting grammar after completing the **START** step.
$S_0 \longrightarrow  S$
$S \longrightarrow ABA \mid B$
$A \longrightarrow 0A \mid 1B1$
$B \longrightarrow 1 \mid 1B \mid \varepsilon$
(b) Give the resulting grammar after completing the **BIN** step.
$S_0 \longrightarrow S$
$S \longrightarrow AT \mid B$
$T \longrightarrow BA$
$A \longrightarrow 0A \mid 1U$
$U \longrightarrow B1$
$B \longrightarrow 1 \mid 1B \mid \varepsilon$
(c) Give the resulting grammar after completing the **DEL** step.
$S_0 \longrightarrow S \mid \varepsilon$
$S \longrightarrow AT \mid B$
$T \longrightarrow BA \mid A$
$A \longrightarrow 0A \mid 1U$
$U \longrightarrow B1 \mid 1$
$B \longrightarrow 1 \mid 1B$ 
(d) Give the resulting grammar after completing the **UNIT** step.
1. Replacing Bs and As
	$S_0 \longrightarrow S \mid \varepsilon$
	$S \longrightarrow AT \mid 1 \mid 1B$
	$T \longrightarrow BA \mid 0A \mid 1U$
	$A \longrightarrow 0A \mid 1U$
	$U \longrightarrow B1 \mid 1$
	$B \longrightarrow 1 \mid 1B$ 
2. Replacing S
	$S_0 \longrightarrow AT \mid 1 \mid 1B \mid \varepsilon$
	$S \longrightarrow AT \mid 1 \mid 1B$
	$T \longrightarrow BA \mid 0A \mid 1U$
	$A \longrightarrow 0A \mid 1U$
	$U \longrightarrow B1 \mid 1$
	$B \longrightarrow 1 \mid 1B$ 

(e) Give The resulting grammar after completing the **TERM** step.
$S_0 \longrightarrow AT \mid 1 \mid XB \mid \varepsilon$
$S \longrightarrow AT \mid 1 \mid XB$
$T \longrightarrow BA \mid YA \mid XU$
$A \longrightarrow YA \mid XU$
$U \longrightarrow BX \mid 1$
$B \longrightarrow 1 \mid XB$ 
$X \longrightarrow 1$
$Y \longrightarrow 0$
### Chomskey Normal Form 2

Consider the following Grammar:
$S \longrightarrow aY \mid bX \mid XY$
$X \longrightarrow YYY \mid aY$
$Y \longrightarrow bX \mid \varepsilon$
In this problem, we will go through the process of converting this grammar to Chomskey Normal Form:

(a) Give the resulting grammar after completing the **START** step.
$S_0 \longrightarrow S$
$S \longrightarrow aY \mid bX \mid XY$
$X \longrightarrow YYY \mid aY$
$Y \longrightarrow bX \mid \varepsilon$

(b) Give the resulting grammar after completing the **BIN** step.
$S_0 \longrightarrow S$
$S \longrightarrow aY \mid bX \mid XY$
$X \longrightarrow YC \mid aY$
$Y \longrightarrow bX \mid \varepsilon$
$C \longrightarrow YY$

(c) Give the resulting grammar after completing the **DEL** step.
1. Subbing for $\varepsilon$ of $Y$:
	$S_0 \longrightarrow S$
	$S \longrightarrow aY \mid bX \mid XY \mid a \mid X$
	$X \longrightarrow YC \mid aY \mid C \mid a$
	$Y \longrightarrow bX \mid \varepsilon$
	$C \longrightarrow YY \mid Y \mid \varepsilon$
2. Subbing for $\varepsilon$ of $C$:
	$S_0 \longrightarrow S$
	$S \longrightarrow aY \mid bX \mid XY \mid a \mid X$
	$X \longrightarrow YC \mid aY \mid C \mid a \mid Y \mid \varepsilon$
	$Y \longrightarrow bX$
	$C \longrightarrow YY \mid Y$
3. Subbing for $\varepsilon$ of X
	$S_0 \longrightarrow S$ 
	$S \longrightarrow aY \mid bX \mid XY \mid a \mid X \mid b \mid Y \mid \varepsilon$
	$X \longrightarrow YC \mid aY \mid C \mid a \mid Y$
	$Y \longrightarrow bX \mid b$
	$C \longrightarrow YY \mid Y$
4. Subbing for $\varepsilon$ of S (final form for this step)
	$S_0 \longrightarrow S \mid \varepsilon$ 
	$S \longrightarrow aY \mid bX \mid XY \mid a \mid X \mid b \mid Y$
	$X \longrightarrow YC \mid aY \mid C \mid a \mid Y$
	$Y \longrightarrow bX \mid b$
	$C \longrightarrow YY \mid Y$

(d) Give the resulting grammar after completing the **UNIT** step.
1. Replacing $C$
	$S_0 \longrightarrow S \mid \varepsilon$ 
	$S \longrightarrow aY \mid bX \mid XY \mid a \mid X \mid b \mid Y$
	$X \longrightarrow YC \mid aY \mid YY \mid Y \mid a \mid Y$
	$Y \longrightarrow bX \mid b$
	$C \longrightarrow YY \mid Y$
2. Replacing $Y$
	$S_0 \longrightarrow S \mid \varepsilon$ 
	$S \longrightarrow aY \mid bX \mid XY \mid a \mid X \mid b \mid bX \mid b$
	$X \longrightarrow YC \mid aY \mid YY \mid a \mid bX \mid b$
	$Y \longrightarrow bX \mid b$
	$C \longrightarrow YY \mid bX \mid b$
3. Replacing $X$
	$S_0 \longrightarrow aY \mid bX \mid XY \mid a \mid YC \mid YY \mid b \mid \varepsilon$ 
	$S \longrightarrow aY \mid bX \mid XY \mid a \mid YC \mid YY \mid b$
	$X \longrightarrow YC \mid aY \mid YY \mid a \mid bX \mid b$
	$Y \longrightarrow bX \mid b$
	$C \longrightarrow YY \mid bX \mid b$
(e) Give the resulting grammar after completing the **TERM** step (Final Form).
	$S_0 \longrightarrow AY \mid BX \mid XY \mid a \mid YC \mid YY \mid b \mid \varepsilon$ 
	$S \longrightarrow AY \mid BX \mid XY \mid a \mid YC \mid YY \mid b$
	$X \longrightarrow YC \mid AY \mid YY \mid a \mid BX \mid b$
	$Y \longrightarrow BX \mid b$
	$C \longrightarrow YY \mid BX \mid b$
	$A \longrightarrow a$
	$B \longrightarrow b$
### Ambiguous Grammars
A grammar is considered **ambiguous** if it has **two or more different leftmost derivations** for some string. A **leftmost derivation** is one in which we expand the leftmost nonterminal symbol in the string at each step.

Consider the following context-free grammar:

$S \longrightarrow SS \mid TST \mid U$
$T \longrightarrow a \mid b$
$U \longrightarrow \varepsilon$

Prove that this grammar is **ambiguous** by giving an example of a string that can be derived in multiple distinct ways by this grammar and giving **two different leftmost** derivations and the corresponding parse trees for that string.
#### Derivations:

1. $S \rightarrow TST \rightarrow aST \rightarrow aUT \rightarrow a\varepsilon T \rightarrow aa$ 
 ![[cs301-hw3-ambigG-1.jpeg]]


2. $S \rightarrow SS \rightarrow TSTS \rightarrow aSTS \rightarrow aUTS \rightarrow a\varepsilon TS \rightarrow aaS \rightarrow aaU \rightarrow aa\varepsilon \rightarrow aa$
![[cs301-hw3-ambigG-2.jpeg]]



## Reference
[[cs301_languages_and_automata]]