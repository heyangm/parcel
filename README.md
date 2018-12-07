
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
开发环境
```bash
    parcel index.html
```
默认 http://localhost:1234/   使用parcel index.html -p < port number>覆盖端口

生产环境
```bash
    parcel build index.html
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
        "autoprefixer": {
        "grid": true
        }
    }
}
```


