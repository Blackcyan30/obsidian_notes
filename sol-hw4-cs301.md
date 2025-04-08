# Written
## Pumping Lemma for CF Languages [20 points]
### Question:
Using the pumping lemma for context-free languages shown in lecture, prove that the following language $L$ is not context-free:
$$
L = \{a^ib^jc^k \mid i, j , k \geq 0 \text{ and } i \leq min(j,k)\}
$$
### Solution:
##### Note: Conditions that satisfy the pumping lemma.
1. $|vy| > 0$
2. $|vxy| \leq p$
3. $uv^ixy^iz$ is in $L$ for every $i \geq 0$ 
#### ***Proof by Contradiction***
- Assume L is context free
- Let $p$ be the pumping length for $L$
Suppose we take the pumping length to be $p$.
So, i.e. Let string $S$ be $S = a^p, b^p, c^p$
For this proof we are assuming all divides will follow the rules: $|vy| > 0$ and $|vxy| \leq p$
#### Case 1:  $v$ and $y$ contain only one type of symbol.
**Case 1.1: v and y contains only a's**
Pumping up,  if i = 2 then $uvvxyyz$ will have more a's than b's or c's which breaks the rules of the language therefore this $S = uv^ixy^iz$ is not in $L$ for every $i > 0$.  
baacaac
**Case 1.2: v and y contain only b's**
Pumping down, if $i = 0$ then $uxz$ will have more a's than b's. Then, $uxz \notin L$ 
**Case 1.3: v and y contain only c's**
Pumping down if $i = 0$ then $uxz$ will have more a's than c's. Then $uxz \notin L$  
#### Case 2: $v$ or $y$ contain more than one type of symbol. 
**Case 2.1: vy contain a's and b's** 
Now suppose we pump up and $i = 2$ then we would have $uvvxyyz$. This means that if we take $vy$ to be a and b then we can possibly end up in a situation where there are more a's than b's which means that $uxz \notin L$ or we have the right number of a's and b's but not in the correct order which again makes it so that $uxz \notin L$. 
**Case 2.2: vy contain b's and c's** 
Now suppose we pump down and $i = 0$ then we could have $uxz$. This means that if we take $vy$ to be b's and c's then we can end up in a situation that we have either 0 b's and c's which means that $uxz \notin L$ or we can possibly have the situation in which we have the right number of b's and c's but not in the correct order like if we pump up we can have this situation like $i = 2$ in which case also $uv^ixy^iz \notin L$.
**Case 2.3: vy contains a's and c's**
Suppose we pump up and $i = 2$. This means we could end up in a situation in which we have the right number of a's and c's but not in the correct order in which case also $uv^ixy^iz \notin L$.
***Therefore:***
This language is not context free as pumping lemma states that it should be possible to divide a string $S$ that is generated from the language $L$ into $u, v, x, y, z$ such that $|vy| > 0$, $|vxy| \leq p$ and $uv^ixy^iz$ is in $L$ for every $i \geq 0$. But it is not possible to divide it like that for every $i$ so the language is not context free.

## TM Descriptions [40 points]
For each of the following languages, give an implementation-level description for a deterministic Turing Machine that decides that language. For each language, a few (non-exhaustive) strings that your TM should accept and reject are given. Your Turing Machine must halt on all inputs.

(a)
### Question:
$A = \{a^nb^m \mid m \neq n\}$, $\Sigma = \{a, b\}$
Accepts: $aaab$, $aaabbbb$, $aa$, $abb$, $bbbbb$
Rejects: $aabb$, $aabba$, $bbbaaa$, $aaaaabbbbb$, $\varepsilon$
#### Implementation-level Description for TM that describes A:
***M: On input string W*** 
1. Scan input from right to left, determine if it has the form a* b*. If it does not **reject**, if it does return the head to the beginning of the tape.
2. Read symbol if **a**, replace with **x**. If no **a** is found, go to step 5.
3. Move to the right until you find **b**, replace with **y**. If no **b** is found and read in a **blank**, **accept**
4. Move left until you reach **x**, Move right then go to step 2. 
5. Move right until you reach **b**, if found **accept**. If no **b** found and reach **blank**, **reject**.

(b)
### Question:
$B = \{0^n1^n2^m \mid n \leq m \leq 2n\}$, $\Sigma = \{0, 1, 2\}$
Accepts: 0011222, 012, 000111222222, 0122, 0000111122222
Rejects: 2, 201, 00112, 012222, 01122
#### Implementation-level Description for TM that describes A:
***M: On input string W*** 
1. Scan input from right to left, determine if it has the form $0^*, 1^* 2^*$. If it does not **reject**, if it does return the head to the beginning of the tape. If tape is empty **accept**
2. Read symbol, if **0**, replace it with **x**, if no **0** then go to step 5. 
3. Move to the right until you find **1**, replace it with a **y**.
4. Move left until you find a **x** then, move to the right and go to step 2. 
5. Move right until you reach a **2**. If you read a **blank**, **reject** 
6. Move left replacing all of the **y** with **1** and all of the **x** with **0** until you reach the start of the tape.
7. Read symbol, if it is **0** Replace with **x**. If **1** move right replacing all of the **z** to a **2** until you reach the end of the tape and then go left replacing all of the **x** with **0** until you reach the start of the tape then go to step 9.  
8. Move right until you find **2** replace it with **z**, move left until you find a **x**, then move right and go to step 1. If not **2**, **reject**.
9. Read symbol, if **0** replace with **x**. Move to the right until finding a **1**.
10. Replace **1** with a **y**. Move right until you find a **2**. If no **2** is found **accept**.
11. Replace **2** with a **z**. Move left until finding a **1** then go to step 10. If no **1** is found go to step 12.
12. Replace all of the **y** with **1** and move left until finding a **0**. If **0** is found, go to step 9. If there are no more **0**, move right until finding a **2**. If no **2** is found, **accept**, Otherwise **reject**.
(c)
### Question:
$C = \{0^i1^j2^k \mid j = i + k\}$, $\Sigma = \{0, 1, 2\}$
Accepts: 0112, 001112, 0011111222, 0000111112, 111222
Rejects: 001122, 0111222, 000111112, 00221111, 000222
#### Implementation-level Description for TM that describes A:
***M: On input string W*** 
1. Scan input from right to left, determine if it has the form $0^*, 1^*, 2^*$. If it does not **reject**, if it does return the head to the beginning of the tape. If tape is empty **accept**. 
2. Read symbol, if it is **0** replace with a **x**, move right until you encounter a **1**, if no **1** found **reject**.
3. Replace **1** with **y**. Move left until you encounter **0** then go to step 2. If no **0** is found go right until you find a **2**. If no 2 **accept**
4. Replace 2 with **z**. Move left until you encounter a **1**, go to step 3. If no **1** is found **reject** 