---
layout: post
title:  "Solving sudokus"
date:   2021-12-26 21:00:00 +0100
categories: uni thesis
excerpt: Solving sudokus the exciting way - with algorithms.
image: /assets/images/sudoku/2021-12-26_sudoku-solver.png
---

Following up from [Minesweeper holidays]({% post_url 2016-12-29-minesweeper-holidays %}), I have built a [sudoku solver](https://hauthorn.me/sudoku-solver/). Well - it solves some preconfigured sudokus, since it's primarily a test bed for the algorithm(s) I've written.

I'm planning to implement the following algorithms:
- [x] Randomized algorithm (simply to see if my UI works as expected)
- [x] Exhaustive search with simple back-tracking
- [ ] Something graph-coloring based (my thesis was about a particular version of weighted graph coloring)
- [ ] Something that acts almost as a human does (considering which numbers could work, and then assigning once ruled out)

### The test bed
A decided to go for Angular with Angular-material for the UI. It allows for Typescript as a coding language, and provided me some of the components I need.

![Sudoku solver](/assets/images/sudoku/2021-12-26_sudoku-solver.png)

I set a couple of sliders to control how fast the algorithm progresses. I decided to run this using an interval, allowing the user to follow the progression visually.

I used 2 sample sudokus from [sudoku.com](https://sudoku.com/easy/) that I found to be challenging to solve by hand (one slightly more so than the other).

One obvious improvement to make it to mark every "group" in the sudoku with thicker lines. That's a todo.

### Randomized algorithm
Just implemented this to be able to test the Start/Stop/Reset controls. I never expect it to solve a single sudoku.

### Exhaustive search
This one is a DFS-like approach, inspired by [this animated gif](https://en.wikipedia.org/wiki/Sudoku_solving_algorithms#/media/File:Sudoku_solved_by_bactracking.gif) at wikipedia. There was no pseudo-code, but the algorithm is fairly simple to write. 
It starts at the top left, and then attempts to assign a valid number to a field. If succesful, it progresses to the next.

If it turns out it's not possible to assign a valid number to a given field, it removes the assignment for the field, and backtracks to a previous field (incrementing that instead).

This is annoyingly fast - I was suspecting it to be rather slow, allowing me to implement a graph coloring algorithm that could keep up. Oh well 🤷‍♀️

```typescript
  step(): void {
    // pick the first field not yet assigned, or the first one that violates the rules
    let field = this.notLocked[this.index];

    // assign 1 or increment it
    if (field.value == null) {
      field.value = 0;
    }
    field.value++;

    // rollover? Clear this one, increment the previous one
    if (field.value > 9) {
      field.value = null;
      this.index--;
    } else if (this.board?.valid) {
      this.index++;
    }
  }
```

### Graph coloring
Seeing how fast the exhaustive search worked I'm not expecting the graph coloring algorithms to work.

I am considering 2 approaches. One is to implement [DSatur](https://en.wikipedia.org/wiki/DSatur) since the heuristic is blindingly fast compared to the exponential time algorithms, but I worry that it might not be able to find a/the solution to the sudoku.

The other is to start with DSatur, then attempting taboo search approach to hopefully reach the solution quickly.

### Something a human does
Trying to consider teach field and the possible assignments to it might also prove useful and fast.

Might actually implement this before the graph-based approaches since it might prove fast to implement.