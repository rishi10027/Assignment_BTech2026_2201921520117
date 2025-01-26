# README - DSA, OOP, and DBMS Problems(26/01/2025)

## 1. DSA Question: **739. Daily Temperatures**

**Platform:** LeetCode

### Problem Statement
Given an array of integers `temperatures` representing the daily temperatures, return an array `answer` such that `answer[i]` is the number of days you have to wait after the `ith` day to get a warmer temperature. If there is no future day for which this is possible, keep `answer[i] == 0` instead.

### Examples
#### Example 1:
**Input:**
```cpp
temperatures = [73,74,75,71,69,72,76,73]
```
**Output:**
```cpp
[1,1,4,2,1,1,0,0]
```

#### Example 2:
**Input:**
```cpp
temperatures = [30,40,50,60]
```
**Output:**
```cpp
[1,1,1,0]
```

#### Example 3:
**Input:**
```cpp
temperatures = [30,60,90]
```
**Output:**
```cpp
[1,1,0]
```

### Constraints:
- `1 <= temperatures.length <= 10^5`
- `30 <= temperatures[i] <= 100`

### Solution Code
#### C++ Implementation:
```cpp
class Solution {
public:
    vector<int> findnge(vector<int> t) {
        vector<int> ans(t.size());
        stack<int> st;
        for(int i = t.size() - 1; i >= 0; i--) {
            while(!st.empty() && t[st.top()] <= t[i]) st.pop();
            ans[i] = st.empty() ? t.size() : st.top();
            st.push(i);
        }
        return ans;
    }
    
    vector<int> dailyTemperatures(vector<int>& t) {
        vector<int> nge = findnge(t);
        for(int i = 0; i < t.size(); i++) {
            if(nge[i] == t.size()) t[i] = 0;
            else t[i] = nge[i] - i;
        }
        return t;
    }
};
```

### Explanation
- The problem is solved using **Monotonic Stack**.
- The `findnge` function finds the **next greater element** for each temperature.
- We traverse the array in reverse and use a **stack** to keep track of indices of temperatures.
- If the stack is not empty and the current temperature is **greater than or equal to** the top of the stack, we pop elements until we find a greater one.
- If no greater temperature is found, we store the array size; otherwise, we store the index of the next greater element.
- Finally, we calculate the waiting days by subtracting indices.

---

## 2. DSA Question: **2. Add Two Numbers**

**Platform:** LeetCode

### Problem Statement
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

### Examples
#### Example 1:
**Input:**
```cpp
l1 = [2,4,3], l2 = [5,6,4]
```
**Output:**
```cpp
[7,0,8]
```
**Explanation:** 342 + 465 = 807.

#### Example 2:
**Input:**
```cpp
l1 = [0], l2 = [0]
```
**Output:**
```cpp
[0]
```

#### Example 3:
**Input:**
```cpp
l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
```
**Output:**
```cpp
[8,9,9,9,0,0,0,1]
```

### Constraints:
- The number of nodes in each linked list is in the range `[1, 100]`.
- `0 <= Node.val <= 9`
- It is guaranteed that the list represents a number that does not have leading zeros.

### Solution Code
#### C++ Implementation:
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        int carry = 0;
        ListNode* dummy = new ListNode(-1); 
        ListNode* current = dummy;

        while (l1 || l2 || carry) {
            int sum = carry;

            if (l1) {
                sum += l1->val;
                l1 = l1->next;
            }
            if (l2) {
                sum += l2->val;
                l2 = l2->next;
            }

            carry = sum / 10; 
            current->next = new ListNode(sum % 10); 
            current = current->next;
        }

        ListNode* result = dummy->next;
        delete dummy; 
        return result;
    }
};
```

### Explanation
- This problem is solved using a **dummy head linked list**.
- We initialize a `carry` variable to handle summation overflow.
- We iterate through both linked lists, adding corresponding nodes.
- If a list is shorter, we continue adding nodes from the longer list.
- If there's a remaining carry after iteration, it's added as a new node.
- The resulting linked list represents the sum in reverse order.

---
## 3. DSA Question: **283. Move Zeroes**

**Platform:** LeetCode

### Problem Statement
Given an integer array `nums`, the goal is to move all `0`s to the end of the array while maintaining the relative order of the non-zero elements. The solution must be done in-place, meaning you cannot create a copy of the array.

### Examples
#### Example 1:
**Input:**
```cpp
nums = [0,1,0,3,12]
```
**Output:**
```cpp
[1,3,12,0,0]
```

#### Example 2:
**Input:**
```cpp
nums = [0]
```
**Output:**
```cpp
[0]
```

### Constraints:
- `1 <= nums.length <= 10^4`
- `2^31 <= nums[i] <= 2^31 - 1`

### Solution Code
#### C++ Implementation:
```cpp
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int index=0;
        for(int i=0;i<nums.size();i++){
            if(nums[i]!=0){
                nums[index]=nums[i];
                index++;
            }
        }
        for(int j=index;j<nums.size();j++){
            nums[j]=0;
        }
    }
};
```

### Explanation

The solution follows a two-step approach:
1. **Move non-zero elements to the front**: We traverse the list, and whenever we find a non-zero element, we place it at the `index` position and increment `index`.
2. **Fill the remaining positions with zeros**: After placing all non-zero elements, the remaining positions from `index` to the end of the list are filled with zeros.

- **First loop**: Iterates through the array to place all non-zero elements at the beginning of the array. The variable `index` tracks the position for the next non-zero element.
- **Second loop**: After the first loop, all elements from `index` to the end of the array are set to zero.

---

## DBMS Question: **595. Big Countries**

**Platform:** LeetCode

### Problem Statement
A country is considered big if:
- It has an area of at least **three million** (i.e., 3,000,000 km²), or
- It has a population of at least **twenty-five million** (i.e., 25,000,000).

Write a SQL query to find the **name, population, and area** of the big countries.

### Example
#### Input:
```
+-------------+-----------+---------+------------+--------------+
| name        | continent | area    | population | gdp          |
+-------------+-----------+---------+------------+--------------+
| Afghanistan | Asia      | 652230  | 25500100   | 20343000000  |
| Albania     | Europe    | 28748   | 2831741    | 12960000000  |
| Algeria     | Africa    | 2381741 | 37100000   | 188681000000 |
+-------------+-----------+---------+------------+--------------+
```

#### Output:
```
+-------------+------------+---------+
| name        | population | area    |
+-------------+------------+---------+
| Afghanistan | 25500100   | 652230  |
| Algeria     | 37100000   | 2381741 |
+-------------+------------+---------+
```

### Solution Code
```sql
SELECT name, population, area
FROM World
WHERE area >= 3000000 OR population >= 25000000;
```

### Explanation
- This query selects the `name`, `population`, and `area` columns.
- It filters countries based on the given conditions using the `WHERE` clause.

---


## OOPS Question: Implement Circle

**Platform:** w3resource

### Problem Statement
Write a C++ program to implement a class called Circle that has private member variables for radius. Include member functions to calculate the circle's area and circumference.### Example

### Solution Code
```cpp
#include <iostream> 
#include <cmath> 
#define PI = 3.14159; 
using namespace std;

class Circle { 
  private: 
    double radius; 
  public:
    Circle(double rad): radius(rad) {}
    double Area() {
      return PI*pow(radius,2);
    }
    double Circumference() {
      return 2*PI*radius; 
    }
};

int main() {
  double radius;
  cin>>radius;
  Circle circle(radius);
  cout<<circle.Area()<<" "<<circle.Circumference()<<endl;
  return 0; 
}
```

### Explanation
- A Circle class is created with a private member variable radius to store the radius of the circle.
- The constructor Circle(double rad) initializes the circle's radius using the value provided when an object is created.
- The Area() method calculates the area of the circle using the formula π*r^2, where r is the radius, and the value of π is predefined.
- The Circumference() method calculates the circumference using the formula 2×π×r.
- In the main() function, the user inputs the radius, a Circle object is created with that radius, and the program then prints the circle's area and circumference.
---



