# 构建与发布

## 构建

当项目开发完毕，只需要运行一行命令就可以打包你的应用：

```bash
# 打包正式环境
pnpm run build
```
> `pnpm run build` 会根据 `/.env.production` 中的 `MICRO_BUILD_MAIN` 配置进行构建默认是`all`。

构建打包成功之后，会在根目录生成 `dist` 文件夹，里面就是构建打包好的文件，通常是 :

```sh
├── dist                    
│   ├── 主框架目录1
│   │   ├── child              # 子项目上级目录
│   │   │   ├── 子项目目录1
│   │   │   ├── 子项目目录...
│   │   ├── css                # 主框架css
│   │   ├── img                # 主框架img
│   │   ├── js                 # 主框架js
│   │   └── index.html         # 主框架index.html
│   ├── 主框架目录2
│   │   ├── child              # 子项目上级目录
│   │   │   ├── 子项目目录1
│   │   │   ├── 子项目目录...
│   │   ├── css                # 主框架css
│   │   ├── img                # 主框架img
│   │   ├── js                 # 主框架js
│   │   └── index.html         # 主框架index.html
│   ├── 主框架目录...

```

如果需要自定义构建，比如指定 `dist` 目录等，则需要通过 `/scripts/config/constants.ts` 的 `BUILD_NAME` 参数进行配置。

## 发布

对于发布来讲，只需要将最终生成的静态文件，也就是通常情况下 `dist` 文件夹的静态文件发布到你的 cdn 或者静态服务器即可，需要注意的是其中的 `index.html` 通常会是你后台服务的入口页面。

项目中，前端路由使用的是 `vue-router` 的 `browserHistory ` 方式，所以需要服务端做一个映射，比如

nginx

```bash
server {
  listen       8080;
  server_name  localhost;

  location / {
    # root   html;
    # index  index.html index.htm;
    try_files $uri $uri/ /index.html;
  }

  location /child/system {
    # root   html;
    # index  index.html index.htm;
    try_files $uri $uri/ /child/system/index.html;
  }
  # article 和 links 等其他子项目的history 配置同上
}

```

