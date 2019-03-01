## WU-UI(维护中...2019-03-01)

<div align="center">
<a href="http://www.wuruijin.cn/wuui" target="_blank">
<img src="http://www.wuruijin.cn/image/ewm/ewm-wuui.png" height="150" width="150" >
</a>
</br>
<a href="http://www.wuruijin.cn/wuui" target="_blank">Live demo</a>
</div>

## 项目介绍

平时项目用的到的组件就是一些交互类型的消息提示组件，因用ui框架太重，所以自己琢磨了一些简单常用的组件！供大家一起学习

## 安装教程

直接引入js
```javascript
<script type="text/javascript" src="static/wu-ui/wu-ui.js"></script>
```
## 使用说明

* wu-ui.js 末尾直接实例化了

```javascript
var wu = new Wu();
```
---
* 进入wu-ui.js，选择要把组件添加到哪个dom节点里面（比如vue 需要添加到实例化的dom元素里面）

```javascript
Wu.prototype.addDom = function(el) {
	//vue
	document.querySelector('#app').appendChild(el);
	//普通页面
	//document.body.appendChild(el);
};
```
---
* vue-cli引入方式
```javascript
// 1- wu-ui.js
...
// 末尾添加：
export default wu;

// 2- main.js
import wu from './assets/wu-ui/wu-ui'; // 把wu-ui文件夹放入assets静态文件夹，这个可以自行选择放哪里
// 把wu注册到vue里
Vue.prototype.$wu = wu;  
...

// 3- app.vue
// 全局css： style 标签里引入css
@import './assets/wu-ui/wu-ui.css';
...

// 4- 调用组件
let vm = this;
vm.$wu.showLoading()
```
---
* 隐藏Toast 用于showLoading, showToast
```javascript
wu.hideToast();
```
---
* 显示加载动画
```javascript
/**
 * showLoading(title)
 * @param {string} 默认空 | 必须：否
 */
wu.showLoading('loading...');
```
---
* 显示带白色背景的加载动画
```javascript
wu.showLoadingBg();
```
---
* 显示消息提示框
```javascript
/**
 * showToast(options)
 * @param {string}  title 无默认值 | 必须：是
 * @param {boolean} mask 默认为false | 必须：否 (是否可穿透屏幕)
 * @param {string}  icon 默认空 | 必须：否 | 可选 icon-success | icon-error | icon-info 空的时候不显示图标
 * @param {number}  duration 默认3000 | 必须：否
 */
wu.showToast({
    title: '提示消息',
    mask: false,
    icon: 'icon-success',
    duration: 3000
});
```
---
* 显示顶部显示的提示信息(适用于表单提示)
```javascript
/**
 * showMessage(options)
 * @param {string} title 无默认值 | 必须：是
 * @param {string} backgroundColor 默认为 'rgba(17, 17, 17, 0.9)' | 必须：否
 * @param {number} duration 默认3000 | 必须：否
 */
wu.showMessage({
    title: "提示信息",
    backgroundColor: 'red',
    duration: 3000
});
```
---
* 显示操作对话框
```javascript
/**
 * showDialog(options)
 * @param {string}   title 默认值 '提示' | 必须：否
 * @param {string}   content 无默认值 | 必须：是
 * @param {boolean}  showCancel 默认false | 必须：是
 * @param {boolean}  showInput 默认false | 必须：是
 * @param {callBack} success(res) 回调函数 | 必须：是 
    | res.value 返回的操作状态有'confirm' 和 'cancel' | res.inputValue 返回输入框的值
 */
wu.showDialog({
    title: 'Hello Wu-ui',
    content: '欢迎使用Wu-ui',
    showCancel: true,        //是否显示取消按钮
    showInput: false,        //是否显示输入框，如果为true则content会隐藏
    success: function(res) {
        if(res.value == "confirm") {
            wu.showToast({
                    title: '点击了确定',
                    duration: 2500
                 })
        }
        if(res.value == "cancel") {
            wu.showToast({
            title: '你取消了',
            duration: 1500
           })
        }
    }
})					        
```
---
* 显示底部弹出操作菜单
```javascript
/**
 * showAction(options)
 * @param {string}   title 无默认值 | 必须：否
 * @param {string}   deleteText 无默认值 | 必须：否
 * @param {array}    menuArray 菜单列表 | 必须：是
 * @param {callBack} success(res) 回调函数 | 必须：是 
    | res.value 返回操作菜单的值 | res.title 返回操作菜单的显示文本
 */
wu.showAction({
    title: '示例标题',
    deleteText: '', //点击删除时弹出框的确认消息
    menuArray: [{
            title: '示例菜单一',
            value: 'menu1',
            color: ''
        },
        {
            title: '示例菜单二',
            value: 'menu2',
            color: ''
        },
        {
            title: 'Delete',
            value: 'delete',
            color: 'red'
        } //如果是删除  value 必须是 "delete"
    ],
    success: function(res) {
        if (res.value == "delete") {
            wu.showToast({
                title: "已删除",
                duration: 1500
            })
        } else {
            wu.showToast({
                title: res.title
            })
        }
    }
})
```
---
* 网络请求超时或失败提示
```javascript
/**
 * showError(title)
 * @param {string} 默认值 '网络请求超时，轻触屏幕刷新' | 必须：否
 */
wu.showError('请求错误, 轻触屏幕刷新')
```
