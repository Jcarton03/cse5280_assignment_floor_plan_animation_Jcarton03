# CSE5280 Assignment: Penalty Functions for Floor Plan Navigation


🚨 Do this first!!🚨 Create your own private repository for the assignment
Follow these instructions: [https://github.com/cse4001/cse4001_course_materials/blob/main/adm/submitting_assignments.md](https://github.com/cse5280/submitting_assignments/blob/main/README.md)

## Introduction

In this assignment, you will extend the cost-function minimization framework described in the
 *Animation by Cost-Function Minimization* notebook to a two-dimensional floor plan consisting of **walls rather than point obstacles**.

**Reference notebook:**

- *Animation by Cost-Function Minimization*
   [https://github.com/eraldoribeiro/cse5280_animation_by_cost_function_minimization](https://github.com/eraldoribeiro/cse5280_animation_by_cost_function_minimization/blob/main/animation_by_cost_minimization.ipynb)

Your goal is to model walls as **continuous penalty fields**, combine them with a **goal-attraction term**, and use **gradient descent** to generate collision-free motion through the environment.

This assignment emphasizes **problem formulation**:

> The animation should emerge entirely from how you define and combine cost functions.

------

## Scope Clarification

This assignment is **not**:

- A shortest-path planning problem
- A graph-search problem
- A discrete collision-detection task

You are **not expected** to compute globally optimal paths or completeness guarantees.

Instead, the focus is on:

- Continuous cost-field design
- Local, gradient-based motion
- Understanding how motion emerges from cost functions

------

## Learning Objectives

By completing this assignment, you will be able to:

- Represent walls as continuous penalty functions
- Convert geometric constraints into scalar cost fields
- Compute and visualize gradients of spatial cost functions
- Generate motion using gradient descent in complex environments
- Analyze the strengths and limitations of potential-field methods

------

## Problem Description

You are given a simple two-dimensional floor plan composed of:

- Axis-aligned walls (line segments)
- A start position
- A goal position

Your task is to design penalty functions that:

- Penalize proximity to walls
- Prevent the animated point from crossing through walls
- Remain differentiable so gradient-based optimization can be applied

The final motion should reach the goal while remaining collision-free.

------

### Expected Behavior

A successful implementation should demonstrate:

- No visible wall crossings
- Convergence toward the goal for reasonable parameter choices
- Qualitatively different paths when wall parameters are changed

------

## Task Breakdown

### Floor Plan Representation

- Represent each wall as a line segment defined by two endpoints
- Store the full floor plan as a collection of wall segments

You may assume:

- Walls do not move
- Walls have a finite thickness or influence radius

> **Terminology:**
>  “Wall thickness” and “influence radius” refer to a user-defined distance parameter that controls how far a wall’s penalty extends.

------

### Wall Penalty Function

For each wall, define a penalty function $C_{\text{wall}}(\mathbf{x})$ that depends on the distance from a point $\mathbf{x}$ to the wall.

Your penalty function must:

- Increase as the point approaches the wall
- Be zero beyond a chosen influence distance
- Be smooth enough to compute gradients numerically

You may adapt or extend penalty functions used in the notebook (e.g., logarithmic or inverse-distance penalties).

Gradients may be computed:

- Analytically, or
- Numerically (e.g., finite differences) or using library functions. 

Closed-form gradients are **not required**.

------

### Combined Cost Function

Define the total cost as

$$
C(\mathbf{x}) =
C_{\text{goal}}(\mathbf{x}) +
\sum_i w_i \, C_{\text{wall},i}(\mathbf{x}),
$$

where:

- $C_{\text{goal}}(\mathbf{x})$ attracts the point toward the goal
- $C_{\text{wall},i}(\mathbf{x})$ are wall penalty terms
- $w_i$ are weighting coefficients

Parameter tuning (e.g., weights, influence radius) is an **expected part** of this assignment and should be discussed in your analysis.

------

### Visualization of Cost Fields

Produce the following visualizations:

- A contour plot of the total cost function over the floor plan
- A vector field showing the negative gradient of the total cost
- A plot showing walls, start position, and goal position

These visualizations should clearly illustrate how walls shape the cost landscape.

------

### Motion Generation via Gradient Descent

- Implement gradient descent to animate a point starting from the given start position
- Use the negative gradient $-\nabla C(\mathbf{x})$ to update the position iteratively
- Stop the animation when the point reaches the goal or after a fixed number of iterations

It is acceptable—and expected—for some configurations to produce **local minima**.
 Understanding why these arise is part of the assignment.

------

### Analysis

Answer the following questions:

1. How does wall thickness or influence radius affect the resulting path?
2. What happens near corners or narrow corridors?
3. Does the method ever get stuck? Why or why not?
4. 4. How did different penalty functions change:
   - path smoothness,
   - clearance from walls,
   - convergence speed,
   - and susceptibility to local minima?


------

## Deliverables

You must submit **a link to a GitHub repository** containing your work.

The repository should contain at minimum:

- `notebook.ipynb`
  - Wall penalty functions
  - Gradient descent implementation
  - Visualizations and animations
  - A comparison of at least three different wall penalty formulations,
  using the same floor plan and start/goal configuration. The comparison should include
both visual results (trajectories, cost fields)
and a qualitative discussion of behavior.
      
- Generated figures:
  - Cost contours
  - Gradient vector field
  - Trajectory overlaid on the floor plan

Your notebook should include sufficient **markdown explanations** to make your approach and analysis clear.

------

## Constraints and Guidelines

- ❌ Do not use discrete collision detection or path-planning algorithms (e.g., A*, RRT)
- ❌ Do not hardcode collision checks (e.g., “if collision then stop”)
- ✅ Motion must be produced **only** by cost-function minimization
- ✅ All avoidance behavior must emerge from your penalty functions

------

## Evaluation Criteria

| Criterion                                   | Weight |
| ------------------------------------------- | ------ |
| Correct modeling of walls as penalty fields | 30%    |
| Quality of cost-field visualizations        | 20%    |
| Correct use of gradients                    | 20%    |
| Analysis and explanation                    | 20%    |
| Code clarity and organization               | 10%    |

------

## Key Takeaway

> In this assignment, **walls are not geometric constraints**—they are features of the **cost landscape**.
>  Your animation succeeds or fails entirely based on how well you design that landscape.
