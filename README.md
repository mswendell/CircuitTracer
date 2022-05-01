****************
* Circuit Tracer
* CS 221
* 4/24/2022
* Michael Wendell
**************** 

OVERVIEW:

The Circuit Tracer will search for the shortest path between a start(1) and end(2) on a circuit board as read from
an input file in the correct format. It will use wither a stack or queue as the storage structure and will display
the output to the console or GUI according to the usage in the command-line arguments.

INCLUDED FILES:

* CircuitBoard.java - source file
* CircuitTracer.java - source file
* InvalidFileFromatException.java - source file
* OccupiedPositionException.java - source file
* Storage.java - source file
* TraceState.java - source file
* README - this file

COMPILING AND RUNNING:

From the directory containing all source files, compile the test
 class (and all dependent classes) with the command:
 $ javac ListTester.java

 Run the compiled ListTester class with the command:
 $ java CircuitTracer [-q for queue|-s for stack] [-c for console | -g for gui] filename.dat

Console or GUI will output a report with all shortest solutions for the circuit board file.

ANALYSIS:

How does the choice of Storage configuration (stack vs queue) affect the sequence in which paths are explored in the 
search algorithm? (This requires more than a "stacks are LIFOs and queues are FIFOs" answer.)

For this implementation a queue would add to all paths one at a time before they hit an end point by finding a solution or 
dead end. On the other hand, a stack would find one complete path at a time and work through each path individually.

Is the total number of search states (possible paths) affected by the choice of stack or queue?

The total number of search states will not change, since both a stack and queue will explore all possible paths. 
 
Is using one of the storage structures likely to find a solution in fewer steps than the other? Always?

Yes, a stack will most of the time find a solution before a queue since it will complete each path one at a time. 
This will result in less steps if the solution is in the first half of paths explored. If a solution lies in the last path 
explored by the stack, then a queue could probably find the solution in less steps. 

Does using either of the storage structures guarantee that the first solution found will be a shortest path?

A queue will check all paths at one time, so the first solution found would be the shortest path as well. A stack would 
not guarantee that the shortest solution would be first, since it would check each individual path to its end. This could potentially 
find the longest solution first.

How is memory use (the maximum number of states in Storage at one time) affected by the choice of underlying structure?

A queue would take a larger amount of space because multiple paths would have to be stored at one time until an end point was found. 
A stack would take less storage since once a path is complete it will either be stored as a solution or removed from the stack.

What is the Big-Oh runtime order for the search algorithm? Does it reflect the maximum size of Storage? Does it reflect the number of 
board positions? Does it reflect the number of paths explored? Does it reflect the maximum path length? Is it something else? What is
 'n'? What is the primary input factor that increases the difficulty of the task?
 
The order of this algorithm is O(n). This number would reflect the number of possible paths explored by the algorithm. Since the while
 loop in the algorithm will loop as long as there are objects in the state storage, the number n will increase with each path added to 
 the storage. As well as each time the path moves to a new state there are 3 more potential objects to be added to the state storage. 



PROGRAM DESIGN AND IMPORTANT CONCEPTS:

The CircuitTracer class is a driver class that will take the command-line arguments as input and create a storage object,
a CircuitBoard object, a list to store paths and an initial TraceState object at each open position adjacent to the 
starting point. The storage object can be either a Stack or Queue designated by the command arguments. The CircuitBoard
is an object that will hold a character array of the board and any changes made to it. The TraceState is an object that 
is created at each possible open point on the board and can keep track of a path of points that it has moved from as a 
new trace is created. All the TraceState objects that are created will be stored in the storage object. 
The CircuitTracer uses all these classes to then generate a solution with its implemented searching algorithm.

The Circuit Tracer's algorithm will retrieve all TraceState objects that were stored in the storage object and check 
if they are adjacent to the end point, which would be a solution. If the path is a solution, and its length is equal to 
previous paths, it will be stored in the BestPaths list. If the new path is shorter than the previous paths, the BestPaths list
will be cleared and then the new path will be added. If the new path is not a solution, then the algorithm will check if there 
are any open adjacent points around the current TraceState object and if there are, it will create a new TraceState object using
the previous TraceState at the open location. This location will then be added to the storage object and the while loop will
continue until all possible paths have been explored. Once all solutions have been determined, the program will print all best 
paths to either the console or a GUI based on the desired input. 

TESTING:

The primary testing for the CircuitTracer was done first using the valid1.dat file and then later the CircuitTracerTester 
class. This was mostly Test-Driven development being that the tester was provided beforehand and then used to determine which
methods needed to be fixed from the pass or fail output. This helped ensure that the CircuitTracer met all functionality needed 
to operate with a variety of different invalid and valid files. The testing includes files with multiple starts, multiple endings,
missing values, invalid characters, and incorrect row or column values.I am fairly confident the Circuit Tracer will work under
all conditions being it passed all of the testers tests using many different valid or invalid format defined in the class. 



