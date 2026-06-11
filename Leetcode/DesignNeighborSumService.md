## Description

You are given a `n x n` 2D array `grid` containing distinct elements in the range `[0, n² - 1]`.

Implement the `NeighborSum` class:

- `NeighborSum(int[][] grid)` initializes the object.
- `int adjacentSum(int value)` returns the sum of elements which are adjacent neighbors of `value`, that is either to the top, left, right, or bottom of `value` in grid.
- `int diagonalSum(int value)` returns the sum of elements which are diagonal neighbors of `value`, that is either to the top-left, top-right, bottom-left, or bottom-right of `value` in grid.

## Code (Java)

```java
class NeighborSum {
private:
    vector<vector<int>> grid;
    vector<pair<int, int>> pos;
    int n;
public:
    NeighborSum(vector<vector<int>>& grid) {
        this->grid = grid;
        n = grid.size();
        pos.resize(n*n);
        for(int i=0; i<n; i++){
            for(int j=0; j<n; j++){
                pos[grid[i][j]] = {i, j};
            }
        }
    }
    
    int adjacentSum(int value) {
        int sum = 0;
        auto [r, c] = pos[value];
        vector<pair<int, int>> dir = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
        for(auto[dr, dc] : dir){
            int nr = r+dr;
            int nc = c+dc;

            if(nr >= 0 && nr < n && nc >= 0 && nc < n){
                sum += grid[nr][nc];
            }
        }
        return sum;
    }
    
    int diagonalSum(int value) {
        int sum = 0;
        auto [r, c] = pos[value];
        vector<pair<int, int>> dir = {{-1, -1}, {-1, 1}, {1, -1}, {1, 1}};

        for(auto[dr, dc]: dir){
            int nr = r+dr;
            int nc = c+dc;

            if(nr >= 0 && nr < n && nc >= 0 && nc < n){
                sum += grid[nr][nc];
            }
        }
        return sum;
    }
};

/**
 * Your NeighborSum object will be instantiated and called as such:
 * NeighborSum* obj = new NeighborSum(grid);
 * int param_1 = obj->adjacentSum(value);
 * int param_2 = obj->diagonalSum(value);
 */
```

## Code (C++)

```c++
class NeighborSum {
private:
    vector<vector<int>> grid;
    vector<pair<int, int>> pos;
    int n;
public:
    NeighborSum(vector<vector<int>>& grid) {
        this->grid = grid;
        n = grid.size();
        pos.resize(n*n);
        for(int i=0; i<n; i++){
            for(int j=0; j<n; j++){
                pos[grid[i][j]] = {i, j};
            }
        }
    }
    
    int adjacentSum(int value) {
        int sum = 0;
        auto [r, c] = pos[value];
        vector<pair<int, int>> dir = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
        for(auto[dr, dc] : dir){
            int nr = r+dr;
            int nc = c+dc;

            if(nr >= 0 && nr < n && nc >= 0 && nc < n){
                sum += grid[nr][nc];
            }
        }
        return sum;
    }
    
    int diagonalSum(int value) {
        int sum = 0;
        auto [r, c] = pos[value];
        vector<pair<int, int>> dir = {{-1, -1}, {-1, 1}, {1, -1}, {1, 1}};

        for(auto[dr, dc]: dir){
            int nr = r+dr;
            int nc = c+dc;

            if(nr >= 0 && nr < n && nc >= 0 && nc < n){
                sum += grid[nr][nc];
            }
        }
        return sum;
    }
};

/**
 * Your NeighborSum object will be instantiated and called as such:
 * NeighborSum* obj = new NeighborSum(grid);
 * int param_1 = obj->adjacentSum(value);
 * int param_2 = obj->diagonalSum(value);
 */
```