Download Link: https://assignmentchef.com/product/solved-mie562-assignment1-dispatch-rules
<br>
The assignment is to write Python 3 code to do the following:

<ul>

 <li>read in a job shop scheduling problem file (with a specified file format – see below)</li>

 <li>solve the problem using the shortest processing time (SPT) dispatch rule</li>

 <li>return the makespan and solution found</li>

</ul>

We have done our best to answer all questions in this document. Please read it carefully. If you have a question that is not covered here (and you are sure), please post it to piazza.

<h1>1             Problem Definition Details</h1>

You can find definitions of the job shop scheduling problem and the SPT dispatch rule in the course slides and/or textbook. In this section, we provide details on how we represent the problem instances and the conventions used.

<h2>1.1           Instance Files</h2>

Each instance file consists of the following:

<ul>

 <li>a line of description</li>

 <li>a line containing the number of jobs and the number of machines</li>

 <li>then one line for each job, listing the machine number and processing time for each step of the job.</li>

</ul>

The machines are implicitly numbered starting at 0. Here is an example instance file.

Sample Instance

2 3

2 1 0 3 1 6

0 8 1 5 2 10

In this instance there are 2 jobs and 3 machines. Job 0 is on line 3 and job 1 line 4. Job 0, operation 0 requires machine 2 and has a processing time of 1. Job 0, operation 1 requires machine 0 and has a processing time of 3. And so on.

This format follows the standard JSP instance format (see <a href="http://people.brunel.ac.uk/~mastjjb/jeb/orlib/files/jobshop1.txt">http://people.brunel.ac.uk/ </a><a href="http://people.brunel.ac.uk/~mastjjb/jeb/orlib/files/jobshop1.txt"><sub>~</sub></a><a href="http://people.brunel.ac.uk/~mastjjb/jeb/orlib/files/jobshop1.txt">mastjjb/jeb/orlib/files/jobshop1.txt</a><a href="http://people.brunel.ac.uk/~mastjjb/jeb/orlib/files/jobshop1.txt">)</a> and so you should be able to find many test problems for your code.

A small set of instances, with answers, has been posted for you on Quercus (see Coding Assignment #1). You are strongly encouraged to create (or find) your own instances to test your code.

<h2>1.2           Job Numbering</h2>

Jobs are numbered starting at zero. Each job row in the instance corresponds to a job with the numbering starting at zero and incrementing by 1 with each line (e.g., the row after Job 0 contains Job 1). Operations within each job are numbered starting at zero; again they increment by one. As such, an operation can be uniquely identified by the pair of its job number and operation number within its job. So the first operation in Job 0 is (0,0), the second operation is (0,1), and so on.

<h2>1.3           Tie Breaking</h2>

It is important that you follow this tie breaking rule to ensure that your algorithm finds the same solutions as the one we have implemented and will compare against.

In your algorithm, you must use the SPT dispatch rule to order the list of available operations on each machine. Depending on the data, you may have to order two or more operations with the same processing time. If this happens, you are guaranteed that each operation will come from a different job.<a href="#_ftn1" name="_ftnref1"><sup>[1]</sup></a> <strong>Therefore, to break ties, you should order the operations in ascending order of job number.</strong>

For example, if you have operation (3,2) (i.e., job 3, operation 2) and operation (4,0) both with processing time 10 and both available to be executed on the same machine, then (3,2) should come before (4,0) in your list because 3 <em>&lt; </em>4.

<h1>2             Coding and Marking Details</h1>

We will use the automated marking system called MarkUS to mark your code (see “Marking Scheme” below). MarkUS is running Python 3.8.3 and your code needs to work with this version of Python.<a href="#_ftn2" name="_ftnref2"><sup>[2]</sup></a>

In this section, we provide the coding requirements and other necessary information for using the MarkUS grading system.

<h2>2.1           Function Definition</h2>

You must submit a Python file called coding1.py that contains (perhaps among other functions) a function with the following signature:

run SPT(instance), where instance is a string of the filename of the instance (e.g.,

“ft06.txt”).

The function should read in the problem instance (assume it is in the same folder as the coding1.py file) and solve the problem with the SPT dispatch rule with tie breaking as described above.

The function should return a tuple containing:

<ul>

 <li>the makespan: integer</li>

 <li>a schedule: a dictionary with keys corresponding to the job number and values being a list of start times for that job’s operations following that job’s operation order.</li>

</ul>

For example the solution to the “Sample Instance” given above is:

(23, {0: [0, 8, 13], 1: [0, 8, 13]})

The makespan is 23. Job 0, operation 0 starts at time 0. Job 0, operation 1 starts at time 8. Etc.

MarkUS will call your function and parse the return value to compare it against the correct answer. It is important that you follow the above instructions exactly.

Do not put any input or print statements in your code.

<h2>2.2           Use of External Modules: Don’t</h2>

You may not use any external modules for your code. The reasons for this is that they really will not help you, we want you to write the algorithm not depend on some other implementation, and MarkUS will crash if you try to use any modules that we have not installed.

If you have a good argument as to why you should be allowed to use a particular external module that does not defeat the purpose of this assignment, I am willing to listen to it. Please email Prof. Beck.