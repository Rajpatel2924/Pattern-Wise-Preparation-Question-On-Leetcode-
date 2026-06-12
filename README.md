<div align="center">

# Pattern-Wise LeetCode Interview Preparation

### A structured roadmap for mastering the patterns behind technical interviews

[![Questions](https://img.shields.io/badge/Curated%20Questions-120-2563eb?style=for-the-badge)](#study-roadmap)
[![Patterns](https://img.shields.io/badge/Core%20Patterns-12-7c3aed?style=for-the-badge)](#study-roadmap)
[![Progress](https://img.shields.io/badge/Progress-Self%20Paced-059669?style=for-the-badge)](#recommended-workflow)

[Explore the roadmap](#study-roadmap) · [Start preparing](#recommended-workflow) · [Track progress](#progress-tracking)

</div>

---

## About This Repository

This repository is a pattern-first interview preparation guide built around carefully selected LeetCode problems. Instead of solving questions at random, use each topic to recognize a reusable technique, understand its trade-offs, and practice applying it under interview conditions.

The collection includes foundational problems, common variations, and advanced questions associated with frequently reported interview patterns at companies such as Amazon, Google, Meta, Microsoft, Bloomberg, Uber, and Airbnb.

> Company tags are directional, not guarantees. Interview question pools and hiring processes change over time.

## Study Roadmap

| # | Pattern | Questions | Primary Skills | Practice |
|---|---------|:---------:|----------------|----------|
| 01 | Two Pointers | 10 | Opposing pointers, sorted arrays, in-place scanning | [Open topic](./01-two-pointers/QUESTIONS.md) |
| 02 | Sliding Window | 10 | Dynamic ranges, frequency maps, substring optimization | [Open topic](./02-sliding-window/QUESTIONS.md) |
| 03 | Breadth-First Search | 10 | Level traversal, shortest paths, multi-source BFS | [Open topic](./03-breadth-first-search/QUESTIONS.md) |
| 04 | Depth-First Search | 10 | Recursion, graph traversal, tree reasoning | [Open topic](./04-depth-first-search/QUESTIONS.md) |
| 05 | Backtracking | 10 | Search trees, constraints, pruning | [Open topic](./05-backtracking/QUESTIONS.md) |
| 06 | Heap / Priority Queue | 10 | Top-k, scheduling, streaming data | [Open topic](./06-heap/QUESTIONS.md) |
| 07 | Binary Search | 10 | Sorted search, boundaries, search on answers | [Open topic](./07-binary-search/QUESTIONS.md) |
| 08 | Dynamic Programming | 10 | State design, transitions, memoization | [Open topic](./08-dynamic-programming/QUESTIONS.md) |
| 09 | Divide and Conquer | 10 | Recursive decomposition, merge sort, quickselect | [Open topic](./09-divide-and-conquer/QUESTIONS.md) |
| 10 | Trie | 10 | Prefix search, autocomplete, bitwise tries | [Open topic](./10-trie/QUESTIONS.md) |
| 11 | Union Find / DSU | 10 | Connectivity, components, minimum spanning trees | [Open topic](./11-union-find/QUESTIONS.md) |
| 12 | Greedy | 10 | Local choices, intervals, reachability | [Open topic](./12-greedy/QUESTIONS.md) |

Some problems intentionally appear in more than one topic because strong interview preparation includes recognizing when multiple patterns can solve the same problem.

## Recommended Workflow

1. **Learn the pattern**

   Read the topic's `TOPIC.md` and identify when the technique is useful.

2. **Solve without hints**

   Open `QUESTIONS.md`, set a timer, and explain your approach before writing code.

3. **Record the attempt**

   Add the result, complexity, mistakes, and key learning to `ATTEMPT_LOG.md`.

4. **Write the final solution**

   Use `SOLUTIONS.md` for the problem description, intuition, multilingual Python/Java/C++ reference, and your final complexity notes.

5. **Revisit strategically**

   Retry missed or slow questions after 1 day, 1 week, and 1 month.

## Progress Tracking

Use the `Status` column in every question sheet:

| Status | Meaning |
|--------|---------|
| `Not started` | The problem has not been attempted yet |
| `In progress` | The approach is understood but needs refinement |
| `Solved` | A correct solution was completed independently |
| `Review` | The problem should be revisited |

A problem is interview-ready when you can:

- Recognize the underlying pattern quickly
- Explain the brute-force and optimized approaches
- Write a correct solution without external help
- State time and space complexity confidently
- Handle edge cases and follow-up questions

## Repository Structure

```text
.
├── 01-two-pointers/
│   ├── TOPIC.md          # Pattern overview and core ideas
│   ├── QUESTIONS.md      # Curated interview question roadmap
│   ├── ATTEMPT_LOG.md    # Personal attempts and learning notes
│   └── SOLUTIONS.md      # Descriptions, intuition, and multilingual references
├── ...
├── 12-greedy/
└── README.md
```

## Preparation Principles

- Prioritize pattern recognition over memorizing solutions.
- Communicate assumptions and trade-offs before coding.
- Prefer simple, correct solutions before optimizing.
- Practice edge cases explicitly.
- Re-solve difficult questions until the approach feels natural.

---

<div align="center">

**Consistency beats intensity. Solve, reflect, revisit, repeat.**

</div>
