# 新增子项目

## 复制现有vue子项目（添加一个links子项目为例）


1、复制`/packages/article`子项目重命名为`/packages/links`。

2、在`/package.json`中的scripts中添加以下命令：

```sh
"scripts": {
  "serve:links": "pnpm run serve -C packages/links",
  "build:links": "pnpm run build -C packages/links",
},
```

3、在`/.env.developent`、`/.env.production`中添加如下配置：

```sh
# 子项目 links
# 子项目目录名
MICRO_LINKS_ROOT_DIR=links
# 开发环境端口
MICRO_LINKS_PORT=8001
# 开发localhost或者ip
MICRO_LINKS_HOST=localhost
```

4、在`/scripts/config/index.ts`中添加如下配置:

```ts
// 在子框架配置childProjectConfig中追加
export const childProjectConfig: Record<string, ChildProjectConfigItem> = {
  'links': {
    rootDir: process.env.MICRO_LINKS_ROOT_DIR,
    outputDir: 'dist',
    host: process.env.MICRO_LINKS_HOST,
    port: Number(process.env.MICRO_LINKS_PORT || 0),
    serveRun: 'serve:links',
    buildRun: 'build:links'
  },
}

// 在主框架配置中，哪个主框架需要就在哪个主框架subproject下添加
export const mainProjectConfig: Record<string, MainProjectConfigItem> = {
  'main': {
    subproject: [
      'links',
    ]
  }
}

```

5、修改子项目vue配置：

- `/packages/links/vue.config.js`中，把 `MICRO_ARTICLE_` 前缀替换成 `MICRO_LINKS_`
- `/packages/links/vue.config.js`中，把 `article` 替换成 `links`
- `/packages/links/vue.config.js`中，把 `8077` 端口号替换成新端口号如 `8001`
- `/packages/links/.env.**`中，把 `VUE_APP_PORT` 端口号替换成新端口号如 `8001`

> 至此基本完成，你可以在此项目下运行`pnpm install`、`pnpm run serve`进行测试。

6、子项目删除不需要的页面和路由如`add`、`edit`等等，添加新的页面和路由（可以参照[admin-element-vue文档](http://admin-element-vue.liqingsong.cc/tsv2/)）。

7、在你需要的主框架中配置`links`子项目的路由，以主框架`/main/src/layouts/QiankunLayout/routes.ts`为例：

```ts
// 追加如下代码
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

8、运行框架进行测试`pnpm run serve`。

