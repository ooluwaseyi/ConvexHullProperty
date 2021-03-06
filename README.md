Date: Monday, on 13th of May 2014  
AUTHOR: Abel Serrano Juste a.k.a Akronix

#CONVEX HULL PROPERTY

##INTRODUCTION

This project is about implementing algorithms to solve the convex hull problem.
The convex hull problem is defined as follows:
Given a set of points X in the Euclidean space, to find the smallest set of points that contains X.

This problem is applicable to the practical scenario where a robot has to go from one point to another, avoiding an obstacle
placed in the middle. The solution path is obtained calculating the convex hull set for the set formed by the departure, the destination and all the obstacle points.

###Notes###
1. It worths to remark that I made this on a GNU/Linux environment.
So that, the end of line of the files will be LF characters. I suggest to use an smart editor, as geany, to open them.
2. in the following, lines preceded by $ sign represents inputs to the terminal.

##STRUCTURE##

In the src/ directory is located all my source code for the project along to one sample test_cases.in

In the images/ directory is located some images related to the project.

In particular, in images/pictures/ you can find the papers of the definition of the convex hull merging problem and of the test cases included in test_cases.in and in images/screenshots/ directory contains screenshots for all the test executed in my machine.

##EXPLANATION OF THE CODE##

I will do a briefly explanation by sections of this code.

####class point

The source code for the class point is located inside the src/point directory.
This class is for 2D points (x and y coordinates only) and the accurate of their coordinates are float numbers. That is why the actual class is called Point2f.  

There is one header file, which defines the functions and the internal representation of the point and one .cpp which implements the functions. 
 
There is a small test for this ADT inside this directoty. It is called test_Point2f.cpp and can be compiled and executed

####class heap

The code for the class heap is all located inside the src/heap directory. Again, I’ve coded one header and one .cpp for the minheap data structure. test_heap.cpp runs some basic functions of the heaps and print the result to be checked by the smarter human.  
Note that for using the heap DT, the following operators has to be defined for the target data type: assignment (‘=’), greater than (‘>’) and equal to (‘==’). 

Also here, you can find the heap sort algorithm, which uses a heap to sort any data type in ascending order according to the greater than implementation defined in that data type.  
It does this task in O(n log n) running time.  
test_heap-sort.cpp generates some unsorted input for heap sort and print the sorted output by heap-sort.

####CH_Algorithms.cpp
Here it is the actual implementation of the convex hull algorithms. Note that some STL libraries are imported for using stacks, queues and dynamic arrays data structures, and other utilities as cmath and iostream.
The input of these algorithms is a set of points and the output is the convex hull for that set of points.

The file has got 600 lines and it can be divided in 3 parts:

1. Common definitions
2. Iterative algorithm
3. Divide and Conquer algorithm

The first one cover until line 70, and it is basically the header documentation, include of libraries and debug utilities. About the debug utilities, I’m using a preprocessor variable DEBUG. It can be defined by #define or undefined by #undef preprocessor commands. When it is enabled, it prints information about what the algorithm is doing for every step and which data is managing.

The second cover up to line 200. And implements the iterative convex hull algorithm, using the upper and lower mids.

The third cover up the rest of the document. It is the implementation for the D&C algorithm and is quite more complex than the other one.

There is another test source file which generates some test cases for either iterative or D&C algorithm, executes them and compares with the expected result. You can define which algorithms you can test defining: TEST_ITERATIVE and TEST_DIVIDE_CONQUEST variables.

####main.cpp
Here I address the particular requirements for this project: to find the shortest path for a robot to go from a starting point to a final point avoiding an obstacle.

The program reads the input initial point, destination point and obstacle set of points from a text file called test_cases.in. The input file has to follow the following syntax:

	NUMCASES numberofcasestoexecute
	case i begin
	init.x init.y
	dest.x dest.y
	numberOfObstPoints
	x y coordinates for each obstacle point.
	end

One test_cases.in with two cases on it is attached as example.

After reading the file, the program calculates the convex hull set and the shortest path of the test cases defined on it, for both iterative and divide and conquest algorithms.  
The output of each one is compared to check if they are returning the same shortest path.  
Auto explicative output is printed about the result of the algorithms over the test cases provided.

##HOW TO COMPILE##

For compiling I’ve used the GNU c++ compiler, so that I can’t know what will happen if it is compiled by microsoft or other compilers. MinGW can be installed in no UNIX machines for using the GNU compiler.  
*Attention*: I am using some features from C++11, so that compilers which does not support this standard could not compile the source code.

In order to compile the main.cpp or any other executable source file I use the following command, once the terminal is situated in the same directory than the file to be compiled:

	$ g++ -std=c++0x -o "%e.o”  "%f”

Where %f must be replaced by the source file, and %e.o by the name for the output executable file.

##HOW TO USE##

Once compiled, the executable can be run typing:
`$ ./%e.o` in the same directory under UNIX systems.
In the case of the main.cpp code, the same directory has to contain a test_cases.in file with the syntax described above.

It is possible to add some code to the test source files and to enable the debug variable in the CH_Algorithms.cpp file to see more detail of the process.

##KNOWN ISSUES##

isUpperTangent and isLowerTangent has a problem when they have to calculate the equation for a line between two points with the same x value, since the standard formula does not work for this particular case.  
This implementation aborts the execution with exit code 1, if this case is reached. The proposal solution for this is, sub-sequentially, to sum or subtract 0.0001 to the x values of  points with the same x value.  
The result will be fairly close to the original and the divide and conquer algorithm will work.

##POSSIBLE IMPROVEMENTS##

There are some possible improvements, basically in the heap ADT and in the data structures used in CH_Algorithms. They are pointed out in the header documentation of the appropriate source file.

isUpper and isLower could be implemented much more efficiently checking if the previous and the next points are in the same side between the two possible sides generated by the line joining the tangent points. This would give a constant time function for them instead of a linear function.

Implement a GUI to plot the points, the obstacle and the path. OpenGL could be used for this matter.

##SUMMARY AND CONCLUSIONS##

The most difficult part was to figure out how to merge the sub-convex hull in the D&C algorithm, the sortClockwise function was not explicitly described in the description of the assignment but is required for this algorithm and took time to think about it.

I still find too complex and worse the Divide and Conquer algorithm compared to the iterative algorithm.

I also had to deal with the STL for the data structures used, which takes time and study of the documentation, as well as with the read of input files.

The project was challenging since it required: time, no short program, choose and use the adequate data structures, critical thinking, knowledge of the programming language, modularity of the implementation and uses of the knowledge learnt in the course.

## CONFIGURATION USED FOR THE DEVELOPMENT OF THE PROJECT ##
* Programming language: C++11  
* Compiler: g++ with -std=c++0x  
* Geany as editor and Eclipse CDT as debugger.  
* Ubuntu 14.04 64-bits as operating system

##BIBLIOGRAPHY##
* Slides of an algorithms course
* C++ Classes and Data Structures. Jeffrey S. Childs. 2008
* ['Merging convex hulls' by Hormoz Pirzadeh](http://cgm.cs.mcgill.ca/~orm/mergech.html "Pirzadeh's merge hulls link"). It inspired me for my Divide and Conquer algorithm. 
