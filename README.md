# 📘 LeetCode 刷题记录目录（Algorithms Roadmap）
> 目标：系统性刷题 + 可复盘 + 可面试回顾  
> 语言：Python  
> 记录方式：每题包含【思路 / 关键点 / 代码】

---

## 🧭 总体进度

- [x] Binary Search（二分查找）✅ 已封档

---

## 1️⃣ Binary Search（二分查找）✅

📄 总结文档：[`Binary_Search_Summary.md`](./BinarySearch/README.md)

> 关键词：单调性 / check(mid) / 二分数组 / 二分答案  
> 状态：**已完成，可复用**

### ✅ 已完成题目

| LeetCode | Title | 备注 |
|--------|------|------|
| 704 | Binary Search | 基础模板 |
| 374 | Guess Number Higher or Lower | 二分答案 |
| 35 | Search Insert Position | return left |
| 34 | Find First and Last Position | 左右边界 |
| 875 | Koko Eating Bananas | 二分答案 + 建模 |
| 1011 | Capacity To Ship Packages | 二分答案 + 贪心 |

### ⚠️ 可选补充（验证题）

| LeetCode | Title | 状态 |
|--------|------|------|
| 69 | Sqrt(x) | ⏳ |
| 278 | First Bad Version | ⏳ |
| 367 | Valid Perfect Square | ⏳ |

---

## 2️⃣ Two Pointers（数组双指针）✅

📄 总结文档：[`TwoPointers-Array.md`](./TwoPointer/README.md)

关键词：快慢指针 / 结果数组不变量 / k 次去重 / 左右夹逼  
状态：已完成，可复用

### ✅ 已完成题目

| LeetCode | Title | 备注 |
|--------|------|------|
| 27 | Remove Element | 过滤型双指针（构建结果前缀） |
| 26 | Remove Duplicates from Sorted Array | 去重模板（k = 1） |
| 80 | Remove Duplicates from Sorted Array II | k 次去重（k = 2，不变量升级） |
| 283 | Move Zeroes | 过滤变体（非 0 前移） |
| 977 | Squares of a Sorted Array | 左右夹逼双指针（从后填） |

---

## 3️⃣ Sliding Window（滑动窗口）✅

📄 总结文档：[`Sliding_Window_Summary.md`](./SlidingWindow/ReadMe.md)

> 关键词：连续区间 / 双指针不回头 / 合法即缩 / ≤K 约束 / 频次窗口  
> 状态：**已完成（核心模型毕业，可稳定应对面试）**

---

### ✅ 已完成题目（核心必刷）

| LeetCode | Title | 主要训练点 |
|--------|------|-----------|
| 209 | Minimum Size Subarray Sum | 数值型窗口 / 最短 |
| 904 | Fruit Into Baskets | 条件型窗口 / ≤2 种 |
| 1004 | Max Consecutive Ones III | ≤K 个坏元素 |
| 76 | Minimum Window Substring | 频次型窗口 / 天花板 |

> 📌 **76 是滑动窗口分水岭题，必须吃透**

---

### ⚠️ 可选补充（巩固 & 变体）

| LeetCode | Title | 训练重点 | 状态 |
|--------|------|--------|------|
| 643 | Maximum Average Subarray I | 固定长度窗口 | ⏳ |
| 438 | Find All Anagrams in a String | 频次窗口（多解） | ⏳ |
| 567 | Permutation in String | 频次窗口（判存在） | ⏳ |
| 239 | Sliding Window Maximum | 单调队列（进阶） | ⏳ |

---

### 🧠 模型总结（一眼判断）

- **连续子数组 / 子串**
- **有明确窗口合法条件**
- **目标是最值（最长 / 最短）**

👉 满足以上三点，**优先考虑滑动窗口**

---
