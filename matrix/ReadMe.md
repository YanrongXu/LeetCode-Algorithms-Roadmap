# 📦 Matrix 专题封档总结

> 覆盖范围：  
> - **路径/遍历型**：54 / 59（螺旋）  
> - **状态/标记型**：73（矩阵置零）  
> - **结构变换型**：867（转置）、832（翻转+取反）、48（旋转）、1861（旋转+重力）  
>
> 核心目标：形成“看题秒换模型”的能力，而不是记代码。

---

## 0. 一眼分流：矩阵题 3 大模型

### A) 路径 / 遍历（你在“走路”）
关键词：顺时针 / 一圈一圈 / 打印路径 / traversal  
代表题：**54、59、498**  
核心工具：**边界 top/bottom/left/right + while +（必要时）if**

### B) 状态 / 标记（你在“记状态”）
关键词：置零 / 标记 / 先扫描再处理 / 常量空间  
代表题：**73**  
核心工具：**第一行/第一列做标记 + 延迟修改**

### C) 结构 / 变换（你在“改结构”）
关键词：transpose / rotate / flip / invert / in-place  
代表题：**867、832、48、1861**  
核心工具：**坐标映射 / 对称交换 / 分解动作（A→B→C）**

---

## 1. 路径模型封档：螺旋矩阵（54 / 59）

### 1.1 四条边界不变量
- `top`：可用最上行
- `bottom`：可用最下行
- `left`：可用最左列
- `right`：可用最右列

### 1.2 一圈 4 步（顺时针）
1) 上边：left → right  
2) 右边：top → bottom  
3) 下边：right → left（可能不存在）  
4) 左边：bottom → top（可能不存在）

### 1.3 while vs if 的职责（必须背）
- `while top <= bottom and left <= right`：**一圈能不能开始**（保证 1、2 存在）
- `if top <= bottom` / `if left <= right`：**这一圈里还剩不剩边**（保护 3、4）

口诀：**while 管一圈能否开始，if 管这一圈还剩不剩边。**

---

## 2. 状态模型封档：矩阵置零（73 的通用要点）

### 2.1 核心思想
不能边扫边改，否则会把“新增的 0”当成原始 0 扩散。  
所以：**先记录状态，再统一修改**。

### 2.2 常量空间经典做法
- 用 **第一行、第一列**做标记位  
- 额外用两个 flag 记录：第一行是否需要置零、第一列是否需要置零  
- 第二趟根据标记清零

---

## 3. 结构变换封档：3 个积木（所有变换题都能拼出来）

### 3.1 转置 Transpose（对角线镜像，不是旋转）
- 映射：`(i, j) -> (j, i)`
- **in-place 转置**不变量：每对 `(i,j)` 与 `(j,i)` **只交换一次**
  - 遍历上三角 `j > i` ✅  
  - 遍历下三角 `j < i` ✅  
  - 全遍历 ❌（交换两次抵消）

### 3.2 行反转（左右翻）
- 映射：`(i, j) -> (i, n-1-j)`
- Python：`row.reverse()`

### 3.3 上下翻转（行顺序反转）
- 映射：`(i, j) -> (n-1-i, j)`
- Python：`matrix.reverse()`

---

## 4. 旋转角度组合表（48 的母公式）

> 仅适用于 **n×n 且 in-place** 的旋转（LC48）。

| 目标 | 等价操作（最稳） |
|---|---|
| 顺时针 90° | **转置 + 行反转** |
| 逆时针 90° | **转置 + 上下翻转** |
| 180° | **上下翻转 + 行反转** |
| 顺时针 270° | = 逆时针 90° |

### 4.1 为什么 48 必须正方形？
限制点不是“能不能旋转”，而是 **in-place**：  
m×n 旋转 90° 会变 n×m，维度变了就无法原地完成。

---

## 5. 题目级封档（你已掌握的关键迁移点）

### 5.1 867 Transpose Matrix（非方阵：必须新建）
- m×n -> n×m，维度变化 => 结果矩阵新建  
- 赋值核心：`res[j][i] = matrix[i][j]`

### 5.2 832 Flipping an Image（两步法稳定 AC）
- 每行 `reverse`
- 二值取反：`x ^= 1`
- 你已 AC，进阶可做双指针一步法（可选）

### 5.3 48 Rotate Image（母题）
- 顺时针 90° = transpose + reverse each row
- 关键坑位：转置只交换一次（`j = i+1...`）

### 5.4 1861 Rotating the Box（分水岭：变换 + 物理模拟）
- 模型：**旋转 + 重力**
- 重力不变量（必须背）：
  1) `*` 永远不动，并切段  
  2) 每段内 `#` 全部压到段底部  
  3) **搬运**石头：新位置写 `#` + 旧位置清 `.`（否则等于复制）

---

## 6. 高频坑位清单（你踩过 & 已纠正）

1) ❌ 把转置当旋转（转置是镜像，不是 90/270）  
2) ❌ 转置全遍历导致交换两次抵消  
3) ❌ 混淆两种 reverse：`row.reverse()`（左右） vs `matrix.reverse()`（上下）  
4) ❌ 旋转/重力操作顺序混乱（先确定方向再写）  
5) ❌ 重力不清空原位置 => 复制石头（1861 关键）

---

## 7. 面试“秒判断”口诀合集

- **螺旋/路径题**：`top/bottom/left/right` + while（必要时 if）  
- **置零/标记题**：先标记，后清零；第一行/列做标记位  
- **旋转 in-place**：先问“是不是 n×n”；90° 用“转置 + 反转哪一维”  
- **重力 + 障碍**：分段（`*`）+ write 指针 + 搬运要清空旧位置

---

## 8. 刷题清单（矩阵专题 5–10 题）

### 路径/遍历
- 59 ⭐（模板源头）
- 54 ⭐（模板验证）
- 498

### 状态/标记
- 73 ⭐（标记分水岭）

### 结构变换
- 867（转置基础）
- 832（翻转+取反）
- 48 ⭐（旋转母题）
- 1861 ⭐⭐（进阶分水岭）

---

## 9. “毕业标准”（你现在到哪了？）

### ✅ 已毕业（可进入下一专题）
- 能不看题解写出 59 / 54（含 while vs if）  
- 能解释 48 为什么必须 n×n，且能口算 90/180/270  
- 能解释 1861 为何必须“搬运要清空旧位置”，并稳定通过样例

### 🔁 建议回刷触发条件
- 写螺旋时开始堆 if（边界模型不稳）  
- 旋转题开始背坐标不敢用组合表  
- 重力题出现“石头变多/穿过障碍”现象

---

✅ Matrix 专题封档完成

---

## 10. 通用模板库（面试可直接复用）

> 说明：模板追求 **稳定 + 清晰 + 不容易写错**。  
> 你可以把这一节单独复制到自己的 `templates.md` 里。

### 10.1 螺旋矩阵（读取，LC54）模板（带 if 保护）
```python
def spiralOrder(matrix):
    if not matrix or not matrix[0]:
        return []
    top, bottom = 0, len(matrix) - 1
    left, right = 0, len(matrix[0]) - 1
    ans = []

    while top <= bottom and left <= right:
        # 1) 上边：left -> right
        for j in range(left, right + 1):
            ans.append(matrix[top][j])
        top += 1

        # 2) 右边：top -> bottom
        for i in range(top, bottom + 1):
            ans.append(matrix[i][right])
        right -= 1

        # 3) 下边：right -> left（可能不存在）
        if top <= bottom:
            for j in range(right, left - 1, -1):
                ans.append(matrix[bottom][j])
            bottom -= 1

        # 4) 左边：bottom -> top（可能不存在）
        if left <= right:
            for i in range(bottom, top - 1, -1):
                ans.append(matrix[i][left])
            left += 1

    return ans
```

### 10.2 螺旋矩阵（生成，LC59）模板（四边界 + 步进）
```python
def generateMatrix(n):
    res = [[0] * n for _ in range(n)]
    top, bottom, left, right = 0, n - 1, 0, n - 1
    num = 1

    while top <= bottom and left <= right:
        for j in range(left, right + 1):
            res[top][j] = num
            num += 1
        top += 1

        for i in range(top, bottom + 1):
            res[i][right] = num
            num += 1
        right -= 1

        if top <= bottom:
            for j in range(right, left - 1, -1):
                res[bottom][j] = num
                num += 1
            bottom -= 1

        if left <= right:
            for i in range(bottom, top - 1, -1):
                res[i][left] = num
                num += 1
            left += 1

    return res
```

### 10.3 矩阵置零（LC73）模板（O(1) 额外空间）
```python
def setZeroes(matrix):
    if not matrix or not matrix[0]:
        return
    m, n = len(matrix), len(matrix[0])

    first_row_zero = any(matrix[0][j] == 0 for j in range(n))
    first_col_zero = any(matrix[i][0] == 0 for i in range(m))

    # 标记
    for i in range(1, m):
        for j in range(1, n):
            if matrix[i][j] == 0:
                matrix[i][0] = 0
                matrix[0][j] = 0

    # 根据标记清零（除第一行/列）
    for i in range(1, m):
        if matrix[i][0] == 0:
            for j in range(1, n):
                matrix[i][j] = 0

    for j in range(1, n):
        if matrix[0][j] == 0:
            for i in range(1, m):
                matrix[i][j] = 0

    # 处理第一行/列
    if first_row_zero:
        for j in range(n):
            matrix[0][j] = 0
    if first_col_zero:
        for i in range(m):
            matrix[i][0] = 0
```

### 10.4 转置（LC867，非方阵）
```python
def transpose(matrix):
    m, n = len(matrix), len(matrix[0])
    res = [[0] * m for _ in range(n)]
    for i in range(m):
        for j in range(n):
            res[j][i] = matrix[i][j]
    return res
```

### 10.5 翻转 + 取反（LC832，两步法）
```python
def flipAndInvertImage(image):
    for row in image:
        row.reverse()
    for i in range(len(image)):
        for j in range(len(image[0])):
            image[i][j] ^= 1
    return image
```

### 10.6 旋转图像（LC48，顺时针 90°，in-place）
```python
def rotate(matrix):
    n = len(matrix)

    # transpose
    for i in range(n):
        for j in range(i + 1, n):
            matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]

    # reverse each row
    for row in matrix:
        row.reverse()
```

### 10.7 旋转图像（逆时针 90° / 顺时针 270°，in-place）
```python
def rotate_ccw_90(matrix):
    n = len(matrix)

    # transpose
    for i in range(n):
        for j in range(i + 1, n):
            matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]

    # reverse row order (up-down flip)
    matrix.reverse()
```

### 10.8 Rotating the Box（LC1861：rotate 后重力，O(mn) 稳定版）
```python
def rotateTheBox(boxGrid):
    if not boxGrid or not boxGrid[0]:
        return boxGrid

    m, n = len(boxGrid), len(boxGrid[0])

    # 1) rotate: transpose + reverse each row => n x m
    res = [['.'] * m for _ in range(n)]
    for i in range(m):
        for j in range(n):
            res[j][i] = boxGrid[i][j]
    for row in res:
        row.reverse()

    # 2) gravity on rotated matrix (downwards)
    rows, cols = len(res), len(res[0])
    for c in range(cols):
        write = rows - 1
        for r in range(rows - 1, -1, -1):
            if res[r][c] == '*':
                write = r - 1
            elif res[r][c] == '#':
                res[r][c] = '.'  # 关键：搬运要清空旧位置
                while write >= 0 and res[write][c] == '*':  # 关键：write 不能落在障碍上
                    write -= 1
                res[write][c] = '#'
                write -= 1
            # '.' -> ignore
    return res
```

