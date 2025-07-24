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





























