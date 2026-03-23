# Assignment 2 — Genetic Algorithm: Knapsack Problem
## Observation Report

**Student Name  :** Aniket Panda  
**Student ID    :** 2310040097  
**Date Submitted:** 23rd March 2026  

---

## How to Submit

1. Run each experiment following the instructions below
2. Fill in every answer box — do not leave placeholders
3. Make sure the `plots/` folder contains all required images
4. Commit this README and the `plots/` folder to your GitHub repo

---

## Before You Begin — Read the Code

Open `ga_knapsack.py` and read through it. Then answer these questions.

**Q1. What does the `fitness()` function return? Why does an overweight solution score 0?**

```
The fitness() function returns the total value of items packed if the total weight is within the 15 kg limit, otherwise it returns 0. Overweight solutions score 0 to heavily penalize invalid solutions and ensure the genetic algorithm avoids exceeding the weight constraint, forcing the population to converge toward valid feasible solutions.
```

**Q2. What does `tournament_select()` do? Why are higher-fitness individuals more likely to be chosen?**

```
The tournament_select() function randomly picks k individuals from the population and returns the one with the highest fitness score. Higher-fitness individuals are more likely to be chosen because they will always win their tournaments against random opponents, leading to more frequent selection for reproduction and thus biasing the search toward better solutions.
```

**Q3. Look at the `run_ga()` loop. Find this line:**
```python
next_gen = [best_chromosome[:]]
```
**What is this doing? Why is it important to always keep the best solution?**

```
This line ensures that the best chromosome found so far is always preserved in the next generation. This is called elitism and is important because it prevents the algorithm from accidentally losing the best solution discovered during evolution, guaranteeing that solution quality never decreases across generations.
```

---

## Experiment 1 — Baseline Run

**Instructions:** Run the program without changing anything.
```bash
python ga_knapsack.py
```

**Fill in this table:**

| Metric | Your result |
|--------|-------------|
| Number of generations | 50 |
| Best value at generation 1 | 60 |
| Final best value | 77 |
| Total weight of best solution (kg) | 14.4 |
| Is solution valid (Yes / No) | Yes |

**Copy the printed packing list here:**
```
  + Water bottle
  + First aid kit
  + Sleeping bag
  + Torch
  + Energy bars (x6)
  + Rain jacket
  + Map & compass
  + Cooking stove
  + Rope (10 m)
  + Sunscreen
  + Power bank
```

**Look at `plots/experiment_1.png` and describe what you see (2–3 sentences).**  
*Where does the biggest improvement happen? Does the curve flatten at some point?*
```
The curve shows rapid initial improvement from generation 1 (value 60) to approximately generation 15, where it reaches the final value of 77, then plateaus and remains flat for the remaining generations. The biggest improvement occurs in the first 15 generations as the genetic algorithm explores the solution space and finds good combinations. After reaching the optimum around generation 15, further mutations and crossovers do not improve the solution, demonstrating diminishing returns.
```

---

## Experiment 2 — Effect of Mutation Rate

**Instructions:** In `ga_knapsack.py`, find the `# EXPERIMENT 2` block in `__main__`.  
Copy it three times and run with `mutation_rate` = **0.01**, **0.05**, and **0.30**.  
Save plots as `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`.

**Results table:**

| mutation_rate | Final best value | Weight (kg) | Valid? | Shape of curve |
|--------------|-----------------|-------------|--------|----------------|
| 0.01         | 75              | 14.9        | Yes    | Slow rise, early plateau |
| 0.05         | 77              | 14.4        | Yes    | Quick rise, stable plateau |
| 0.30         | 78              | 14.1        | Yes    | Consistent increase |

**Compare the three plots. What happens when mutation is too low? Too high? (3–4 sentences)**  
*Hint: Too low = no diversity, may get stuck. Too high = random search. What is the sweet spot?*
```
When mutation rate is too low (0.01), the population loses genetic diversity quickly and converges prematurely to a suboptimal solution (75), getting stuck due to insufficient exploration. When mutation rate is high but balanced (0.30), the population maintains enough diversity to escape local optima and finds slightly better solutions (78). The mutation rate of 0.05 (baseline) provides a good balance between exploration and exploitation, reliably converging to value 77. The sweet spot appears to be moderate to moderately-high mutation rates (0.05-0.30) that maintain population diversity without becoming pure random search.
```

**Which mutation_rate gave the best result? Why do you think that is?**
```
The mutation_rate of 0.30 gave the best result (value 78). This higher mutation rate maintains greater genetic diversity throughout the generations, allowing the algorithm to explore the solution space more thoroughly and escape local optima that trap lower mutation rates. Although 0.30 involves more random changes, in this problem it provides enough exploration to discover better solutions while still benefiting from elitism which preserves the best solutions found.
```

---

## Summary

**Complete this table with your best result from each experiment:**

| Experiment | Key setting | Final value | Main finding in one sentence |
|------------|-------------|-------------|------------------------------|
| 1 — Baseline | mutation_rate = 0.05 | 77 | A moderate mutation rate of 0.05 provides good convergence to value 77 with stable early convergence followed by a plateau. |
| 2 — Mutation rate | mutation_rate = 0.30 | 78 | Higher mutation rates (0.30) maintain greater population diversity and allow escape from local optima, achieving better solutions (78). |

**In your own words — what is the most important thing you learned about Genetic Algorithms from these experiments? (3–5 sentences)**
```
The most important lesson is that mutation rate is a critical hyperparameter that controls the balance between exploration (searching for new solutions) and exploitation (refining good solutions). Too little mutation causes premature convergence to suboptimal solutions due to loss of genetic diversity, while too much mutation can maintain diversity but risks disrupting good solutions. This experiment demonstrated that the optimal mutation rate is problem-dependent; in this knapsack problem, higher mutation (0.30) turned out better than moderate (0.05), but in other problems the balance might be different. The key insight is that genetic algorithms require careful tuning of parameters like mutation rate to match the problem landscape and desired exploration-exploitation tradeoff. Additionally, elitism ensures we never lose the best solutions, allowing the algorithm to reliably improve or maintain the best-found solution over generations.
```

---

## Submission Checklist

- [x] Student name and ID filled in
- [x] Q1, Q2, Q3 answered
- [x] Experiment 1: table filled, packing list pasted, plot observation written
- [x] Experiment 2: results table filled (3 rows), observation and answer written
- [x] Summary table completed and reflection written
- [x] `plots/` contains: `experiment_1.png`, `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`
