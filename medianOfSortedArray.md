

public class Solution {

    public double findMedianSortedArrays(int\[\] nums1, int\[\] nums2) {

        if (nums1.length \> nums2.length) {

            // Ensure nums1 is smaller

            return findMedianSortedArrays(nums2, nums1);

        }

        int m \= nums1.length;

        int n \= nums2.length;

        int left \= 0, right \= m;

        while (left \<= right) {

            int i \= (left \+ right) / 2;

            int j \= (m \+ n \+ 1\) / 2 \- i;

            int nums1LeftMax \= (i \== 0\) ? Integer.MIN\_VALUE : nums1\[i \- 1\];

            int nums1RightMin \= (i \== m) ? Integer.MAX\_VALUE : nums1\[i\];

            int nums2LeftMax \= (j \== 0\) ? Integer.MIN\_VALUE : nums2\[j \- 1\];

            int nums2RightMin \= (j \== n) ? Integer.MAX\_VALUE : nums2\[j\];

            if (nums1LeftMax \<= nums2RightMin && nums2LeftMax \<= nums1RightMin) {

                if ((m \+ n) % 2 \== 0\) {

                    return ((double)Math.max(nums1LeftMax, nums2LeftMax) \+

                            Math.min(nums1RightMin, nums2RightMin)) / 2;

                } else {

                    return (double)Math.max(nums1LeftMax, nums2LeftMax);

                }

            } else if (nums1LeftMax \> nums2RightMin) {

                right \= i \- 1;

            } else {

                left \= i \+ 1;

            }

        }

        throw new IllegalArgumentException();

    }

}

✅ **Let’s break down this median-finding program into easy steps with visuals to help you understand\!**

---

## **🌟 What is this program solving?**

👉 You have two sorted arrays `nums1` and `nums2`.  
 👉 You want to find the median of their combined elements **without merging them**, in **O(log(min(m, n))) time**.

---

## **🚀 High-level steps**

1️⃣ Make sure `nums1` is the smaller array (to make binary search efficient).  
 2️⃣ Use binary search on `nums1` to find a partition.  
 3️⃣ Partition both arrays so that:

sql  
CopyEdit  
`left side of nums1 + nums2 <= right side of nums1 + nums2`

4️⃣ When the correct partition is found:

* If total is even → average of middle two values.

* If total is odd → max of left side.

---

## **📝 Step-by-step logic**

---

### **1️⃣ Ensure nums1 is smaller**

java  
CopyEdit  
`if (nums1.length > nums2.length) {`  
    `return findMedianSortedArrays(nums2, nums1);`  
`}`

✅ This keeps our binary search efficient.

---

### **2️⃣ Binary search to partition**

We want to split arrays like:

sql  
CopyEdit  
`nums1: [ ... left ] | [ right ... ]`  
`nums2: [ ... left ] | [ right ... ]`

We choose `i` elements for `nums1` left, and `j` for `nums2` left:

nginx  
CopyEdit  
`i + j = (m + n + 1) / 2`

➡ This makes sure left has equal (or 1 more) elements than right.

---

### **3️⃣ Check partition correctness**

We want:

nginx  
CopyEdit  
`nums1LeftMax <= nums2RightMin`  
`nums2LeftMax <= nums1RightMin`

If true → partition is correct → compute median\!

---

### **4️⃣ Adjust binary search**

If not correct:

css  
CopyEdit  
`if nums1LeftMax > nums2RightMin → move i left`  
`else → move i right`

---

## **🌈 Visual example**

Say:

ini  
CopyEdit  
`nums1 = [1, 3]`  
`nums2 = [2, 4, 5, 6]`

Total \= 6  
 Half \= 3

---

🎯 Try `i = 1`, `j = 2`  
 Partitions:

makefile  
CopyEdit  
`nums1: [1] | [3]`  
`nums2: [2, 4] | [5, 6]`

`nums1LeftMax = 1`  
`nums1RightMin = 3`  
`nums2LeftMax = 4`  
`nums2RightMin = 5`

✅ Check:

CopyEdit  
`1 <= 5 ✔️`  
`4 <= 3 ❌`

`nums2LeftMax > nums1RightMin` → move `i` right

---

🎯 Try `i = 2`, `j = 1`

makefile  
CopyEdit  
`nums1: [1, 3] | []`  
`nums2: [2] | [4, 5, 6]`

`nums1LeftMax = 3`  
`nums1RightMin = ∞`  
`nums2LeftMax = 2`  
`nums2RightMin = 4`

✅ Check:

CopyEdit  
`3 <= 4 ✔️`  
`2 <= ∞ ✔️`

➡ Found partition\!

Since total is even:

lua  
CopyEdit  
`median = (max(3, 2) + min(∞, 4)) / 2`  
       `= (3 + 4) / 2`  
       `= 3.5`

---

## **💡 Simple flowchart**

sql  
CopyEdit  
`1️⃣ Pick i`  
`2️⃣ Compute j = (m + n + 1)/2 - i`  
`3️⃣ If nums1[i-1] > nums2[j] → move left`  
`4️⃣ If nums2[j-1] > nums1[i] → move right`  
`5️⃣ Else → compute median!`

---

## **✅ Final median formula**

* Even total:

lua  
CopyEdit  
`(max(nums1LeftMax, nums2LeftMax) + min(nums1RightMin, nums2RightMin)) / 2`

* Odd total:

scss  
CopyEdit  
`max(nums1LeftMax, nums2LeftMax)`

## **Let’s break down the logic behind this key condition in simple terms so it’s crystal clear\!**

## ---

## **🎯 The goal of the partition**

## **We’re trying to split the two arrays like this:**

## **css**

## **CopyEdit**

## **`[ nums1_left  |  nums1_right ]`**

## **`[ nums2_left  |  nums2_right ]`**

## 

## **where all numbers on the left side are ≤ all numbers on the right side.**

## ---

## **📝 What are we checking?**

## **We need:**

## **nginx**

## **CopyEdit**

## **`nums1LeftMax <= nums2RightMin`**

## **`nums2LeftMax <= nums1RightMin`**

## 

## **These ensure that:**

* ## **The largest value on the left is smaller than the smallest value on the right.** 

## ---

## **🔑 So why do we move `i` left or right?**

### **🚩 Case 1: `nums1LeftMax > nums2RightMin`**

## **➡ The biggest number on `nums1` left is too big—it violates the rule that all left numbers ≤ all right numbers.**  **➡ Fix: Take fewer numbers from `nums1` left (so the big number moves to the right)**  **➡ Action: Move `i` left → decrease `i`**

## **ini**

## **CopyEdit**

## **`right = i - 1;`**

## 

## ---

### **🚩 Case 2: `nums2LeftMax > nums1RightMin`**

## **➡ The biggest number on `nums2` left is too big.**  **➡ Fix: Take more numbers from `nums1` left to balance out.**  **➡ Action: Move `i` right → increase `i`**

## **ini**

## **CopyEdit**

## **`left = i + 1;`**

## 

## ---

### **🚩 Otherwise:**

## **If neither condition happens → we have a valid partition\!**

## ---

## **🌈 Visual example**

## **ini**

## **CopyEdit**

## **`nums1 = [1, 3]`**

## **`nums2 = [2, 4, 5, 6]`**

## 

## **Suppose:**

## **ini**

## **CopyEdit**

## **`i = 1`**

## **`j = 2`**

## 

## **Partitions:**

## **makefile**

## **CopyEdit**

## **`nums1_left: [1]`**

## **`nums1_right: [3]`**

## **`nums2_left: [2, 4]`**

## **`nums2_right: [5, 6]`**

## 

## **`nums1LeftMax = 1`**

## **`nums1RightMin = 3`**

## **`nums2LeftMax = 4`**

## **`nums2RightMin = 5`**

## 

## **✅ Check:**

## **sql**

## **CopyEdit**

## **`1 <= 5 ✔️`**

## **`4 <= 3 ❌ (violates condition)`**

## 

## **➡ `nums2LeftMax > nums1RightMin`**  **➡ Need to take more from nums1 left**  **➡ Move `i` right → `i = i + 1`**

## ---

## **💡 Summary logic**

## **sql**

## **CopyEdit**

## **`if nums1LeftMax > nums2RightMin:`**

##     **`move i left (right = i - 1)`**

## **`else:`**

##     **`move i right (left = i + 1)`**

## 

## **👉 Because:**

* ## **If `nums1LeftMax` is too big → too many big elements on left → reduce `i`** 

* ## **Otherwise → not enough big elements on left → increase `i`** 

## 

