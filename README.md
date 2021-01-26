# Shortest path to get food

## https://leetcode.com/problems/shortest-path-to-get-food

You are starving and you want to eat food as quickly as possible. You want to find the shortest path to arrive at any food cell.

```
You are given an m x n character matrix, grid, of these different types of cells:

'*' is your location. There is exactly one '*' cell.
'#' is a food cell. There may be multiple food cells.
'O' is free space, and you can travel through these cells.
'X' is an obstacle, and you cannot travel through these cells.
```
You can travel to any adjacent cell north, east, south, or west of your current location if there is not an obstacle.

### Return the length of the shortest path for you to reach any food cell. If there is no path for you to reach food, return -1.


## Solution 1 : BFS
```java
class Solution {
    public int getFood(char[][] grid) {
        Queue<int[]> q = new LinkedList<>();
        
        int rows = grid.length;
        int columns = grid[0].length;
        Set<String> set = new HashSet<>();
        for(int i = 0; i < rows; i++) {
            for(int j = 0; j < columns; j++) {
                // there will be exactly one *
                if(grid[i][j] == '*') {
                    q.add(new int[]{i,j});
                    break;
                }
            }
        }
        set.add("0,0");
        int minSteps = 1;
        int[][] directions = {{0, 1}, {0,-1}, {-1, 0}, {1, 0}};
        while(!q.isEmpty()) {
            int size = q.size();
            for(int i = 0; i < size; i++) {
                int[] position = q.remove();
                for(int[] direction : directions) {
                    int x = position[0] + direction[0];
                    int y = position[1] + direction[1];
                    if(x < 0 || x >= rows || y < 0 || y >= columns || grid[x][y] == 'X') 
                        continue;
                    if(grid[x][y] == '#')
                        return minSteps;
                    if(!set.contains(x+","+y)) {
                        q.add(new int[]{x,y});
                        set.add(x+","+y);
                    }
                }
            }
            minSteps++;
        }
       return -1; 
    }
}
```
