# 调账审核系统 - 产品需求说明文档

## 1. 概述

调账审核系统由 Vantage 平台的三个核心模块组成，用于管理不同类型的财务调账操作：

- **Funding 调账审核** (`index.html`) — Funding / Prep / VTS 账户调账
- **Cash Adjustment Audit New** (`mt-adjustment.html`) — MT 交易账户现金调账
- **Credit Adjustment Audit New** (`credit-adjustment.html`) — 交易账户信用调账

所有页面部署地址：`https://delia88888.github.io/0818Adjustment/`

---

## 2. Funding 调账审核 (index.html)

### 2.1 页面结构

- **导航栏**：英文菜单（Users、Client、Account、Reports、Task、Funding、Security、System Setting、Partner）
- **面包屑**：Home / Funding / Adjustment Audit
- **当前用户**：lemon

### 2.2 查询条件

| 字段名 | 控件类型 |
|--------|----------|
| Adjustment Application ID | 文本输入框 |
| Account Adjustment OrderID | 文本输入框 |
| Internal Account OrderID | 文本输入框 |
| UID | 文本输入框 |
| Funding Account ID | 文本输入框 |

### 2.3 Tab 筛选

- All（全部）
- **Unapproved**（未审批，默认选中，红色高亮）
- Approved（已审批）
- Related to Me（与我相关）

### 2.4 操作按钮

| 按钮 | 功能说明 |
|------|----------|
| Approve | 批量审批选中记录 |
| Reject | 批量拒绝选中记录 |
| + Add | 打开新增调账弹窗 |
| Download（下载图标） | 导出数据 |
| Settings（齿轮图标） | 列设置 |

### 2.5 数据列表字段

Adjustment Application ID、Account Adjustment OrderID、Internal Account OrderID、UID、Account Type、Account ID、Adjustment Type、Coin、Amount、Internal Account ID、Campaign ID、Comment、Note、Reject Reason、Applicant、Reviewer、Application Status、UpdateTime (UTC+3)、Action

### 2.6 新增调账弹窗

#### 单条模式（Single）

| 字段 | 是否必填 | 控件类型 | 枚举值/说明 |
|------|----------|----------|-------------|
| UID | 是 | 文本输入框 | - |
| Account Type | 是 | 下拉选择 | Funding / Prep / VTS |
| Account | 是（仅 VTS） | 下拉选择 | 根据 UID 动态加载 |
| Adjustment Type | 是 | 下拉选择 | Adjustment Deposit / Adjustment Withdraw / Adjustment Reward |
| Coin | 是 | 下拉选择 | USD / USDT / ETH / BTC（Prep/VTS 自动填充） |
| Amount | 是 | 文本输入框 | - |
| Internal Account | 是 | 下拉选择 | 多个内部账户选项 |
| Campaign ID | 否 | 下拉选择 | 可选 ID |
| Comment | 是 | 下拉选择 | System Generated |
| Note | 否 | 文本域 | 最多 100 字符 |

**条件联动逻辑**：
- Account Type = Prep：Coin 自动设为 USD（禁用），Account 字段隐藏
- Account Type = VTS：显示 Account 下拉框，选择账户后 Coin 自动设为 USD
- Account Type = Funding：Coin 下拉框可用，Account 字段隐藏

#### 批量模式（Batch）

- 点击 "Select File" 按钮后，打开**批量确认页面**（二次确认）
- 确认页面展示宽表格，显示解析后的 CSV 数据
- 表格列：UID、Account Type、Account ID、Adjustment Type、Coin、Amount、Internal Account、Campaign ID、Comment、Note、Validation Status、Validation Fail Reason
- 底部按钮：Back / Submit

---

## 3. Cash Adjustment Audit New (mt-adjustment.html)

### 3.1 页面结构

- **导航栏**：中文菜单，含下拉子菜单（用户管理、客户管理、账户管理、统计报表、**任务管理**（含完整子菜单列表）、钱包管理、系统设置）
- **面包屑**：主页 / 任务管理 / Cash Adjustment Audit New
- **当前用户**：Delia Zhao

### 3.2 查询条件

| 字段名 | 控件类型 |
|--------|----------|
| License | 文本输入框 |
| User ID | 文本输入框 |
| Adjustment OrderID | 文本输入框 |
| Account | 文本输入框 |
| Account Type | 下拉选择（Trading Account / Rebate Account） |

### 3.3 操作按钮

| 按钮 | 功能说明 |
|------|----------|
| + New Adjustment | 打开单条调账弹窗 |
| Batch CSV | 打开批量 CSV 导入弹窗 |
| Approve | 批量审批 |
| Reject | 批量拒绝 |
| Download | 导出数据 |
| Settings（齿轮图标） | 列设置 |

### 3.4 数据列表字段

Adjustment OrderID、License、User ID、Account、Account Type、Type、Amount、Currency、Status（Completed / Rejected / Pending）、Comment、Application Note、Applicant、Creation Time、Update Time、Reviewer、Reject Reason、System Type

### 3.5 New Adjustment 弹窗（单条新增）

| 字段 | 是否必填 | 控件类型 | 枚举值/说明 |
|------|----------|----------|-------------|
| UID | 是 | 文本输入框 | - |
| Account Type | 是 | 下拉选择 | MT Trading Account / VTS Account |
| Account | 是 | 下拉选择 | 动态加载 |
| Adjustment Type | 是 | 下拉选择 | Deposit / Withdraw |
| Currency | 否 | 自动填充 | 根据账户验证结果填充 |
| Amount | 是 | 文本输入框 | - |
| Comment | 是 | 下拉选择 | Cash Adjustment / Cash Adjustment - Deposit / Cash Adjustment - Withdraw / Cash Adj-AU VPS Reimbursement / Cash Adj-Cost-Rebate UK / Cash Adj-Cost-Rebate_192858 / Cash Adj-Cost-Rebate_58547 / Cash Adj-Cost-Rebate_74381 |
| Application Note | 否 | 文本域 | 最多 300 字符 |

### 3.6 Batch CSV 导入

批量 CSV 弹窗包含两个 Tab 页签：

#### Funding Account（Funding 账户）
- 下载模板：`funding_adjustment_template.csv`
- 上传 CSV 文件
- 点击 Upload 按钮后打开 **Import Preview（导入预览）** 弹窗

#### Non-Funding Account（非 Funding 账户）
- 下载模板：`non_funding_adjustment_template.csv`
- 上传 CSV 文件
- 点击 Upload 按钮后打开 **Import Preview（导入预览）** 弹窗

### 3.7 Import Preview 弹窗（批量上传二次确认）

弹窗宽度：90vw（最大 1400px），确保所有列完整展示。

#### Funding Account 预览表格

| 列名 | 说明 |
|------|------|
| UID | 用户 ID |
| Type | 调账类型 |
| Coin | 币种 |
| Amount | 调账金额 |
| Comment | 备注 |
| Application Note | 申请说明 |
| Fail Reason | 校验通过显示 "-"；校验失败显示红色错误信息，如 "Insufficient cash for Cash Out operation" |
| Action | 校验通过为空；校验失败显示红色 "Remove" 按钮，可移除该条记录 |

#### Non-Funding Account 预览表格

| 列名 | 说明 |
|------|------|
| Account | 账户号 |
| Type | Deposit / Withdraw |
| Amount | 调账金额 |
| Comment | 备注 |
| Ticket ID | 关联工单 ID |
| Fail Reason | 校验通过显示 "-"；校验失败显示红色错误信息 |
| Action | 校验通过为空；校验失败显示红色 "Remove" 按钮 |

**底部按钮**：Cancel / Confirm import

---

## 4. Credit Adjustment Audit New (credit-adjustment.html)

### 4.1 页面结构

- **导航栏**：中文菜单，含下拉子菜单（与 Cash Adjustment 页面一致，任务管理子菜单包含跳转至 `mt-adjustment.html` 和 `credit-adjustment.html` 的链接）
- **面包屑**：主页 / 任务管理 / Credit Adjustment Audit New
- **当前用户**：lemon
- **区域标题**：操作按钮上方显示 "Search Table"

### 4.2 查询条件

| 字段名 | 控件类型 |
|--------|----------|
| User ID | 文本输入框 |
| Account | 文本输入框 |
| Adjustment OrderID | 文本输入框 |
| Account Group | 文本输入框 |
| Account Type | 下拉选择（MT Trading Account / VTS Trading Account） |
| Type | 下拉选择（Credit In / Credit Out） |

### 4.3 操作按钮

| 按钮 | 样式 | 功能说明 |
|------|------|----------|
| Single Item Upload | 蓝色实心 | 打开单条上传弹窗 |
| Batch Import | 黑色/深色实心 | 打开批量 CSV 导入弹窗 |
| Approve | 默认边框 | 批量审批 |
| Reject | 默认边框 | 批量拒绝 |
| Download | 图标按钮 | 导出数据 |
| Settings | 图标按钮 | 列设置 |

### 4.4 数据列表字段

| 列名 | 是否可排序 | 说明 |
|------|-----------|------|
| Adjustment OrderID | 是 | 排在复选框后的第一列 |
| License | 否 | 如 SVG |
| User ID | 是 | - |
| Account | 是 | - |
| Account Group | 否 | 如 TEST_MY_USD、TEST\TEST_RISK_USD |
| Account Type | 否 | MT Trading Account / VTS Trading Account |
| Type | 是 | Credit In / Credit Out |
| Credits | 是 | 数值 |
| Currency | 是 | 如 USD |
| Status | 否 | COMPLETED（绿色圆点）/ SUBMITTED（橙色圆点），**位于 Comment 列之前** |
| Comment | 否 | 如 Remark、Credit out-User Request、Credit Out-Debt W/O |
| Application Note | 否 | - |
| Creation Time | 是 | 日期时间格式 |
| Update Time | 是 | 日期时间格式 |
| Applicant | 否 | - |
| Reviewer | 否 | - |
| Reject Reason | 否 | - |
| System Type | 否 | New System / Old System |
| Blacklist | 否 | 图标链接 |

### 4.5 Single Item Upload 弹窗（单条上传）

采用**双列表单布局**：

| 行 | 左侧字段 | 右侧字段 |
|----|----------|----------|
| 第 1 行 | *Account（文本输入框，placeholder: "Please enter account"） | *Type（下拉选择：Credit In / Credit Out） |
| 第 2 行 | *Currency（下拉选择：USD / EUR / GBP） | *Credit（文本输入框，placeholder: "Please enter credit"） |
| 第 3 行 | *Comment（下拉选择，占满整行：Remark / Credit out-User Request / Credit Out-Debt W/O） | - |
| 第 4 行 | Application Note（文本域，占满整行，placeholder: "Please enter"） | - |

表单下方：**操作历史记录表格**

| 列名 |
|------|
| Operation ID |
| Operation Time |
| Operation Content |
| Credits |
| Operation |
| Comment |
| Application Note |

默认状态：显示 "No data" 空数据占位。

**底部按钮**：Cancel / Confirm

### 4.6 Batch Import 弹窗（批量导入）

- 模板文件：`credit_adjustment_template.csv`
- 下载链接：`https://pj4w2l1pwuq.sg.larksuite.com/sheets/KziIs5djJhxOgVtxSjplTHotgid?sheet=2LMNn4`
- CSV 文件上传区域
- **底部按钮**：Cancel / Upload

### 4.7 分页

- 总计 601 条记录
- 每页条数选项：10 / 20 / 50 / 100
- 页码导航含省略号

---

## 5. 跨模块导航

三个页面共享统一的顶部导航栏，任务管理下拉菜单包含以下可跳转链接：

- Cash Adjustment Audit New → `mt-adjustment.html`
- Credit Adjustment Audit New → `credit-adjustment.html`

其他菜单项链接为占位符（`#`）。

---

## 6. 部署信息

| 环境 | 地址 |
|------|------|
| GitHub Pages 首页 | `https://delia88888.github.io/0818Adjustment/` |
| Funding 调账审核 | `https://delia88888.github.io/0818Adjustment/index.html` |
| Cash Adjustment Audit New | `https://delia88888.github.io/0818Adjustment/mt-adjustment.html` |
| Credit Adjustment Audit New | `https://delia88888.github.io/0818Adjustment/credit-adjustment.html` |
