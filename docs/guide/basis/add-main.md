# 新增主框架

## 复制现有vue主框架（添加一个main-oa主框架为例）

1、在根目录下复制`main`主框架重命名为`main-oa`。

2、在`/package.json`中的scripts中添加以下命令：

```sh
"scripts": {
  "serve:main-oa": "pnpm run -C main-oa serve",
  "build:main-oa": "pnpm run -C main-oa build",
},
```

3、在`/package.json` 的`workspaces`参数下追加框架目录名`main-oa`

4、在`/pnpm-workspace.yaml` 的`packages`下追加框架目录名`main-oa`

5、在`/scripts/config/index.ts`中添加如下配置:

```ts
// 在主框架配置中追加
export const mainProjectConfig: Record<string, MainProjectConfigItem> = {
  'main-oa': {
    buildChildParentName: process.env.MICRO_BUILD_CHILD_NAME,
    rootDir: 'main-oa',
    outputDir: 'dist',
    serveRun: 'serve:main-oa',
    buildRun: 'build:main-oa',
    subproject: [ // 此框架需要的子项目
      'system',
      'article',
    ]
  }
}

```

6、修改新主框架入口文件 `/main-oa/src/main.ts`:

```ts
- const Apps = childProjectAll('main',{parentRouter: router, parentStore: store});
// 上面替换为下面
+ const Apps = childProjectAll('main-oa',{parentRouter: router, parentStore: store});
```

7、在新主框架`main-oa/src/layouts/QiankunLayout/routes.ts`中增删路由,如：

```ts
const QiankunLayoutRoutes: Array<RoutesDataItem> = [
  {
    icon: 'menu-links',
    title: 'qiankun-layout.menu.links',
    path: '/links',
    redirect: '/links/list',
    roles: ['links'],
    component: BlankLayout,
    children: [
      {
        title: 'qiankun-layout.menu.links.list',
        path: 'list',
        roles: ['links-list'],
        component: QianKunStartScreen
      },
    ]
  },
]
```

8、运行测试


