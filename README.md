# Live2D Widget

![](https://forthebadge.com/images/badges/built-with-love.svg)
![](https://forthebadge.com/images/badges/uses-html.svg)
![](https://forthebadge.com/images/badges/made-with-javascript.svg)
![](https://forthebadge.com/images/badges/contains-cat-gifs.svg)
![](https://forthebadge.com/images/badges/powered-by-electricity.svg)
![](https://forthebadge.com/images/badges/makes-people-smile.svg)

## 特性 Feature

在網頁中添加 Live2D 看板娘。兼容 PJAX，支持無刷新加載。
Add Live2D widget to web page. Compatible with PJAX.

**警告：本項目使用了大量 ES6 語法，不支持 IE 11 等老舊瀏覽器。 **
**WARNING: This project does not support legacy browsers such as IE 11.**

## 示例 Demo

在[米米的博客](https://zhangshuqiao.org)的左下角可查看效果。 （注：以下人物模型僅供展示之用，本倉庫並不包含任何模型。）

<img src="assets/screenshot-2.png" width="280"><img src="assets/screenshot-3.png" width="280"><img src="assets/screenshot-1.png " width="270">

你也可以在允許的範圍內進行二次開發，這裡有一些示例

- [demo.html](https://mi.js.org/live2d-widget/demo/demo.html) ，展現基礎效果
- [login.html](https://mi.js.org/live2d-widget/demo/login.html) ，仿 NPM 的登陸界面

## 依賴 Dependencies

本插件需要 Font Awesome (v4 或 v5) 圖標支持，請確保相關樣式表已在頁面中加載。以 Font Awesome v4 為例，請在 `<head>` 中加入：
Font Awesome (v4 or v5) is required for this plugin. Take Font Awesome v4 as an example, please add the following in `<head>`:
```xml
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/font-awesome/css/font-awesome.min.css">
```
否則圖標將無法正常顯示。 （如果網頁中已經加載了任何版本的 Font Awesome，就不要重複加載了）

## 使用 Usage

將這一行代碼加入 `<head>` 或 `<body>`，即可展現出效果：
```xml
<script src="https://cdn.jsdelivr.net/gh/stevenjoezhang/live2d-widget@latest/autoload.js"></script>
```
如果網站啟用了 PJAX，由於看板娘不必每頁刷新，因此要注意將相關腳本放到 PJAX 刷新區域之外。

換句話說，如果你是小白，或者只需要最基礎的功能，就只用把這一行代碼，連同前面加載 Font Awesome 的一行代碼，一起放到 html 的 `<head>` 中即可。
對於用各種模版引擎（例如 Nunjucks，Jinja 或者 PHP）生成的頁面，也要自行修改，方法類似，只是可能略為麻煩。以 [Hexo](https://hexo.io) 為例，需要在主題相關的 ejs 或 njk 模版中正確配置路徑，才可以加載。

**但是！我們強烈推薦自己進行配置，否則很多功能是不完整的，並且可能產生問題！ **
如果你有興趣自己折騰的話，請看下面的詳細說明。

### Using CDN

要自定義有關內容，可以把這個倉庫 Fork 一份，然後進行修改。這時，使用方法對應地變為
```xml
<script src="https://cdn.jsdelivr.net/gh/username/live2d-widget@latest/autoload.js"></script>
```
將此處的 `username` 替換為你的 GitHub 用戶名。為了使 CDN 的內容正常刷新，需要創建新的 git tag 並推送至 GitHub 倉庫中，否則此處的 `@latest` 仍然指向更新前的文件。此外 CDN 本身存在緩存，因此改動可能需要一定的時間生效。相關文檔：
- [Git Basics - Tagging](https://git-scm.com/book/en/v2/Git-Basics-Tagging)
- [Managing releases in a repository](https://help.github.com/en/github/administering-a-repository/managing-releases-in-a-repository)

### Self-host

你也可以直接把這些文件放到服務器上，而不是通過 CDN 加載。

- 如果你能夠通過 `ssh` 訪問你的主機，請把整個倉庫克隆到服務器上。執行：
  ```bash
  cd /path/to/your/webroot
  # Clone this repository
  git clone https://github.com/stevenjoezhang/live2d-widget.git
  ```
- 如果你的主機無法用 `ssh` 連接（例如一般的虛擬主機），請選擇 `Download ZIP`，然後通過 `ftp` 等方式上傳到主機上，再解壓到網站的目錄下。
- 如果你是通過 Hexo 等工具部署的靜態博客，請在博客源文件（即 `source`）目錄下，執行前述的 `git clone` 命令。重新部署博客時，相關文件就會自動上傳到對應的路徑下。為了避免這些文件被 Hexo 插件錯誤地修改，可能需要設置 `skip_render`。

這樣，整個項目就可以通過你的服務器 IP 或者域名從公網訪問了。不妨試試能否正常地通過瀏覽器打開 `autoload.js` 和 `live2d.min.js` 等文件，並確認這些文件的內容是完整和正確的。
一切正常的話，接下來修改一些配置就行了。 （需要通過服務器上的文本編輯器修改；你也可以先在本地完成這一步驟，再上傳到服務器上）
修改 `autoload.js` 中的常量 `live2d_path` 為 `live2d-widget` 這一目錄的 URL。比如說，如果你能夠通過
```
https://example.com/path/to/live2d-widget/live2d.min.js
```
訪問到 `live2d.min.js`，那麼就把 `live2d_path` 的值修改為
```
https://example.com/path/to/live2d-widget/
```
路徑末尾的 `/` 一定要加上。具體可以參考 `autoload.js` 內的註釋。
完成後，在你要添加看板娘的界面加入
```xml
<script src="https://example.com/path/to/live2d-widget/autoload.js"></script>
```
就可以加載了。

## 後端 API

`initWidget` 方法接受名為 `apiPath` 和 `cdnPath` 的參數，兩者設置其中一項即可。其中 `apiPath` 為後端 API 的 URL，可以自行搭建，並增加模型（需要修改的內容比較多，此處不再贅述）。而 `cdnPath` 則是通過 jsDelivr 這樣的 CDN 服務加載資源，更加穩定。

## 目錄結構 Files

- `waifu-tips.js` 包含了按鈕和對話框的邏輯；
- `waifu-tips.json` 中定義了觸發條件（`selector`，CSS 選擇器）和触發時顯示的文字（`text`）；
- `waifu.css` 是看板娘的樣式表。

源文件是對 Hexo 的 [NexT 主題](http://github.com/next-theme/hexo-theme-next)有效的，為了適用於你自己的網頁，可能需要自行修改，或增加新內容。
**警告：作者不對包括但不限於 `waifu-tips.js` 和 `waifu-tips.json` 文件中的內容負責，請自行確保它們是合適的。 **

如果有任何疑問，歡迎提 Issue。如果有任何修改建議，歡迎提 Pull Request。

## 鳴謝 Thanks

<a href="https://www.browserstack.com/"><img height="80" src="https://live.browserstack.com/images/opensource/browserstack-logo.svg" alt=" BrowserStack Logo"></a>

> 感謝 BrowserStack 容許我們在真實的瀏覽器中測試此項目。
> Thanks to [BrowserStack](https://www.browserstack.com/) for providing the infrastructure that allows us to test in real browsers!

<a href="https://www.jsdelivr.com"><img height="80" src="https://raw.githubusercontent.com/jsdelivr/jsdelivr-media/master/default/svg/jsdelivr- logo-horizo​​ntal.svg"></a>

> 感謝 jsDelivr 提供的 CDN 服務。
> Thanks jsDelivr for providing public CDN service.

代碼自這篇博文魔改而來：
https://www.fghrsh.net/post/123.html

點擊看板娘的紙飛機按鈕時，會出現一個彩蛋，這來自於 [WebsiteAsteroids](http://www.websiteasteroids.com)。

## 更多 More

更多內容可以參考：
https://imjad.cn/archives/lab/add-dynamic-poster-girl-with-live2d-to-your-blog-02
https://github.com/xiazeyu/live2d-widget.js
https://github.com/summerscar/live2dDemo

關於後端 API 模型：
https://github.com/fghrsh/live2d_api 
https://github.com/xiazeyu/live2d-widget-models  
https://github.com/xiaoski/live2d_models_collection

除此之外，還有桌面版本：
https://github.com/amorist/platelet
https://github.com/akiroz/Live2D-Widget
https://github.com/zenghongtu/PPet
https://github.com/LikeNeko/L2dPetForMac

以及 Wallpaper Engine：
https://github.com/guansss/nep-live2d

## 許可證 License

Released under the GNU General Public License v3
http://www.gnu.org/licenses/gpl-3.0.html

本倉庫並不包含任何模型，用作展示的所有 Live2D 模型、圖片、動作數據等版權均屬於其原作者，僅供研究學習，不得用於商業用途。

Live2D 官方網站：
https://www.live2d.com/en/
https://live2d.github.io

Live2D Cubism Core は Live2D Proprietary Software License で提供しています。
https://www.live2d.com/eula/live2d-proprietary-software-license-agreement_en.html
Live2D Cubism Components は Live2D Open Software License で提供しています。
http://www.live2d.com/eula/live2d-open-software-license-agreement_en.html

> The terms and conditions do prohibit modification, but obfuscating in `live2d.min.js` would not be considered illegal modification.

https://community.live2d.com/discussion/140/webgl-developer-licence-and-javascript-question

## 更新 Update

2018年10月31日，由 fghrsh 提供的原 API 停用，請更新至新地址。參考文章：
https://www.fghrsh.net/post/170.html

2020年1月1日起，本項目不再依賴於 jQuery。
