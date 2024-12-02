# 自定义数据生成器

一个 Chrome 扩展，用于快速生成和填充表单数据。支持自定义数据生成规则，让测试工作更轻松。

## 主要功能

- ✨ 自定义数据生成规则
- 🖱️ 右键菜单快速填充
- 💾 支持导入导出配置
- 🔍 实时预览生成结果
- 🔗 支持元素绑定生成器
- 🌐 跨域名复用绑定关系
- ⚡ 快捷键支持

## 使用方法

### 1. 安装扩展
1. 下载源代码
2. 打开 Chrome 扩展管理页面 (`chrome://extensions/`)
3. 开启"开发者模式"
4. 点击"加载已解压的扩展程序"，选择源代码目录

### 2. 创建生成器
1. 点击扩展图标
2. 输入生成器名称和生成规则
3. 点击"预览"测试结果
4. 点击"保存"完成创建

### 3. 使用生成器

#### 方式一：右键菜单
1. 在输入框中右键点击
2. 选择"填充数据"
3. 点击要使用的生成器
4. 生成器会自动与该输入框绑定，显示快捷图标

#### 方式二：快捷键
- Alt + 双击：使用默认生成器填充数据

#### 方式三：快捷图标
- 点击输入框右侧的生成器图标即可快速填充数据

### 4. 元素绑定
- 当使用右键菜单选择生成器时，会自动建立输入框与生成器的绑定关系
- 绑定后会在输入框右侧显示生成器图标
- 点击图标可快速生成数据
- 绑定关系会跨域名保存，相同结构的元素在不同网站上可复用

## 代码示例

```javascript
// 示例1：使用 ES6 生成随机中文姓名
const firstNames = ['张', '李', '王', '赵', '钱'];
const lastNames = ['明', '华', '强', '伟', '勇'];
const firstName = firstNames[Math.floor(Math.random() * firstNames.length)];
const lastName = lastNames[Math.floor(Math.random() * lastNames.length)];
return `${firstName}${lastName}`;

// 示例2：使用 ES6 生成随机手机号
const prefix = ['3', '4', '5', '7', '8'];
return `1${prefix[Math.floor(Math.random() * prefix.length)]}${
  Array(9).fill().map(() => Math.floor(Math.random() * 10)).join('')
}`;

// 示例3：使用 ES6 生成随机邮箱
const domains = ['gmail.com', 'yahoo.com', 'hotmail.com', 'outlook.com'];
const chars = 'abcdefghijklmnopqrstuvwxyz0123456789';
const length = 8 + Math.floor(Math.random() * 5);
const name = Array(length).fill()
  .map(() => chars[Math.floor(Math.random() * chars.length)])
  .join('');
return `${name}@${domains[Math.floor(Math.random() * domains.length)]}`;
```

## 注意事项

1. 生成器代码必须包含 return 语句
2. 只能返回字符串或数字类型
3. 直接写方法体，无需写 function 定义
4. 代码在安全的沙箱环境中执行
5. 元素绑定关系会跨域名生效
6. 绑定关系基于元素的结构特征，与域名无关

## 开发相关

### 目录结构
```
├── manifest.json    // 扩展配置
├── popup.html      // 弹窗界面
├── popup.js       // 弹窗逻辑
├── content.js     // 内容脚本
├── background.js  // 后台脚本
├── interpreter.js // 代码解释器
├── icons/        // 图标资源
│   ├── icon16.png
│   ├── icon32.png
│   ├── icon48.png
│   └── icon128.png
└── lib/          // 第三方库
    ├── eval5.js
    └── eval5.min.js
```

### 技术栈

- Chrome Extension API
- JavaScript (ES6+)
- eval5 (安全的代码执行环境)
- Babel (ES6+ 代码转换)

## 配置导入导出

- 点击"导出配置"将所有生成器和绑定关系保存为 JSON 文件
- 点击"导入配置"从 JSON 文件中恢复生成器和绑定关系