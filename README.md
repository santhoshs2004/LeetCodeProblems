# LeetCodeProblems 
# ALGOMAP-DATA STRUCTURES-JAVA

# Bit Manipulation

# 504. Base 7 
## Given an integer num, return a string of its base 7 representation.
```
time= O(log₇(num))
space= O(log₇(num))

class Solution {
    public String convertToBase7(int num) {
        //inbuild method
        return Integer.toString(num,7);        
    }
}

time= O(log₇(num))
space= O(log₇(num))

class Solution {
    public String convertToBase7(int num) {
        //using bit manipulation 
        if (num==0) return "0";
        int absNum=Math.abs(num);
        StringBuilder res=new StringBuilder();
        while(absNum>0){
            int digit=absNum%7;
            res.append(digit);
            absNum/=7;
        }
        if (num<0){
            res.append('-');
        }
        return res.reverse().toString();
    }
}

```

# 136. Single Number

## Given a non-empty array of integers nums, every element appears twice except for one. Find that single one.You must implement a solution with a linear runtime complexity and use only constant extra space.

 ```
time=O(nlogn)
space=O(1)
class Solution {
    public int singleNumber(int[] nums) {
//using sorting techniques
        int n=nums.length;
        if (n==1) return nums[0];
        Arrays.sort(nums);
        for(int i=0;i<n-1;i+=2){ //increment by 2
            if (nums[i]!=nums[i+1]){
                return nums[i];
            }
        }
        return nums[n-1];
    }
}

time= O(n)
space=O(1)

class Solution {
    public int singleNumber(int[] nums) {
        //using bit manipulations
        int res=0;
        for(int num:nums){
            res=res^num;
        }
        return res;
    }
}

time=O(n)
space=O(n)

class Solution {
    public int singleNumber(int[] nums) {
        //using hashset
        HashSet<Integer> set=new HashSet<>();
        for(int num:nums){
            if (set.contains(num)){
                set.remove(num);
            }
            else{
                set.add(num);
            }
            
        }
        for(int single:set){
            return single;
        }
        return -1;
    }
}

```

# 191. Number of 1 Bits

## Given a positive integer n, write a function that returns the number of set bits in its binary representation (also known as the Hamming weight).

```
time=O(k)
space= O(1)

class Solution {
    public int hammingWeight(int n) {
        //using bit manipulations...
        int count=0;
        while(n!=0){
            n=n&(n-1); //remove the rightmost 1-bit...
            count++;
        }
        return count;
    }
}

```

# 67. Add Binary
## Given two binary strings a and b, return their sum as a binary string.

```
time=O(n)
space= O(n)

import java.math.BigInteger;
class Solution {
    public String addBinary(String a, String b) {
        BigInteger num1=new BigInteger(a,2);
        BigInteger num2=new BigInteger(b,2);
        BigInteger sum= num1.add(num2);
        return sum.toString(2); //converts back to binary string
    }
}

```
# BINARY SEARCH

# 704. Binary Search

## Given an array of integers nums which is sorted in ascending order, and an integer target, write a function to search target in nums. If target exists, then return its index. Otherwise, return -1.You must write an algorithm with O(log n) runtime complexity.
```
time=O(logn)
space= O(1)

class Solution {
    public int search(int[] nums, int target) {
        //using binary search......
        
        int left=0;
        int right=nums.length-1;
        while(left<=right){
            int mid=(right+left)/2;
            if (nums[mid]==target) {
                return mid;
            }
        
            else if (nums[mid]>target){
                right=mid-1;
                //left=mid+1;
            }
            else{
                 left=mid+1;
            }
        }
        return -1;
    }
}
```

# 35. Search Insert Position
## Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.You must write an algorithm with O(log n) runtime complexity.
```
time=O(logn)
space=O(1)

class Solution {
    public int searchInsert(int[] nums, int target) {
        int left=0;
        int right=nums.length-1;
        while(left<=right){
            int mid=(right+left)/2;
            if (nums[mid]==target) return mid;
            else if(nums[mid]<target) left=mid+1;
            else right=mid-1;
        }
        return left;
    }
}
```

# 278. First Bad Version
## You are a product manager and currently leading a team to develop a new product. Unfortunately, the latest version of your product fails the quality check. Since each version is developed based on the previous version, all the versions after a bad version are also bad.Suppose you have n versions [1, 2, ..., n] and you want to find out the first bad one, which causes all the following ones to be bad.You are given an API bool isBadVersion(version) which returns whether version is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API.
```
time=O(logn)
space=O(1)

/* The isBadVersion API is defined in the parent class VersionControl.
      boolean isBadVersion(int version); */

public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        int left=1;
        int right=n;
        while(left<right){
            int mid=left+(right-left)/2;
            if (isBadVersion(mid)){
                right=mid;
            }
            else{
                left=mid+1;
            }
        }
        return left;
    }
}
```

# 367. Valid Perfect Square
## Given a positive integer num, return true if num is a perfect square or false otherwise.A perfect square is an integer that is the square of an integer. In other words, it is the product of some integer with itself.You must not use any built-in library function, such as sqrt.
```
time=O(n)
space=O(1)

class Solution {
    public boolean isPerfectSquare(int num) {
        //using sqrt...
        if(num==1) return true;
        for(int i=1;i<=Math.sqrt(num);i++){ //use i<=num/i same as math.sqrt().....
            if (i*i==num){
                return true;
            }
        }
        return false;
    }
}

time= O(logn)
space= O(1)

class Solution {
    public boolean isPerfectSquare(int num) {
        //using binary search...
        int low=1;
        int high=num;
        while(low<=high){
            int mid=low+(high-low)/2;
            if (mid*mid==num) return true;
            else if (mid*mid>num) high=mid-1;
            else low=mid+1;
        }
        return false;
    }
}
```
# 74. Search a 2D Matrix

## You are given an m x n integer matrix matrix with the following two properties:Each row is sorted in non-decreasing order.The first integer of each row is greater than the last integer of the previous row.Given an integer target, return true if target is in matrix or false otherwise. You must write a solution in O(log(m * n)) time complexity.

```
time= O(log(m × n))
space= O(1)

class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        //using binary search..
        int m=matrix.length;
        int n=matrix[0].length;
        int left=0;
        int right=m*n-1;
        while(left<=right){
            int mid=left+(right-left)/2;
            int row=mid/n;
            int col=mid%n;
            int midIndex=matrix[row][col];
            if (midIndex==target) return true;
            else if (midIndex>target) right=mid-1;
            else left=mid+1;
        }
        return false;
    }
}
```

# 153. Find Minimum in Rotated Sorted Array
## Suppose an array of length n sorted in ascending order is rotated between 1 and n times. For example, the array nums = [0,1,2,4,5,6,7] might become:[4,5,6,7,0,1,2] if it was rotated 4 times.[0,1,2,4,5,6,7] if it was rotated 7 times. Notice that rotating an array [a[0], a[1], a[2], ..., a[n-1]] 1 time results in the array [a[n-1], a[0], a[1], a[2], ..., a[n-2]].Given the sorted rotated array nums of unique elements, return the minimum element of this array.You must write an algorithm that runs in O(log n) time.

```
time=O(nlogn)
space=O(1)

class Solution {
    public int findMin(int[] nums) {
        Arrays.sort(nums);
        return nums[0];
    }
}

time=O(logn)
space=O(1)

class Solution {
    public int findMin(int[] nums) {
        //using binary search...
        int left=0;
        int right=nums.length-1;
        while(left<right){
            int mid=left+(right-left)/2; //calculate mid values
            if (nums[mid]>nums[right]){ //if mid is greater then move to right 
                left=mid+1;
            }
            else{
                right=mid; 
            }
        }
        return nums[left];
    }
}

```

# 2210. Count Hills and Valleys in an Array

## You are given a 0-indexed integer array nums. An index i is part of a hill in nums if the closest non-equal neighbors of i are smaller than nums[i]. Similarly, an index i is part of a valley in nums if the closest non-equal neighbors of i are larger than nums[i]. Adjacent indices i and j are part of the same hill or valley if nums[i] == nums[j].Note that for an index to be part of a hill or valley, it must have a non-equal neighbor on both the left and right of the index.Return the number of hills and valleys in nums.
```
time=O(n)
space=O(1)

class Solution {
    public int countHillValley(int[] nums) {
        int count=0;
        for(int i=1;i<nums.length-1;i++){
            if (nums[i] == nums[i - 1]) continue;

            int prev=i-1;
            int next=i+1;
            //skip duplicates in left
            while(prev>=0 && nums[prev]==nums[i]){
                prev--;
            }
            //skip duplicates in right
            while(next<nums.length&& nums[next]==nums[i]){
                next++;
            }//count hill and valley....
            if (prev>=0 && next<nums.length){
                if ((nums[prev] <  nums[i] && nums[i] > nums[next]) || (nums[prev]>nums[i] && nums[i]<nums[next])){
                    count++;
                }
            }
        }
        return count;
    }
}

```













