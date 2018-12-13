[parcel](https://www.parceljs.cn/getting_started.html)
## 使用
安装

``` bash
yarn global add parcel-bundler
```

创建package.json

``` bash
yarn init -y
```

### 运行

####开发环境

```bash
    parcel index.html
```
默认 http://localhost:1234/   使用```parcel index.html -p < port number>```覆盖端口

####生产环境

```bash
    parcel build index.html
```
设置输出目录:
```bash
parcel build index.html --out-dir build/output
//或者
parcel build index.html -d build/output
```
设置输出路径
```
parcel build entry.js --public-url ./
```

### 入口文件

可以使用任何类型的文件作为入口，但是最好还是使用 HTML 或 JavaScript 文件

### plugins 
js : 默认使用 babel-preset-env . 其他安装并添加配置文件 .babelrc ：

```bash
    yarn add babel-preset-react
```

```bash 
    {
        "presets":[
            "react"
        ]
    }
```

css : 安装plugins ，添加配置文件 .postcssrc || .postcssrc.js || .postcss.config.js ：

```
    yarn add postcss-modules autoprefixer
```
```
{
    "modules": true,
    "plugins": {
        'postcss-pxtorem': {
            rootValue: 50,
            propList: ['*']
        },
        "autoprefixer": {
            "grid": true
        }
    }
}

```

###代码拆分
 通过import()语法动态引入其他模块 ，返回一个promise
 
 ```
 //./page.js
 export function render(){
     
 }
 ```
 ```
 //index.js
    import('./page').then((page)=>{
    console.log(page.render)
})
 ```


### react 配置
 安装react依赖
```
yarn add react
yarn add react-dom
yarn add --dev parcel-bundler
yarn add --dev babel-preset-env
yarn add --dev babel-preset-react
```
添加.babelrc
```
{
  "presets": ["env", "react"]
}
```
