# CMPS 6610 Extra Credit Answers
  
In this extra credit assignment, we will test and review concepts you
   have learned since the midterm exam. Please add your written answers
   to `answers.md` which you can convert to a PDF using
   `convert.sh`. Alternatively, you may scan and upload written
   answers to a file named `answers.pdf`.



1. **Algorithmic Paradigms**
- My favorite algorithmic paradigm is Dynamic Programming (DP). I think inituitively it is very interesting and elegant. More specifically, it is fascinating because it allows us to solve problems that initially appear to require exponential time (like $O(2^n)$) by identifying overlapping subproblems (for example, the Fibonacci sequence). Through memoization by simply caching (building a hash table) the results of these subproblems (top-down approach) or building them iteratively (tabulation) through a bottom-up approach, we can reduce the complexity to polynomial time (often $O(n^2)$ or $O(n^3)$). DP effectively illustrates the trade-off between space and time.


2. **Divide and Conquer**
- Yes, problems that can be solved by a divide and conquer approach necessarily satisfy the optimal substructure property.
- **Proof**:
   - We will prove this by contradiction.
   - Let $P$ represent a problem that can be dolved by a Divide and Conquer Algorithm. The algorithm works by dividing $P$ into distinct subproblems $P_1, P_2, ..., P_k$ solving them to obtain solutions $S_1, S_2, ..., S_k$ and then combining these solutions into an integrated global solution $S$.
   - Optimal substructure is defined as the property wherby an optimal solution to the problem contains optimal solutions to its subproblems within it.
   - We will assume for the sake of contradiction that the optimal global solution $S$ is constructed from a sub-solution $S_i$ that is not optimal for subproblem $P_i$. This implies that there exists a different solution $S_i'$ to $P_i$ that is "better" than $S_i$.
   - The combination of the step is monotonic in that improving a component improves of maintains the quality of the while. It follows that we could replace $S_i$ with $S_i'$ to generate a new global solution $S'$. Since $S_i'$ is better than $S_i$, $S'$ would be tter than $S$. However, this contradicts the assumption that $S$ was the optimal solution. Therefore, the optimal solution $S$ must be compaosed of optimal sub-solutions $S_i$ and problems that can be solved by a divide and conquer approach necessarily satisfy the optimal substructure property.

3. **Randomization**

- 3a. 
- Let $X$ be the random variable for the number of comparisons. We know $E[X] \approx C n \ln n$ for some constant $C$. We are asking for the probability that $X \ge k n^2$ for some constant $k$.Using Markov's Inequality:$$P[X \ge k n^2] \le \frac{E[X]}{k n^2} = \frac{C n \ln n}{k n^2} = \frac{C \ln n}{k n}$$

$$\lim_{n \to \infty} \frac{C \ln n}{k n}$$
- Apply L'Hopital's Rule: Take the derivative with respect to $n$ of the numerator and the denominator separately.
   - Numerator: $\frac{d}{dn}(C \ln n) = \frac{C}{n}$
   - Denominator: $\frac{d}{dn}(k n) = k$
   - Evaluate the New Limit:$$\lim_{n \to \infty} \frac{\frac{C}{n}}{k} = \lim_{n \to \infty} \frac{C}{k n}$$
   Hence, as $n \to \infty$, the term $\frac{C}{kn}$ clearly goes to 0.

As $n \rightarrow \infty$, this probability approaches 0. The probability is bounded by $O(\frac{\log n}{n})$.
- 3b. We will calculate the probability that Quicksort does $10^c n \ln n$ comparisons, for a given $c>0$.
1. First, we will apply Markov's Inequality. We are given: 
   - Random Variable $X$: The number of comparisons Quicksort makes.
   - Expected Value $E[X]$: We know Quicksort's expected work is $E[X] \approx K n \ln n$ (where $K$ is a constant, typically around $2$  depending on the base of the logarithm).
   - Threshold $\alpha$: $10^c n \ln n$
   
- As for 3a, Markov's Inequality states:$$P(X \ge \alpha) \le \frac{E[X]}{\alpha}$$
- Substitute our values:$$P(X \ge 10^c n \ln n) \le \frac{K n \ln n}{10^c n \ln n}$$
2. We can then simplify and the $n \ln n$ terms cancel out:$$P(X \ge 10^c n \ln n) \le \frac{K}{10^c}$$ (Using the standard upper bound $E[X] \le 2 n \ln n$ - from the summation of the Harmonic series, this would be $\frac{2}{10^c}$ as we discussed in class in Jupyter book 3 of the randomized algorithms module).

- This result has implications for the "concentration" of the expected work for Quicksort in terms of the tail distribution. This suggests that there is a rapid decay as the parameter $c$ increases. The probability of the runtime reaching $10^c n \ln n$ decreases exponentially (specifically as $10^{-c}$ from the term $\frac{1}{10^c}$ ). Hence, it is extremely unlikely for Quicksort to take a very long time. For example, if $c = 2$, (checking $100nlnn$ comparisons), the probability is bounded by $\approx \frac{2}{100} = 0.02$.
4. **Greedy Algorithms**
- We will prove that scheduling jobs in order of their processing times (i.e., shortest-job-first) results in an optimal schedule where the cost is the average waiting time.
- The core logic for the proof will be based upon an "Exchange Argument"
   - Assume there is an optimal solution ($O$) that does not make the greedy choice.
   - Identify the first place where $O$ differs from the greedy choice.
   - Modify (Exchange) the optimal solution by swapping the non-greedy choice with the greedy choice.
   - Prove that this new solution is valid and no worse than the original optimal solution (or strictly better, which contradicts the optimality of the original).
- **Proof**: 
- Greedy Criterion:Our goal is to select the job with the shortest processing time first (Shortest-Job-First).
1. Optimal Substructure: 
   - Definition: An optimal solution can be constructed from optimal solutions of smaller subproblems. Application of optimal substructure:If we schedule the shortest job $j_1$ first, the problem reduces to finding the optimal schedule for the remaining $n-1$ jobs. The waiting time for the remaining jobs will be affected by $j_1$'s length, but their relative ordering to minimize their own "internal" waiting times remains a self-contained subproblem. Thus, we can solve for the first job and then recursively solve for the rest.
2. Greedy Choice Property:
   - Definition: The greedy choice (shortest job) must be in some optimal solution.
   - **Proof (by Exchange Argument)**: 
   - Let $G$ be the greedy strategy (picking the shortest job first).Let $O$ be an optimal schedule that minimizes total waiting time.
   - Assumption (Contradiction): Suppose the optimal schedule $O$ does not start with the shortest job. Let $a$ be the job with the shortest processing time ($p_a$ is minimal). Suppose $O$ starts with a different job $b$ (where $p_b > p_a$), and $a$ is scheduled somewhere later at position $k$.
   - Exchange (The Swap): Consider a new schedule $O'$ created by swapping job $a$ and job $b$.Job $a$ moves to the front (position 1).Job $b$ moves to position $k$
   - Analysis of Cost (Waiting Time):We compare the cost $C(O)$ and $C(O')$.
      - Job $a$: Waits less in $O'$ (moves to front). Reduction: it no longer waits for $b$ or the jobs between 1 and $k$
      - Job $b$: Waits more in $O'$ (moves back). Increase: it now waits for $a$ and the jobs between 1 and $k$.
      - Jobs in between: Their waiting times decrease because the long job $b$ was replaced by the shorter job $a$ in front of them.
      - Jobs after position $k$: Their total waiting time remains unchanged (the total time for the first $k$ jobs is the same since we just swapped two of them
   - The critical simplification is looking at the swap of just two adjacent inverted jobs. If we swap $b$ and $a$, the change in total waiting time is strictly: $$\Delta Cost = p_a - p_b$$
   - Since $p_a < p_b$ (because $a$ is the shortest job), the change is negative
   - Conclusion:$C(O') < C(O)$.This means the new schedule $O'$ is strictly better than the "optimal" schedule $O$. This is a contradiction.Therefore, the optimal solution $O$ must start with the shortest job $a$.Hence, by combining the Greedy Choice Property (the shortest job goes first) with Optimal Substructure (we solve the rest of the list recursively), we prove that the Greedy strategy produces the optimal schedule.
5. **Dynamic Programming**
Maximum Span (No Parallelism):Recurrence: $T(n) = T(n-1) + O(1)$Example: Calculating the $n$-th number in a sequence where each number depends strictly on the previous one, such as a naive iterative Fibonacci calculation ($F_i = F_{i-1} + F_{i-2}$) or finding the Longest Common Subsequence using the standard diagonal dependency.Span: $O(n)$. The dependency graph is a simple chain (line), so you cannot compute the $n$-th step until the $(n-1)$-th is finished.Polylogarithmic Span (Ideal Parallelism):Recurrence: $T(n) = T(n/2) + O(1)$ (in terms of depth)Example: A Divide and Conquer approach to DP, such as summing a list of numbers using a tree structure (Reduce/Tree Contraction) or parallel prefix sum.Span: $O(\log n)$. The dependency graph is a tree with depth $\log n$, allowing many branches to be computed simultaneously.
6. **Graphs**
Correction: The prompt text "largest weight cycle" 9 is likely a typo for "heaviest edge in a cycle." A Minimum Spanning Tree (MST) by definition contains no cycles, so proving it doesn't contain a "cycle" is trivial. The standard "Cycle Property" states that the heaviest edge in any cycle is not in the MST.Proof (for Heaviest Edge):Let $C$ be a cycle in graph $G$.Let $e = (u, v)$ be the heaviest edge (maximum weight) in cycle $C$.Assume for contradiction that $e$ is part of the Minimum Spanning Tree, $T$.If we remove $e$ from $T$, the tree $T$ breaks into two disconnected components, $T_u$ (containing $u$) and $T_v$ (containing $v$).Since $e$ was part of the cycle $C$, there must be a path consisting of other edges in $C$ that connects $u$ and $v$.For this path to get from $u$ (in $T_u$) to $v$ (in $T_v$), it must cross the "cut" between the components at least once. Let $f$ be an edge on this path that crosses the cut.Since $e$ is the unique heaviest edge in $C$, $weight(f) < weight(e)$. (If weights are not unique, $weight(f) \le weight(e)$).We can construct a new spanning tree $T'$ by removing $e$ and adding $f$.$Weight(T') = Weight(T) - weight(e) + weight(f)$.Since $weight(f) < weight(e)$, then $Weight(T') < Weight(T)$.This contradicts the fact that $T$ is a Minimum Spanning Tree.Therefore, the heaviest edge $e$ cannot be in the MST.