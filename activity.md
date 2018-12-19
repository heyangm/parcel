---
category: 各产品相关组件
name: 组件整理
---

## 各产品活动相关组件

### 文学漫画h5和native通信库 nejsbridge
[nejsbridge](https://www.npmjs.com/package/nejsbridge)<br/>
[阅读jsbridge接口协议](http://doc.hz.netease.com/pages/viewpage.action?pageId=105039339)<br/>
[蜗牛jsbridge接口列表](http://doc.hz.netease.com/pages/viewpage.action?pageId=117465770)<br/>
[漫画jsbridge接口协议](http://doc.hz.netease.com/pages/viewpage.action?pageId=85264165)<br/>


## 常用组件

 ### 通用 ： 
 
[分享组件](https://g.hz.netease.com/winman-f2e/common-modules/tree/master/packages/nw-share)  
```js
import {setOrUpdate, share} from 'nw-share';
let shareDate={
    title: '',
    description: '',
    activityId: '', //只能是数字
    picurl: '',
    text: '', //分享到微博文案
    link: loaction.href,
    channel:"['_share_weixin','_share_weixinquan','_share_qqfriend','_share_qzone']" //云阅读分享渠道设置
}
setOrUpdate(shareDate,callback)
share()
```

[ua组件](https://g.hz.netease.com/winman-f2e/common-modules/tree/master/packages/nw-detect) 
```js
import {isYueduApp,isSnail,isLofter,isWeixin,ios,isiPad,isQQ,isAndroid} from 'nw-detect'
if(isWeixin()){
}
```

### 阅读 ： 

[打点]
在html中添加以下js:
```js
<script type="text/javascript">
	(function(document,datracker,root){function loadJsSDK(){var script,first_script;script=document.createElement("script");script.type="text/javascript";script.async=true;script.src="https://hubble-js-bucket.nosdn.127.net/DATracker.globals.1.6.8.js";first_script=document.getElementsByTagName("script")[0];first_script.parentNode.insertBefore(script,first_script)}if(!datracker["__SV"]){var win=window;var gen_fn,functions,i,lib_name="DATracker";window[lib_name]=datracker;datracker["_i"]=[];datracker["init"]=function(token,config,name){var target=datracker;if(typeof(name)!=="undefined"){target=datracker[name]=[]}else{name=lib_name}target["people"]=target["people"]||[];target["abtest"]=target["abtest"]||[];target["toString"]=function(no_stub){var str=lib_name;if(name!==lib_name){str+="."+name}if(!no_stub){str+=" (stub)"}return str};target["people"]["toString"]=function(){return target.toString(1)+".people (stub)"};function _set_and_defer(target,fn){var split=fn.split(".");if(split.length==2){target=target[split[0]];fn=split[1]}target[fn]=function(){target.push([fn].concat(Array.prototype.slice.call(arguments,0)))}}functions="track_heatmap register_attributes register_attributes_once clear_attributes unregister_attributes current_attributes single_pageview disable time_event get_appStatus track set_userId track_pageview track_links track_forms register register_once alias unregister identify login logout signup name_tag set_config reset people.set people.set_once people.set_realname people.set_country people.set_province people.set_city people.set_age people.set_gender people.increment people.append people.union people.track_charge people.clear_charges people.delete_user people.set_populationWithAccount  people.set_location people.set_birthday people.set_region people.set_account abtest.get_variation abtest.async_get_variable".split(" ");for(i=0;i<functions.length;i++){_set_and_defer(target,functions[i])}datracker["_i"].push([token,config,name])};datracker["__SV"]=1.6;loadJsSDK()}})(document,window["DATracker"]||[],window);
        DATracker.init('MA-A1FF-A578E03E2D7B', {abtest: { enable_abtest: false},truncateLength: 255,persistence: "localStorage",cross_subdomain_cookie: false});
</script>
```
js中打点：
```js
DATracker.track('wbg2-3',{cateroy:cateroy,action:action,label:label});
```

[云阅读登录组件](https://www.npmjs.com/package/nw-login-readapp)
```js
import LoginReadApp from 'nw-login-readapp'
const loginReadApp = new LoginReadApp();
//同步客户端登录信息
//强制调起客户端登录
loginReadApp.syncLoginAtApp(true, true,callback)
//不强制调起客户端登录
loginReadApp.syncLoginAtApp(true, false,callback)

//获取用户信息
function getUser(){
     axios('/login/context.json').then(res=>{
        return res.data.user
    })
 }

```


[打开阅读app](https://g.hz.netease.com/winman-f2e/common-modules/tree/master/packages/nw-app-read) 
```js
import {openAppRead} from 'nw-app-read'
//打开书籍详情页
 openAppRead({
    path: 'detail',//打开详情页面
    query: {
        id: bookId //阅读bookId
    },
    h5Fallback: true  //可选 true时，打不开app跳转wap详情页
})
//打开发现页
 openAppRead({
    path: 'webview'
})

```
|path|query|参数描述|
|-------|------|-------|
|webview|  无  |  发现页|
|detail | id：书籍id|书籍详情页 |
|news |id:资讯源id, cid:资讯文章id | 资讯详情页|
|shelf |无 | 书架|
|baoyue |id:阅读bookId |包月详情 |
|recharge |aid:活动id，可选  money: 要充值的阅点数，可选 url: 要打开的h5页面url,可选| 充值页|
|trade |id:阅读bookId, title: 书籍title,  full:0 按章购买 1 全本购买, url:要打开的h5页面url | 购买页|
|packagebuy |  pid: 打包购pid, url: 要打开的h5页面url| 打包购|
|audio | id:听书id |听书详情 |
|bookshelf| 无|书架页(v6.0) |
|mobileBind |无 |手机号绑定页(v6.0) |
|rank|  url: '/store/merged/rankNavi.json?uuid=b5648dd3c4f24d9796f590cd81ca076e&rankType=112',title: '排行榜'| 排行页(v6.0)|
|bookstore |tab_index: 1 |书城(v6.0)|
|category | tab_index:  1, sub_tab_index: 2 | 分类(v6.0)|
|package | baoyue_id:包月id | 包月详情(v6.0)|


### 蜗牛 ：

[蜗牛登录组件](https://www.npmjs.com/package/snail-login)
```js
import Login from 'snail-login'
const login = new Login(); 
checkLogin(callback,true)
checkLogin(callback,needlogin){
     login.isLogined().then( result => {
         if(result){  //已登录返回用户信息
            userData = result
            callback()
         }else if(needlogin){  //未登录调起登录
             login.login({
                 fn:fn,
                 targetUrl: location.href
             })
         }
     })
}
```


[打开蜗牛app](https://g.hz.netease.com/winman-f2e/common-modules/tree/master/packages/nw-app-snail)
```js

import openAppSnail from 'nw-app-snail'
//打开书籍详情页
openAppSnail({
    path: 'bookdetail',
    query: {
        bookId: 286436
    }
})
```
| path | query | 描述 |
| --- | --- | --- |
| bookdetail | bookId：书籍id | 书籍详情 |
| bookcontent | bookId：书籍id articleId：章节id 非必传| 书籍正文页 |
| booklist | bookListId：书单id | 书单页（书单功能已弃用） |
| webview | url：打开的连接地址 inside：boolean变量，是否用内嵌浏览器打开，默认为false（即外部浏览器打开） | 通过浏览器或者webview打开url |
| userinfo | uuid：用户uuid | 用户个人主页 |
| privatemsg | useruuid：用户uuid | 用户私信对话界面 |
| bookrank | moduleId：模块id entryId：排行榜id title：榜单名称 type：榜单类型（read：在读榜，new：新书榜）| 书籍排行榜 |
| bookreview | bookReviewId：书评id | 书评详情页 |
| newbookreview | 无 | 写书评 |
| question | questionId: 问题id | 问题回答页 |
| questionlist | bookId: 书籍id | 书籍的问题列表 |
| bookstore | 无 | 书城（目前的分类页） |
| messagenotify | 无 | 消息列表通知选项卡 |
| messagecomment | 无 | 消息列表评论选项卡 |
| messageanswer | 无 | 消息列表回答选项卡 |
| messagelist | 无 | 我的消息列表 |
| feedback | 无 | 用户反馈 |
| followlist | type：follow表示关注列表，fans表示粉丝列表  uuid：用户uuid，如果不传表示当前登录用户| 用户反馈 |
| setting | 无 | 设置 |
| subject | moduleId：模块id entryId：专题id（如果不传表示获取专题列表）| 专题页 |
| bookexchange | type：exchanged表示已兑换页面，book表示兑换页面 | 书籍兑换页面 |


[蜗牛哈勃打点](https://g.hz.netease.com/winman-f2e/snailreader-component/tree/master/packages/snail-log)
```js
import Log from 'snail-log'
const log = new Log('h5/web/mp', true, 1234);
log.sendLog('a1-1', ['category', 'action', 'label']);

```
### Lofter 
[打开lofterApp](https://g.hz.netease.com/winman-f2e/common-modules/tree/master/packages/nw-app-lofter)
```js
import {openAppLofter} from 'nw-app-lofter'
openAppLofter({
    path: 'webview',
    query: {
        url: 'http://qatest5.lofter.com'
    }
})
```

参数为Object类型，参数各字段定义如下：

| 参数属性 | 类型 | 描述 |
| --- | --- | --- |
| path | String | webview或具体页面类型 |
| query | Object | 参数 |

具体可用path和query参数如下：

| path | query | 描述 |
| --- | --- | --- |
| webview | url：WAP页面的url  | 如果指定WAP页面已实现APP打开功能，则打开APP内的对应页面；否则通过webview打开 |
| homepage | id：用户id | 个人主页 |
| post | id: 帖子id，userId：用户id | 单日志页 |
| tag | tagName：标签名 | 标签页 |
| publishText | userId：用户id，tagName：标签名(逗号分隔) | 发布文字页 |
| publishPhoto | userId：用户id，tagName：标签名(逗号分隔) | 发布图片页 |
| publishVideo | userId：用户id，tagName：标签名(逗号分隔) | 发布视频页 |

其中，path为webview时，url指定为WAP页url。如APP可打开对应页面，则打开；否则通过webview打开。

