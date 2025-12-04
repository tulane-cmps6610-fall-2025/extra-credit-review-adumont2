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
- 3b.
1. Apply Markov's InequalityWe are given:Random Variable $X$: The number of comparisons Quicksort makes.Expected Value $E[X]$: We know Quicksort's expected work is $E[X] \approx K n \ln n$ (where $K$ is a constant, typically around $2$ or $1.39$ depending on the base of the logarithm).Threshold $\alpha$: $10^c n \ln n$.Markov's Inequality states:$$P(X \ge \alpha) \le \frac{E[X]}{\alpha}$$Substitute our values:$$P(X \ge 10^c n \ln n) \le \frac{K n \ln n}{10^c n \ln n}$$2. SimplifyThe $n \ln n$ terms cancel out:$$P(X \ge 10^c n \ln n) \le \frac{K}{10^c}$$(Using the standard upper bound $E[X] \le 2 n \ln n$, this would be $\frac{2}{10^c}$).3. Interpretation of "Concentration"This result tells us about the tail of the distribution:Rapid Decay: As the parameter $c$ increases, the probability of the runtime reaching $10^c n \ln n$ decreases exponentially (specifically as $10^{-c}$).Implication: It is extremely unlikely for Quicksort to take a very long time. For example, if $c=2$ (checking for $100 n \ln n$ comparisons), the probability is bounded by $\approx \frac{2}{100} = 0.02$.Limitations of Markov: While this shows the probability gets small, Markov's inequality is actually a very "loose" bound. It only proves polynomial decay ($1/k$) relative to the multiplier. In reality, Quicksort's concentration is much stronger (it has "exponentially decaying tails" provable via Chernoff bounds), meaning the actual probability is vastly lower than what Markov predicts. Markov simply gives us the worst-case guarantee that the work is unlikely to deviate wildly from the mean.
4. **Greedy Algorithms**

5. **Dynamic Programming**

6. **Graphs**
