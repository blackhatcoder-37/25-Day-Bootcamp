# 🚀 25-Day DSA Launchpad Bootcamp — LeetCode Solutions

Welcome to the official solutions repository for the 25-Day Data Structures & Algorithms (DSA) Bootcamp! This repository is explicitly created for my students and contains the optimized answers, implementations, and structural approaches to the 25 core LeetCode problems we solve throughout this program.

Every code file within this repository maps directly to the daily coding challenges followed from the custom-curated bootcamp website:
🔗 **[DSA Launchpad](https://dsa-launchpad.vercel.app/)**

---

## 🗺️ Day-by-Day LeetCode Problem Explanations

### 📥 Phase 1: Core Fundamentals, Big-O, & Linear Sequences (Days 1–5)

#### Day 1: LeetCode 217 — Contains Duplicate
* **The Problem:** Given an integer array, determine if any value appears at least twice in the array. Return `true` if any value appears more than once, and `false` if every element is distinct.
* **The Naive Approach ($\mathcal{O}(n^2)$):** Running a nested loop configuration where every single element is compared against every other element in the array. This requires quadratic operations, leading to execution timeouts for large inputs.
* **The Optimized Solution ($\mathcal{O}(n)$ Time, $\mathcal{O}(n)$ Space):** We leverage a hash set to keep track of historical data as we iterate through the array. For each element, we perform a constant-time $\mathcal{O}(1)$ lookup to see if it already exists in our set. If it does, we instantly confirm a duplicate exists. If the loop completes without a hit, the elements are uniquely distributed. This shifts the runtime from a quadratic scale down to a linear pass by utilizing extra space to remember past inputs.

#### Day 2: LeetCode 1 — Two Sum
* **The Problem:** Given an array of integers and an integer target, return the indices of the two numbers such that they add up to the target. You may assume that each input would have exactly one solution, and you may not use the same element twice.
* **The Naive Approach ($\mathcal{O}(n^2)$):** Utilizing nested loops to check every possible pair of numbers in the array until their sum matches the target value, resulting in an inefficient quadratic runtime.
* **The Optimized Solution ($\mathcal{O}(n)$ Time, $\mathcal{O}(n)$ Space):** Instead of searching for two items simultaneously, we reframe the problem mathematically: $	ext{complement} = 	ext{target} - 	ext{current value}$. As we iterate through the list in a single linear pass, we check if the required complement is already stored in a hash map. If it is present, we have found our matching pair and immediately return their indices. If it is absent, we store the current value alongside its index in the hash map. This approach converts a nested lookup into an instantaneous $\mathcal{O}(1)$ query, bypassing the need for secondary search passes.

#### Day 3: LeetCode 125 — Valid Palindrome
* **The Problem:** Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.
* **The Naive Approach ($\mathcal{O}(n)$ Time, $\mathcal{O}(n)$ Space):** Filtering out invalid characters, creating a completely reversed copy of the string in memory, and checking if the two sequences are identical. While linear in time, copying strings in Python repeatedly triggers heavy garbage collection and overhead.
* **The Optimized Solution ($\mathcal{O}(n)$ Time, $\mathcal{O}(1)$ Space):** We implement the *Two-Pointer Pattern* to achieve maximum memory efficiency. We place a `left` pointer at the start of the string and a `right` pointer at the absolute end. In a single loop, these pointers march inward toward the center. We use quick checks to skip non-alphanumeric characters without altering the string. At each valid step, we compare the characters under both pointers. If a mismatch occurs, we immediately break and declare it invalid, completing the validation with zero auxiliary memory allocations.

#### Day 4: LeetCode 242 — Valid Anagram
* **The Problem:** Given two strings `s` and `t`, return `true` if `t` is an anagram of `s`, and `false` otherwise. An anagram is a word formed by rearranging the letters of another.
* **The Naive Approach ($\mathcal{O}(n \log n)$):** Sorting both strings alphabetically and checking if their sorted sequences are identical. While this uses minimal extra memory ($\mathcal{O}(1)$ or $\mathcal{O}(n)$ depending on the sorting algorithm), the sorting step forces a logarithmic runtime bottleneck.
* **The Optimized Solution ($\mathcal{O}(n)$ Time, $\mathcal{O}(1)$ Space — bounded by character set size):** We count character frequencies to analyze the internal composition of both strings directly. We construct a frequency mapping dictionary for the first string, incrementing counters for each character. Then, we loop through the second string, decrementing those same character counters. If any counter drops below zero or if the strings are of unequal lengths, they cannot be anagrams. This approach optimizes the process into a single linear sweep, using a bounded hash map containing a maximum of 26 character slots.

#### Day 5: LeetCode 206 — Reverse Linked List
* **The Problem:** Given the head of a singly linked list, reverse the list, and return its new inverted head node.
* **The Naive Approach ($\mathcal{O}(n)$ Time, $\mathcal{O}(n)$ Space):** Iterating through the list, copying all values into an array, reversing that array, and rebuilding a brand-new set of linked nodes from scratch, wasting system heap memory.
* **The Optimized Solution ($\mathcal{O}(n)$ Time, $\mathcal{O}(1)$ Space):** We re-wire the existing node connections directly in memory. By tracking three consecutive pointers—`prev` (initially null), `curr` (starting at head), and `next_node` (to temporarily hold the rest of the chain)—we update the reference pointers one node at a time. Within a single pass, we point `curr.next` backward to `prev`, then slide our tracking references forward. When `curr` reaches the end of the list, `prev` is left pointing directly at the new head of the completely reversed chain.

---

### 📥 Phase 2: Linear Data Structures & Search Paradigms (Days 6–10)

#### Day 6: LeetCode 20 — Valid Parentheses
* **The Problem:** Given a string containing just the characters `(`, `)`, `{`, `}`, `[` and `]`, determine if the input string is valid based on correct opening and nesting order.
* **The Naive Approach ($\mathcal{O}(n^2)$):** Repeatedly searching and replacing valid adjacent pairs (like replacing `"()"` or `"{}"` with `""`) across the string until no matching pairs remain, which triggers multiple expensive string scans.
* **The Optimized Solution ($\mathcal{O}(n)$ Time, $\mathcal{O}(n)$ Space):** We implement a *Stack* data structure to enforce Last-In, First-Out (LIFO) tracking. As we step through the string, every opening bracket is pushed onto the stack. When we encounter a closing bracket, we check the top of the stack. If the stack is empty or the top element does not match the required opening pair, the structure is invalid. If it matches, we pop the opening bracket off and continue. The string is valid only if the stack is completely empty after checking every character.

#### Day 7: LeetCode 225 — Implement Stack using Queues
* **The Problem:** Implement a Last-In, First-Out (LIFO) stack using only standard First-In, First-Out (FIFO) queues.
* **The Core Challenge:** A queue naturally processes data in the opposite order of a stack. To make a queue behave like a stack, we must systematically reverse its processing order during data insertions.
* **The Solution ($\mathcal{O}(n)$ Push, $\mathcal{O}(1)$ Pop):** We use a single `collections.deque` as our primary queue structure. When a new element is pushed, we append it to the rear of the queue as usual. Then, to simulate stack behavior, we exploit the queue's circular nature: we pop elements from the front and immediately re-append them to the rear for a total of `size - 1` times. This rotates the newly added element all the way to the front of the queue, making it the first item available to be removed and achieving true LIFO behavior.

#### Day 8: LeetCode 704 — Binary Search
* **The Problem:** Given an array of integers which is already sorted in ascending order, and a target value, search for the target inside the array. If it exists, return its index; otherwise, return `-1`.
* **The Naive Approach ($\mathcal{O}(n)$):** Performing a standard linear search from left to right, inspecting each element one by one, which fails to take advantage of the sorted data.
* **The Optimized Solution ($\mathcal{O}(\log n)$ Time, $\mathcal{O}(1)$ Space):** We use the *Divide and Conquer* strategy. By maintaining a `low` pointer and a `high` pointer, we calculate the exact midpoint index of our active search space. We compare the midpoint value against our target: if it matches, we return the index; if the target is smaller, we shift our `high` pointer to discard the right half; if it is larger, we shift our `low` pointer to discard the left half. This continuous halving cuts down our remaining search space exponentially, finding the target in logarithmic time.

#### Day 9: LeetCode 121 — Best Time to Buy and Sell Stock
* **The Problem:** Given an array of daily stock prices, find the maximum profit you can achieve by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.
* **The Naive Approach ($\mathcal{O}(n^2)$):** Using nested loops to evaluate every possible combination of buy and sell days, which causes execution timeouts on larger price arrays.
* **The Optimized Solution ($\mathcal{O}(n)$ Time, $\mathcal{O}(1)$ Space):** We use a single-pass *Sliding Window* strategy to track the lowest price seen so far. As we sweep through the prices, we update our minimum buying price whenever we find a lower value. At the same time, we calculate the potential profit at the current day's price relative to that minimum. If this current profit is higher than our maximum recorded profit, we update our target goal, solving the challenge in a single linear pass.

#### Day 10: LeetCode 912 — Sort an Array
* **The Problem:** Given an array of integers, sort the elements in ascending order.
* **The Bootcamp Application:** While advanced production environments rely on $\mathcal{O}(n \log n)$ algorithms like Merge Sort, today we implement *Insertion Sort* on controlled, smaller test datasets to master core in-place array manipulation.
* **The Mechanics ($\mathcal{O}(n^2)$ Time, $\mathcal{O}(1)$ Space):** Insertion Sort works by dividing the array into a sorted and an unsorted segment. We iterate through the unsorted portion from left to right. For each element, we extract it and slide it backward through the sorted segment, swapping it with larger numbers until it reaches its correct sorted position. This helps students build a solid foundation in loop constraints and in-place boundary management.

---

### 🔄 Phase 3: Recursion & Advanced Sorting (Days 11–15)

#### Day 11: LeetCode 509 — Fibonacci Number
* **The Problem:** Calculate the $n$-th number in the Fibonacci sequence, where each number is the sum of the two preceding ones, starting from 0 and 1.
* **The Naive Approach ($\mathcal{O}(2^n)$):** Implementing the pure mathematical formula recursively without optimization: `return fib(n-1) + fib(n-2)`. This creates a massive tree of redundant function calls that repeatedly calculates the exact same values, causing performance to drop off exponentially.
* **The Balanced Solution ($\mathcal{O}(n)$ Time, $\mathcal{O}(1)$ Space):** While this problem can be solved recursively using memoization, we implement the iterative solution to demonstrate structural balance. By using two variables to store only the last two calculated numbers, we loop forward from 2 up to $n$, updating our variables as we go. This replaces an expensive, deep recursive call stack with a simple linear loop that uses zero extra memory.

#### Day 12: LeetCode 88 — Merge Sorted Array
* **The Problem:** Given two sorted integer arrays `nums1` and `nums2`, merge `nums2` into `nums1` as a single, combined sorted array. `nums1` has a large enough buffer at the end to hold the extra elements from `nums2`.
* **The Naive Approach ($\mathcal{O}((m+n) \log(m+n))$):** Appending all elements from `nums2` directly into the empty space at the end of `nums1`, then running a built-in sort function across the entire array.
* **The Optimized Solution ($\mathcal{O}(m+n)$ Time, $\mathcal{O}(1)$ Space):** We use a *Three-Pointer Pattern* that processes the arrays from back to front to avoid overwriting unexamined data in `nums1`. We place pointers at the end of the initialized values in `nums1`, the end of `nums2`, and the absolute end of `nums1`'s memory buffer. We compare elements from largest to smallest, placing the larger value into the back of the buffer and moving the corresponding pointers leftward. This fills the container securely in a single pass without using any extra memory.

#### Day 13: LeetCode 215 — Kth Largest Element in an Array
* **The Problem:** Find the $k$-th largest element in an unsorted integer array. Note that it is the $k$-th largest element in sorted order, not the $k$-th distinct element.
* **The Naive Approach ($\mathcal{O}(n \log n)$):** Sorting the entire array in descending order and returning the element at index `k - 1`.
* **The Optimized Solution ($\mathcal{O}(n)$ Average Time, $\mathcal{O}(1)$ Space):** We implement the *Quickselect* algorithm, which leverages the partitioning logic of Quick Sort. We select a pivot element and rearrange the array so that all elements smaller than the pivot move to its left and all larger elements move to its right. We then check the pivot's final index. If it matches our target index, we have found our answer. If it doesn't, we narrow our search and recursively partition only the sub-array that contains our target index. This allows us to skip sorting the other half of the data entirely, reducing our average runtime to a linear scale.

#### Day 14: LeetCode 73 — Set Matrix Zeroes
* **The Problem:** Given an $m 	imes n$ integer matrix, if an element is 0, set its entire row and column to 0s. Do this in-place.
* **The Naive Approach ($\mathcal{O}(m \cdot n)$ Space):** Creating a complete duplicate of the matrix to read zeroes from while overwriting the original grid, or using extra arrays of size $m$ and $n$ to track which rows and columns should be zeroed out.
* **The Optimized Solution ($\mathcal{O}(m \cdot n)$ Time, $\mathcal{O}(1)$ Space):** We use the first row and the first column of the matrix itself as tracking flags. We scan the rest of the grid; if we find a 0 at cell `(r, c)`, we set the flags at `matrix[r][0]` and `matrix[0][c]` to 0. After marking all flags, we iterate through the grid a second time, using those flags to safely fill the appropriate rows and columns with zeroes. We handle the first row and column with two dedicated variables to prevent our tracking flags from overwriting each other.

#### Day 15: LeetCode 387 — First Unique Character in a String
* **The Problem:** Given a string `s`, find the first non-repeating character in it and return its index. If it does not exist, return `-1`.
* **The Naive Approach ($\mathcal{O}(n^2)$):** Using nested loops where each character is compared against every other character in the string to verify uniqueness, which becomes highly inefficient for long text inputs.
* **The Optimized Solution ($\mathcal{O}(n)$ Time, $\mathcal{O}(1)$ Space):** We use a structural two-pass lookup approach. In the first pass, we loop through the string to build a character frequency map, counting how many times each letter appears. In the second pass, we loop through the string again in order, checking our frequency map for each character. The first character we find with a frequency count of exactly one is our first unique character, and we return its index immediately.

---

## 🌲 Phase 4: Trees, Graphs & Traversal Strategies (Days 16–20)

#### Day 16: LeetCode 700 — Search in a Binary Search Tree
* **The Problem:** Find the node in a Binary Search Tree (BST) whose value matches the given target, and return the entire subtree rooted at that node. If it doesn't exist, return `null`.
* **The Naive Approach ($\mathcal{O}(n)$):** Performing a standard traversal (like DFS or BFS) across every single node in the tree, ignoring the structural rules of a BST.
* **The Optimized Solution ($\mathcal{O}(\log n)$ Time, $\mathcal{O}(1)$ Space - Iterative):** We leverage the ordering property of a BST: every value in a node's left subtree is smaller than its own value, and every value in its right subtree is larger. Starting at the root, if our target is smaller than the current node's value, we move to the left child; if it's larger, we move to the right child. This allows us to trace a single path down the tree, matching the efficiency of binary search.

#### Day 17: LeetCode 94 — Binary Tree Inorder Traversal
* **The Problem:** Given the root of a binary tree, return the in-order traversal of its nodes' values as a list.
* **The Algorithmic Concept:** An in-order traversal follows a strict processing order: left subtree first, then the current parent node, and finally the right subtree.
* **The Solution ($\mathcal{O}(n)$ Time, $\mathcal{O}(n)$ Space):** We implement a recursive function that follows this exact pattern. The function first calls itself on the left child, then records the current node's value into a results list, and finally calls itself on the right child. This ensures that every node in the tree is visited exactly once, processing values from left to right.

#### Day 18: LeetCode 102 — Binary Tree Level Order Traversal
* **The Problem:** Given the root of a binary tree, return the level-order traversal of its nodes' values grouped by their respective levels (i.e., layer by layer from left to right).
* **The Algorithmic Concept:** Horizontal layer-by-layer traversal requires a *Breadth-First Search (BFS)* strategy, which relies on a First-In, First-Out (FIFO) queue to track nodes in the order they are discovered.
* **The Solution ($\mathcal{O}(n)$ Time, $\mathcal{O}(n)$ Space):** We initialize a queue containing the root node. To group values by level, we use a nested loop structure inside our main BFS loop. At the start of each level iteration, we record the queue's current size. This tells us exactly how many nodes belong to the current layer. We then loop through that exact number of nodes, popping each one from the front, adding its value to a temporary level list, and appending its left and right children to the back of the queue.

#### Day 19: LeetCode 1971 — Find if Path Exists in Graph
* **The Problem:** Given an undirected graph represented as a list of edges, determine if there is a valid path that connects a source vertex to a destination vertex.
* **The Core Graph Preparation:** Raw edge lists are inefficient to traverse directly. To search the network efficiently, we must first convert the edge list into an *Adjacency List* using a dictionary.
* **The Solution ($\mathcal{O}(V + E)$ Time, $\mathcal{O}(V + E)$ Space):** After building our adjacency list to map out the graph's connections, we run a standard traversal (DFS or BFS) starting from the source vertex. We maintain a visited set to avoid getting trapped in cycles. As we explore neighbor nodes, if we encounter our destination vertex, we immediately return `true`. If our traversal finishes and the destination remains unvisited, no path exists.

#### Day 20: LeetCode 200 — Number of Islands
* **The Problem:** Given an $m 	imes n$ 2D binary grid map of land (`'1'`) and water (`'0'`), return the total number of distinct islands. An island is surrounded by water and formed by connecting adjacent land cells horizontally or vertically.
* **The Algorithmic Concept:** We treat the 2D grid as a graph network where adjacent land cells share connecting edges.
* **The Solution ($\mathcal{O}(m \cdot n)$ Time, $\mathcal{O}(m \cdot n)$ Space):** We iterate through the grid row by row. When we encounter an unvisited land cell (`'1'`), we have discovered a new island, so we increment our island counter. We then trigger a full traversal (DFS or BFS) starting from that cell to find all connected land cells. As we visit each piece of land, we change its value to `'0'` (or add it to a visited set) to mark it as processed, effectively sinking the island so it won't be counted again.

---

### 🏆 Phase 5: Advanced Optimization & Capstone Pitch (Days 21–25)

#### Day 21: LeetCode 1046 — Last Stone Weight
* **The Problem:** You are given an array of integers representing the weights of stones. Each turn, we choose the two heaviest stones and smash them together. If they are of equal weight, both are destroyed; if not, the smaller stone is destroyed and the larger stone's weight is reduced by the smaller stone's weight. Repeat this until at most one stone remains.
* **The Naive Approach ($\mathcal{O}(n^2 \log n)$):** Sorting the array to find the two heaviest stones, smashing them, adding the remainder back into the list, and re-sorting the array on every single turn.
* **The Optimized Solution ($\mathcal{O}(n \log n)$ Time, $\mathcal{O}(n)$ Space):** We use a *Max-Heap* to automatically track the heaviest stones. Since Python’s `heapq` module implements a Min-Heap by default, we invert all stone weights (multiplying them by -1) before loading them into the heap. On each turn, we easily pop the two largest weights in logarithmic $\mathcal{O}(\log n)$ time, calculate the result of the smash, and if a remainder exists, push it back into the heap. This avoids expensive re-sorting passes.

#### Day 22: LeetCode 53 — Maximum Subarray
* **The Problem:** Given an integer array, find the contiguous subarray which has the largest sum and return its sum.
* **The Naive Approach ($\mathcal{O}(n^2)$):** Using nested loops to calculate the sum of every possible contiguous subarray combination to find the maximum, which is too slow for large arrays.
* **The Optimized Solution ($\mathcal{O}(n)$ Time, $\mathcal{O}(1)$ Space):** We implement *Kadane’s Algorithm*, a classic greedy strategy. As we iterate through the array, we make an immediate, local decision at each index: should we add the current number to our running subarray sum, or should we discard the past and start a brand-new subarray right here? If our running sum drops below zero, it would only reduce the value of future additions, so we reset our running sum to the current number. We track the highest sum seen throughout the pass, solving the problem in a single sweep.

#### Day 23: LeetCode 70 — Climbing Stairs
* **The Problem:** You are climbing a staircase that takes $n$ steps to reach the top. Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?
* **The Naive Approach ($\mathcal{O}(2^n)$):** Using simple recursion to calculate the steps: `climb(n-1) + climb(n-2)`. This creates a massive, deep tree of duplicate calculations that slows down exponentially as $n$ grows.
* **The Optimized Solution ($\mathcal{O}(n)$ Time, $\mathcal{O}(n)$ Space):** We apply *Dynamic Programming via Memoization*. We reframe the problem by realizing that the number of ways to reach the current step is simply the sum of the ways to reach the two steps right below it. To eliminate duplicate calculations, we use a dictionary or array as a memory state table to store the results of each step size after computing it the first time. Before running a calculation, we check our table—if the answer is already there, we return it instantly, reducing the runtime to a clean linear scale.

#### Day 24: LeetCode 136 — Single Number
* **The Problem:** Given a non-empty array of integers, every element appears twice except for one. Find that single unique element.
* **The Naive Approach ($\mathcal{O}(n)$ Time, $\mathcal{O}(n)$ Space):** Using a hash map or set to count occurrences or track elements, which uses extra memory.
* **The Optimized Solution ($\mathcal{O}(n)$ Time, $\mathcal{O}(1)$ Space):** We use *Bit Manipulation* by applying the Bitwise XOR (`^`) operator across the array. XOR operations follow unique logical rules: any number XORed with itself cancels out and results in 0 ($A \oplus A = 0$), while any number XORed with 0 remains unchanged ($A \oplus 0 = A$). By initializing a tracker to 0 and XORing it with every number in the array, all duplicate pairs completely cancel each other out, leaving behind exactly the single unique value without using any extra memory.

#### Day 25: LeetCode 344 — Reverse String
* **The Problem:** Write a function that reverses a string. The input string is given as an array of characters. You must mutate the input array in-place with $\mathcal{O}(1)$ extra memory.
* **The Bootcamp Significance:** A classic, clear challenge to wrap up the bootcamp, bringing our journey full circle by returning to the core pointer and memory concepts learned on Day 1.
* **The Solution ($\mathcal{O}(n)$ Time, $\mathcal{O}(1)$ Space):** We use the *Two-Pointer Pattern*. We position a `left` pointer at index 0 and a `right` pointer at the final index of the character array. In a simple loop, we swap the characters under the two pointers, then move the pointers inward (`left += 1`, `right -= 1`). The loop finishes as soon as the pointers meet or cross in the center, completing the array inversion in-place with zero extra memory overhead.

---

## 🛠️ How to Navigate This Codebase

* **Folder Mapping:** Each day's directory contains the complete, standalone Python solution file for the corresponding LeetCode problem explained above.
* **Verification:** All solutions are fully optimized and verified to pass all automated test suites on LeetCode.
* **Study Guide:** Use this README to review the core algorithmic patterns (such as sliding windows, two-pointers, stacks, queues, and heaps) before diving into the individual code implementations.

**"Love a little more and hate a little less"** — Let's continue writing clean, efficient, and beautifully optimized code! Happy coding! 🚀
