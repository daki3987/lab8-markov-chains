# Lab 8 — Markov Chains
This file contains answers for Lab 8.

---

## 1. Matrix Multiplication

Let A be an `ℓ × m` matrix and B be an `m × n` matrix. The (i, j)-entry of AB is:

```text
(AB)_{i,j} = sum_{k=1}^{m} a_{i,k} * b_{k,j}
```

**Answer:** Each thread can compute a single entry, a full row, or a block of rows. Assigning **one row per thread** is common and efficient because each thread can calculate all entries of a row independently. This avoids conflicts and makes good use of parallel processing.

---

## 2. Walks and Matrix Powers

Let A be the adjacency matrix of a directed graph G = (V, E), with A[i,j] = 1 if there is an edge from i → j, and 0 otherwise.

1. **(i,j)-entry of A²:** Counts the number of walks of length 2 from vertex i to vertex j. Each intermediate vertex contributes to a possible walk.
2. **(i,j)-entry of Aᵏ:** Counts the number of walks of length k from i to j. Powers of A let us quickly compute longer paths without listing them individually.

---

## 3. Markov Chains

A Markov chain is an n × n matrix M where:

* M[i,j] ≥ 0 for all i,j
* Each row sums to 1

M[i,j] is the probability of moving from state i to state j in one step.

### 3.1 Is Mᵏ a Markov chain?

Yes. Multiplying row-stochastic matrices preserves row sums of 1. Therefore, Mᵏ is also a Markov chain, and its rows remain valid probability distributions.

### 3.2 What does (Mᵏ)[i,j] represent?

(Mᵏ)[i,j] is the probability of being in state j after k steps starting from state i. It helps predict future states over multiple steps:

```text
(Mᵏ)[i,j] = P(X_{t+k} = j | X_t = i)
```

---

## 4. Using Markov Chains for Predictive Paging

* **States:** Each page in memory is a state.
* **Transitions:** M[i,j] = probability that page j is accessed after page i.

**Applications:**

* **Prefetching:** Use M or Mᵏ to predict which pages will likely be needed next and load them in advance. This can reduce page faults.
* **Eviction (optional):** Choose to remove the page with the lowest probability of being needed soon according to Mᵏ, instead of always using LRU.

**Summary:** M shows next-page probabilities. Powers of M show probabilities over multiple steps. These probabilities guide both prefetching and eviction in a simple and effective way.

---

**End of Lab 8 Answers**
