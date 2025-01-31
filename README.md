# Optimal Project Team Formation - Dynamic Programming Approach

## Overview
This project implements a dynamic programming algorithm designed to select an optimal team from an organization tree structure based on employees' skill levels. The algorithm calculates the total skill level of the selected team while ensuring a broad skill set by considering the inclusion and exclusion of employees from the team.

### Objective
The algorithm aims to find the optimal team where:
1. The total skill level is maximized.
2. The team has a broad skill set by including employees with diverse skill levels.
3. It uses dynamic programming to solve the problem efficiently for various sizes of organizations (from small to large).
4. The algorithm specifically identifies the best two team members to be paired with each other, ensuring that no more than two members are selected.

## Algorithm Details

### Pseudo-code
The algorithm works through a post-order traversal of the organization tree and computes the optimal team using the following recurrence relations:

- `dp_in[v]`: Skill level of node `v` when the node is included, plus the optimal contribution of its children excluding them.
- `dp_out[v]`: Maximum possible contribution when node `v` is excluded, by considering the optimal contribution of its children (either included or excluded).

### Key Functions:
1. **PostOrderTraversal(node)**: A recursive function to traverse the tree and calculate the `dp_in` and `dp_out` values for each node.
2. **ReconstructOptimalTeam(node, include)**: Reconstructs the optimal team based on the values of `dp_in` and `dp_out`.
3. **FindOptimalTeams()**: Executes the algorithm to find the optimal team, determines the total skill level, and outputs the optimal team members along with their skills.

### Recursive Function Inspiration:
To ensure the correctness of the recursive function, we drew inspiration from well-known problems like the **Maximum Weighted Independent Set** problem and the **Largest Independent Set** problem. These provided valuable insights into structuring the team selection process while respecting the hierarchy and maximizing the skill distribution.

### Recurrence Relations:
- `dp_in[v] = skillLevel[v] + ∑(dp_out[c] for each child c)`
- `dp_out[v] = ∑(max(dp_in[c], dp_out[c]) for each child c)`

### Base Case:
- If a node is a leaf node, then:
  - `dp_in[v] = skillLevel[v]`
  - `dp_out[v] = 0`

### Time and Space Complexity
- **Time Complexity**: O(n)
  - The algorithm processes each node once during the post-order traversal.
- **Space Complexity**: O(n)
  - The space is used to store the `dp_in` and `dp_out` values for each node.

## Experimental Results
The dynamic programming algorithm has been tested on organizations of various sizes:

### Example 1: Small Organization (5 Employees)
- **Input**:
```
0 : Sarah : 1 : 15
1 : Ali : 2 : 10
1 : Layla : 3 : 12
2 : Hassan : 4 : 8
2 : Aisha : 5 : 9
```

- **Output**:
```
Optimal Total Skill Level: 15
Optimal Team:
Sarah (Skill: 15)
Hassan (Skill: 8)
Aisha (Skill: 9)
```

### Example 2: Medium Organization (10 Employees)
- **Input**:
```
0 : Ahmed : 1 : 20
1 : Omar : 2 : 18
1 : Youssef : 3 : 16
2 : Layla : 4 : 14
2 : Hassan : 5 : 12
2 : Noor : 6 : 10
3 : Khalid : 7 : 13
3 : Salma : 8 : 11
4 : Zain : 9 : 9
4 : Lina : 10 : 8
```
- **Output**:
```
Optimal Total Skill Level: 83
Optimal Team:
Ahmed (Skill: 20)
Zain (Skill: 9)
Lina (Skill: 8)
Hassan (Skill: 12)
Noor (Skill: 10)
Khalid (Skill: 13)
Salma (Skill: 11)
```

### Example 3: Large Organization (20 Employees)
- **Input**: 
```
0 : Ahmed : 1 : 30
1 : Omar : 2 : 28
1 : Youssef : 3 : 25
2 : Layla : 4 : 22
2 : Hassan : 5 : 20
2 : Noor : 6 : 18
3 : Khalid : 7 : 23
3 : Salma : 8 : 21
4 : Zain : 9 : 19
4 : Lina : 10 : 17
5 : Sami : 11 : 15
5 : Tarek : 12 : 14
6 : Fatima : 13 : 16
6 : Rami : 14 : 12
7 : Huda : 15 : 13
7 : Fadi : 16 : 11
8 : Samiha : 17 : 9
8 : Imran : 18 : 8
9 : Samir : 19 : 10
9 : Yasmine : 20 : 7
```

- **Output**:
```
  - Optimal Total Skill Level: 187
  - Optimal Team:
    - Omar (Skill: 28)
    - Zain (Skill: 19)
    - Lina (Skill: 17)
    - Sami (Skill: 15)
    - Tarek (Skill: 14)
    - Fatima (Skill: 16)
    - Rami (Skill: 12)
    - Youssef (Skill: 25)
    - Huda (Skill: 13)
    - Fadi (Skill: 11)
    - Samiha (Skill: 9)
    - Imran (Skill: 8)
```

