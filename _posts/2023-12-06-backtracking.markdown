---
layout: post
title: "Backtracking"
date: 2023-12-06 21:19:00 -0800
permalink: /blog/:title
---

## BackTracking

Found out about two ways to implement backtracking and I want to write them down here before I forget. 

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

The stack tree looks something like so given candidates [2, 3] and target 4

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

The other way of doing backtracking involves a very different call stack, I myself am more inclined to think in this way, hence this article. 

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
