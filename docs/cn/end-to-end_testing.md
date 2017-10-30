# 端对端测试

对于端到端测试，electron-vue 使用 [Spectron](http://electron.atom.io/spectron/) 和 测试框架 [Mocha](https://mochajs.org/) \(以及 [Chai](http://chaijs.com/)\)。Mocha 和 Chai 的 API (包括 `expect`、`should` 以及 `assert` 在内) 均在全局范围内可用。

### 运行测试

```bash
# 开始 Mocha
npm run e2e
```

##### 注意

在运行端到端测试之前，为了使 Spectron 在测试的时候可用，请调用 `npm run pack` 来创建一个产品构建。

### 文件结构

```
my-project
├─ test
|  ├─ e2e
│  │  ├─ specs/
│  │  ├─ index.js
└─ └─ └─ utils.js
```

**在大多数情况下，你可以忽略** `index.js` **，只专注于编写** `specs/` **。**

#### `specs/`

这个目录里面是编写实际测试代码的地方。由于 `babel-register` 的强大功能，你可以完全依照 ES2015 进行编写。

#### `index.js`

这是 Mocha 入口文件，并收集加载在 `specs/` 内的所有测试代码用于测试。

#### `utils.js`

在这里，你会发现一些通用的函数，你可以在 `specs/` 中使用。其基本功能包括处理 electron 创建/销毁过程的 `beforeEach` 和 `afterEach`。

### 关于 Spectron

Spectron 是使用 [ChromeDriver](https://sites.google.com/a/chromium.org/chromedriver/) 和 [WebDriverIO](http://webdriver.io/) 来操作 DOM 元素的 [electron]（http://electron.atom.io）官方测试框架。

#### WebDriverIO 的使用

如 Spectron 的 [文档](https://github.com/electron/spectron#client) 中所述，你可以通过访问 `this.app.client` 来访问 [WebDriverIO APIs](http://webdriver.io/api.html)。 由于 electron-vue 使用了 Mocha，`this` 在 `afterEach`、`beforeEach` 和 `it` 之间共享。 因此，值得注意的是，ES2015 的 箭头函数 (arrow function) 不能在某些情况下使用，因为 `this` 的语境将被覆盖 \([更多信息](https://mochajs.org/#arrow-functions)\)。
