[中文](README_CN.md)

# Chii

[![NPM version][npm-image]][npm-url]
[![Build status][ci-image]][ci-url]
[![License][license-image]][npm-url]

[npm-image]: https://img.shields.io/npm/v/chii?style=flat-square
[npm-url]: https://npmjs.org/package/chii
[ci-image]: https://img.shields.io/github/workflow/status/liriliri/chii/CI?style=flat-square
[ci-url]: https://github.com/liriliri/chii/actions/workflows/main.yml
[license-image]: https://img.shields.io/npm/l/chii?style=flat-square

Remote debugging tool like [weinre](https://people.apache.org/~pmuellr/weinre/docs/latest/Home.html), replacing web inspector with the latest [chrome devtools frontend](https://github.com/ChromeDevTools/devtools-frontend).

![Chii](https://res.liriliri.io/chii/screenshot.jpg)

## Demo

![Demo](https://res.liriliri.io/chii/qrcode.png)

Browse it on your phone: [https://chii.liriliri.io/test/demo.html](https://chii.liriliri.io/test/demo.html)

Open [https://chii.liriliri.io/](https://chii.liriliri.io/) and click inspect to start debugging the demo page.

In order to try it for different sites, execute the script below on browser address bar.

```javascript
javascript:(function () { var script = document.createElement('script'); script.src="//chii.liriliri.io/target.js"; document.body.appendChild(script); })();
```

## Install

You can get it on npm.

```bash
npm install chii -g
```

## Usage

Start the server with the following command.

```bash
chii start -p 8080
```

Use this script to inject the target code into your webpage.

```html
<script src="//host-machine-ip:8080/target.js"></script>
```

Then browse to localhost:8080 to start debugging your page.

## Related Projects

* [whistle.chii](https://github.com/liriliri/whistle.chii): Whistle Chii plugin.
* [chobitsu](https://github.com/liriliri/chobitsu): Chrome devtools protocol JavaScript implementation.

## 搭建本地环境

1. 拉取 Chrome DevTools frontend 最新代码
```sh
$ npm run init:front_end
```

2. 构建 Chrome DevTools frontend 并复制到 public 目录
```sh
$ npm run dev:front_end
```

3. 启动调试服务
```
$ node bin/chii.js start -p 8080
```
访问 [http://localhost:8080/](http://localhost:8080/)

### 遇到的问题及解决方法

- 没有 autoninja 命令

```sh
$ git clone https://chromium.googlesource.com/chromium/tools/depot_tools.git
```

在 ~/.bash_profile 加入 `export PATH=$PATH:/path/to/depot_tools`
```sh
$ source ~/.bash_profile
```

- 遇到 `unable to get local issuer certificate` 异常

给 `devtools/devtools-frontend/scripts/deps/download_emscripten.py` 增加代码忽略 ssl 校验
```python
import ssl 
ssl._create_default_https_context = ssl._create_unverified_context
```

然后运行

```sh
$ npm run init:front_end_try
```