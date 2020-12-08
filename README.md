# greedy-algo-
My solution for algo

Solves this algo: 


Thumbnail Image
NEW
Google Android Developer Interview
Google Android Engineer Interview Process and Preparation.

Minimum Number Of Jumps To Reach End

Difficulty: Hard

Asked in: Amazon, Google, Ebay

Understanding The Problem
Problem Description

Given an array of non-negative integers arr[] of length n, where each element represents the max number of steps that can be made forward from that element. You are initially positioned at the first index of the array. Write a program to return the minimum number of jumps to reach the last index of the array.

Problem Note

If it is not possible to reach the last index, return -1.
If an element is 0, then you cannot move through that element.
Example 1

Input: arr[] = [2, 1, 1] 
Output: 1 
Explanation: The minimum number of jumps to reach the last index is 1. Jump 2 steps from index 0 to 2.
Example 2

Input: arr[] = [2, 3, 2, 4, 4] 
Output: 2 
Explanation: The minimum number of jumps to reach the last index is 2. Jump 1 step from index 0 to 1, then 3 steps to the last index.
Solutions
Brute Force Solution → We will start with the ‘0’th index and try all options. After taking a jump to an index, we recursively try all options from that index.
Dynamic Programming → For each value at the ith index, move from ith index to ith+ar[i] and update the minimum number of jumps till there.
Optimized Dynamic Programming
You can try to solve the problem here.

1. Brute Force Solution
The most basic approach for the problem is to start from the first element and recursively call for all the elements reachable from the first element.

The minimum number of jumps to reach the end from first can be calculated using the minimum number of jumps needed to reach the end from the elements reachable from first.
minJumps(start, end) = Min ( minJumps(k, end) ) for all k reachable from start.

In other words, from start move to all such indexes that are reachable from start and then recursively get the minimum number of jumps needed to reach the end from these reachable options.

Look at the below example:


Solution Steps

Create a recursive function which will return the minimum number of jumps needed to reach from the current position to the end
a minJump will store the minimum number of jumps as an answer
maxSteps will store the maximum number of positions we can move from the currPos
Iterate till maxSteps > 0 and for each position, call the recursive function to reach till the end and thereby increment the jumps by 1 for each jump.
Pseudo Code

int decideJump(int[] nums, int n, int currPos){
    if(currPos >=  n-1){
        return 0
    }
    int minJump = INT_MAX
    int maxSteps = nums[currPos]
    while(maxSteps > 0){
        minJump = min(minJump, 1 + decideJump(nums,n,currPos+maxSteps))
        maxSteps = maxSteps - 1
    }
    return minJump
}
   
int jump(int[] nums, int n) {
    return decideJump(nums, n, 0)
}
Complexity Analysis

Time Complexity: O(n^n)

Space Complexity: O(1), not considering recursion stack space.

Critical Ideas To Think

What is the recurrence relation for this approach?
Why did we maintain the maxSteps variable here?
Why did we initialize minJump with INT_MAX?
2. Dynamic Programming
You must have noticed that we were recalculating the minimum number of steps to reach the end of the brute force approach. If we could remove such recalculations by memorizing the minimum jumps from each index to reach the end will lead to a more optimized solution which is called dynamic programming.

How will we do that?

We will go with the elements of dynamic programming:-

1. Define the problem variable and decide the states: There is only one parameter on which the state of the problem depends i.e. which is N here.

2. Define Table Structure and Size: To store the solution of smaller sub-problems in the bottom-up approach, we need to define the table structure and table size.

The table structure is defined by the number of problem variables. Since the number of problem variables, in this case, is 1, we can construct a one-dimensional array to store the solution of the sub-problems.
The size of this table is defined by the number of subproblems. There are a total of N subproblems.
3. Table Initialization: We can initialize the table by using the base cases from the recursion. (Think)

minJumps[0] = 0
4. Iterative Structure to fill the table: We can define the iterative structure to fill the table by using the recurrence relation of the recursive solution.

minJumps[i] = 1 + min(minJumps[i], 1 + 
                        min( minJumps[i+1], 
                             minJumps[i+2], 
                             . . . 
                             minJumps[i + minJumps[i] + 1]
                           )
                     )
5. Termination and returning final solution: After filling the table, our final solution gets stored at the last Index of the array i.e. return minJumps[N-1].

Look at the below example to understand the discussed scenario. The respective colored boxes represent overlapping subproblems.


Solution Steps

Create a dp array minJumps of size n to store the minimum number of jumps from ith index to reach the end and initialize it with INT_MAX.
Initialize minJumps[0] = 0 (Why?)
Fill the table by following the iterative structure discussed above.
Return the last index of minJumps
Pseudo Code

int minJump(int[] num, int n){
    int[n] minJumps = {INT_MAX}
    minJumps[0] = 0
    for(i = 0 to i < n){
        for(j = i+1 to j < min(i+num[i]+1, n)) {
            minJumps[j] = min(minJumps[j], 1 + minJumps[i])
        }
    }
    return minJumps[n-1]
}
Complexity Analysis

Time Complexity: O(n²)

Space Complexity: O(n)

Critical Ideas To Think

What do the elements of dynamic programming mean?
How did we reach the iterative structure?
Why did we maintain a 1-D Dp array?
Thumbnail Image
NEW
Android App Development Online Course by MindOrks
Start your career in Android Development. Learn by doing real projects.

3. Greedy Approach
The difference between greedy and dynamic approach is that the DP solves subproblems first, then uses those solutions to make an optimal choice whereas Greedy makes an optimal choice (without knowing solutions to subproblems) and then solve remaining subproblem(s), but both apply to problems with optimal substructure.

Here, the problem only asks for the min number of jumps. So we do not have to figure out each jump position. We only need to store the max_reach of the previous jump position. If we go beyond that, we need one more jump.
