# 🧠 Binary Search（二分查找）专项总结

> 状态：**已完成 · 封档**  
> 目标：将二分查找内化为「工具」，而不是记忆题目

---

## 一、二分的本质（核心结论）

**二分不是“找值”，而是：**

> 👉 **在一个单调区间中，寻找 True / False 的分界点**

能否使用二分的唯一判断标准：

- 是否存在一个 **单调的 check(x)**  
- 形态必须是以下之一：

```
False False False True True True
```

或

```
True True True False False False
```

---

## 二、二分的两大类型（必须区分）

### 1️⃣ 二分数组（Binary Search on Index）

**特征**
- 数组有序
- 二分对象：下标 `index`
- 常见题目：704 / 35 / 34

**核心 check**
- 左边界：`nums[mid] >= target`
- 右边界：`nums[mid] > target`

**关键结论**
- 左边界 = 第一个 `>= target` 的位置
- 右边界 = 第一个 `> target` 的位置 − 1

---

### 2️⃣ 二分答案（Binary Search on Value）

**特征**
- 不要求数组有序
- 二分对象：答案空间（速度 / 容量 / 数值）
- 常见题目：875 / 1011

**核心思想**
- `mid` 是一个「候选答案」
- `check(mid)` 判断这个答案是否 **可行**

---

## 三、统一二分模板（Python 推荐）

```python
left, right = ...  # 搜索区间 [left, right)
while left < right:
    mid = (left + right) // 2
    if check(mid):
        right = mid
    else:
        left = mid + 1
return left
```

**模板特性**
- 永远使用 `[left, right)`
- 永远使用 `while left < right`
- 永远返回 `left`
- 不直接返回 `mid`

---

## 四、check(mid) 的本质

> **check(mid) = 判断 mid 这个“候选答案”是否满足题目条件**

常见三类 check：

1. **数组边界类**
   - `nums[mid] >= target`
   - `nums[mid] > target`

2. **限制判断类**
   - 吃香蕉时间 ≤ h
   - 运货天数 ≤ days

3. **数值越界类**
   - `mid * mid > x`

---

## 五、关键易错点（已掌握）

### ✅ 为什么右边界要用 `nums[mid] > target`
- 二分找的是「第一次离开 target」
- 真正右边界在 `left - 1`

### ✅ 为什么右边界是 `left - 1`
- `left` 指向的是第一个 **不等于 target** 的位置
- 必须回退一格

### ✅ 为什么 875 / 1011 不需要排序
- 二分的不是数组
- 二分的是 **答案空间**
- 只要答案空间单调 → 可以二分

### ✅ `(x + k - 1) // k` 的正确理解
- 本质是：`ceil(x / k)`
- 不要求现场推导
- 可先写 `math.ceil`，公式是优化手段

---

## 六、已完成题目清单（核心）

### ✅ 已完成（主干题）
- 704. Binary Search  
- 374. Guess Number Higher or Lower  
- 35. Search Insert Position  
- 34. Find First and Last Position  
- 875. Koko Eating Bananas  
- 1011. Capacity To Ship Packages  

👉 覆盖 **90% 高频二分模型**

### ⚠️ 可选补充（验证题）
- 69. Sqrt(x)
- 278. First Bad Version
- 367. Valid Perfect Square

---

## 七、二分题通用「三问法」

在写代码前，先回答：

```
1️⃣ 我在二分什么？（index / value）
2️⃣ check(mid) 是什么？
3️⃣ True 在哪一边？
```

只要这三问清楚，题目已经解了一半。

---

## 八、阶段性结论（封档）

> **二分查找已从“知识点”升级为“工具”**

当前阶段：✅ 完成，可停

**何时再刷二分？**
- 新题属于「二分答案 + 新建模」
- 或二分只是综合题中的一环

否则无需刻意回头。

---

## 📌 备注
- 本文档可长期复用
- 适用于：刷题前校准思路 / 面试前快速回顾
