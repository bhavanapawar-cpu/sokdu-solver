# sokdu-solver
sudoku_grid = [
    [5, 3, 0, 0, 7, 0, 0, 0, 0],
    [6, 0, 0, 1, 9, 5, 0, 0, 0],
    [0, 9, 8, 0, 0, 0, 0, 6, 0],
    
    [8, 0, 0, 0, 6, 0, 0, 0, 3],
    [4, 0, 0, 8, 0, 3, 0, 0, 1],
    [7, 0, 0, 0, 2, 0, 0, 0, 6],
    
    [0, 6, 0, 0, 0, 0, 2, 8, 0],
    [0, 0, 0, 4, 1, 9, 0, 0, 5],
    [0, 0, 0, 0, 8, 0, 0, 7, 9]
]
def is_valid(grid, row, col, num):
    # Check row and column
    for i in range(9):
        if grid[row][i] == num or grid[i][col] == num:
            return False
    
    # Check 3x3 box
    box_x = row // 3 * 3
    box_y = col // 3 * 3
    for i in range(3):
        for j in range(3):
            if grid[box_x + i][box_y + j] == num:
                return False
    return True
def solve(grid):
    for row in range(9):
        for col in range(9):
            if grid[row][col] == 0:
                for num in range(1, 10):
                    if is_valid(grid, row, col, num):
                        grid[row][col] = num
                        if solve(grid):
                            return True
                        grid[row][col] = 0
                return False
    return True
def print_grid(grid):
    for row in grid:
        print(" ".join(str(num) for num in row))
if solve(sudoku_grid):
    print("Solved Sudoku:")
    print_grid(sudoku_grid)
else:
    print("No solution exists.")
