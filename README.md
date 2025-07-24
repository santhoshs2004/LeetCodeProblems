# LeetCodeProblems 
# ALGOMAP-DATA STRUCTURES-JAVA

# Bit Manipulation

## 504. Base 7 
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

## 


































