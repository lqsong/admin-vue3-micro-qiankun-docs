# 配置

配置是开发一个后台项目的重要环节，它是一个后台项目的基础。想要了解一个后台项目，先要了解它的配置。

## 框架配置

`admin-vue3-micro-qiankun` 内置了一个框架配置文件 `/scripts/config/index.ts`。

```ts
// 主框架配置
export interface MainProjectConfigItem {
  // 主框架项目目录名，也作为生产主应用目录名
  rootDir: string;
  // 主框架项目内部构建目录名
  outputDir: string;
  // 主框架项目的子项目上级目录名
  buildChildParentName: string;
  // 开发命令，需要在框架根目录/package.json中scripts内配置好
  serveRun: string;
  // 构建命令，需要在框架根目录/package.json中scripts内配置好
  buildRun: string;
  // 子项目名称(childProjectConfig的key)数组
  subproject: string[];
}

// 子项目配置
export interface ChildProjectConfigItem {
  // 子项目目录名，也作为生产子应用目录名
  rootDir: string;
  // 子项目内部构建目录名
  outputDir: string;
  // 开发 localhost 或者 ip
  host: string;
  // 开发端口
  port: number;
  // 开发命令，需要在框架根目录/package.json中scripts内配置好
  serveRun: string;
  // 构建命令，需要在框架根目录/package.json中scripts内配置好
  buildRun: string;
}

export const mainProjectConfig: Record<string, MainProjectConfigItem> = {
  'main': {
    buildChildParentName: process.env.MICRO_BUILD_CHILD_NAME,
    rootDir: 'main',
    outputDir: 'dist',
    serveRun: 'serve:main',
    buildRun: 'build:main',
    subproject: [
      'system',
      'article',
      'links',
    ]
  },
  'main-antd': {
    buildChildParentName: process.env.MICRO_BUILD_CHILD_NAME,
    rootDir: 'main-antd',
    outputDir: 'dist',
    serveRun: 'serve:main-antd',
    buildRun: 'build:main-antd',
    subproject: [
      'system',
      'article',
      'links',
    ]
  }
}

export const childProjectConfig: Record<string, ChildProjectConfigItem> = {
  'system': {
    rootDir: process.env.MICRO_SYSTEM_ROOT_DIR,
    outputDir: 'dist',
    host: process.env.MICRO_SYSTEM_HOST,
    port: Number(process.env.MICRO_SYSTEM_PORT || 0),
    serveRun: 'serve:system',
    buildRun: 'build:system'
  },
  'article': {
    rootDir: process.env.MICRO_ARTICLE_ROOT_DIR,
    outputDir: 'dist',
    host: process.env.MICRO_ARTICLE_HOST,
    port: Number(process.env.MICRO_ARTICLE_PORT || 0),
    serveRun: 'serve:article',
    buildRun: 'build:article'
  },
  'links': {
    rootDir: process.env.MICRO_LINKS_ROOT_DIR,
    outputDir: 'dist',
    host: process.env.MICRO_LINKS_HOST,
    port: Number(process.env.MICRO_LINKS_PORT || 0),
    serveRun: 'serve:links',
    buildRun: 'build:links'
  },
}

export default {}

```

## 环境变量

`admin-vue3-micro-qiankun` 自定义了环境变量服务 `/scripts/server/env.js`，可以根据不同模式配置环境变量：

- `development` 模式用于 `pnpm run serve`
- `production` 模式用于 `pnpm run build`

你可以在你的项目根目录中放置下列文件来指定环境变量：

```sh
/.env.development
/.env.development.local
/.env.production
/.env.production.local
```


