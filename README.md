译文数据库介绍 
==================

[![Build status](https://ci.appveyor.com/api/projects/status/pv3klmx1u7qu4woa?svg=true)](https://ci.appveyor.com/project/EhTagApi-Bot/database)
[![LICENSE](https://img.shields.io/badge/license-by--nc--sa-orange.svg?logo=creative-commons)](LICENSE.md)

## 协议

数据库文本内容除另有声明外，均在[知识共享(Creative Commons) 署名-非商业性使用-相同方式共享 3.0 协议](LICENSE.md)下提供，附加条款亦可能应用。

数据库内容归全体编辑者共同所有，在本项目里发布内容即表示您允许将您编辑的内容无偿且自由地使用到 EhTagTranslation 的各下游项目中。

## 参与翻译

请使用 [EhTag Editor](https://EhTagTranslation.github.io/Editor)，在编辑前请先查阅[参与翻译](CONTRIBUTING.md)指南。

## 使用翻译

### 一般用户

一般用户可通过以下项目使用本数据库的翻译，也可以通过这些项目向本数据库贡献翻译内容。

* [EhTagBuilder](https://github.com/Mapaler/EhTagTranslator/wiki/EhTagBuilder)  
  ![][plat-web]  
  EhTagBuilder 简称 "ETB"。

  翻译实现方式：ETB 先获取 Wiki 数据库网页，获得翻译数据，生成对应格式的 CSS 代码，再由 Stylus 扩展附加到 E 绅士网页上。

* [EhTagSyringe](https://github.com/Mapaler/EhTagTranslator/wiki/EhTagSyringe)  
  ![][plat-web]  
  将 E 绅士标签翻译成中文，并注入到E站体内

  EhTagSyringe 是 EhTagTranslator 主项目下走功能全面、开箱即用路线的子项目。

  按照 EhTagTranslator 思路，重新编写并内置样式注入器,并增加一些方便的功能

  >  H 是人类的第一生产力

* [E-Viewer](https://github.com/OpportunityLiu/E-Viewer)  
  ![][plat-uwp]  
  An UWP Client for <https://e-hentai.org>.

* [EhViewer](https://github.com/seven332/EhViewer)  
  ![][plat-android]  
  An Unofficial E-Hentai Application for Android.

* [Dai-Hentai](https://github.com/DaidoujiChen/Dai-Hentai)  
  ![][plat-ios]  
  一個普通的看漫畫 App。
  
* [E-HentaiViewer](https://github.com/kayanouriko/E-HentaiViewer)  
  ![][plat-ios]  
  一个 E-Hentai 的 iOS 端阅读器。
  
### 开发者

下游项目使用本项目数据库前，请在本项目提交一份附上项目的简介或地址的 Issue。

#### 获取数据库内容

推荐使用 [Github Release](https://github.com/EhTagTranslation/Database/releases)，发布的 JSON 对象格式可参照 [interface.d.ts](tools/interface.d.ts)。

后缀：
- `*.json` 是 JSON 表示的数据库；
- `*.json.gz` 是其 gzip 压缩后的版本；
- `*.js` 是用于 JSONP 调用的脚本，回调函数名为 `load_ehtagtranslation_${前缀}_${中缀}`，由于 GitHub 的跨域限制，浏览器端仅能使用此方案。

中缀：
- `*.raw.*` 包含了 MarkDown 版本的名称、描述和外部链接；
- `*.html.*` 包含了渲染为 HTML 的名称、描述和外部链接；
- `*.text.*` 包含了去除图片和链接的的名称、描述和外部链接；
- `*.ast.*` 包含了 JSON 表示的 MarkDown 的语法树结构；
- `*.full.*` 包含了以上所有信息。

前缀：
- `db.*` 包含了全部内容；
- `diff.*` 包含了本版本和上一版本的 `version`, `head`（分别以 `new`, `old` 区分），并包含了以 [JSONPatch](http://jsonpatch.com/) 格式存储的 `data`。

以下为 node 代码示例。
``` js
const fetch = require('node-fetch');
async function getDownloadLink(owner, repo, filename)
{
    const uri = `https://api.github.com/repos/${owner}/${repo}/releases/latest`;
    const info = await (await fetch(uri)).json();
    const asset = info.assets.find(i => i.name === filename);
    return asset && asset.browser_download_url;
}
const resourceUrl = await getDownloadLink('ehtagtranslation', 'Database', 'db.html.json');
const db = await (await fetch(resourceUrl)).json();
```

也可以使用 git 或 Github API 直接获取 MarkDown 并自行解析，此时需要注意 [`version`](version) 文件表明的[数据库结构版本](database-version-info.md)。

#### 编辑数据库内容

请参考 [EhTagConnector](https://github.com/EhTagTranslation/EhTagConnector)、[EhTag Editor](https://github.com/EhTagTranslation/Editor) 及本项目[参与翻译](CONTRIBUTING.md)指南。

[plat-web]: https://img.shields.io/badge/platform-web-red.svg?logo=javascript
[plat-ios]: https://img.shields.io/badge/platform-iOS-lightgrey.svg?logo=apple
[plat-uwp]: https://img.shields.io/badge/platform-UWP-blue.svg?logo=windows
[plat-android]: https://img.shields.io/badge/platform-Android-brightgreen.svg?logo=android
