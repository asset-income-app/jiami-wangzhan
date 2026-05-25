# 开发文档

## 代码结构

`index.html` 采用单文件结构，包含三个部分：

```
index.html
├── <style>     # CSS 样式
├── <body>      # HTML 结构
└── <script>    # JavaScript 逻辑
```

## CSS 样式说明

### 主要样式类

| 类名 | 说明 |
|------|------|
| `.container` | 主容器，最大宽度 1200px |
| `.products-grid` | 产品网格布局 |
| `.product-card` | 产品卡片 |
| `.product-image` | 产品图片区域 |
| `.product-info` | 产品信息区域 |
| `.contact-btn` | 联系按钮 |
| `.modal-overlay` | 模态窗口遮罩 |
| `.modal-content` | 模态窗口内容 |

### 响应式断点

```css
@media (max-width: 768px) {
    /* 手机端样式 */
    .products-grid {
        grid-template-columns: 1fr;
    }
}
```

### 配色方案

| 用途 | 颜色值 |
|------|--------|
| 主色调（绿色） | `#4a9c6d` |
| 背景深色 | `#1a1a2e`, `#16213e`, `#0f0f23` |
| 边框色 | `#3d5a4a`, `#2d4a3e` |
| 文字色 | `#e0e0e0`, `#a0a0a0`, `#8a8a8a` |

## JavaScript 模块说明

### 主要函数

#### `getContactedProducts()`

获取已联系的产品 ID 列表。

```javascript
function getContactedProducts() {
    // 从 localStorage 读取 contacted_products 数组
    // 返回: ['product-1', 'product-2', ...]
}
```

#### `saveContactedProduct(productId)`

保存已联系的产品 ID。

```javascript
function saveContactedProduct(productId) {
    // 将 productId 添加到 localStorage
}
```

#### `createProductCard(product)`

创建产品卡片 DOM 元素。

```javascript
function createProductCard(product) {
    // 参数: product 对象 { id, name, description, icon }
    // 返回: HTMLElement
}
```

#### `renderProducts()`

渲染所有产品卡片。

```javascript
function renderProducts() {
    // 遍历 PRODUCTS 数组
    // 检查 localStorage 中的已联系列表
    // 渲染可见的产品卡片
}
```

#### `fetchTempEmail(callback)`

获取临时邮箱地址。

```javascript
function fetchTempEmail(callback) {
    // 调用 Guerrilla Mail API
    // 成功: callback(null, email)
    // 失败: callback(error, null)
}
```

#### `showModal(productName, email, isFallback)`

显示模态窗口。

```javascript
function showModal(productName, email, isFallback) {
    // productName: 产品名称
    // email: 邮箱地址
    // isFallback: 是否为备用邮箱
}
```

#### `hideModal()`

隐藏模态窗口。

```javascript
function hideModal() {
    // 移除 .active 类
}
```

#### `handleContactClick(event)`

处理联系按钮点击事件。

```javascript
function handleContactClick(event) {
    // 1. 隐藏产品卡片
    // 2. 保存到 localStorage
    // 3. 获取临时邮箱
    // 4. 显示模态窗口
}
```

#### `init()`

初始化应用。

```javascript
function init() {
    // 1. 渲染产品
    // 2. 绑定事件监听器
}
```

### 数据结构

#### 产品对象

```javascript
{
    id: 'product-1',           // 唯一标识
    name: '天眼-3 侦察无人机',  // 产品名称
    description: '...',        // 产品描述
    icon: '✈'                  // 图标（Unicode 字符）
}
```

#### localStorage 数据

```javascript
// Key: 'military_products_contacted'
// Value: JSON 字符串数组
'["product-1", "product-3"]'
```

## API 接口

### Guerrilla Mail API

**获取临时邮箱地址**

```
GET https://api.guerrillamail.com/ajax.php?f=get_email_address
```

**响应示例**

```
abc123@guerrillamail.com
```

**错误处理**

- 请求超时：5 秒
- 失败时使用备用邮箱 `contact@example.com`
- 错误信息记录到控制台

## 事件处理

### 点击事件

| 元素 | 事件 | 处理函数 |
|------|------|----------|
| `.contact-btn` | click | `handleContactClick` |
| `.modal-overlay` | click | `hideModal`（点击遮罩关闭） |
| document | keydown | `hideModal`（ESC 键关闭） |

## 扩展开发

### 添加新产品

1. 在 `PRODUCTS` 数组中添加新对象
2. 设置唯一的 `id`
3. 选择合适的 `icon`（Unicode 字符）

### 修改样式

1. 修改 `<style>` 标签内的 CSS
2. 颜色值建议使用十六进制格式
3. 动画使用 CSS transition

### 替换临时邮箱 API

修改 `fetchTempEmail` 函数：

```javascript
function fetchTempEmail(callback) {
    // 替换为其他 API
    var xhr = new XMLHttpRequest();
    xhr.open('GET', 'https://your-api.com/get-email', true);
    // ...
}
```

## 调试说明

### 控制台日志

- API 请求失败时会输出错误信息
- localStorage 操作失败时会输出错误信息

### 清除测试数据

在浏览器控制台执行：

```javascript
localStorage.removeItem('military_products_contacted');
location.reload();
```

### 测试 API

在浏览器控制台执行：

```javascript
fetch('https://api.guerrillamail.com/ajax.php?f=get_email_address')
    .then(r => r.text())
    .then(console.log);
```
