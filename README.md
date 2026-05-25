# 军事装备展示平台

一个纯前端、无后端的军事装备展示网站，支持产品展示和联系厂家功能。

## 功能特性

- **产品展示**：展示军事装备产品卡片，包含图片、名称、描述
- **联系厂家**：点击联系按钮后弹出模态窗口，显示临时邮箱
- **持久化存储**：已联系的产品使用 localStorage 记录，刷新后保持隐藏
- **响应式设计**：自适应手机和电脑屏幕
- **军事风格**：深色背景、墨绿/灰色调、硬朗边框

## 技术栈

- 纯 HTML/CSS/JavaScript
- 无框架、无第三方库
- Guerrilla Mail API（临时邮箱）
- localStorage（本地存储）

## 快速开始

### 本地预览

直接在浏览器中打开 `index.html` 文件即可。

### 部署到静态托管

本项目为纯静态网站，可部署到任何静态托管服务：

#### GitHub Pages

1. 创建 GitHub 仓库
2. 上传 `index.html` 文件
3. 进入仓库 Settings → Pages
4. 选择分支和目录，点击 Save
5. 访问生成的 `https://username.github.io/repo-name/`

#### Cloudflare Pages

1. 登录 Cloudflare Dashboard
2. 进入 Pages → Create a project
3. 上传文件或连接 Git 仓库
4. 部署完成后访问生成的 URL

#### 阿里云 OSS

1. 登录阿里云 OSS 控制台
2. 创建 Bucket，开启静态网站托管
3. 上传 `index.html` 文件
4. 设置默认首页为 `index.html`
5. 访问 Bucket 域名

## 项目结构

```
加密网站/
├── index.html      # 主页面（包含所有代码）
├── README.md       # 项目说明文档
└── DEV.md          # 开发文档
```

## 配置说明

### 修改产品数据

在 `index.html` 中找到 `PRODUCTS` 数组，修改产品信息：

```javascript
var PRODUCTS = [
    {
        id: 'product-1',           // 产品唯一标识
        name: '产品名称',           // 产品名称
        description: '产品描述',    // 产品描述
        icon: '✈'                  // 产品图标
    },
    // ...
];
```

### 修改备用邮箱

在 `index.html` 中找到 `FALLBACK_EMAIL` 变量：

```javascript
var FALLBACK_EMAIL = 'contact@example.com';
```

### 修改倒计时时间

在 `showModal` 函数中修改 `countdown` 变量的初始值：

```javascript
var countdown = 3;  // 修改为你需要的秒数
```

## 安全性说明

- 不收集任何用户个人信息
- 不使用后端服务器，无数据库
- 临时邮箱由 API 动态生成，无法长期使用
- 使用 HTTPS 调用 API

## 法律声明

本网站仅展示公开信息，所有产品仅供参考。联系前请确认具备合法资质。

## 许可证

MIT License
