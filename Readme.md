# README - DSA, OOP, and DBMS Problems(27/01/2025)

## 1. DSA Question: **7. Reverse Integer**

**Platform:** LeetCode

### Problem Statement
Given a signed 32-bit integer x, return x with its digits reversed. If reversing x causes the value to go outside the signed 32-bit integer range [-231, 231 - 1], then return 0.
Assume the environment does not allow you to store 64-bit integers (signed or unsigned).

### Examples
#### Example 1:

Input: x = 123
Output: 321

#### Example 2:

Input: x = -123
Output: -321

#### Example 3:

Input: x = 120
Output: 21
 
### Constraints:
- `-231 <= x <= 231 - 1`
  
### Solution Code
#### C++ Implementation:
```cpp
class Solution {
public:
    int reverse(int x) {
        if(x>INT_MAX || x<INT_MIN || x==0) return 0;
       long long int num=x;
       if(x<0){
           num = abs(x);
       }
       int digits=log10(num);
       long long int rev=0;
       int factor=digits;
       while(num>0){
           int rem=num%10;
           rev = rev +( rem*pow(10,factor) );
           factor--;
           num=num/10;
        }
        if(rev>INT_MAX || rev<INT_MIN ) return 0;
        int ans=rev;
        if(x<0){
            ans= -rev;
        }
        return ans;
    }
};
```

### Explanation
- Reversing the Number: The program repeatedly extracts the last digit of the integer x using x % 10 and appends it to the reversed number rev. This is done by multiplying the current reversed number by 10 and adding the extracted digit.
- Overflow Check: After updating the reversed number rev, the program checks if it exceeds the integer boundaries (INT_MAX or INT_MIN). If it does, it returns 0 to indicate overflow.
- Handling the Input Sign: The code handles both positive and negative numbers correctly without explicitly checking for the sign beforehand. It works with the digits directly and handles overflow conditions for both positive and negative reversed values.
- Dividing the Input: The number x is divided by 10 in each iteration (x /= 10), effectively removing the last digit until the entire number is processed.
- Return the Result: Finally, the reversed number rev is cast to an int and returned. If an overflow was detected during the reversal, 0 is returned.
---

## 2. DSA Question: **28. Find the Index of the First Occurrence in a String**

**Platform:** LeetCode

### Problem Statement
Given two strings needle and haystack, return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

### Examples
Example 1:

Input: haystack = "sadbutsad", needle = "sad"
Output: 0
Explanation: "sad" occurs at index 0 and 6.
The first occurrence is at index 0, so we return 0.

Example 2:

Input: haystack = "leetcode", needle = "leeto"
Output: -1
Explanation: "leeto" did not occur in "leetcode", so we return -1.

### Constraints:
- 1 <= haystack.length, needle.length <= 104
- haystack and needle consist of only lowercase English characters.

### Solution Code
#### C++ Implementation:
```cpp
class Solution {
public:
int search(char c,string str,int x){
    for(int i=x;i<str.length();i++){
        if(str[i]==c){
            return i;
        }
    }
    return -1;
}
bool isPossible(string x,string y,int index){
    int j=0;
    for(int i=index;i<index+y.length();i++){
        if(x[i]!=y[j]){
            return 0;
        }
        else{
            j++;
        }
    }
    return 1;
}
    int strStr(string haystack, string needle) {
        if(haystack.length()<needle.length()){
            return -1;
        }
        int first=needle[0];
        int j=0;
        int index=search(first,haystack,0);
        while(index<haystack.length()){

            if(index==-1){
                return index;
            }
            else if(isPossible(haystack,needle,index)){
                return index;
            }
            else{
                index=search(first,haystack,index+1);
            }
        }
        return index;
    }
};
```

### Explanation
- search() Function: Finds the first occurrence of a character c in haystack starting from a given index x. Returns the index or -1 if not found.
- isPossible() Function: Compares the substring of haystack starting from a given index with needle to check if they match completely.
- Main strStr() Function: Finds the first occurrence of needle in haystack by using search() to find the first character and isPossible() to verify the match.
- Iterative Search: It iteratively searches for needle by checking each possible starting position in haystack until a match is found or the string is exhausted.
- Edge Cases: Handles cases where haystack is shorter than needle or when no match is found by returning -1. If needle is empty, it returns 0.
---

## 3. DSA Question: **41. First Missing Positive**

**Platform:** LeetCode

### Problem Statement
Given an unsorted integer array nums. Return the smallest positive integer that is not present in nums.
You must implement an algorithm that runs in O(n) time and uses O(1) auxiliary space.

### Examples
Example 1:

Input: nums = [1,2,0]
Output: 3
Explanation: The numbers in the range [1,2] are all in the array.

Example 2:

Input: nums = [3,4,-1,1]
Output: 2
Explanation: 1 is in the array but 2 is missing.

Example 3:

Input: nums = [7,8,9,11,12]
Output: 1
Explanation: The smallest positive integer 1 is missing.

### Constraints:
- `1 <= nums.length <= 105`
- `231 <= nums[i] <= 231 - 1`

### Solution Code
#### C++ Implementation:
```cpp
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        set<int>s;

        for(int i=0;i<nums.size();i++){
            s.insert(nums[i]);
        }
        
        int ans;
        
        for(int i=1;i<=s.size()+1;i++){
            if(s.count(i)==0){
                ans=i;
                break;
            }
        }
        return ans;
    }
};
```

### Explanation

- Function Purpose: The function firstMissingPositive() finds the smallest missing positive integer in the given vector nums.
- Using a Set: It creates a set s to store unique elements from the nums array.
- Populating the Set: It iterates through the nums vector, inserting each number into the set.
- Checking Missing Positive: It iterates from 1 up to s.size() + 1, checking if each integer is present in the set. The first integer not found is the missing positive.
- Return Value: It returns the first missing positive integer once found; otherwise, it returns the smallest integer greater than all existing elements in the set.
---

## DBMS Question: **1148. Article Views**

**Platform:** LeetCode

### Problem Statement
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| article_id    | int     |
| author_id     | int     |
| viewer_id     | int     |
| view_date     | date    |
+---------------+---------+
There is no primary key (column with unique values) for this table, the table may have duplicate rows.
Each row of this table indicates that some viewer viewed an article (written by some author) on some date. 
Note that equal author_id and viewer_id indicate the same person.
 

Write a solution to find all the authors that viewed at least one of their own articles.

Return the result table sorted by id in ascending order.

### Example
#### Input:
```
Views table:
+------------+-----------+-----------+------------+
| article_id | author_id | viewer_id | view_date  |
+------------+-----------+-----------+------------+
| 1          | 3         | 5         | 2019-08-01 |
| 1          | 3         | 6         | 2019-08-02 |
| 2          | 7         | 7         | 2019-08-01 |
| 2          | 7         | 6         | 2019-08-02 |
| 4          | 7         | 1         | 2019-07-22 |
| 3          | 4         | 4         | 2019-07-21 |
| 3          | 4         | 4         | 2019-07-21 |
+------------+-----------+-----------+------------+
```

#### Output:
```
+------+
| id   |
+------+
| 4    |
| 7    |
+------+
```

### Solution Code
```sql
SELECT DISTINCT author_id AS id
FROM Views
WHERE author_id=viewer_id
ORDER BY id;
```

### Explanation
- This query selects unique `id` from views table.
- It filters countries based on the given conditions using the `WHERE` clause and then orders it accordingly.
---


## OOPS Question: Implement Circle

**Platform:** w3resource

### Problem Statement
Write a C++ program to create a class called Rectangle that has private member variables for length and width. Implement member functions to calculate the rectangle's area and perimeter.

### Solution Code
```cpp
#include <iostream> 
class Rectangle { 
  private: 
    double length; 
    double width; 

  public:
    Rectangle(double len, double wid): length(len), width(wid) {}

    double calculateArea() {
      return length * width; 
    }
    double calculatePerimeter() {
      return 2 * (length + width); 
    }
};

int main() {
  double length, width;
  std::cout << "Input the length of the rectangle: ";
  std::cin >> length;
  std::cout << "Input the width of the rectangle: ";
  std::cin >> width;
  Rectangle rectangle(length, width);
  double area = rectangle.calculateArea(); 
  std::cout << "\nArea: " << area << std::endl; 
  double perimeter = rectangle.calculatePerimeter(); 
  std::cout << "Perimeter: " << perimeter << std::endl; 

  return 0; 
}
```

### Explanation
- Class Definition (Rectangle): The program defines a class Rectangle with two private attributes, length and width, to store the dimensions of the rectangle.
- Constructor Initialization: The constructor Rectangle(double len, double wid) initializes the length and width variables when an object of the class is created.
- calculateArea(): Computes the area of the rectangle using the formula length × width.
- calculatePerimeter(): Computes the perimeter using the formula 2 × (length + width).
- User Input and Object Creation: The main function prompts the user to input length and width, then creates a Rectangle object using these values.
- Displaying Results: The program calculates and displays the area and perimeter of the rectangle using the corresponding member functions and prints them to the console.
---

