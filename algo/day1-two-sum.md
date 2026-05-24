# 01. 两数之和 (Two Sum)

**来源**：LeetCode 热题 100  
**难度**：简单  
**标签**：`数组` `哈希表`  
**完成时间**：2026-05-24  

---

## 📝 题目描述

给定一个整数数组 `nums` 和一个整数目标值 `target`，请你在该数组中找出和为目标值的那两个整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案，且同样的元素不能被重复利用。

**示例**：
输入：nums = [2,7,11,15], target = 9
输出：[0,1]
解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。

---

## 💡 解题思路

### 方法一：暴力枚举
- 双重循环遍历所有数对，检查是否和等于 target。
- 时间复杂度 O(n²)，空间复杂度 O(1)。

### 方法二：哈希表（一次遍历）
- 使用哈希表存储已经遍历过的数和它的索引。
- 对于当前数 `nums[i]`，计算 `complement = target - nums[i]`。
- 如果 `complement` 已经在哈希表中，直接返回 `[hash[complement], i]`。
- 否则，把 `(nums[i], i)` 存入哈希表。
- 时间复杂度 O(n)，空间复杂度 O(n)。

---

## 🧪 代码实现

### C++ 版本
\`\`\`cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> hash;
        for (int i = 0; i < nums.size(); ++i) {
            int complement = target - nums[i];
            if (hash.count(complement)) {
                return {hash[complement], i};
            }
            hash[nums[i]] = i;
        }
        return {};
    }
};
\`\`\`

### Python 版本
\`\`\`python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hash = {}
        for i, num in enumerate(nums):
            complement = target - num
            if complement in hash:
                return [hash[complement], i]
            hash[num] = i
        return []
\`\`\`

---

## ⚠️ 易错点 & 反思
- 一开始想用双指针，但发现排序后会丢失原始索引，行不通。
- 哈希表查找是 O(1)，用 `unordered_map` 比 `map` 更快。
- 这题的关键在于：**用空间换时间**，把已经访问过的元素存下来，让后续的查找变成 O(1)。