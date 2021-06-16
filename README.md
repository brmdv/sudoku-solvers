# Solving sudoku's with Numpy

This is a simple **recursive sudoku solver**, that I made as an excersise for myself. I wanted to see if I could do this without looking up how this is usually done. There are probably better, more efficient and more clever ways do this this. 

If you just want to solve a difficult sudoku, there is a live [webdemo](https://brams-sudoku-solver.herokuapp.com/) that I created to play around with Flask and Heroku.

## Try it

The script provides a `Sudoku` class. It takes a 9 by 9 Numpy `ndarray`, where the empty fields are set to zero. To solve it, use the function `solve(sudoku)` in the same file. It stops at the first succesful solve, so if the sudoku has more than one solution (which it shouldn't in theory) you'll miss out.

## The algorithm

The `Sudoku` class saves the sudoku internally as a 9×9×9 dimensional boolean array. For each position in the grid, the 9 booleans store which numbers (1–9) are still possible for each position.

The method `Sudoku.update()` updates these posibilities according to all the sudoku rules, so it is called after a new number is filled in. 

The complete solving algorithm can then be summarized as follows. 

1. The sudoku is `.update()`d, so that the internal possibilities comply with the current state.

2. Often, this has the result that some fields get "filled in" automatically, i.e. that there are no other options there anymore. So the updating is repeated until nothing chenages anymore.

3. When this easy solving is stuck, the recursive part starts. A field which has the least amount of possibilies left is chosen. One by one, the `solve()` function calls itself recursively with one of those possibilities.

4. If a complete solution is found, the recurive loop is broken and that solution is returned. 
