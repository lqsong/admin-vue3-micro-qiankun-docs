# 介绍


`admin-vue3-micro-qiankun` [![GitHub stars](https://img.shields.io/github/stars/lqsong/admin-vue3-micro-qiankun.svg?style=social&label=Stars)](https://github.com/lqsong/admin-vue3-micro-qiankun)是一个微前端后台解决方案，它基于 [Qiankun.js](https://qiankun.umijs.org/) 结合 [admin-element-vue](http://admin-element-vue.liqingsong.cc/) 和 [admin-antd-vue](http://admin-antd-vue.liqingsong.cc)实现。它使用了最新的前端技术栈、多主框架、多子框架、动态路由、权限验证、国际化、Mock 数据等，它可以帮助你快速搭建企业级微前端中台产品原型。相信不管你的需求是什么，本项目都能帮助到你。


## 功能

```
- 登录 / 注销 / 注册

- 权限验证
  - 页面权限
  - 按钮操作
  - 权限配置

- 全局功能
  - 国际化多语言
  - 黑白主题
  - 动态侧边栏（支持多级路由嵌套）
  - 动态面包屑（支持自定义配置）
  - tabNav
  - Svg Sprite 图标
  - Mock 数据
  - 权限验证

- 综合实例
  - 引导页
  - main主框架（基于admin-element-vue调整）
  - main-antd主框架（基于admin-antd-vue调整）
  - System子项目（基于admin-element-vue调整）
  - Article子项目（基于admin-element-vue调整）
  - Links子项目 （基于admin-antd-vue调整） 
  
```

| [main-demo](http://main-demo.admin-vue3-micro-qiankun.liqingsong.cc/)  |
:-------------------------:
| [main-antd-demo](http://main-antd-demo.admin-vue3-micro-qiankun.liqingsong.cc/)  |
| ![Home](/images/index.png)  |



## 前序准备

在开始之前，推荐先学习  [pnpm](https://pnpm.io/) 、[Qiankun.js](https://qiankun.umijs.org/) 、 [TypeScript](https://github.com/Microsoft/TypeScript) 、[admin-element-vue](http://admin-element-vue.liqingsong.cc/) 和 [admin-antd-vue](http://admin-antd-vue.liqingsong.cc) ，提前了解和学习这些知识会对使用本项目有很大的帮助，因为本项目技术栈都是基于它们。并且你需要在本地安装 [node 版本10.13 或以上](http://nodejs.org/) 和 [git](https://git-scm.com/)。

**本项目不支持低版本浏览器(如 ie)**

## 目录结构

本项目已经为你生成了一个完整的开发框架，下面是整个项目的目录结构。

```bash
├── main                       # main主框架Demo（基于admin-element-vue调整）
├── main-antd                  # main-antd主框架Demo（基于admin-antd-vue调整）
├── packages                   # 子项目工作空间 (基于pnpm-workspace工作空间 )
│   ├── article                # 文章管理子项目Demo（基于admin-element-vue调整）
│   ├── links                  # 友情链接子项目Demo（基于admin-antd-vue调整）
│   └── system                 # 系统设置子项目Demo（基于admin-element-vue调整）
├── scripts                    # pnpm scripts 配置
│   ├── config                 # 配置目录
│   │   ├── constants.ts       # 静态变量文件
│   │   ├── index.ts           # 配置入口
│   │   └── paths.ts           # 路径配置
│   ├── server                 # 基于qiankun自定义后的server
│   │   │── env.js             # .env 功能
│   │   │── qiankun.ts         # 基于qiankun.js定义的方法
│   │   └── qiankunActions.ts  # qiankun.js 全局状态
│   ├── utils                  
│   ├── gulpbuild.ts           # 构建
│   ├── gulpinit.ts            # gulp init
│   └── gulpserve.ts           # 开发
├── typings                    # ts配置
├── .editorconfig              # 编辑器配置
├── .env.development           # 开发环境变量配置
├── .env.production            # 生产环境变量配置
├── .gitignore                 # babel-loader 配置
├── package.json               # 项目信息
├── pnpm-workspace.yaml        # pnpm workspace 配置
├── README.md                  # readme
└── tsconfig.json              # TypeScript 配置
```

## 安装

```bash
# 克隆项目
git clone https://github.com/lqsong/admin-vue3-micro-qiankun.git

# 进入项目目录
cd admin-vue3-micro-qiankun

# 复制文件
copy .env.development  .env.development.local # 启用或修改里面的参数

# 安装依赖，请使用 pnpm
pnpm install

# 本地开发 启动项目
pnpm run serve # 根据.env.development 中 MICRO_SERVE_MAIN 配置来启动框架,默认all
```

> 请使用 pnpm , **[pnpm的安装与使用](http://liqingsong.cc/article/detail/26)** 。


<br/>

如果`.env.development` 中 `MICRO_SERVE_MAIN=all` 后启动所有主框架和子项目，你可以打开浏览器访问 [http://localhost:8080](http://localhost:8080)、[http://localhost:9090](http://localhost:9090) 两个主框架地址， 你看到下面的页面就代表操作成功了。

![Home](/images/index.png)

接下来你可以修改代码进行业务开发了，本项目内基于 [admin-element-vue](http://admin-element-vue.liqingsong.cc/) 和 [admin-antd-vue](http://admin-antd-vue.liqingsong.cc) 分别创建了主框架和子项目的Demo来辅助开发，你可以继续阅读和探索左侧的其它文档。

:::tip 注意
`.env.development` 中 `MICRO_SERVE_MAIN=all` 会启动所有主框架和子项目，你可以修改此参数，如：`main` 指定启动主框架，他只会启动此主框架和其下需要的子项目。

或者你可以不运行`pnpm run serve`，单独运行如：`pnpm run serve:main`、`pnpm run serve:article`来进行开发，这样可以减轻因启动太多服务电脑卡顿。
:::


## Contribution

本文档项目地址 [admin-vue3-micro-qiankun-docs](https://github.com/lqsong/admin-vue3-micro-qiankun-docs) 基于 [vuepress](https://github.com/vuejs/vuepress)开发。

有任何修改和建议都可以该项目 pr 和 issue

[admin-vue3-micro-qiankun](https://github.com/lqsong/admin-vue3-micro-qiankun) 还在持续迭代中，逐步沉淀和总结出更多功能和相应的实现代码，总结中后台产品模板/组件/业务场景的最佳实践。本项目也十分期待你的参与和[反馈](https://github.com/lqsong/admin-vue3-micro-qiankun/issues)。

## 捐赠

如果你觉得这个项目帮助到了你，请帮助 [![GitHub stars](https://img.shields.io/github/stars/lqsong/admin-vue3-micro-qiankun.svg?style=social&label=Stars)](https://github.com/lqsong/admin-vue3-micro-qiankun)，你也可以请作者喝咖啡表示鼓励 :coffee:

**ALIPAY**             |  **WECHAT**
:-------------------------:|:-------------------------:
![Alipay](http://uploads.liqingsong.cc/20210430/f62d2436-8d92-407d-977f-35f1e4b891fc.png)  |  ![Wechat](http://uploads.liqingsong.cc/20210430/3e24efa9-8e79-4606-9bd9-8215ce1235ac.png)
