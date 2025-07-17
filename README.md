Project 1		CS205: Artificial Intelligence, DR. Eammon Keogh

Jordan Peck  
SID: 862311857  
Email: [jpeck008@ucr.edu](mailto:jpeck008@ucr.edu)  
Date: May-10-2024

Resources referenced in completing this assignment:

* Blind Search and Heuristic Search lecture slides  
* Python 3.12.3 Documentation (found here: [https://docs.python.org/3/index.html](https://docs.python.org/3/index.html))  
* Matplotlib Documentation (found here: https://matplotlib.org/stable/api/index)

All important code in my implementation is original aside from the use of the libraries:

* **heapq:** to maintain the order of states in the queue  
* **copy:** to create deep copies of function input to prevent undesired modification of parameters  
* **time:** to track performance of algorithms  
* **matplotlib.pyplot:** to visualize the performance of the algorithms

I affirm that I did not use ChatGPT or similar to write the code or text in this work.

Report Outline:

* Cover Page: 					Page 	1  
* My Report: 					Pages 2 to 5  
* Sample trace of an easy problem:		Page 	6  
* Sample trace of a hard problem:		Pages	7 to 8  
* My Code 					Pages 9 to 14  
  (Can also be found and run a…t) https://colab.research.google.com/drive/1uGIOtqnrlZ5QxfiVELT4gH8WfxuMssT1?usp=sharing 

CS:205 Project 1: Analysis of three algorithms for solving the 8-puzzle  
Jordan Peck, SID 862311857 May-10-2024

Introduction  
The 8-puzzle is a particular variant of the more general n-puzzle game in which the player is tasked with arranging a shuffled set of n numbered tiles into their proper order in a square grid. For this variant, 8 tiles numbered 1-8 are arranged on a 3 by 3 grid leaving a single empty space which a tile can be slid into, leaving a new empty space. The goal of this game is to slide the tiles in such a way that the tiles are arranged in order from top left to bottom right, ensuring that the empty space ends up at the end.

In this assignment I explore the application of uniform cost search as well as A\* search using misplaced tile and manhattan distance heuristics to solve the 8-puzzle and compare their performance in time and space. I chose to write my implementation for this problem in Python (version 3\) in the google colab environment. The puzzle itself is represented as the state of a search node as a 3 by 3 array of integers where the empty space is represented by 0\. The NPuzProb class contains definitions for all possible operations on a given puzzle state, namely, swapping the 0 entry with elements to the left, up, right, or down.

Comparison of Algorithms  
The three algorithms I will be comparing are Uniform Cost Search, A\* search using the Misplaced Tile heuristic, and A\* search using the Manhattan Distance heuristic.

Uniform Cost Search  
In Uniform Cost Search the only consideration for nodes to be explored is the cost g(n) to a given node. In other words we simply expand any unexplored node which is the closest to the initial node. In the context of the 8-puzzle problem the cost to perform any operation is 1 meaning each child node’s cost is one greater than its parent. Because of this, Uniform Cost Search is simply Breadth First Search for the 8-puzzle.  
Misplaced Tile Heuristic  
The Misplaced Tile Heuristic adds a layer of sophistication to our search algorithm, allowing us to take advantage of A\* search. For this algorithm we introduce the score h(n) which is the heuristic score at a given node n. We continue to expand a node with the lowest score but now the cost at a node is calculated g(n)+h(n) or the cost to the node and the cost to the solution through the node n estimated by the heuristic h. For the Misplaced Tile Heuristic we simply count the number of tiles which are not currently in their proper position, skipping 0\. It is important to not that this heuristic is admissible in that the number of moves required to reach the goal state from a node n will certainly be greater than the number of misplaced integers.’

Manhattan Distance Heuristic  
For this algorithm we also take advantage of A\* search. However, we introduce an even more sophisticated notion of counting the distance of each entry of the puzzle from its desired position in the goal state and summing them together (again skipping 0). The intuition here is to count how far each tile would have to move if it could travel a direct path to its destination. Again we can convince ourselves that this heuristic is admissible as the paths we calculate for each entry consider no collisions or detours due to other tiles.

Comparison of Algorithms on Sample Puzzles  
Below are the sample 8-puzzles provided by Dr. Keogh to test the algorithms. The puzzles increase in their difficulty to solve with solutions states found at depths 0, 2, 4, 6, 12, 16, 20, and 24\. I ran each of the search algorithms on the given puzzles and gathered the following metrics: Number of Nodes Expanded, Maximum Size of Search Queue, and Runtime. By observing these results we can gain an insight into the time and space consumption of each algorithm.

Number of Nodes Expanded  
From this graph we can see that both heuristic searches explore far less extraneous paths before reaching the solution state when compared to Uniform Cost Search at every level of difficulty. Further, we see that the Manhattan Search converges more directly than Misplaced Tile Search.

<img width="390" height="268" alt="Screenshot 2025-07-16 223854" src="https://github.com/user-attachments/assets/dd67beef-b5c4-425d-809b-6666ee485995" />

Runtime  
We see similar results for runtime as we saw with nodes explored. Again, the heuristic searches greatly outperform Uniform Cost Search and Manhattan Search has the greatest performance of the three.

<img width="384" height="285" alt="Screenshot 2025-07-16 224026" src="https://github.com/user-attachments/assets/d5003a23-3096-4a48-ba09-51f7c5ac26a3" />

Maximum Queue Size  
Lastly, to compare the memory performance of the algorithms we observe the maximum number of nodes held in the queue over the course of performing the search. We see that the heuristic algorithms also outperform Uniform Cost Search is space usage and similarly to our other results Manhattan Search uses the smallest memory of all three search algorithms

<img width="391" height="285" alt="Screenshot 2025-07-16 224108" src="https://github.com/user-attachments/assets/8ce288d1-f4a5-4115-86dd-658021c9b60d" />

Conclusion  
It can be seen from the comparison of the three search algorithms that the application of the Misplaced Tile and Manhattan heuristics greatly increases the rate at which the search algorithms converge on a solution to the 8-puzzle, reducing both time and space usage. Further, we can confirm the intuition that the Manhattan heuristic, which adheres more closely to the reality of the operations in the n-puzzle problem than Misplaced Tile, performs the best across every metric. This emphasizes the importance of choosing an admissible heuristic that resembles the true nature of the problem at hand as closely as possible (with restraints due to complexity).  
Trace of the Solution of an Easy Problem  
Solution depth:  4  Maximum queue size:  7  Nodes visited:  5  Total runtime:  0.0  
\[1, 2, 3\]  
\[5, 0, 6\]  
\[4, 7, 8\]  
 g(n): 0 h(n): 0 f(n) 0  
\[1, 2, 3\]  
\[0, 5, 6\]  
\[4, 7, 8\]  
 g(n): 1 h(n): 3 f(n) 4  
\[1, 2, 3\]  
\[4, 5, 6\]  
\[0, 7, 8\]  
 g(n): 2 h(n): 2 f(n) 4  
\[1, 2, 3\]  
\[4, 5, 6\]  
\[7, 0, 8\]  
 g(n): 3 h(n): 1 f(n) 4  
\[1, 2, 3\]  
\[4, 5, 6\]  
\[7, 8, 0\]  
 g(n): 4 h(n): 0 f(n) 4

Sample Trace of a Hard Problem  
Solution depth:  26  Maximum queue size:  1796  Nodes visited:  3258  Total runtime:  0.24  
\[0, 7, 2\]  
\[4, 6, 1\]  
\[3, 5, 8\]  
 g(n): 0 h(n): 0 f(n) 0  
\[7, 0, 2\]  
\[4, 6, 1\]  
\[3, 5, 8\]  
 g(n): 1 h(n): 13 f(n) 14  
\[7, 6, 2\]  
\[4, 0, 1\]  
\[3, 5, 8\]  
 g(n): 2 h(n): 14 f(n) 16  
\[7, 6, 2\]  
\[0, 4, 1\]  
\[3, 5, 8\]  
 g(n): 3 h(n): 15 f(n) 18  
\[0, 6, 2\]  
\[7, 4, 1\]  
\[3, 5, 8\]  
 g(n): 4 h(n): 14 f(n) 18  
\[6, 0, 2\]  
\[7, 4, 1\]  
\[3, 5, 8\]  
 g(n): 5 h(n): 15 f(n) 20  
\[6, 4, 2\]  
\[7, 0, 1\]  
\[3, 5, 8\]  
 g(n): 6 h(n): 16 f(n) 22  
\[6, 4, 2\]  
\[7, 1, 0\]  
\[3, 5, 8\]  
 g(n): 7 h(n): 15 f(n) 22  
\[6, 4, 2\]  
\[7, 1, 8\]  
\[3, 5, 0\]  
 g(n): 8 h(n): 16 f(n) 24  
\[6, 4, 2\]  
\[7, 1, 8\]  
\[3, 0, 5\]  
 g(n): 9 h(n): 17 f(n) 26  
\[6, 4, 2\]  
\[7, 1, 8\]  
\[0, 3, 5\]  
 g(n): 10 h(n): 16 f(n) 26  
\[6, 4, 2\]  
\[0, 1, 8\]  
\[7, 3, 5\]  
 g(n): 11 h(n): 15 f(n) 26  
\[6, 4, 2\]  
\[1, 0, 8\]  
\[7, 3, 5\]  
 g(n): 12 h(n): 14 f(n) 26  
\[6, 4, 2\]  
\[1, 3, 8\]  
\[7, 0, 5\]  
 g(n): 13 h(n): 13 f(n) 26  
\[6, 4, 2\]  
\[1, 3, 8\]  
\[7, 5, 0\]  
 g(n): 14 h(n): 12 f(n) 26  
\[6, 4, 2\]  
\[1, 3, 0\]  
\[7, 5, 8\]  
 g(n): 15 h(n): 11 f(n) 26  
\[6, 4, 2\]  
\[1, 0, 3\]  
\[7, 5, 8\]  
 g(n): 16 h(n): 10 f(n) 26  
\[6, 0, 2\]  
\[1, 4, 3\]  
\[7, 5, 8\]  
 g(n): 17 h(n): 9 f(n) 26  
\[0, 6, 2\]  
\[1, 4, 3\]  
\[7, 5, 8\]  
 g(n): 18 h(n): 8 f(n) 26  
\[1, 6, 2\]  
\[0, 4, 3\]  
\[7, 5, 8\]  
 g(n): 19 h(n): 7 f(n) 26  
\[1, 6, 2\]  
\[4, 0, 3\]  
\[7, 5, 8\]  
 g(n): 20 h(n): 6 f(n) 26  
\[1, 0, 2\]  
\[4, 6, 3\]  
\[7, 5, 8\]  
 g(n): 21 h(n): 5 f(n) 26  
\[1, 2, 0\]  
\[4, 6, 3\]  
\[7, 5, 8\]  
 g(n): 22 h(n): 4 f(n) 26  
\[1, 2, 3\]  
\[4, 6, 0\]  
\[7, 5, 8\]  
 g(n): 23 h(n): 3 f(n) 26  
\[1, 2, 3\]  
\[4, 0, 6\]  
\[7, 5, 8\]  
 g(n): 24 h(n): 2 f(n) 26  
\[1, 2, 3\]  
\[4, 5, 6\]  
\[7, 0, 8\]  
 g(n): 25 h(n): 1 f(n) 26  
\[1, 2, 3\]  
\[4, 5, 6\]  
\[7, 8, 0\]  
 g(n): 26 h(n): 0 f(n) 26
