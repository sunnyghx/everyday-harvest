# 每日收获

标签（空格分隔）： 收获

---

##javascript

###异步
[深入理解 JavaScript 异步系列](http://www.cnblogs.com/wangfupeng1988/p/6513070.html)

####async、await
[vue中异步函数async和await的用法][1]

###数据类型


---
####**Array**
##### splice

```javascript
this.allSelectedEnergy =this.allSelectedEnergy - parseInt(this.allSelected[index].wx_todaysmovement_unit*this.allSelected[index].exercise_kcal/this.allSelected[index].exercise_time);
let allSelected = JSON.parse(JSON.stringify(this.allSelected));
this.allSelected.splice(index, 1);
this.wxercise = this.allSelected;
```

splice会直接**更改原数组**，所以下面的写法是错误的

    this.allSelected=this.allSelected.splice(index,1)

##### indexOf
判断某元素是否在数组中，在数组中则返回第一个出现的下标，没有的话返回-1

##### remove
删除指定元素内容，需要在Array原型中加入
```javascript
Array.prototype.remove = function(val) { 
var index = this.indexOf(val); 
if (index > -1) { 
    this.splice(index, 1); 
    } 
};

```
##### concat
数组连接 不会改变原数组

- 数组循环的方法
 - forEach
 - map
 - for
- 空数组
[js 空数组是true还是false][2]

####**Object**


####**函数**
##### **js调用函数时加括号与不加括号的区别**
函数名其实就是指向函数体的指针 
不加括号， 可以认为是查看该函数的完整信息， 
不加括号传参，相当于传入函数整体 
加括号 表示立即调用（执行）这个函数里面的代码（花括号部分的代码）

例： vue中 在mounted和created生命周期函数中 调用methods的方法就必须要加()
而在@click等绑定事件的时候就不要加()



####**Math**
|方法|描述|
| :----:| --------   | 
|acos(x)|	返回数的反余弦值。|
|asin(x)|	返回数的反正弦值。|
|atan(x)|	以介于 -PI/2 与 PI/2 弧度之间的数值来返回 x 的反正切值。|
|atan2(y,x)|返回从 x 轴到点 (x,y) 的角度（介于 -PI/2 与 PI/2 弧度之间）。|
|ceil(x)|	对数进行上舍入。|
|cos(x)|	返回数的余弦。|
|exp(x)	|返回 e 的指数。|
|floor(x)|	对数进行下舍入。|
|log(x)|	返回数的自然对数（底为e）。|
|max(x,y)|返回 x 和 y 中的最高值。|
|min(x,y)|	返回 x 和 y 中的最低值。|
|pow(x,y)	|返回 x 的 y 次幂。|
|random()|	返回 0 ~ 1 之间的随机数。|
|round(x)|	把数四舍五入为最接近的整数。|
|sin(x)|	返回数的正弦。|
|sqrt(x)|	返回数的平方根。|
|tan(x)	|返回角的正切。|
|toSource()	|返回该对象的源代码。|
|valueOf()|	返回 Math 对象的原始值。|


##**css**
移动端设置最外层div背景颜色 内容撑不起全屏的问题： 设置div的min-height:100vh

---

模态框mask显示时  底部的内容还能滚动的问题：  在显示的时候设置body(vue为该组件的最父元素)设置height:100vh; overflow:hidden;

---

transition实现手风琴效果 通过width height的数值变化控制显示隐藏，注意外部div里需要有一个固定撑起高度的div 方式width height变为0的过程中内容被压扁。

---

让图片在div中垂直居中
display: inline-block;
vertical-align: middle;
水平居中：
padding-left:50%;
margin-left:-(元素的宽度)

---

子元素设置margin-top后，父元素跟随下移的问题
为父元素增加一个border-top或者padding-top即可解决这个问题。

---

媒体查询：用于制作响应式
注意，书写顺序要从范围大的到范围小的
@media (max-width:700px){}
@media (max-width:300px){}	

---

CSS 实现隐藏滚动条同时又可以滚动
.element::-webkit-scrollbar {display:none}
https://www.cnblogs.com/alice626/p/6206760.html

---

pointer-events: none
设置一个元素的css属性为pointer-events: none。它将不会捕获任何click事件，而是让事件穿过该元素到达下面的元素


##**css3**
###渐变字
[CSS3下的渐变文字效果实现][3]

###filter(滤镜)


##**命名规范**

[如何规范 CSS 的命名和书写？][4]
[JS命名规范][5]

##**Vue**

###项目优化
main.js 拆分优化
router/index.js 拆分优化
公共css样式拆分优化
路径别名的巧妙使用

---

###生命周期函数

---

###计算属性

[computed、methods、watched以及它们的区别][6]

---

###事件的$event
阻止事件冒泡：@click.stop="show()"
阻止事件默认行为：@contextmenu.prevent="show()"



###Vue Router
[官方文档][7]

####在router中设置缓存

    {
        path: '/msite',
        component: msite,
        meta: { keepAlive: true },
    },
使用：

    <keep-alive>
        <router-view v-if="$route.meta.keepAlive"></router-view>
    </keep-alive>

####滚动行为
```javascript
const router = new VueRouter({
	routes,
	mode: routerMode,
	strict: process.env.NODE_ENV !== 'production',
	scrollBehavior (to, from, savedPosition) {
		console.log(to, from, savedPosition,'滚动')
	    if (savedPosition) {
		    return savedPosition
		} else {
			if (from.meta.keepAlive) {
				from.meta.savedPosition = document.body.scrollTop;
			}
		    return { x: 0, y: to.meta.savedPosition || 0 }
		}
	}
})
```

####路由过渡
路由跳转时添加transition过渡效果

    <transition name="router-fade" mode="out-in">
    	<keep-alive>
    	    <router-view v-if="$route.meta.keepAlive"></router-view>
    	</keep-alive>
    </transition>

```css
.router-fade-enter-active, .router-fade-leave-active {
  	transition: opacity .3s;
}
.router-fade-enter, .router-fade-leave-active {
  	opacity: 0;
}
```
[transition文档传送门][8]

再添加svg动画


####按需加载

[vue按需加载组件 ----3种方法][9]



###报错
vue报错 Do not use built-in or reserved HTML elements as component id:header
组件，不能和html标签重复
由于在模板需要插入到 DOM 中，所以模板中的标签名必须能够被 DOM 正确地解析。主要有三种情况：
　　　　一是完全不合法的标签名，例如 </>；
　　　　二是与 HTML 元素重名会产生不确定的行为，例如使用 input 做组件名不会解析到自定义组件，使用 button 在 Chrome 上正常但在 IE 上不正常；
　　　　三是与 Vue 保留的 slot、partial、component 重名，因为会优先以本身的意义解析，从而产生非预期的结果。
　　　　

###缓存
data中的数据尤其是在切换选项卡等的  一定要注意缓存数据（脂玫乐H5 echarts图周月年切换）


###其它
事件的$event
阻止事件冒泡：@click.stop="show()"
阻止事件默认行为：@contextmenu.prevent="show()"

在函数的一个对象参数中慎用this

vue 定义封装全局函数
https://blog.csdn.net/wandoumm/article/details/80167751

vue中使用animate.css
https://www.jb51.net/article/130344.htm

vue中关闭eslint
在config文件夹的index.js中


vue往data中存的数据如果是对象数组，默认是空对象，页面中直接取数组中某元素的属性会报错，因为ajax请求数据和往data中赋值是异步的，解决方法：给对象的属性设默认值
　　　　
vue中使用promise会造成this指向改变，vue的原型方法无法使用，解决办法 hack   let that=this;

vue处理异步和全局数据方案 ： sessionStorage和Promise Vue.prototype 配合解决少量全局异步数据

vue中父与子组件通信 如果父组件通信给子组件的数据是异步数据，子组件需要在watch中监听这个数据，否则只能拿到初始值而拿不到异步数据

###ref

//获取元素样式值,为元素ref="ele"(在样式里面写死了的高度)
var heightCss = window.getComputedStyle(this.$refs.ele).height; // ？px
在左滑删除组件 中 删除按钮高度设置时用到了

vue获取dom元素高度的方法
https://www.cnblogs.com/lhl66/p/7908133.html



### :key的作用
[我的博文][10]

###vue touch事件：
touch的开始事件是@touchstart，
移动过程是@touchmove,
结束事件是@touchend

---


###组件封装

####组件命名

聊聊 Vue 组件命名那些事：
https://cnodejs.org/topic/5816aabdcf18d0333412d323

####组件通信

#####父与子通信
父组件是通过props属性给子组件通信的来看下代码：
父组件：
```javasceript
<parent>
    <child :child-com="content"></child> //注意这里用驼峰写法哦
</parent>

data(){
    return {
        content:'sichaoyun'
    };
}
```
子组件通过props来接受数据
第一种方法

    props: ['childCom']

第二种方法

    props: {
        childCom: String //这里指定了字符串类型，如果类型不一致会警告的哦
    }


第三种方法

    props: {
        childCom: {
            type: String,
            default: 'sichaoyun' 
        }
    }
    
    
在做组件封装时推荐第三种方法

子组件与父组件通信
vue2.0只允许单向数据传递，我们通过出发事件来改变组件的数据

子组件代码

```javascript
<template>
    <div @click="open"></div>
</template>

methods: {
   open() {
        this.$emit('showbox','the msg'); //触发showbox方法，'the msg'为向父组件传递的数据
    }
}
```

父组件
```javascript
<child @showbox="toshow" :msg="msg"></child> //监听子组件触发的showbox事件,然后调用toshow方法

methods: {
    toshow(msg) {
        this.msg = msg;
    }
}
```

###vue-devtools
很好用，多用
Vue.js devtool插件安装后无法使用的解决办法
https://blog.csdn.net/TheBeauty2016/article/details/72472344

---

##**vuex**
https://segmentfault.com/a/1190000012015742

为什么用vue 数据缓存后 页面就不会再重新渲染了

vuex的异步数据  在页面created或mounted中要使用的话 很可能获取不到，因为ajax请求数据还没走完，需要在watch中监听



---

##**React**

路由异步加载
http://developer.51cto.com/art/201707/544250.htm

事件参数e和其它参数一起传递
onChange={this.InputSearch.bind(this,0)} 
InputSearch(tip,e){
console.log(tip,e.target.value)
}

e都是最后一个参数 注意要绑定一下this

注意：this.setState不是同步的，可以使用它的回调函数来解决
https://www.cnblogs.com/little-ab/articles/6958852.html

React只要state状态不变 视图就不会重新渲染 就像Table里的checkbox 控制是否选中

---


##**React Native**

优点：
1.跨平台
2.热更新
3.代码复用率高
4.开发成本低 效率高

环境搭建
1.安装nodejs 使用它的npm包管理工具
2.安装脚手架工具 npm i -g react-native-cli  测试：react-native -h(帮助)  -v(版本)
3.安装Android开发工具 AndroidStudio
http://www.android-studio.org/index.php/download/androidstudio-download-baidudisk

Ios搭建  需再下载一个Xcode软件  打开开发者菜单区别 commend+d

4.初始化项目：命令行 react-native init FirstApp
设置淘宝镜像： 在nodejs的安装目录下nodejs\node_modules\npm的npmrc加入
registry = http://registry.npm.taobao.org 

5.启动方式：
（1）使用命令行  在项目文件夹里 react-native run-andriod 来启动安卓app
前提是先启动andriod studio 
（2）使用andriod studio加载项目文件夹里的andriod文件夹 点击run
前提是先在项目文件夹里 npm start
刷新页面： 按住ctrl在单击两次左键

---


##**Echarts**

绘图方式
（1）canvas绘图 基于像素点
（2）svg  矢量 不失真
echarts是基于canvas绘图

---


##**微信小程序**

常用组件：view、image、text
事件：bindtap 点击事件

5.25
生命周期函数
onLoad :监听页面加载
onReady:监听页面初次渲染完成
onShow：监听页面显示

模块化
https://developers.weixin.qq.com/miniprogram/dev/framework/app-service/module.html?search-key=globalData

全局状态、数据
在app.js中globalData

image的样式需要用元素选择器 既image{}
在wx:for中<image src="{{item.img}}" />  需要带引号

torecord:function(){
let that=this;
that.setData({
isrecord:!that.isrecord    //注意 不能isrecord:!isrecord
})
}

微信小程序中使用echars
https://blog.csdn.net/nmyangmo/article/details/79413030
https://github.com/ecomfe/echarts-for-weixin

事件 bind和catch的区别

target和currentTarget的区别
https://www.cnblogs.com/lxm-ivamos/p/7613883.html

微信小程序让view高度布满全屏
.record{
position: fixed;   //最外面的view用fixed定位
height: 100%;
width: 100%;
}

去除button默认样式
button::after{
border: none
}
对于button的边框设置，要放在::after里面设置，才生效，要不然会出现各种怪异现象


巨坑：
setData 设置对象或数组其中的属性或元素 不能用[]或.来访问，可以将需设置的对象先用字符串拼起来
比如：
let index=option.currentTarget.dataset.index;
let copynum=`settings[${index}].num`;
that.setData({
[copynum]:theNum    //注意要用[]括起来
})

<view class="btn-sure {{btn3==true?'cfff':'cccc'}}">
注意外面要用双引号，这样里面就有使用单引号的机会

picker组件的使用

函数使用data中的数据   that.data.XXX

###webview
https://211.qinziheng.com/lesson/548/

####支付
[小程序webview能使用微信h5支付吗？小程序web-view中使用哪种微信支付方式更好？][11]
[小程序实现h5页面的微信支付][12]

####小程序和webview交互

[微信小程序webview跳转小程序内路由][13]



<web-view src="{{item.img}}" class="slide-image"> </web-view>

navigator 跳转 类似a标签 只能跳内部链接
开发过程中可以设置  详情——不校验合法域名
坑：
navigator 不能跳转到tapbar页面   可用用success 和fail 打印e来查看报错

如需跳转tapbar页面 使用 wx.switchTab  Tab切换，跳转的页面必须是app.json 中 tabBar 配置的页面。


只有在tabBar中设置了的页面才会有底部导航栏

<text class="font22 numpos">{{index+1}}</text>


open-type

https://developers.weixin.qq.com/miniprogram/dev/component/button.html


切换tapbar注意哪些数据会变化 有可能变化的数据都要重新请求一下



微信小程序自定义分享标题和图片

onShareAppMessage
注意区分是页面内的button分享还是右上角原点分享
path 注意是跟相对路径 既/pages/xxx/xxx


button取消点击效果 如点击的背景颜色  在button标签上hover-class="none"

微信小程序场景值

onShow中跑过的函数  onLoad里就不用跑了

<button open-type="getUserInfo" bindgetuserinfo="getUserInfo" class="font30 cfff"> 
未打卡
</button> 

微信小程序  canvas map video等原生组件层级最高的问题
使用<cover-view>  <cover-image>

小程序继承复制this来调取data的数据
http://www.jb51.net/article/105467.htm

---

##**微信开发**

openid与unionid的区别
静默授权

获取ip： https://httpbin.org/ip
获取城市：  http://ip.taobao.com/service/getIpInfo.php?ip=113.247.20.142  淘宝ip地址库

---

##mpvue



---

##**webpack**

---

##**GIT**

###git flow

[WOT谯洪敏：滴滴前端工程化思维][14]

---

##**命名规范**

###css:
https://www.zhihu.com/question/19586885

###变量：

http://www.fefancier.com/2018/06/08/js%e5%91%bd%e5%90%8d%e8%a7%84%e8%8c%83/

---


##**NPM**

####npm 查看全局安装模块

    npm list -g --depth=0

####npm设置淘宝镜像

    npm config set registry https://registry.npm.taobao.org
    
####全局环境变量配置
[npm 全局环境变量配置][15] 
注意：用户变量 如果不是administrator 则应在此处修改



![修改用户变量][16]

##**echarts**
####折线图连接空数据
series的connectNulls属性支持连接空值


##**H5+**
真机调试 mui

##**项目优化**

###路径优化
main.js 拆分优化
router/index.js 拆分优化
公共css样式拆分优化
路径别名的巧妙使用

###速度优化

####fastclick

---

##Chrome

[20个Chrome DevTools调试技巧][17]

###打印对象
在使用console.log();的时候，不仅仅打印变量，而是要打印对象，用大括号({})将变量包围起来。这样的优点是不仅会把变量的值打印，同时还会将变量名打印出来。

###使用console.table来打印多条目数据
如果你要打印的变量是一个数组，每一个元素都是一个对象。我建议你使用console.table来打印，其表格化的呈现更加美观易读。

##vscode

###关闭eslint
在设置中 搜索 eslint.enable  设置为false

###设置vscode代码片段
文件--首选项--用户代码片段 搜索vue 修改vue.json


```
{
  "Print to console": {
   "prefix": "vue",
   "body": [
    "<!-- $0 -->",
    "<template>",
    " <div></div>",
    "</template>",
    "",
    "<script>",
    "export default {",
    " components: {},",
    " data () {",
    " return {",
    " }",
    " },",
    "",

    "",
    " computed:{},",
    "",
    " created(){},",
    "",
    " mounted(){},",
    "",
    " methods:{}",
    "}",
    "",
    "</script>",
    "<style lang='stylus' scoped rel=‘stylesheet/stylus’>",
    "</style>",
    ""
  ],
   "description": "Log output to console"
  }
}
```

##资讯站

###[FunDebug][18]

###[思否][19]

###[CSDN][20]

###[博客园][21]

###[掘金][22]

###[infoq][23]

###[开源中国][24]

###[IT搜123][25]


  [1]: http://blog.sina.com.cn/s/blog_13d06fc1f0102wzfr.html
  [2]: https://blog.csdn.net/aerchi/article/details/51169323
  [3]: https://www.zhangxinxu.com/wordpress/2011/04/%E5%B0%8Ftipcss3%E4%B8%8B%E7%9A%84%E6%B8%90%E5%8F%98%E6%96%87%E5%AD%97%E6%95%88%E6%9E%9C%E5%AE%9E%E7%8E%B0/
  [4]: https://www.zhihu.com/question/19586885
  [5]: http://www.fefancier.com/2018/06/08/js%E5%91%BD%E5%90%8D%E8%A7%84%E8%8C%83/
  [6]: https://blog.csdn.net/seven_an/article/details/73204679
  [7]: https://router.vuejs.org/zh/
  [8]: https://cn.vuejs.org/v2/api/#transition
  [9]: https://blog.csdn.net/qq_31965515/article/details/80092849
  [10]: http://www.fefancier.com/2018/08/29/vue%E4%B8%AD-%EF%BC%9Akey%E7%9A%84%E4%BD%9C%E7%94%A8/
  [11]: https://blog.csdn.net/towtotow/article/details/79444067
  [12]: https://blog.csdn.net/chen_pan_pan/article/details/80352411
  [13]: https://blog.csdn.net/u012411480/article/details/79239531
  [14]: http://developer.51cto.com/art/201806/576334.htm
  [15]: https://www.cnblogs.com/WhiteCusp/p/4200220.html
  [16]: https://gehx.oss-cn-hangzhou.aliyuncs.com/meijie/nav/12.png
  [17]: https://blog.fundebug.com/2018/08/22/art-of-debugging-with-chrome-devtools/
  [18]: https://blog.fundebug.com/
  [19]: https://segmentfault.com/channel/frontend
  [20]: https://www.csdn.net/nav/web
  [21]: https://www.cnblogs.com/
  [22]: https://juejin.im/welcome/frontend
  [23]: http://www.infoq.com/cn/Front-end/?utm_source=infoq&utm_medium=header_graybar&utm_campaign=topic_clk
  [24]: https://www.oschina.net/blog?classification=428612
  [25]: https://itso123.com/