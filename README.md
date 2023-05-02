Download Link: https://assignmentchef.com/product/solved-coms4701-homework1-npuzzle-game
<br>
In this assignment you will create an agent to solve the N­puzzle game. You will implement and compare several search algorithms, and collect some statistics related to their performances. Visit <u>m</u> <u>ypuzzle.org/sliding</u> for the game’s rules. Please read all sections carefully:

<ol>

 <li>Introduction</li>

 <li>Algorithm Review</li>

</ol>

<ul>

 <li>What You Need To Submit</li>

</ul>

<ol>

 <li>What Your Program Outputs V. Implementation and Testing</li>

 <li>Before You Finish</li>

</ol>

<h1>I. Introduction</h1>

The N­puzzle game consists of a board holding N = m^2 − 1 distinct movable tiles, plus one empty space. There is one tile for each number in the set {1, …, m^2 − 1}. In this assignment, we will represent the blank s pace with the number 0 and focus on the m = 3 case (8­puzzle).

In this combinatorial search problem, the aim is to get from any initial board state to the configuration with all tiles arranged in ascending order ⟨0, 1,…, m^2 − 1⟩ ­­ this is your goal state. The search space is the set of all possible states reachable from the initial state. Each move consists of swapping the empty space with a component in one of the four directions {‘Up’, ‘Down’, ‘Left’, ‘Right’}. Give each move a cost of one. Thus, the total cost of a path will be equal to the number of moves made.




<h1>II. Algorithm Review</h1>

Recall from lecture that search begins by visiting the root node of the search tree, given by the initial state. Three main events occur when visiting a node:

­  First, we remove a node from the frontier set.

­ Second, we check if this node matches the goal state.

­    If not, we then expand the node. To expand a node, we generate all of its immediate successors and add them to the frontier, if they (i) are not yet already in the frontier, and (ii) have not been visited yet.

This describes the life cycle of a visit, and is the basic order of operations for search agents in this assignment—(1) remove, (2) check, and (3) expand. We will implement the assignment algorithms as described here. Please refer to lecture notes for further details, and review the lecture pseudo­code before you begin.




<strong>IMPORTANT:</strong><strong> You may encounter implementations that attempt to short­circuit this order by performing the goal­check on successor nodes immediately upon expansion of a parent node. For example, Russell &amp; Norvig’s implementation of BFS does precisely this. Doing so may lead to edge­case gains in efficiency, but do not alter the general characteristics of complexity and optimality for each method. For simplicity and grading purposes in this assignment, do not make such modifications to algorithms learned in lecture. </strong>

<strong>IMPORTANT</strong><strong>:</strong> <strong> If you are using Python 3, please name your file </strong><strong>d</strong> <strong>river_3.py</strong><strong>,</strong> <strong> so we use the correct version while grading. If you name your file </strong><strong>d</strong> <strong>river.py</strong><strong>,</strong> <strong> the default version for our box is Python 2. </strong>

<h1>IV. What Your Program Outputs</h1>

Your program will create and/or write to a file called o utput.txt,  containing the following statistics:




path_to_goal:  the sequence of moves taken to reach the goal cost_of_path:  the number of moves taken to reach the goal nodes_expanded:  the number of nodes that have been expanded search_depth:  the depth within the search tree when the goal node is found max_search_depth:   the maximum depth of the search tree in the lifetime of the algorithm running_time:  the total running time of the search instance, reported in seconds max_ram_usage:  the maximum RAM usage in the lifetime of the process as measured by the <strong>r</strong> <strong>u_maxrss</strong> attribute in the <strong>r</strong> <strong>esource</strong> module, reported in megabytes

<strong> </strong>

<h2>Example #1: Breadth­First Search</h2>

Suppose the program is executed for breadth­first search as follows:




$ python driver.py bfs 1,2,5,3,4,0,6,7,8




This should result in the solution path:




.T he output file will contain <strong>e</strong> <strong>xactly</strong> the following lines:




path_to_goal: [‘Up’, ‘Left’, ‘Left’] cost_of_path: 3 nodes_expanded: 10 search_depth: 3 max_search_depth: 4 running_time: 0.00188088

max_ram_usage: 0.07812500




<h2>Example #2: Depth­First Search</h2>

.

Suppose the program is executed for depth­first search as follows:




$ python driver.py dfs 1,2,5,3,4,0,6,7,8




This should result in the solution path:

.

The output file will contain <strong>e</strong> <strong>xactly</strong> the following lines:




path_to_goal: [‘Up’, ‘Left’, ‘Left’] cost_of_path: 3 nodes_expanded: 181437 search_depth: 3 max_search_depth: 66125 running_time: 5.01608433

max_ram_usage: 4.23940217

.

More test cases are provided in <strong>t</strong> <strong>he FAQs</strong>.




<h2>Note on Correctness</h2>

.

<u>All variables</u>,  except  running_time and m ax_ram_usage,  have  <strong>one and only one  </strong>correct answer when running BFS and DFS. A*  nodes_expanded might vary depending on implementation details. You’ll be fine as long as your algorithm follows all specifications listed in these instructions.

As  running_time and m ax_ram_usage values vary greatly depending on your machine and implementation details, there is no “correct” value to look for. They are for you to monitor time and space complexity of your code, which we highly recommend. A good way to check the correctness of your program is to walk through small examples by hand, like the ones above.




<h1>V. Implementation and Testing</h1>

For your first programming project, we are providing hints and explicit instructions. Before posting a question on the discussion board, make sure your question is not already answered here or in the FAQs.




<h2>1. Implementation</h2>

You will implement the following three algorithms as demonstrated in lecture. In particular:

<ul>

 <li><strong>Breadth­First Search</strong>. Use an explicit queue, as shown in lecture.</li>

 <li><strong>Depth­First Search</strong>. Use an explicit stack, as shown in lecture.</li>

 <li><strong>A­Star Search</strong>. Use a priority queue, as shown in lecture. For the choice of heuristic, use the <u>M anhattan priority function</u>;  that is, the sum of the distances of the tiles from their goal positions. Note that the blanks space is not considered an actual tile here.</li>

</ul>




<h2>2. Order of Visits</h2>

In this assignment, where an arbitrary choice must be made, we always <strong>v</strong> <strong>isit</strong> child nodes in the

“<strong>U</strong> <strong>DLR</strong>”  order; that is, [‘Up’, ‘Down’, ‘Left’, ‘Right’] in that exact order. Specifically:

<ul>

 <li><strong>Breadth­First Search</strong>. Enqueue in UDLR order; de­queuing results in UDLR order.</li>

 <li><strong>Depth­First Search</strong>. Push onto the stack in reverse­UDLR order; popping off results in UDLR order.</li>

 <li><strong>A­Star Search</strong>. Since you are using a priority queue, what happens with duplicate keys? How do you ensure nodes are retrieved from the priority queue in the desired order?</li>

</ul>

<h2>5. Tips on Getting Started</h2>

Begin by writing a class to represent the <strong>s</strong> <strong>tate</strong> of the game at a given turn, including parent and child nodes. We suggest writing a separate <strong>s</strong> <strong>olver</strong> class to work with the state class. Feel free to experiment with your design, for example including a <strong>b</strong> <strong>oard</strong> class to represent the low­level physical configuration of the tiles, delegating the high­level functionality to the state class.

You will not be graded on your design, so you are at a liberty to choose among your favorite programming paradigms. Students have successfully completed this project using an entirely object­oriented approach, and others have done so with a purely functional approach. Your submission will receive full credit as long as your driver program outputs the correct information.

<h1>VI. Before You Finish</h1>

<ul>

 <li><strong>Make sure</strong> your code passes at least the submission test cases.</li>

 <li><strong>Make sure</strong> your algorithms generate the correct solution for an arbitrary solvable problem instance of 8­puzzle.</li>

 <li><strong>Make sure</strong> your program always terminates without error, and in a reasonable amount of time. <strong>Y</strong> <strong>ou will receive zero points from the grader if your program fails to terminate. Running times of more than a minute or two may indicate a problem with your implementation.</strong> If your implementation exceeds the time limit allocated (20 minutes for all test cases), your grade may be incomplete.</li>

 <li><strong>Make sure</strong> your program output follows <u>t he specified format exactly.</u> In particular, for the path to goal, use square brackets to surround the list of items, use single quotes around each item, and capitalize the first letter of each item. Round floating­point numbers to 8 places after the decimal. You will not receive proper credit from the grader if your format differs from the provided examples above.</li>

</ul>





