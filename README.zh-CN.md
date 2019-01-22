
# myou-vue-admin

> 本模板工程为快速开发后端管理平台而设计。
基于vue-element-admin框架，为适应公司业务形态进行的二次开发，能让开发者从搭建工程到发布做到开箱即用。

## 简介

[myou-vue-admin](https://github.com/leesny/myou-vue-admin) 是一个后台集成解决方案，它基于 [vue](https://github.com/vuejs/vue) 、 [element](https://github.com/ElemeFE/element)、[vue-element-admin](https://github.com/PanJiaChen/vue-element-admin)。它使用了最新的前端技术栈，内置了 i18 国际化解决方案，动态路由，权限验证，提炼了典型的业务模型，提供了丰富的功能组件，它可以帮助你快速搭建企业级中后台产品原型。相信不管你的需求是什么，本项目都能帮助到你。

- [原官方在线访问](http://panjiachen.github.io/vue-element-admin)

- [原官方使用文档](https://panjiachen.github.io/vue-element-admin-site/zh/)


**注意：该项目使用 element-ui@2.3.0+ 版本，所以最低兼容 vue@2.5.0+**

**从`v3.8.0`开始使用`webpack4`。所以若还想使用`webpack3`开发，请使用该分支[webpack3](https://github.com/PanJiaChen/vue-element-admin/tree/webpack3)**

**该项目不支持低版本浏览器(如 ie)，有需求请自行添加 polyfill [详情](https://github.com/PanJiaChen/vue-element-admin/wiki#babel-polyfill)**


## 前序准备

你需要在本地安装 [node](http://nodejs.org/) 和 [git](https://git-scm.com/)。
本项目技术栈基于 [ES2015+](http://es6.ruanyifeng.com/)、[vue](https://cn.vuejs.org/index.html)、[vuex](https://vuex.vuejs.org/zh-cn/)、[vue-router](https://router.vuejs.org/zh-cn/) 、[axios](https://github.com/axios/axios) 和 [element-ui](https://github.com/ElemeFE/element)，所有的请求数据都使用[Mock.js](https://github.com/nuysoft/Mock)模拟，提前了解和学习这些知识会对使用本项目有很大的帮助。

## 功能

```
- 登录 / 注销

- 权限验证
  - 页面权限
  - 指令权限
  - 二步登录

- 多环境发布
  - dev sit stage prod

- 全局功能
  - 国际化多语言
  - 多种动态换肤
  - 动态侧边栏（支持多级路由嵌套）
  - 动态面包屑
  - 快捷导航(标签页)
  - Svg Sprite 图标
  - 本地mock数据
  - Screenfull全屏
  - 自适应收缩侧边栏

- 编辑器
  - 富文本
  - Markdown
  - JSON 等多格式

- Excel
  - 导出excel
  - 导出zip
  - 导入excel
  - 前端可视化excel

- 表格
  - 动态表格
  - 拖拽表格
  - 树形表格
  - 内联编辑

- 错误页面
  - 401
  - 404

- 組件
  - 头像上传
  - 返回顶部
  - 拖拽Dialog
  - 拖拽Select
  - 拖拽看板
  - 列表拖拽
  - SplitPane
  - Dropzone
  - Sticky
  - CountTo

- 综合实例
- 错误日志
- Dashboard
- 引导页
- ECharts 图表
- Clipboard(剪贴复制)
- Markdown2html
```

## 开发

```bash
# 克隆项目
git clone https://github.com/PanJiaChen/vue-element-admin.git

# 安装依赖
npm install

# 建议不要用 cnpm 安装 会有各种诡异的bug 可以通过如下操作解决 npm 下载速度慢的问题
npm install --registry=https://registry.npm.taobao.org

# 启动服务
npm run dev
```

浏览器访问 http://localhost:9527

## 发布

```bash
# 构建测试环境
npm run build:sit

# 构建生产环境
npm run build:prod
```

## 其它

```bash
# --report to build with bundle size analytics
npm run build:prod

# --generate a bundle size analytics. default: bundle-report.html
npm run build:prod --generate_report

# --preview to start a server in local to preview
npm run build:prod --preview

# lint code
npm run lint

# auto fix
npm run lint -- --fix
```


## [编码规范](/doc/开发规范.md)
> 统一的编码规范，可使代码更易于阅读，易于理解，易于维护。尽量按照ESLint格式要求编写代码，请仔细阅读开发规范文档...

## [踩坑日记](/doc/踩坑日记.md)
> 记录开发中踩坑的技术要点，问题集锦等

## 推荐编辑器
> [Visual Studio Code](https://code.visualstudio.com/)

## git提交信息规范
在提交代码时，应遵守以下规范：

+ 修改的文件如果涉及多个板块，应单独先提交。
+ 提交信息格式：
  - 页面或组件：新增/修改/删除页面名、组件名、utils文件名等（改动点），例如 发票信息页面（修改返回字段）。 SingleInput组件（扩展xxx功能，增加size属性用于设置输入框高度，默认为md [44px]，目前支持lg [54px]）
  - utils：新增/修改/删除文件名(改动点), 例如 新增util/common.js(增加xxx方法)
  - 接口：新增/修改/删除接口名， 例如 删除xxx接口
  - 框架文件：新增/修改/删除/优化/扩展等 功能点（扩展特性说明）  例如 新增scss支持（支持 scss 并兼容css-modules）



更多信息请参考 [使用文档](https://panjiachen.github.io/vue-element-admin-site/zh/)

