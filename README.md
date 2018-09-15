# 一、vue-project for JavaScript
## 1、安装 webpack
```
 npm install webpack webpack-cli -g
 ```
 
 ## 2、安装 vue-cli
 ```
 npm install -g vue-cli
 ```
 
 ## 3、用vue-cli来构建项目
 ```
 vue init webpack projectName
 ```
 
 ## 4、安装依赖
 ```
 cd projectName
 npm install
```
 
 ## 5、启动项目
 ```
 npm run dev
 ```
 
 ## 6、打包上线
 ```
 npm run build
```


# 二、vue-project for TypeScript

- 编辑器 强烈建议您使用 Visual Studio Code
https://github.com/Microsoft/TypeScript-Vue-Starter

## 1、创建新工程
```
$ mkdir vue-waiter
$ cd vue-waiter
$ mkdir dist
$ mkdir src
$ cd src
$ mkdir components
$ cd ..
```
## 2、 初始化项目
```
npm init
```
## 3、安装依赖
```
$ yarn add --dev typescript webpack ts-loader css-loader vue vue-loader vue-template-compiler serve
```

## 4、添加TypeScript配置文件 tsconfig.json
```
{
    "compilerOptions": {
        "outDir": "./built/",
        "sourceMap": true,
        "strict": true,
        "noImplicitReturns": true,
        "module": "es2015",
        "moduleResolution": "node",
        "target": "es5"
    },
    "include": [
        "./src/**/*"
    ]
}
```

## 5、添加 Webpack配置文件 webpack.config.js
```
var path = require('path')
var webpack = require('webpack')

module.exports = {
  entry: './src/index.ts',
  output: {
    path: path.resolve(__dirname, './dist'),
    publicPath: '/dist/',
    filename: 'build.js'
  },
  module: {
    rules: [
      {
        test: /\.vue$/,
        loader: 'vue-loader',
        options: {
          loaders: {
            // Since sass-loader (weirdly) has SCSS as its default parse mode, we map
            // the "scss" and "sass" values for the lang attribute to the right configs here.
            // other preprocessors should work out of the box, no loader config like this necessary.
            'scss': 'vue-style-loader!css-loader!sass-loader',
            'sass': 'vue-style-loader!css-loader!sass-loader?indentedSyntax',
          }
          // other vue-loader options go here
        }
      },
      {
        test: /\.tsx?$/,
        loader: 'ts-loader',
        exclude: /node_modules/,
        options: {
          appendTsSuffixTo: [/\.vue$/],
        }
      },
      {
        test: /\.(png|jpg|gif|svg)$/,
        loader: 'file-loader',
        options: {
          name: '[name].[ext]?[hash]'
        }
      }
    ]
  },
  resolve: {
    extensions: ['.ts', '.js', '.vue', '.json'],
    alias: {
      'vue$': 'vue/dist/vue.esm.js'
    }
  },
  devServer: {
    historyApiFallback: true,
    noInfo: true
  },
  performance: {
    hints: false
  },
  devtool: '#eval-source-map'
}

if (process.env.NODE_ENV === 'production') {
  module.exports.devtool = '#source-map'
  // http://vue-loader.vuejs.org/en/workflow/production.html
  module.exports.plugins = (module.exports.plugins || []).concat([
    new webpack.DefinePlugin({
      'process.env': {
        NODE_ENV: '"production"'
      }
    }),
    new webpack.optimize.UglifyJsPlugin({
      sourceMap: true,
      compress: {
        warnings: false
      }
    }),
    new webpack.LoaderOptionsPlugin({
      minimize: true
    })
  ])
}
```
## 6、添加生成脚本 
在package.json文件中修改
```
"scripts": {
    "dev": "webpack --watch & node node_modules/serve/bin/serve",
    "build": "webpack",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
```

## 7、创建一个基本项目
- 在项目根目录下 src 中创建 index.ts
```
// src/index.ts

import Vue from "vue";

let v = new Vue({
    el: "#app",
    template: `
    <div>
        <div>Hello {{name}}!</div>
        Name: <input v-model="name" type="text">
    </div>`,
    data: {
        name: "World"
    }
});
```
- 在项目根目录下创建 index.html
```
<!doctype html>
<html>
<head></head>

<body>
    <div id="app"></div>
</body>
<script src="./dist/build.js"></script>

</html>
```

## 8、创建一个组件
```
// src/components/Hello.ts

import Vue from "vue";

export default Vue.extend({
    template: `
        <div>
            <div>Hello {{name}}{{exclamationMarks}}</div>
            <button @click="decrement">-</button>
            <button @click="increment">+</button>
        </div>
    `,
    props: ['name', 'initialEnthusiasm'],
    data() {
        return {
            enthusiasm: this.initialEnthusiasm,
        }
    },
    methods: {
        increment() { this.enthusiasm++; },
        decrement() {
            if (this.enthusiasm > 1) {
                this.enthusiasm--;
            }
        },
    },
    computed: {
        exclamationMarks(): string {
            return Array(this.enthusiasm + 1).join('!');
        }
    }
});

```
## 9、运行项目完善index.ts
```
// src/index.ts

import Vue from "vue";
import HelloComponent from "./components/Hello";

let v = new Vue({
    el: "#app",
    template: `
    <div>
        Name: <input v-model="name" type="text">
        <hello-component :name="name" :initialEnthusiasm="5" />
    </div>
    `,
    data: { name: "World" },
    components: {
        HelloComponent
    }
});
```

## 10、运行项目
```
npm run dev
```
- 在浏览器地址栏输入  http://localhost:5000/ 访问



# 三、vue-project for TypeScript （cli）

- 编辑器 强烈建议您使用 Visual Studio Code
https://github.com/Microsoft/TypeScript-Vue-Starter

## 1、安装 Vue CLI 3
```
npm install --global @vue/cli
```

## 2、创建新工程
```
vue create vue-waiter
? Please pick a preset: default (babel, eslint)
? Pick the package manager to use when installing dependencies: Yarn

$ cd vue-waiter
$ yarn serve
```
## 3、工程目录结构
 ```
vue-waiter
  babel.config.js
  node_modules
  package.json
  public
  src
  yarn.lock
```
## 4、安装依赖
```
$ cd vue-waiter
$ yarn add --dev typescript webpack ts-loader css-loader vue vue-loader vue-template-compiler serve
```

## 5、添加TypeScript配置文件 tsconfig.json
```
{
    "compilerOptions": {
        "outDir": "./built/",
        "sourceMap": true,
        "strict": true,
        "noImplicitReturns": true,
        "module": "es2015",
        "moduleResolution": "node",
        "target": "es5"
    },
    "include": [
        "./src/**/*"
    ]
}
```

## 6、添加 Webpack配置文件 webpack.config.js
```
var path = require('path')
var webpack = require('webpack')

module.exports = {
  entry: './src/index.ts',
  output: {
    path: path.resolve(__dirname, './dist'),
    publicPath: '/dist/',
    filename: 'build.js'
  },
  module: {
    rules: [
      {
        test: /\.vue$/,
        loader: 'vue-loader',
        options: {
          loaders: {
            // Since sass-loader (weirdly) has SCSS as its default parse mode, we map
            // the "scss" and "sass" values for the lang attribute to the right configs here.
            // other preprocessors should work out of the box, no loader config like this necessary.
            'scss': 'vue-style-loader!css-loader!sass-loader',
            'sass': 'vue-style-loader!css-loader!sass-loader?indentedSyntax',
          }
          // other vue-loader options go here
        }
      },
      {
        test: /\.tsx?$/,
        loader: 'ts-loader',
        exclude: /node_modules/,
        options: {
          appendTsSuffixTo: [/\.vue$/],
        }
      },
      {
        test: /\.(png|jpg|gif|svg)$/,
        loader: 'file-loader',
        options: {
          name: '[name].[ext]?[hash]'
        }
      }
    ]
  },
  resolve: {
    extensions: ['.ts', '.js', '.vue', '.json'],
    alias: {
      'vue$': 'vue/dist/vue.esm.js'
    }
  },
  devServer: {
    historyApiFallback: true,
    noInfo: true
  },
  performance: {
    hints: false
  },
  devtool: '#eval-source-map'
}

if (process.env.NODE_ENV === 'production') {
  module.exports.devtool = '#source-map'
  // http://vue-loader.vuejs.org/en/workflow/production.html
  module.exports.plugins = (module.exports.plugins || []).concat([
    new webpack.DefinePlugin({
      'process.env': {
        NODE_ENV: '"production"'
      }
    }),
    new webpack.optimize.UglifyJsPlugin({
      sourceMap: true,
      compress: {
        warnings: false
      }
    }),
    new webpack.LoaderOptionsPlugin({
      minimize: true
    })
  ])
}
```
## 7、添加生成脚本 
在package.json文件中修改
```
"scripts": {
     "dev": "webpack --watch & node node_modules/serve/bin/serve",
    "build": "webpack",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
```
## 8、

## 6、运行项目
```
npm ru
```
- 在浏览器地址栏输入  http://localhost:5000/ 访问
```
$ yarn serve
```
- 在浏览器地址栏输入  http://localhost:8080/ 访问



## 4、TypeScript在Vue中基本用法


