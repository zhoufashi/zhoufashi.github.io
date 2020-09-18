```
.json 后缀的 JSON 配置文件
.wxml 后缀的 WXML 模板文件
.wxss 后缀的 WXSS 样式文件
.js 后缀的 JS 脚本逻辑文件

{
  "pages":[
    "pages/index/index",
    "pages/logs/logs"
  ],
  "window":{
    "backgroundTextStyle":"light",
    "navigationBarBackgroundColor": "#fff",
    "navigationBarTitleText": "WeChat",
    "navigationBarTextStyle":"black"
  }
}
小程序配置 app.json
app.json 是当前小程序的全局配置，包括了小程序的所有页面路径、界面表现、网络超时时间、底部 tab 等
pages字段 —— 用于描述当前小程序所有页面路径，这是为了让微信客户端知道当前你的小程序页面定义在哪个目录。
window字段 —— 定义小程序所有页面的顶部背景颜色，文字颜色定义等。
工具配置 project.config.json
小程序开发者工具在每个项目的根目录都会生成一个 project.config.json，
你在工具上做的任何配置都会写入到这个文件，当你重新安装工具或者换电脑工作时，
你只要载入同一个项目的代码包
页面配置 page.json
顶部颜色、是否允许下拉刷新

WXML 模板
用来描述当前这个页面的结构
由标签、属性等等构成
WXSS 样式
具有 CSS 大部分的特性

JS 交互逻辑
通过编写 JS 脚本文件来处理用户的操作。
```
[返回](../) 