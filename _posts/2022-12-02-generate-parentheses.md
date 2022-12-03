---
layout: post
title: Generate Parentheses
date: 2022-12-02 22:17 +0530
author: "Gaurav Kumar"
tags: "java recursion stack neetcode backtracking"
categories: "neetcode"
---

## Problem Description

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

[leetcode](https://leetcode.com/problems/generate-parentheses/description/)

### Solution

[NeetCode Youtube](https://www.youtube.com/watch?v=s9fokUqJ76A)

```java
class Solution {

    public List<String> generateParenthesis(int n) {
        generateParenthesisHelper(n, 0, 0, "");
        return ans;
    }

    List<String> ans = new ArrayList<>();

    public void generateParenthesisHelper(int n, int openCount, int closeCount, String current){
        
        //if total number of open and close brackets is n*2 because n pairs are allowed
        if(openCount + closeCount == n*2){
            ans.add(new String(current));
            return;
        }

        //If we have more open brackets, we can add a closing one
        if(openCount > closeCount && openCount < n){

            //add open bracket
            generateParenthesisHelper(n, openCount+1, closeCount, current += "(");

            //bracktack
            current = current.substring(0, current.length()-1);

            //add closing bracket
            generateParenthesisHelper(n, openCount, closeCount+1, current += ")");

        //if open brackets are equal to n, we cannot add anymore open brackets
        }else if(openCount == n){
            generateParenthesisHelper(n, openCount, closeCount+1, current += ")");

        //otherwise, the only option is to start with open bracket
        }else{
            generateParenthesisHelper(n, openCount+1, closeCount, current += "(");
        }

    }

}
```

### Better Code

```java
class Solution {

    public List<String> generateParenthesis(int n) {
        List<String> ans = new ArrayList();
        backtrack(ans, new StringBuilder(), 0, 0, n);
        return ans;
    }

    public void backtrack(List<String> ans, StringBuilder cur, int open, int close, int max){
        if (cur.length() == max * 2) {
            ans.add(cur.toString());
            return;
        }

        if (open < max) {
            cur.append("(");
            backtrack(ans, cur, open+1, close, max);
            cur.deleteCharAt(cur.length() - 1);
        }
        if (close < open) {
            cur.append(")");
            backtrack(ans, cur, open, close+1, max);
            cur.deleteCharAt(cur.length() - 1);
        }
    }
}
```