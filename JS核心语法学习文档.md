# JavaScript 核心高频语法零基础学习文档

> **这是给完全零基础的你的一份"保姆级"学习资料**，包含讲义、例子、练习和答案。
> 读完这份文档 + 动手跑完练习，你就能看懂 WebGIS 项目里最常见的 JS 代码（axios 请求、GeoJSON 数据处理、Cesium 加载数据）。

---

## 目录

- [第 0 步 · 开始之前：环境准备（10 分钟）](#第-0-步--开始之前环境准备10-分钟)
  - [0.1 你需要准备的东西](#01-你需要准备的东西)
  - [0.2 打开浏览器控制台](#02-打开浏览器控制台以后天天用先学会)
  - [0.3 安装 VS Code](#03-安装-vs-code强烈推荐10-分钟)
  - [0.4 怎么运行本套练习](#04-怎么运行本套练习重要)
- [第 1 章 · 变量与数据类型](#第-1-章--变量与数据类型)
  - [1.1 变量是什么](#11-变量是什么给数据起名字)
  - [1.2 let 和 const](#12-let-和-const怎么声明变量)
  - [1.3 基本类型 vs 引用类型](#13-基本类型-vs-引用类型cesium-核心依赖)
  - [1.4 typeof](#14-typeof怎么判断一个值是什么类型)
  - [1.5 本章小结 + 自测题](#15-本章小结--自测题)
- [第 2 章 · 数组高频方法](#第-2-章--数组高频方法)
  - [2.1 先认识数组](#21-先认识数组)
  - [2.2 map：一对一映射](#22-map一对一映射每个元素--一个新值形式数组mapfunction元素return-条件)
  - [2.3 filter：筛选](#23-filter筛选留下满足条件的形式数组filterfunction元素return-条件)
  - [2.4 find：找到就停](#24-find找到就停返回第一个满足条件的形式数组findfunction元素return-条件)
  - [2.5 reduce：聚合](#25-reduce聚合多合一最难但最强大)
  - [2.6 记忆口诀 + 对比表](#26-记忆口诀--对比表)
  - [2.7 箭头函数](#27-箭头函数先认识一下后面全用它)
- [第 3 章 · 解构与展开](#第-3-章--解构与展开)
  - [3.1 对象解构](#31-对象解构从对象里拆出属性)
  - [3.2 数组解构](#32-数组解构从数组里按顺序拆值)
  - [3.3 展开运算符 `...`](#33-展开运算符-把数组对象摊开)
  - [3.4 实战：解构 + 展开处理 GeoJSON](#34-实战解构--展开处理-geojson)
- [第 4 章 · 异步核心（重中之重）](#第-4-章--异步核心重中之重)
  - [4.1 同步 vs 异步](#41-先搞懂什么是同步什么是异步)
  - [4.2 为什么 WebGIS 里全是异步](#42-为什么-webgis-里全是异步)
  - [4.3 Promise 是什么](#43-promise-是什么一张欠条)
  - [4.4 Promise 三种状态](#44-promise-的三种状态状态机)
  - [4.5 .then 和 .catch](#45-怎么消费-promisethen-和-catch)
  - [4.6 .then 链式调用](#46-then-链式调用先-token-后数据真实项目场景)
    - [先理解：用生活例子类比](#先理解用生活例子类比)
    - [示例一：token → 数据](#示例一token--数据经典两步链)
    - [示例二：GeoJSON 场景](#示例二geojson-场景先拿文件再统计更贴近你的项目)
    - [一张图看懂链式调用](#一张图看懂链式调用)
    - [常见错误：忘写 return](#常见错误忘写-return)
  - [4.7 async/await](#47-asyncawait让异步代码像同步一样好读)
  - [4.8 try/catch](#48-trycatch把错误兜住)
  - [4.9 本章小结](#49-本章小结)
- [第 5 章 · axios 实战](#第-5-章--axios-实战)
  - [5.1 axios 是什么](#51-axios-是什么怎么引入)
  - [5.2 GET 请求](#52-get-请求读数据)
  - [5.3 POST 请求](#53-post-请求发数据)
  - [5.4 请求/响应拦截器](#54-请求响应拦截器统一处理)
  - [5.5 错误处理](#55-错误处理)
- [第 6 章 · 每日练习（题目 + 答案 + 解析）](#第-6-章--每日练习题目--答案--解析)
  - [练习 1~5：Promise 五连练](#练习-15promise-五连练模拟-token--数据--错误捕获)
  - [练习 6：axios 请求 GeoJSON](#练习-6用-axios-请求本地-geojson输出-features-数组长度)
  - [练习 7：map 提取 properties](#练习-7用-map-把-features-的-properties-提取为新数组)
  - [练习 8：filter 筛选 building](#练习-8用-filter-筛选出-type-为-building-的要素)
  - [练习 9：reduce 统计数量](#练习-9用-reduce-统计不同-type-的要素数量)
- [附录 A · 三天学习计划表](#附录-a--三天学习计划表)
- [附录 B · 常见报错自救手册](#附录-b--常见报错自救手册)
- [附录 C · 术语小词典](#附录-c--术语小词典)

---

## 第 0 步 · 开始之前：环境准备（10 分钟）

### 0.1 你需要准备的东西

| 东西 | 说明 | 你有吗？ |
|---|---|---|
| 浏览器 | Chrome 或 Edge（电脑自带 Edge） | ✅ 一定有 |
| 编辑器 | VS Code（推荐）或记事本 | 需要装（见 0.3） |
| Python | 用来启动本地服务器，跑练习 | ✅ 你电脑已装（3.14 版） |

不需要装 Node.js（虽然你电脑也有，练习页面用不上）。

### 0.2 打开浏览器控制台（以后天天用，先学会）

控制台（Console）是你学 JS 最好的"草稿纸"，写一行看一行结果。

1. 打开 Chrome 或 Edge 浏览器
2. 在任意页面按键盘最上面一排的 **F12** 键
3. 右边或下面会弹出一个面板，点 **Console（控制台）** 这个标签
4. 在下方光标处输入 `console.log("你好，世界")`，按回车

你会看到输出 `你好，世界`。恭喜，你写出了第一行 JS！

> 💡 `console.log(...)` 的意思是：把括号里的东西打印到控制台。后面所有例子都用它来看结果。

### 0.3 安装 VS Code（强烈推荐，10 分钟）

记事本也能写代码，但 VS Code 会"高亮"代码、提示错误，对新手友好得多。

1. 打开浏览器，访问 `https://code.visualstudio.com`
2. 点蓝色下载按钮，下载 Windows 版
3. 双击安装包，一路点"下一步"，**安装时勾选"添加到 PATH"**（如果有这个选项）
4. 装完后打开，点击左侧"扩展"图标（四个方块那个），搜索 **Chinese**，安装"中文（简体）语言包"，重启 VS Code 就是中文界面了

### 0.4 怎么运行本套练习（重要！）

练习文件在 `practice` 文件夹里。**注意：不能直接双击打开 practice.html**，因为浏览器出于安全考虑，会禁止页面直接读取本地文件（这叫跨域限制，后面第 5 章会讲）。必须用"本地服务器"的方式打开，步骤如下：

1. 打开 `practice` 文件夹
2. 在文件夹的**地址栏**（就是显示路径的地方）输入 `cmd`，按回车 —— 会弹出一个黑色命令行窗口
3. 在黑色窗口里输入下面这行命令，按回车：

   ```
   python -m http.server 8000
   ```

   出现 `Serving HTTP on :: port 8000` 之类的话就说明服务器起来了（窗口先别关）
4. 打开浏览器，地址栏输入 `http://localhost:8000/practice.html`，回车

页面会自动运行全部 9 道练习，结果直接显示在页面上；按 F12 打开控制台也能看到同样的输出。

> 💡 不想用命令行？也可以：用 VS Code 打开 practice 文件夹 → 安装扩展 **Live Server** → 右键 `practice.html` → "Open with Live Server"，效果一样。

---

## 第 1 章 · 变量与数据类型

### 1.1 变量是什么：给数据起名字

程序就是"处理数据"。数据需要一个名字，你叫它 A，程序才能找到它、用它。这个名字就叫**变量**。

```js
let name = "兰州";      // 把字符串 "兰州" 存进变量 name
let height = 173;       // 把数字 173 存进变量 height
console.log(name);      // 输出：兰州
console.log(height);    // 输出：173
```

`let` 是声明变量的关键字（语法的一部分），`=` 是赋值（把右边的东西装进左边），末尾的 `;` 表示这句话结束（可写可不写，建议写）。

### 1.2 let 和 const：怎么声明变量

现在的 JS 里，声明变量只用两个：**let**（可以改）和 **const**（不许改）。

> ⭐ **重点记忆**

| 关键字 | 意思 | 例子 |
|---|---|---|
| `let` | 变量，值可以**重新赋值** | `let a = 1; a = 2;` ✅ 合法 |
| `const` | 常量，声明后**不能重新赋值** | `const b = 1; b = 2;` ❌ 报错 |
| `var`（老古董） | 以前的写法，有很多坑，**现在别用** | 知道它存在就行 |

```js
let score = 60;
score = 90;          // ✅ let 可以改
console.log(score);  // 90

const city = "兰州";
// city = "北京";     // ❌ 会报错：Assignment to constant variable
```

**💡 小提示：let 和 const 怎么选？**

- 确定以后**不会变**的值 → 用 `const`（比如经纬度常量、请求地址、颜色配置）
- 以后**可能变**的值 → 用 `let`（比如循环计数、用户输入、分数）
- 默认都用 `const`，遇到要改的再改成 `let` —— 这是现在社区的主流习惯

> 💡 注意一个细节：`const` 说的是"不能重新赋值"，不是说"里面的东西不能变"。比如 `const arr = [1,2]`，你 `arr.push(3)` 是合法的（往数组里加东西没重新赋值），但 `arr = [3]` 不合法。这个区别值得注意。

### 1.3 基本类型 vs 引用类型（Cesium 核心依赖）

这是 JS 里最重要的概念之一，很多 bug 都出在这里。

**基本类型（一共 7 个）**：存的是"值本身"，就像一张纸条上写着一个数字。

```js
let a = 10;
let b = a;      // 把 a 的值"复制"给 b
b = 20;
console.log(a); // 还是 10（b 改了不影响 a，因为它们是两份独立的纸条）
```

| 基本类型 | 例子 | 说明 |
|---|---|---|
| number | `10`、`3.14` | 数字，整数小数都是它 |
| string | `"兰州"`、`'hello'` | 字符串，用引号包起来 |
| boolean | `true`、`false` | 布尔值，真/假 |
| undefined | `let x;` | 声明了但没赋值 |
| null | `null` | 主动表示"空" |
| bigint | `10n` | 超大整数（很少用） |
| symbol | `Symbol()` | 唯一标识（很少用） |

**引用类型（就一个：object 对象，数组/函数都是它的特殊形式）**：存的是"地址"，就像一张写着"东西放在仓库 3 号货架"的纸条。复制变量时复制的是地址，两个变量指向**同一个仓库**。

```js
let obj1 = { name: "教学楼A" };
let obj2 = obj1;        // 复制的是"地址"，obj1 和 obj2 指向同一个对象
obj2.name = "图书馆";
console.log(obj1.name); // 输出：图书馆！（obj2 改的就是 obj1 那个对象）
```

**数组也是引用类型**：

```js
let arr1 = [1, 2, 3];
let arr2 = arr1;      // 复制地址，不是复制数组
arr2.push(4);// 往 arr2 里加 4，arr1 也被改了！
console.log(arr1);    // [1, 2, 3, 4] —— arr1 也被改了！
```

**怎么真正复制一份？**（平时也常用）

```js
// 浅拷贝：复制第一层
let arr2 = [...arr1];                 // 数组：用展开运算符
let obj2 = { ...obj1 };               // 对象：用展开运算符
let obj2 = Object.assign({}, obj1);   // 对象：另一种写法

// 深拷贝（里面还有对象/数组时用）
let deepCopy = JSON.parse(JSON.stringify(obj1));// 深拷贝：用 JSON.stringify() 转换为字符串，再用 JSON.parse() 转换为对象
```

> 💡 为什么 Cesium/GeoJSON 场景非常重要？因为 GeoJSON 对象很大、嵌套很深，你在项目里不小心"复制"了别人的引用，改了一个就把原始数据也改了，地图上的数据就会莫名其妙变掉。记住：**基本类型按值传递，引用类型按引用传递**。

**🌰 举个 GeoJSON 实战例子，一步步看"坑"在哪**：

假设后端给了你一份原始 GeoJSON 数据，你的任务是"复制一份，改了之后提交"，但你不能动原始数据：

```js
// 原始数据（后端给的，不能动）
let original = {
  type: "Feature",
  geometry: {
    type: "Point",
    coordinates: [103.83, 36.06]   // 兰州的经纬度
  },
  properties: {
    name: "教学楼A",
    height: 20
  }
};
```

**❌ 错误做法：直接复制（你以为复制了，其实没有）**

```js
let copy = original;                    // 你以为复制了，其实只复制了"地址"
copy.properties.name = "图书馆";        // 改 copy 的 name
console.log(original.properties.name);  // 输出：图书馆 ← 原始数据也被改了！
```

为什么？因为 `copy` 和 `original` 指向的是**同一个对象**，就像两个人拿的是同一把钥匙，谁开门进去改东西，另一个看到的就是改过的。用图理解就是：

```
original ──→ 📦 { type, geometry, properties }  ←── copy 也指向这里
                   ↑
              只有一个对象！两个变量都指向它
```

**❌ 进阶错误：用浅拷贝以为安全了，结果全是坑**

```js
let copy = { ...original };              // 浅拷贝：只复制了第一层
copy.properties.name = "图书馆";         // 改 properties
console.log(original.properties.name);   // "图书馆" ← 被改了！
```

为什么 `properties` 也被改了？因为 `{ ...original }` 只复制了**最外层**，里面的 `geometry` 和 `properties` 复制的是"地址"，两个变量指向的还是同一个对象。验证一下：

```js
console.log(copy.properties === original.properties); // true ← 同一个对象！
console.log(copy.geometry === original.geometry);     // true ← 同一个对象！
```

所以不管改 `copy.properties` 还是 `copy.geometry`，`original` 都会跟着变：

```js
copy.geometry.coordinates[0] = 120;
console.log(original.geometry.coordinates); // [120, 36.06] ← 也被改了！
```

用图理解：

```
浅拷贝 { ...original } 之后：
original ──→ 📦 { type: "Feature", geometry: ─→ 📦 { type, coordinates: ─→ [103.83, 36.06] }, properties: ─→ 📦 { name, height } }
copy     ──→ 📦 { type: "Feature", geometry: ─→ 同一个 📦 ↑,              properties: ─→ 同一个 📦 ↑ }
                                               ↑                                ↑
                               geometry 和 properties 都是共用的！展开运算符只拆了最外层盒子
```

**✅ 正确做法：深拷贝，真正做到"完全独立一份"**

```js
let copy = JSON.parse(JSON.stringify(original));  // 深拷贝：里里外外全复制
copy.properties.name = "图书馆";
copy.geometry.coordinates[0] = 120;
console.log(original.properties.name);       // "教学楼A" ← 原数据纹丝不动！
console.log(original.geometry.coordinates);  // [103.83, 36.06] ← 原数据纹丝不动！
```

> 🎯 **一句话总结**：浅拷贝只复制"第一层"，深拷贝复制"每一层"。GeoJSON 的 `geometry`、`coordinates` 都是嵌套的，所以项目中处理 GeoJSON 数据，要么用 `JSON.parse(JSON.stringify())` 深拷贝，要么用 `structuredClone()`（现代浏览器支持），总之别直接赋值。

**✏️ 小练习：看代码，猜输出**

```js
let data = {
  name: "兰州",
  center: [103.83, 36.06]
};

let copy1 = data;                    // 做法 1
let copy2 = { ...data };             // 做法 2
let copy3 = JSON.parse(JSON.stringify(data)); // 做法 3

copy1.name = "北京";
copy2.center[0] = 110;
copy3.name = "上海";

console.log(data.name);        // ① 输出什么？（北京）
console.log(data.center[0]);   // ② 输出什么？（110）
```

<details>
<summary>点击查看答案</summary>

```
① "北京"
   → copy1 和 data 是同一个对象，copy1.name = "北京" 直接改了 data

② 110
   → copy2 是浅拷贝，只复制了第一层。copy2.center 和 data.center 指向同一个数组，
     所以 copy2.center[0] = 110 把 data.center 也改了

③ copy3 = JSON.parse(JSON.stringify(data)) 是深拷贝，和 data 完全独立，
   所以 copy3.name = "上海" 不影响 data.name
```

</details>

### 1.4 typeof：怎么判断一个值是什么类型

```js
console.log(typeof 10);          // "number"
console.log(typeof "兰州");       // "string"
console.log(typeof true);        // "boolean"
console.log(typeof undefined);   // "undefined"
console.log(typeof { a: 1 });    // "object"
console.log(typeof [1, 2]);      // "object"  ← 注意！数组也是 object
console.log(typeof null);        // "object"  ← 历史遗留 bug，记住这个坑就行
console.log(typeof function(){});// "function"
```

**两个坑**（需要注意）：
1. `typeof null` 返回 `"object"` —— 这是 JS 诞生时的 bug，一直没修。判断 null 要用 `x === null`
2. `typeof [1,2]` 返回 `"object"` —— 想判断是不是数组要用 `Array.isArray(x)`

**🔍 怎么判断一个变量是不是数组？**

因为 `typeof` 对数组返回的是 `"object"`，所以判断数组得用专门的方法：

```js
let arr = [1, 2, 3];
let obj = { a: 1 };
let str = "hello";

console.log(Array.isArray(arr)); // true  ← 是数组，console.log（array.isarray(arr)）
console.log(Array.isArray(obj)); // false ← 普通对象
console.log(Array.isArray(str)); // false ← 字符串
```

> ⭐ `Array.isArray(x)` —— 一行搞定，现代 JS 唯一推荐写法。

### 1.5 本章小结 + 自测题

- 声明用 `let`（可变）和 `const`（不可变），`var` 别用
- 基本类型存值、引用类型存地址；复制引用类型要浅拷贝/深拷贝
- `typeof` 判断类型，但 null 和数组要用别的方法判断

**自测（想一下答案，再翻到文末答案区）**：
1. `const a = [1,2]; a.push(3);` 合法吗？a 现在是？
2. `let x = 5; let y = x; y = 9;` x 是几？为什么？
3. 怎么判断一个变量是不是数组？

---

## 第 2 章 · 数组高频方法

### 2.1 先认识数组

数组就是一排数据的集合，用 `[]` 包起来。

#### 2.1.1 数组的基本操作

```js
let arr = [10, 20, 30];

// ① 取值：通过下标（从 0 开始数）
console.log(arr[0]);        // 10（第 0 个）
console.log(arr[1]);        // 20（第 1 个）
console.log(arr[2]);        // 30（第 2 个）
console.log(arr[3]);        // undefined（没有第 3 个）

// ② 长度
console.log(arr.length);    // 3

// ③ 修改某个位置的值
arr[1] = 99;
console.log(arr);           // [10, 99, 30]

// ④ 往末尾加一个元素
arr.push(40);
console.log(arr);           // [10, 99, 30, 40]

// ⑤ 删除末尾一个元素
arr.pop();
console.log(arr);           // [10, 99, 30]

// ⑥ 往开头加一个元素
arr.unshift(5);
console.log(arr);           // [5, 10, 99, 30]

// ⑦ 删除开头一个元素
arr.shift();
console.log(arr);           // [10, 99, 30]
```

| 操作 | 方法 | 说明 |
|---|---|---|
| 取值 | `arr[下标]` | 下标从 0 开始，超出范围返回 `undefined` |
| 长度 | `arr.length` | 数组里有多少个元素 |
| 末尾添加 | `arr.push(x)` | 往最后加一个，返回新长度 |
| 末尾删除 | `arr.pop()` | 删除最后一个，返回被删的元素 |
| 开头添加 | `arr.unshift(x)` | 往最前面加一个 |
| 开头删除 | `arr.shift()` | 删除最前面一个 |

> ⭐ **从数组里取一条数据**：`arr[下标]` 是最常用的操作。在 GeoJSON 里，`geojson.features[0]` 就是取第一条要素，`geojson.features[1]` 取第二条，以此类推。拿到一条数据后，可以继续 `.` 出它的属性：
> ```js
> let first = geojson.features[0];           // 取第一条
> console.log(first.properties.name);        // "教学楼A"
> console.log(first.geometry.type);          // "Polygon"
> ```

#### 2.1.2 数组里能放什么？

数组里什么都能放——数字、字符串、对象、甚至另一个数组：

```js
let mixed = [
  1,                        // 数字
  "hello",                  // 字符串
  { name: "教学楼A" },       // 对象
  [10, 20],                 // 数组里套数组（二维数组）
  true                      // 布尔值
];

console.log(mixed[2].name);    // "教学楼A"（先取第 2 个元素，再取它的 name 属性）
console.log(mixed[3][0]);      // 10（先取第 3 个元素（是个数组），再取它的第 0 个）
```

#### 2.1.3 遍历数组：for 循环和 forEach

```js
let arr = ["教学楼A", "主干道", "人工湖"];

// 方式一：普通 for 循环
for (let i = 0; i < arr.length; i++) {
  console.log("第" + i + "个：" + arr[i]);
}
// 输出：
// 第0个：教学楼A
// 第1个：主干道
// 第2个：人工湖

// 方式二：forEach（更简洁，推荐）
arr.forEach(function (item, index) {
  console.log("第" + index + "个：" + item);
});
// 输出同上
```

> 💡 `forEach` 是专门用来遍历数组的，和 `for` 循环效果一样但更简洁。后面学的 `map`、`filter` 本质上也是遍历。

#### 2.1.4 GeoJSON 中的数组

在 WebGIS 里，你拿到手的 GeoJSON 数据长这样（简化）：

```js
let geojson = {
  features: [
    { properties: { type: "building", name: "教学楼A" } },
    { properties: { type: "road",    name: "主干道"   } },
    { properties: { type: "water",   name: "人工湖"   } }
  ]
};
```

`geojson.features` 就是一个**数组**，里面每个元素是一个对象。下面 4 个方法就是专门用来处理这种数组的。

### 2.2 map：一对一映射（每个元素 → 一个新值）(形式：数组.map(function(元素){return 条件;}))

**大白话**：把数组里每个元素"加工"一下，得到同样长度的新数组。**不修改原数组**。

```js
let nums = [1, 2, 3];
let doubled = nums.map(function (n) {
  return n * 2;          // 每个都乘 2
});
console.log(doubled);    // [2, 4, 6]
console.log(nums);       // [1, 2, 3]（原数组没变）
```

**GeoJSON 场景**：把每个要素的 properties 提取出来（这就是每日练习 7 的答案雏形）：

```js
let names = geojson.features.map(function (f) {
  return f.properties.name;
});
console.log(names);      // ["教学楼A", "主干道", "人工湖"]
```

**注意**：`map` 必须 `return` 一个值，不然新数组里全是 `undefined`。这是新手最常见的错。

### 2.3 filter：筛选（留下满足条件的）(形式：数组.filter(function(元素){return 条件;}))

**大白话**：遍历数组，把"条件为 true"的元素留下来，组成新数组。**不修改原数组**。

```js
let nums = [1, 2, 3, 4, 5, 6];
let evens = nums.filter(function (n) {
  return n % 2 === 0;    // 留下偶数
});
console.log(evens);      // [2, 4, 6]
```

**GeoJSON 场景**：筛选出所有 building 要素（练习 8 的雏形）：

```js
let buildings = geojson.features.filter(function (f) {
  return f.properties.type === "building";
});
```

### 2.4 find：找到就停（返回第一个满足条件的）(形式：数组.find(function(元素){return 条件;}))

**大白话**：从头往后找，找到第一个满足条件的就返回它（是那个元素本身，不是数组），找不到返回 `undefined`。**只找一个**。

```js
let nums = [5, 12, 8, 130, 44];
let found = nums.find(function (n) {
  return n > 10;         // 第一个大于 10 的是谁？
});
console.log(found);      // 12（不是 130！find 找到第一个就停了）
```

**GeoJSON 场景**：找名叫"图书馆"的要素：

```js
let lib = geojson.features.find(function (f) {
  return f.properties.name === "图书馆";
});
// 找不到时返回 undefined，所以用之前最好判断一下
if (lib) {
  console.log("找到了：", lib.properties);
}
```

**🌰 更多 GeoJSON 实战案例**（用 `geodata.json` 的 10 条数据练手）：

```js
// 案例1：找第一个"楼层大于5层"的 building
let tallBuilding = geojson.features.find(function (f) {
  return f.properties.type === "building" && f.properties.floors > 5;
});
console.log(tallBuilding.properties.name);  // "教学楼A"（教学楼A 6层，第一个满足）

// 案例2：找名叫"喷泉"的要素
let fountain = geojson.features.find(function (f) {
  return f.properties.name === "喷泉";
});
console.log(fountain.geometry.type);        // "Point"（喷泉是点要素）

// 案例3：找第一条"宽度大于10"的路
let wideRoad = geojson.features.find(function (f) {
  return f.properties.type === "road" && f.properties.width > 10;
});
console.log(wideRoad.properties.name);      // "主干道"（width=20 > 10，排在第一个，直接返回）
// 注意：find 找的是"第一个"，主干道 width=20 已经满足条件，就不会再往后找"环路"了
```

> ⚠️ **find 和 filter 的区别**：想找"所有满足条件的"用 `filter`，想找"第一个满足条件的"用 `find`。比如找所有 building 用 `filter`，找第一个 building 用 `find`。

### 2.5 reduce：聚合（多合一，最难但最强大）

**大白话**：把整个数组"揉"成一个值。比如求和、计数、统计。

**固定格式**：`reduce(回调, 初始值)`，回调里有 4 个参数，常用的前两个是：

- `acc`：累加器（上一轮的结果，第一次是初始值）
- `cur`：当前元素

```js
let nums = [1, 2, 3, 4];
let sum = nums.reduce(function (acc, cur) {
  return acc + cur;      // 把当前元素加进累加器
}, 0);                   // 0 是初始值
console.log(sum);        // 10（1+2+3+4）
```

**手工走一遍**（理解 acc 怎么变）：

| 轮次 | acc（进来时） | cur | return（=下一轮 acc） |
|---|---|---|---|
| 第1轮 | 0（初始值） | 1 | 1 |
| 第2轮 | 1 | 2 | 3 |
| 第3轮 | 3 | 3 | 6 |
| 第4轮 | 6 | 4 | 10 |

**GeoJSON 场景：统计各种 type 的数量**（练习 9 的雏形）：

```js
let typeCount = geojson.features.reduce(function (acc, f) {
  let t = f.properties.type;        // 取当前要素的 type
  acc[t] = (acc[t] || 0) + 1;       // 之前没有就按 0 算，然后 +1
  return acc;                        // 把更新后的 acc 还回去
}, {});                              // 初始值是一个空对象
console.log(typeCount);  // { building: 1, road: 1, water: 1 }
```

> ⭐ **重点**：`acc[t] || 0` 的意思是：如果 `acc[t]` 是 `undefined`（第一次见到这个 type），就用 0 代替，再加 1。这是 reduce 统计的经典写法，背下来。

### 2.6 记忆口诀 + 对比表

> **map 映射（一对一）、filter 过滤（一筛选）、find 找到就停（一找一）、reduce 聚合（多合一）。**

| 方法 | 返回什么 | 返回几个 | 改原数组？ | 一句话 |
|---|---|---|---|---|
| `map` | 新数组 | 跟原数组一样多 | 不改 | 每个元素加工后返回 |
| `filter` | 新数组 | 0~全部（满足条件的） | 不改 | 留下满足条件的 |
| `find` | 一个元素 | 最多 1 个 | 不改 | 找第一个满足的 |
| `reduce` | 任何值（数字/对象/数组） | 1 个"汇总" | 不改 | 整个数组揉成一个 |

> 💡 记忆口诀：**"映射选 map，筛选选 filter，找一个用 find，汇总用 reduce"**。

### 2.7 箭头函数（先认识一下，后面全用它）

现代 JS 代码里，`function (x) { return x * 2 }` 通常写成箭头函数 `(x) => x * 2`，更短。**箭头函数 = 匿名函数的最简写法**：

```js
// 普通写法
let a = nums.map(function (n) { return n * 2; });
// 箭头函数写法（等价）
let b = nums.map((n) => n * 2);
// 如果只有一个参数，括号也能省
let c = nums.map(n => n * 2);
```

- 参数只有 1 个时，`()` 可省：`n => n * 2`
- 函数体只有一句 `return` 时，`{}` 和 `return` 都可省：`n => n * 2`
- 参数多个或没有，必须带括号：`(a, b) => a + b`、`() => 1`
- 函数体有多句时，必须写 `{}` 和 `return`：`(n) => { let x = n + 1; return x; }`

**练习 6-9 的答案里我会用箭头函数写一份、普通函数写一份，你对照看。**

---

## 第 3 章 · 解构与展开

### 3.1 对象解构：从对象里"拆"出属性

**大白话**：以前要写 `obj.name` 才能拿到 name，解构可以直接声明一个变量，名字和属性一样，自动取值。

```js
let person = { name: "小明", age: 20, city: "兰州" };

// 老写法
// let name = person.name;
// let age = person.age;

// 解构写法
let { name, age } = person;
console.log(name);   // 小明
console.log(age);    // 20
```

**GeoJSON 场景**（拿 properties 里的字段）：

```js
let f = { properties: { type: "building", name: "图书馆", floors: 8 } };
let { type, name, floors } = f.properties;
console.log(type, name, floors);   // building 图书馆 8
```

### 3.2 数组解构：从数组里按顺序"拆"值

```js
let arr = ["兰州", "成都", "西安"];
let [a, b] = arr;      // 按顺序取前两个
console.log(a);        // 兰州
console.log(b);        // 成都

// 跳过某个：用逗号占位
let [, , c] = arr;
console.log(c);        // 西安

// 交换两个变量的值（经典技巧）
let x = 1, y = 2;
[x, y] = [y, x];
console.log(x, y);     // 2 1
```

### 3.3 展开运算符 `...`：把数组/对象"摊开"

**展开数组**：

```js
let arr1 = [1, 2];
let arr2 = [3, 4];
let merged = [...arr1, ...arr2];   // 合并数组
console.log(merged);               // [1, 2, 3, 4]

let copy = [...arr1];              // 复制数组（浅拷贝，第 1 章讲过）
```

**展开对象**：

```js
let base = { type: "Feature", properties: { name: "教学楼A" } };
let withId = { ...base, id: 1 };   // 复制 base 再加一个字段
console.log(withId);               // { type: "Feature", properties: {...}, id: 1 }
```

> 💡 展开时**后面的属性会覆盖前面的同名属性**：`{ ...a, name: "新名字" }` 会把 a 里的 name 覆盖成"新名字"。这是改对象时常用的"不可变更新"技巧。

### 3.4 实战：解构 + 展开处理 GeoJSON

```js
let feature = {
  type: "Feature",
  properties: { type: "building", name: "实验楼", floors: 4 },
  geometry: { type: "Polygon", coordinates: [] }
};

// 解构取出
let { properties } = feature;
let { name, floors } = properties;

// 展开添加新字段（不改原对象）
let enhanced = {
  ...feature,
  properties: { ...feature.properties, label: name + "（" + floors + "层）" }
};
console.log(enhanced.properties.label);   // 实验楼（4层）
console.log(feature.properties.label);    // undefined（原对象没被改）
```

---

## 第 4 章 · 异步核心（重中之重）

### 4.1 先搞懂：什么是同步，什么是异步

**同步（sync）**：一件事做完，才能做下一件。像食堂打饭，排队，前面的人没打完，你只能等着。

**异步（async）**：先干别的，等结果出来了再回来处理。像点外卖，你下单后不用站在店里等，可以回家玩手机，外卖到了再去取。

```js
// 同步例子：会卡住 3 秒，然后才输出"完"
// console.log("开始");
// 这里如果有 sleep(3)，下面一行必须等 3 秒
// console.log("完");

// 异步例子（JS 最常用的两个异步方法）：
console.log("开始");
setTimeout(function () {     // setTimeout：过一会儿再执行
  console.log("2 秒后执行我");
}, 2000);
console.log("结束");          // 先输出"结束"，2 秒后输出"2 秒后执行我"
```

**JS 是单线程的**（一次只干一件事），但它通过"事件循环"实现了异步：把耗时的活（网络请求、读文件）交给底层去干，干完了再回来通知 JS。所以 JS 代码永远先跑完"立即能跑的"，再回头处理"异步回来的"。

### 4.2 为什么 WebGIS 里全是异步？

你在 WebGIS 项目里做的每一件重要的事，几乎都是异步的：

| 场景 | 为什么异步 |
|---|---|
| axios 请求 GeoJSON 数据 | 网络请求要多长时间不确定，不能卡死页面 |
| Cesium 加载瓦片、3D 模型 | 数据从服务器下载，要等 |
| 接口联调（token、用户信息） | 要先拿到 A 接口的结果，才能请求 B 接口 |

如果你不懂异步，你写的代码会变成"页面白屏等数据"或者"数据还没回来就报错"。**不理解 async/await，WebGIS 就是死路**——这句话是真的。

### 4.3 Promise 是什么：一张"欠条"

Promise 就是 JS 用来管理异步的"欠条"对象。你发起一个异步操作（比如发请求），它先给你一张欠条（Promise），承诺：**将来**要么成功（给你结果），要么失败（给你错误原因）。

```js
let p = new Promise(function (resolve, reject) {
  // 这里放异步操作（比如 setTimeout、axios 请求）
  // 成功时调用 resolve(结果)   —— 兑现欠条
  // 失败时调用 reject(错误)    —— 撕票
});
```

- `resolve(值)`：表示成功了，把结果交出去
- `reject(错误)`：表示失败了，把错误原因交出去

### 4.4 Promise 的三种状态（状态机）

一个 Promise 一生只有三种状态，**一旦变化就不能再变**：

```
    pending（进行中）
         │
         ├── resolve ──▶ fulfilled（已成功）
         │
         └── reject ───▶ rejected（已失败）

    状态一旦确定，永远不会再变
```

- **pending**（等待中）：异步操作还在进行
- **fulfilled**（已成功）：调用了 resolve
- **rejected**（已失败）：调用了 reject

**关键点**：pending → fulfilled 或 pending → rejected，只能发生一次。状态定了就不会回头。

### 4.5 怎么消费 Promise：.then 和 .catch

拿结果用 `.then`，接错误用 `.catch`：

```js
let p = new Promise(function (resolve, reject) {
  setTimeout(function () {  
     //setTimeout：setTimeout(要做的事, 延迟毫秒数) 是 JS 自带的定时器，等一段时间后，再执行一段代码。
    resolve("1 秒后给你这个结果");
    // reject(new Error("如果失败了，传这个错误"));
  }, 1000);//1000ms 后执行
});

p.then(function (data) {
  console.log("成功，拿到：", data);   // 成功时执行
}).catch(function (err) {
  console.log("失败，原因是：", err);  // 失败时执行
});
```

`.then(成功回调)` 里的回调在 Promise 成功时执行；`.catch(失败回调)` 里的回调在失败时执行。**.catch 还能兜住 .then 里抛出的错误**，所以永远记得在链条末尾挂一个 .catch。

### 4.6 .then 链式调用：先 token 后数据（真实项目场景）

真实项目里，经常要"先拿到 A，再用 A 去拿 B"。

#### 先理解：用生活例子类比

> 🍔 **汉堡店取餐**：你走进汉堡店，不是"点完餐立刻拿到汉堡"，而是：
> 1. **先排队点餐**（发请求）→ 拿到一张**小票**（token）
> 2. **拿着小票去取餐台**（再用 token 发请求）→ 拿到**汉堡**（数据）
>
> 你不能跳过第 1 步直接拿汉堡，因为取餐员只认小票。这就是 `.then` 链式调用的本质：**等上一个结果出来，再拿着它做下一件事**。

换成代码就是：**先请求 token，再用 token 请求数据**。

#### 示例一：token → 数据（经典两步链）

```js
// 第 1 步：模拟请求 token
// 相当于"去柜台点餐，等叫号"——返回一个 Promise，500ms 后给你小票
function getToken() {
  return new Promise(function (resolve) {
    setTimeout(function () {
      resolve("token-abc123");   // 500ms 后，resolve 把 token 传出去
    }, 500);                      // 500 毫秒 = 0.5 秒，模拟网络延迟
  });
}

// 第 2 步：模拟用 token 换数据
// 相当于"拿着小票去取餐台"——需要上一个函数给的 token 才能工作
function getData(token) {        // token 参数来自上一个 .then
  return new Promise(function (resolve) {
    setTimeout(function () {
      resolve("用 " + token + " 换来的数据");   // 拼接 token，返回数据
    }, 500);                                     // 又是 0.5 秒延迟
  });
}

// ══════ 链式调用正式开始 ══════
getToken()                                  // 回到"点餐"，开始排队
  .then(function (token) {                  // 拿到小票了！
    console.log("第 1 步，拿到 token：", token);  // 输出：token-abc123
    return getData(token);                  // ★ 用小票去取餐，返回新 Promise
  })                                        //    如果不 return，链条就断了！
  .then(function (data) {                   // 汉堡到手了！
    console.log("第 2 步，拿到数据：", data);    // 输出：用 token-abc123 换来的数据
  })
  .catch(function (err) {                   // 任何一步失败（比如小票丢了），
    console.log("出错了：", err);            // 都会跳到这里
  });
```

> ⭐ **链式调用的核心规则**：`.then` 的回调里**必须 `return` 一个新 Promise**，后面的 `.then` 才能接到它。中间的某一步 reject 了，后面的 `.then` 全部跳过，直接进 `.catch`。

#### 示例二：GeoJSON 场景——先拿文件，再统计（更贴近你的项目）

```js
// 第 1 步：模拟"从服务器下载 GeoJSON 文件"
// 真实项目里是 axios.get('/api/geojson')，这里用 setTimeout 模拟
function fetchGeoJSON() {
  return new Promise(function (resolve) {
    setTimeout(function () {
      resolve({
        type: "FeatureCollection",
        features: [
          { properties: { type: "building", name: "教学楼A" } },
          { properties: { type: "building", name: "图书馆" } },
          { properties: { type: "road",    name: "主干道" } },
          { properties: { type: "road",    name: "林荫小路" } },
        ]
      });
    }, 800);   // 模拟 800ms 网络延迟
  });
}

// 第 2 步：统计 building 的数量
// 需要拿到第 1 步的 geojson 对象才能工作
function countBuildings(geojson) {         // geojson 参数来自上一个 .then
  return new Promise(function (resolve) {
    let count = geojson.features.filter(function (f) {
      return f.properties.type === "building";
    }).length;
    resolve(count);                        // 把统计结果传出去
  });
}

// ══════ 链式调用 ══════
fetchGeoJSON()                             // 开始下载文件
  .then(function (geojson) {               // 下载完成，拿到 geojson 对象
    console.log("文件下载完毕，共", geojson.features.length, "个要素");
    return countBuildings(geojson);        // ★ 把 geojson 传给下一个函数
  })
  .then(function (count) {                 // 统计完成
    console.log("building 数量：", count); // 输出：2
  })
  .catch(function (err) {                  // 下载失败 or 统计失败
    console.log("出错了：", err);
  });
```

#### 一张图看懂链式调用

```
getToken()                  .then(token)                 .then(data)
    │                            |                            │
    │ 返回 Promise               |返回新 Promise               │ 拿到最终结果
    ▼                            ▼                            ▼
 [等待] ───────────────────▶ "token-abc123" ───────────▶ "用 token 换来的数据"
                                 │                            │
                                 └──────── 失败 ──────────▶ .catch
```

#### 常见错误：忘写 return

```js
// ❌ 错误写法：忘了 return
getToken()
  .then(function (token) {
    getData(token);            // 没有 return！后面的 .then 拿到的是 undefined
  })
  .then(function (data) {
    console.log(data);         // undefined —— 懵逼了
  });

// ✅ 正确写法：必须 return
getToken()
  .then(function (token) {
    return getData(token);     // ★ 有 return，链条才能传下去
  })
  .then(function (data) {
    console.log(data);         // "用 token-abc123 换来的数据"
  });
```

### 4.7 async/await：让异步代码像同步一样好读

`.then` 链写多了会变成"回调地狱"，很难读。`async/await` 就是它的**语法糖**：用看起来像同步的写法写异步代码。

规则只有两条：

1. 函数前面加 `async`，这个函数就变成"异步函数"，里面才能用 `await`
2. `await` 放在一个 Promise 前面，意思"**等它出结果**"，成功就拿到 resolve 的值，失败就抛异常

```js
async function main() {
  let token = await getToken();       // 等 token，拿到的就是 resolve 的值
  console.log("拿到 token：", token);
  let data = await getData(token);    // 等数据
  console.log("拿到数据：", data);
}
main();
```

对比 4.6 的链式写法，`await` 版本是不是像从上往下读的同步代码？**这就是它存在的意义**：代码更直白、更好排错。

### 4.8 try/catch：把错误兜住

`await` 出错了会"抛异常"，用 `try/catch` 接住：

```js
async function main() {
  try {
    let token = await getToken();
    let data = await getData(token);
    console.log("成功：", data);
  } catch (err) {
    // 上面任何一步出错，都会跳到这里
    console.log("出错了：", err.message);
  }
}
main();
```

**try/catch 的作用**：把"可能会出错"的代码放进 `try {}`，出错时不会让程序崩溃，而是跳进 `catch (err) {}` 让你处理。就像开车有安全气囊，不是为了防止撞车，而是撞了车不至于没命。

### 4.9 本章小结

- 异步 = 不等结果，先干别的，结果回来再处理
- Promise = 管理异步的"欠条"，三种状态：pending → fulfilled / rejected
- `.then()` 拿成功结果，`.catch()` 接错误，链式调用靠 `return` 新 Promise
- `async/await` = 让异步代码像同步一样好读，`await` 后面跟 Promise
- `try/catch` 兜住 await 抛出的错误

---

## 第 5 章 · axios 实战

### 5.1 axios 是什么、怎么引入

axios 是一个**发 HTTP 请求的库**（别人写好、你直接用的 JS 代码）。它内部就是用 Promise 实现的，所以返回的就是 Promise，可以用 `.then/.catch` 或 `async/await` 处理。

**引入方式**：在 HTML 里加一行（本套练习页面已经加了）：

```html
<script src="https://cdn.jsdelivr.net/npm/axios@1.6.8/dist/axios.min.js"></script>
```

或者在 Node.js 项目里：`npm install axios`，然后 `import axios from "axios";`

### 5.2 GET 请求（读数据）

```js
// 方式一：.then/.catch
axios.get("https://api.example.com/geodata.json")
  .then(function (res) {
    console.log("数据：", res.data);   // res.data 才是响应数据
  })
  .catch(function (err) {
    console.log("出错：", err.message);
  });

// 方式二：async/await（推荐，更好读）
async function loadData() {
  try {
    let res = await axios.get("https://api.example.com/geodata.json");
    console.log("数据：", res.data);
  } catch (err) {
    console.log("出错：", err.message);
  }
}
```

**重要**：axios 返回的 `res` 是一个响应对象，里面 `res.data` 才是服务器返回的数据（GeoJSON 就在里面），`res.status` 是状态码（200 表示成功），`res.headers` 是响应头。

### 5.3 POST 请求（发数据）

```js
async function login() {
  try {
    let res = await axios.post("https://api.example.com/login", {
      username: "admin",
      password: "123456"
    });
    console.log("登录成功，token：", res.data.token);
  } catch (err) {
    console.log("登录失败：", err.message);
  }
}
```

`axios.post(url, 数据对象)`：第二个参数是你要发给服务器的数据，axios 会自动转成 JSON。

### 5.4 请求/响应拦截器（统一处理）

拦截器 = "中间检查站"。**请求拦截器**在请求发出前执行（比如统一加 token），**响应拦截器**在响应回来时执行（比如统一检查错误码）。

```js
// 创建你自己的 axios 实例（建议项目里都这么做）
const http = axios.create({
  baseURL: "https://api.example.com",
  timeout: 10000          // 10 秒超时
});

// 请求拦截器：每次发请求前，自动带上 token
http.interceptors.request.use(function (config) {
  let token = localStorage.getItem("token");   // 从本地存储取登录凭证
  if (token) {
    config.headers.Authorization = "Bearer " + token;  // 加到请求头
  }
  return config;    // 必须返回 config，否则请求发不出去
}, function (error) {
  return Promise.reject(error);
});

// 响应拦截器：统一处理业务错误码
http.interceptors.response.use(function (response) {
  // 服务器返回的业务码（假设 0 表示成功）
  if (response.data && response.data.code !== 0) {
    return Promise.reject(new Error(response.data.message));
  }
  return response;
}, function (error) {
  // 网络错误 / HTTP 状态码不是 2xx 会进这里
  console.error("网络错误：", error.message);
  return Promise.reject(error);
});
```

有了拦截器，你每个接口就不用重复写"加 token""判断错误码"了。这是实际项目里的标准做法。

### 5.5 错误处理

```js
async function safeRequest() {
  try {
    let res = await http.get("/geodata.json");
    console.log(res.data);
  } catch (err) {
    if (err.response) {
      // 服务器有响应，但状态码不是 2xx（比如 404、500）
      console.log("HTTP 状态码：", err.response.status);
      console.log("服务器返回：", err.response.data);
    } else if (err.request) {
      // 请求发出去了，但没收到响应（比如断网、超时）
      console.log("没有收到响应：", err.message);
    } else {
      // 请求根本没发出去（比如参数写错）
      console.log("请求配置出错：", err.message);
    }
  }
}
```

**axios 错误的三层判断**（项目里也常用）：

| 情况 | 怎么判断 | 含义 |
|---|---|---|
| 服务器返回了非 2xx | `err.response` 存在 | 比如 404 找不到、500 服务器崩了 |
| 请求发出但没响应 | `err.request` 存在 | 断网、超时、服务器没回 |
| 请求没发出去 | 都没有 | 配置写错、URL 非法 |

---

## 第 6 章 · 每日练习（题目 + 答案 + 解析）

> 练习文件在 `practice` 文件夹：`geodata.json`（模拟的 GeoJSON 数据）+ `practice.html`（所有练习的可运行版）。
> 打开方式见 [0.4 节](#04-怎么运行本套练习重要)。
> 下面是每道题的**题目、答案和逐行解析**。建议先自己写一遍，实在写不出再看答案。

### 练习 1~5：Promise 五连练（模拟 token → 数据 → 错误捕获）

**练习 1：创建一个 Promise，1 秒后成功**

```js
let p1 = new Promise(function (resolve, reject) {
  setTimeout(function () {
    resolve("1 秒到啦");
  }, 1000);
});
p1.then(function (data) {
  console.log(data);        // 1 秒后输出：1 秒到啦
});
```

**解析**：`new Promise((resolve, reject) => {...})` 里放异步操作；1 秒后调用 `resolve("1 秒到啦")`，Promise 从 pending 变成 fulfilled；`.then` 的回调拿到 `"1 秒到啦"`。

---

**练习 2：模拟失败，用 .catch 捕获**

```js
let p2 = new Promise(function (resolve, reject) {
  setTimeout(function () {
    reject(new Error("模拟：服务器 500 错误"));
  }, 500);
});
p2.then(function (data) {
  console.log("不会执行", data);     // 这行不会执行
}).catch(function (err) {
  console.log("捕获到错误：", err.message);   // 输出：捕获到错误：模拟：服务器 500 错误
});
```

**解析**：`reject(错误)` 让 Promise 变成 rejected；`.then` 不会执行（它只管成功）；`.catch` 接住错误并打印 `err.message`（错误信息文本）。

---

**练习 3：Promise 链 —— 先请求 token，再用 token 请求数据**

```js
function getToken() {
  return new Promise(function (resolve) {
    setTimeout(function () { resolve("token-abc123"); }, 500);
  });
}
function getData(token) {
  return new Promise(function (resolve) {
    setTimeout(function () { resolve("用 " + token + " 换来的数据"); }, 500);
  });
}

getToken()
  .then(function (token) {
    console.log("第 1 步：", token);          // 第 1 步：token-abc123
    return getData(token);                   // ★ 关键：return 新 Promise
  })
  .then(function (data) {
    console.log("第 2 步：", data);           // 第 2 步：用 token-abc123 换来的数据
  });
```

**解析**：第一个 `.then` 里 `return getData(token)`，把新 Promise 交还给链条，第二个 `.then` 拿到它的结果。**不 return 的话，第二个 .then 拿到的会是 undefined**。

---

**练习 4：链条中间失败，观察错误如何被统一捕获**

```js
function getTokenFail() {
  return new Promise(function (resolve, reject) {
    setTimeout(function () { reject(new Error("获取 token 失败（网络断开）")); }, 400);
  });
}

getTokenFail()
  .then(function (token) {
    console.log("不会执行：", token);          // 不执行
    return getData(token);
  })
  .then(function (data) {
    console.log("也不会执行：", data);         // 不执行
  })
  .catch(function (err) {
    console.log("捕获到错误：", err.message);   // 捕获到错误：获取 token 失败（网络断开）
  });
```

**解析**：第一步 reject 后，整个链条进入"失败模式"，后面所有 `.then` 全部跳过，直接进 `.catch`。这就是把 `.catch` 挂在链尾的原因：**任何一步出错，都能被它兜住**。

---

**练习 5：用 async/await + try/catch 重写练习 3**

```js
async function main() {
  try {
    let token = await getToken();
    console.log("第 1 步：", token);          // 第 1 步：token-abc123
    let data = await getData(token);
    console.log("第 2 步：", data);           // 第 2 步：用 token-abc123 换来的数据
  } catch (err) {
    console.log("出错：", err.message);
  }
}
main();
```

**解析**：`async` 声明异步函数，`await` 等 Promise 出结果并直接拿到 resolve 的值；任何一步失败都会抛异常并被 `catch` 接住。和练习 3 的链式写法完全等价，但好读得多。

---

### 练习 6：用 axios 请求本地 GeoJSON，输出 features 数组长度

**答案（普通函数版）**：

```js
async function loadGeoJSON() {
  try {
    let res = await axios.get("geodata.json");
    let geojson = res.data;
    console.log("features 数组长度：", geojson.features.length);   // 10
  } catch (err) {
    console.log("请求失败：", err.message);
  }
}
loadGeoJSON();
```

**答案（箭头函数版，等价）**：

```js
const loadGeoJSON = async () => {
  try {
    const res = await axios.get("geodata.json");
    const geojson = res.data;
    console.log("features 数组长度：", geojson.features.length);   // 10
  } catch (err) {
    console.log("请求失败：", err.message);
  }
};
loadGeoJSON();
```

**解析**：`axios.get("geodata.json")` 返回 Promise，`await` 等它完成；`res.data` 是 JSON 解析后的对象；`geojson.features` 是要素数组，`.length` 是长度。**如果请求失败（比如直接双击打开页面），会走 catch 并提示跨域问题**——这是练习 6 故意设计的"坑"。

### 练习 7：用 map 把 features 的 properties 提取为新数组

```js
// 前提：已经拿到 geojson（练习 6 的 res.data）
let allProps = geojson.features.map(function (f) {
  return f.properties;      // 每个要素 → 它的 properties
});
console.log(allProps);
// 输出：[{type:"building",name:"教学楼A",floors:6}, {type:"building",...}, ...] 共 10 个
```

**解析**：`features` 数组每个元素 `f` 是一个要素对象，`f.properties` 是它的属性。`map` 把每个 `f` 映射成 `f.properties`，得到 10 个 properties 组成的新数组。

### 练习 8：用 filter 筛选出 type 为 "building" 的要素

```js
let buildings = geojson.features.filter(function (f) {
  return f.properties.type === "building";
});
console.log("building 数量：", buildings.length);   // 3
console.log(buildings.map(f => f.properties.name));
// 输出：["教学楼A", "图书馆", "实验楼"]
```

**解析**：`filter` 的回调里写判断条件，`=== "building"` 为 true 的留下。结果是 3 个（教学楼A、图书馆、实验楼）。最后一行又用了一次 `map` 只取名字，展示"map + filter 组合使用"。

### 练习 9：用 reduce 统计不同 type 的要素数量

```js
let typeCount = geojson.features.reduce(function (acc, f) {
  let t = f.properties.type;
  acc[t] = (acc[t] || 0) + 1;      // 关键行
  return acc;
}, {});                            // 初始值：空对象

console.log(typeCount);
// 输出：{ building: 3, road: 3, water: 2, tree: 2 }
```

**解析**：`acc` 从 `{}` 开始。每遇到一个要素，取它的 `type` 当键：第一次遇到 `building` 时 `acc["building"]` 是 `undefined`，`undefined || 0` 得 0，0+1=1；以后再遇到就累加。跑完整个数组，得到每种 type 的数量。**这是 reduce 最经典的"分组计数"用法，一定要背会。**

---

## 附录 A · 三天学习计划表

| 天数 | 学习内容 | 用时建议 | 做完的成果 |
|---|---|---|---|
| Day 1 | 第 0 步环境准备 + 第 1 章变量与数据类型 + 第 2 章数组方法 | 3~4 小时 | 能看懂 let/const、基本/引用类型；会写 map/filter/find/reduce |
| Day 2 | 第 3 章解构展开 + 第 4 章异步核心 | 3~4 小时 | 看懂 Promise 状态、.then 链、async/await；完成练习 1~5 |
| Day 3 | 第 5 章 axios + 第 6 章练习 6~9 | 3 小时 | 跑通本地 GeoJSON 请求，用 map/filter/reduce 处理数据 |

**学习建议**：
1. **每段代码都手敲一遍**（不要复制粘贴），敲错了报错也是学习
2. 控制台是你最好的老师：写一行，跑一行，看结果
3. 练习先自己做，卡住 10 分钟再看答案
4. 全部完成后，把 practice.html 里的练习代码"抄"到一个新文件里，去掉注释，看自己能不能写出来

## 附录 B · 常见报错自救手册

| 报错信息 | 什么意思 | 怎么办 |
|---|---|---|
| `ReferenceError: xxx is not defined` | 用了没声明过的变量 | 检查变量名拼写，或有没有声明 |
| `TypeError: Cannot read properties of undefined` | 对 undefined 取属性了（比如 `undefined.length`） | 说明你访问的对象不存在，先 `console.log` 看看它到底是什么 |
| `Assignment to constant variable` | 给 const 重新赋值了 | 把 const 改成 let，或确认你确实想改 |
| `Unexpected token` / `SyntaxError` | 语法错误，多半是漏了括号、引号、逗号 | 检查括号成对、字符串引号闭合 |
| `Failed to fetch` / `Network Error` | 请求失败 | 确认本地服务器开了、URL 对不对、是不是直接双击打开页面了 |
| axios 相关报错 `err.response` 有值 | 服务器返回了错误状态码 | 看 `err.response.status`（404/500 等）和 `err.response.data` |

## 附录 C · 术语小词典

| 术语 | 大白话解释 |
|---|---|
| 变量 | 给数据起的名字 |
| 常量（const） | 不能重新赋值的变量 |
| 基本类型 | 存值本身的数据（数字、字符串等 7 种） |
| 引用类型 | 存地址的对象（对象、数组、函数） |
| 数组 | 一列数据，用 [] 包着 |
| 回调函数 | 传给另一个函数、由它回头调用的函数 |
| 箭头函数 | 匿名函数的简写：`(x) => x * 2` |
| 异步 | 不等结果、先干别的，结果回来再处理 |
| Promise | 管理异步的"欠条"，三种状态 pending/fulfilled/rejected |
| resolve / reject | 让 Promise 成功 / 失败 |
| .then / .catch | 拿成功结果 / 接失败错误 |
| async/await | 让异步代码像同步一样好读的语法糖 |
| try/catch | 捕获并处理错误的语法 |
| 拦截器 | axios 里统一处理请求/响应的"检查站" |
| GeoJSON | 用 JSON 描述地理数据（点线面要素）的标准格式 |

---

### 自测题答案

1. `const a = [1,2]; a.push(3);` —— **合法**。`a` 现在是 `[1, 2, 3]`。const 只是不能重新赋值（`a = ...`），数组里的内容可以改。
2. `x` 是 **5**。`let y = x` 把 x 的**值**（5）复制给 y，之后 y 改多少都不影响 x。这是基本类型"按值传递"。
3. 用 `Array.isArray(x)` 返回 true 就是数组。`typeof` 对数组返回 `"object"`，不能用它判断。

---

> **写在最后**：三天学完这些，你已经有能力读懂 WebGIS 项目里大部分 JS 代码了。接下来最有效的做法是：打开一个真实的 Cesium 示例（比如加载 GeoJSON 数据的官方 Demo），把你学到的 axios + 数组方法 + async/await 套进去看。**看十遍不如写一遍，写十遍不如跑一遍。**