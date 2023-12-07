---
layout: post
title: "Backtracking"
date: 2023-12-06 21:19:00 -0800
permalink: /blog/:title
---

Found out about two ways to implement backtracking and I want to write them down here before I forget. 

This article is trying to highlight the 2 different ways I have used to do backtracking problems. 

One way of doing it is littered in all of LeetCode. 

{% highlight ruby %}
public class CombinationSum {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(result, candidates, target, 0, new ArrayList<>(), 0);
        return result;
    }

    private void backtrack(List<List<Integer>> result, int[] candidates, int target, int start, List<Integer> cur, int total) {
        if (total == target) {
            result.add(new ArrayList<>(cur));
            return;
        }
        if (start >= candidates.length || total > target) {
            return;
        }

        for(int i = start; i < candidates.length; i++) {
          cur.add(candidates[i]);
          backtrack(result, candidates, target, i, cur, total + candidates[i]);
          cur.remove(cur.size() - 1);
        }
    }
}
{% endhighlight%}

This iterates through each element of the array in the for loop, adding it into the total. 

The stack tree looks something like so given candidates = [2, 3, 6] and target = 6

backtrack(start, cur, total) 
- `start` being the current index of the candidates array
- `cur` being the current combination list that is being constructed
- `total` being the current total of the `cur` list 

{% highlight ruby %}
combinationSum([2, 3, 6], 6)
|
|-- backtrack(0, [], 0) (Initial Call)
|   |
|   |-- backtrack(0, [2], 2) (Include 2)
|   |   |
|   |   |-- backtrack(0, [2, 2], 4) (Include 2)
|   |   |   |
|   |   |   |-- backtrack(0, [2, 2, 2], 6) (Include 2) [Target reached, backtrack]
|   |   |   |
|   |   |   |-- backtrack(1, [2, 2, 3], 7) (Include 3) [Exceeds target, backtrack]
|   |   |   |
|   |   |   |-- backtrack(2, [2, 2, 6], 10) (Include 6) [Exceeds target, backtrack]
|   |   |
|   |   |-- backtrack(1, [2, 3], 5) (Include 3)
|   |   |   |
|   |   |   |-- backtrack(1, [2, 3, 3], 8) (Include 3) [Exceeds target, backtrack]
|   |   |   |
|   |   |   |-- backtrack(2, [2, 3, 6], 11) (Include 6) [Exceeds target, backtrack]
|   |   |
|   |   |-- backtrack(2, [2, 6], 8) (Include 6) [Exceeds target, backtrack]
|   |
|   |-- backtrack(1, [3], 3) (Include 3)
|       |
|       |-- backtrack(1, [3, 3], 6) (Include 3) [Target reached, backtrack]
|       |
|       |-- backtrack(2, [3, 6], 9) (Include 6) [Exceeds target, backtrack]
|
|-- backtrack(2, [6], 6) (Include 6) [Target reached, backtrack]
{% endhighlight%}

The way I can think about this is a way of reducing the problem space. We add the current element into the total and the combination list, and then we reduce the problem space by moving up the start pointer. 

The other way of doing backtracking involves a very different call stack, I myself am more inclined to think in this way whenever faced with a backtracking problem, hence the reason why I wrote this article. 

Although, this way tends to be less efficient (on larger problems) and tend trip me up a lot more when coding it out. 

Instead of thinking about reducing the problem space, we think of each step and whether or not we want to include the current element in the candidates list or do we exclude the current element and move on? 

{% highlight ruby %}
public class CombinationSum {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(result, candidates, target, 0, new ArrayList<>(), 0);
        return result;
    }

    private void backtrack(List<List<Integer>> result, int[] candidates, int target, int start, List<Integer> cur, int total) {
        if (total == target) {
            result.add(new ArrayList<>(cur));
            return;
        }
        if (start >= candidates.length || total > target) {
            return;
        }

        cur.add(candidates[start]);
        backtrack(result, candidates, target, start, cur, total + candidates[start]); // Increase the total
        cur.remove(cur.size() - 1);

        backtrack(result, candidates, target, start + 1, cur, total); // Do not include the current candidate
    }
}
{% endhighlight%}

And the recursive stack tree looks like this instead.

{% highlight ruby %}
combinationSum([2, 3, 6], 6)
|
|-- backtrack(0, [], 0) (Initial Call)
|   |
|   |-- backtrack(0, [2], 2) (Include 2)
|   |   |
|   |   |-- backtrack(0, [2, 2], 4) (Include 2)
|   |   |   |
|   |   |   |-- backtrack(0, [2, 2, 2], 6) (Include 2) [Target reached, backtrack]
|   |   |   |
|   |   |   |-- backtrack(1, [2, 2], 4) (Exclude last 2, try next candidate)
|   |   |       |
|   |   |       |-- backtrack(1, [2, 2, 3], 7) (Include 3) [Exceeds target, backtrack]
|   |   |       |
|   |   |       |-- backtrack(2, [2, 2], 4) (Exclude last 3, try next candidate)
|   |   |           |
|   |   |           |-- backtrack(2, [2, 2, 6], 10) (Include 6) [Exceeds target, backtrack]
|   |   |           |
|   |   |           |-- backtrack(3, [2, 2], 4) (Exclude last 6) [No more candidates, backtrack]
|   |   |
|   |   |-- backtrack(1, [2], 2) (Exclude last 2, try next candidate)
|   |       |
|   |       |-- backtrack(1, [2, 3], 5) (Include 3)
|   |       |   |
|   |       |   |-- backtrack(1, [2, 3, 3], 8) (Include 3) [Exceeds target, backtrack]
|   |       |   |
|   |       |   |-- backtrack(2, [2, 3], 5) (Exclude last 3, try next candidate)
|   |       |       |
|   |       |       |-- backtrack(2, [2, 3, 6], 11) (Include 6) [Exceeds target, backtrack]
|   |       |       |
|   |       |       |-- backtrack(3, [2, 3], 5) (Exclude last 6) [No more candidates, backtrack]
|   |       |
|   |       |-- backtrack(2, [2], 2) (Exclude last 3, try next candidate)
|   |           |
|   |           |-- backtrack(2, [2, 6], 8) (Include 6) [Exceeds target, backtrack]
|   |           |
|   |           |-- backtrack(3, [2], 2) (Exclude last 6) [No more candidates, backtrack]
|   |
|   |-- backtrack(1, [], 0) (Exclude first 2, try next candidate)
|       |
|       |-- backtrack(1, [3], 3) (Include 3)
|       |   |
|       |   |-- backtrack(1, [3, 3], 6) (Include 3) [Target reached, backtrack]
|       |   |
|       |   |-- backtrack(2, [3], 3) (Exclude last 3, try next candidate)
|       |       |
|       |       |-- backtrack(2, [3, 6], 9) (Include 6) [Exceeds target, backtrack]
|       |       |
|       |       |-- backtrack(3, [3], 3) (Exclude last 6) [No more candidates, backtrack]
|       |
|       |-- backtrack(2, [], 0) (Exclude first 3, try next candidate)
|           |
|           |-- backtrack(2, [6], 6) (Include 6) [Target reached, backtrack]
|           |
|           |-- backtrack(3, [], 0) (Exclude first 6) [No more candidates, backtrack]

{% endhighlight%}

So, I imagine this as a decision tree. At each call of the `backtrack` method, we decide between including the current element, or excluding the current element and including the next element instead. 

###Time and Space Complexity:

First Implementation (With for Loop):

This implementation uses a for loop to explore each candidate starting from the start index to the end of the candidates array. This ensures each combination is considered without repetition.
The depth of the recursion is still bounded by target/min(candidates), but the branching factor at each level of the tree is reduced compared to the first implementation. Instead of making two calls for every candidate at each level, it only explores the remaining candidates.

Time Complexity: The time complexity is exponential, but it's generally more efficient than the second approach. The exact complexity is hard to define in a simple formula as it depends heavily on the distribution of the candidates and the target value. However, it's typically closer to O(N^(T/M)), where N is the number of candidates.

Second Implementation (Without for Loop):

In this implementation, there are two recursive calls for each element in the candidates array, one including the candidate and the other excluding it.
The maximum depth of the recursion tree can be target/min(candidates), as the smallest candidate will take the maximum number of steps to reach the target.

Time Complexity: The time complexity is O(2^(T/M)), where T is the target value and M is the minimum value in the candidates. This exponential growth is due to the binary nature of choices (include or exclude) at each step.


In both cases:

The space complexity is primarily determined by the depth of the recursion tree, which is O(T/M), and the space to store the current combination, which varies depending on the combination length.
In summary, both implementations have exponential time complexities, but the second implementation is generally more efficient due to its reduced branching factor. The actual time complexity can vary significantly based on the input values and the distribution of the candidates.