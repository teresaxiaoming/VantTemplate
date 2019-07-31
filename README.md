# Vant-demo
Vant 示例工程，基于 vue-cli 3 搭建。

## 目录

### base

base 工程示范了如何用 vant 搭建几个简单的电商页面，包含如下功能：
- 基于 vant 搭建
- 基于 vue-router 的单页面应用
- 组件按需引入
- 视图异步加载

### rem

rem 工程在 base 工程的基础上增加了移动端 rem 适配的配置。（已添加进入了base工程中）

### viewport

viewport 工程在 base 工程的基础上增加了移动端 vw/vh 适配的配置。
- vue.config.js中将rem的pxtorem修改为：
~~~
pxtoviewport({
    viewportWidth: 375,
    // 该项仅在使用 Circle 组件时需要
    // 原因参见 https://github.com/youzan/vant/issues/1948
    selectorBlackList: ['van-circle__layer']
})
~~~
- package.json中安装viewport：
~~~
"devDependencies": {
   "postcss-px-to-viewport": "^1.1.0",
},
~~~

### theme

theme 工程在 base 工程的基础上增加了自定义主题色的配置。
- babel.config.js中配置：
~~~
  plugins: [
    [
      'import',
      {
        libraryName: 'vant',
        libraryDirectory: 'es',
        style: name => `${name}/style/less`
      },
      'vant'
    ]
  ]
~~~
- vue.config.js中配置：
~~~
 css: {
    loaderOptions: {
        less: {
        modifyVars: {
            red: '#03a9f4',
            blue: '#3eaf7c',
            orange: '#f08d49',
            'text-color': '#111'
        }
        }
    }
 }
~~~

### typescript

基于 typescript 的工程，使用 ts-import-plugin 实现组件按需引入。
- 安装ts-import-plugin：
~~~
  "devDependencies": {
    "ts-import-plugin": "^1.5.5",
    "typescript": "^3.5.1",
  },
~~~
- vue.config.js中配置：
~~~
  chainWebpack: config => {
    config.module
      .rule('ts')
      .use('ts-loader')
      .tap(options => {
        options = merge(options, {
          transpileOnly: true,
          getCustomTransformers: () => ({
            before: [
              tsImportPluginFactory({
                libraryName: 'vant',
                libraryDirectory: 'es',
                style: true
              })
            ]
          }),
          compilerOptions: {
            module: 'es2015'
          }
        });
        return options;
      });
  }
~~~



## 开发命令

``` bash
# 安装依赖
# 注意：请切换到对应的子目录下安装
cd base
npm install

# 本地开发
# 通过 localhost:8080 访问页面
npm run serve

# 生产环境构建
npm run build

# 代码格式校验
npm run lint
```
