# Problem 6: From Gradient Descent to Momentum, RMSProp and Adam

**Course:** Algorithms and Data Structures
**University:** SRH University of Applied Sciences, Berlin
**Program:** BSc Computer Science

## Group members

| # | Name | Matriculation no. | Questions |
|---|------|-------------------|-----------|
| 1 | Manas Dogra | 100006131 | Q1, Q2 |
| 2 | Monish Chopra | 100007201 | Q3, Q4 |
| 3 | Aaditya Dawer | 100006382 | Q5, Q6 |

## What this project is about

A model learns by lowering its error (the loss). An optimizer is the rule that decides how to change the model's settings, step by step, to make that error smaller.

Plain gradient descent has two weaknesses: it is slow on large data, and it zig-zags in narrow valleys. This project builds a ladder of five improvements, where each stage fixes a weakness of the one before, and compares them with Newton's method.

| Stage | Method | What it fixes | Extra memory |
|---|---|---|---|
| 1 | Batch Gradient Descent | Baseline, uses all N data points per step | 0 |
| 2 | Mini-batch GD | Cheap steps, uses only b random points | 0 |
| 3 | Momentum | Smooths the zig-zag with a running average of gradients | 1d |
| 4 | RMSProp | Gives each direction its own step size | 1d |
| 5 | Adam | Momentum + RMSProp + bias correction | 2d |
| - | Newton | Uses curvature, very fast on simple bowls but costly | d^2 |

(d = number of parameters, N = number of data points, b = batch size)

## Repository contents

| File | Description |
|---|---|
| `optimizers_problem6.ipynb` | The optimizers, the tests, and three experiments |
| `experiment1_trajectories.png` | Paths on the canyon and Rosenbrock functions |
| `experiment2_loss_time_memory.png` | Loss, time and memory on linear regression (N = 50,000) |
| `experiment3_time_vs_N.png` | Time per step as the data size N grows |

## What the notebook does

1. **Optimizers:** `GD`, `MiniBatchGD`, `Momentum`, `RMSProp`, `Adam` and `Newton`. Each has one method, `step(w, g)`.
2. **Tests:** the code reproduces our hand-worked answers for Q1 to Q5 (for example Adam's first step lands at (3.5, 0.5), and bias correction turns 0.1 into 10).
3. **Experiment 1:** paths of all optimizers on the canyon function and on the Rosenbrock valley, 200 steps each.
4. **Experiment 2:** linear regression with 50,000 samples, comparing loss against time and peak memory.
5. **Experiment 3:** time per step for full-batch and mini-batch as N grows.

## Results from our run

Experiment 2 (N = 50,000, d = 50). Times and memory change a little from computer to computer.

| Method | Final loss | Time | Peak memory |
|---|---|---|---|
| Full-batch GD | 0.315 | about 0.7 s | about 390 KB |
| Mini-batch GD | 0.009 | about 0.1 s | about 55 KB |
| Momentum | 0.009 | about 0.2 s | about 55 KB |
| RMSProp | 0.008 | about 0.2 s | about 55 KB |
| Adam | 0.007 | about 0.2 s | about 56 KB |

The loss cannot go below about 0.005, because of the noise in the data.

Main observations:
- On the canyon, Newton reaches the minimum in one step. Gradient Descent zig-zags, and Adam and RMSProp follow a smoother curve.
- On Rosenbrock, only Adam and Newton get close to the minimum (1, 1) within 200 steps. The other first-order methods barely leave the start.
- Full-batch GD is slow because every step touches all 50,000 rows. The extra arrays of Momentum, RMSProp and Adam are tiny (400 to 800 bytes here).

## Complexity summary

| Method | Time per step | Extra memory |
|---|---|---|
| Batch GD | Theta(N*d) | 0 |
| Mini-batch GD | Theta(b*d) | 0 |
| Momentum | Theta(b*d) | 1d |
| RMSProp | Theta(b*d) | 1d |
| Adam | Theta(b*d) | 2d |
| Newton | Theta(N*d + d^3) | d^2 |

## How to run

**Google Colab (easiest):** open colab.research.google.com, choose File, then Upload notebook, select `optimizers_problem6.ipynb`, then Runtime, then Run all.

**On your own computer:**
```
pip install numpy matplotlib jupyter
jupyter notebook optimizers_problem6.ipynb
```

The notebook only needs `numpy` and `matplotlib`, and runs in about a minute.
