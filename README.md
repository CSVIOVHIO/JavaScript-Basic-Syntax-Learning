# JS 核心语法学习

> 一份给零基础同学的 JavaScript 核心高频语法学习资料，面向 WebGIS 场景（Cesium、GeoJSON、axios 请求等）。

---

## 📖 内容概览

| 章节 | 内容 |
|------|------|
| 第 0 步 | 环境准备（浏览器控制台、VS Code、本地服务器） |
| 第 1 章 | 变量与数据类型（let/const、基本类型 vs 引用类型、typeof） |
| 第 2 章 | 数组高频方法（map、filter、find、reduce、箭头函数） |
| 第 3 章 | 解构与展开（对象解构、数组解构、展开运算符 `...`） |
| 第 4 章 | 异步核心（Promise、.then/.catch、async/await、try/catch） |
| 第 5 章 | axios 实战（GET/POST、拦截器、错误处理） |
| 第 6 章 | 每日练习（9 道练习题 + 答案 + 解析） |
| 附录 | 三天学习计划表、常见报错手册、术语词典 |

---

## 🚀 快速开始

### 1. 克隆仓库

```bash
git clone https://github.com/CSVIOVHIO/js-.git
```

### 2. 启动本地服务器

进入 `practice` 文件夹，启动 Python 本地服务器：

```bash
cd practice
python -m http.server 8000
```

### 3. 打开练习页面

浏览器访问：**http://localhost:8000/practice.html**

打开页面后按 `F12` 打开控制台，即可看到练习输出结果。

---

## 📂 项目结构

```
js核心语法学习/
├── JS核心语法学习文档.md    # 完整学习文档（讲义 + 例子 + 答案）
├── practice/
│   ├── practice.html        # 练习页面（打开即用）
│   └── geodata.json         # 练习用的 GeoJSON 数据
└── README.md
```

---

## 🛠 环境要求

- **浏览器**：Chrome 或 Edge（推荐）
- **编辑器**：VS Code（推荐）
- **Python**：3.x（用于启动本地服务器）

---

## 📝 学习路线

建议按 **三天计划** 学习：

| 天数 | 内容 |
|------|------|
| Day 1 | 变量与数据类型 + 数组高频方法 |
| Day 2 | 解构与展开 + 异步核心（Promise） |
| Day 3 | axios 实战 + 每日练习 |