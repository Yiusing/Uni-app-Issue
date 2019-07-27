# Uni-App开发过程遇到的问题
## 一、小程序中弹出框阻止遮罩层下的穿透滑动
在uni-app中的uni-ui中有uniPopup这个组件(详细介绍：[uniPopup组件](https://ext.dcloud.net.cn/plugin?id=329))，这个组件可以弹出一个置顶的框并且带有遮罩，当需求为弹出层中有内容是固定高度并且可以滑动时，uniPopup这个组件会有穿透滑动bug，即当滑动某些地方时，遮罩层后的内容也会跟着滑动。
## 解决方法
- 首先给整个弹出层加上`@touchmove.stop.prevent="moveHandle"`
事件，该事件可以直接`return`，若需要某些操作亦可以加在里面（ps.小程序的话可以加上`catchtouchmove=”true” `）。
- 第二步是至关重要的一步，通过第一步加了事件后，发现弹出层里面的内容怎么也滑动不了，原因是阻止了默认事件。然后把需要滑动的内容的最外层换成`scroll-view`组件并添加`scroll-y=true`属性，而不是用`view`组件来嵌套，这样就可以使弹出层中内容可以滑动，并且阻止了穿透滑动事件。
### 至于为什么利用`scroll-view`组件可以使已经阻止默认行为的事件失效并且达到滑动的效果的原因本人暂未清楚，若有大神知道原因的话可以留言评论。
---
## 后续
突然发现uniPopup组件里面用的就是`scroll-view`组件来嵌套滑动内容，具体代码请自行参考uni-app **Hello**项目，但是由于他把`@touchmove.stop.prevent="moveHandle"`事件放在遮罩层上，所以当弹出框除了列表内容外还有其他内容，滑动其他内容会出现穿透滑动，所以建议把`@touchmove.stop.prevent="moveHandle"`放到最外层`view`上。
## 效果图
### Before
![image](https://raw.githubusercontent.com/Yiusing/Uni-app-Issue/master/2.gif)
### After
![image](https://raw.githubusercontent.com/Yiusing/Uni-app-Issue/master/1.gif)


---
---
---
## 二、关于 `Cannot read property "$children" of undefined` 错误。
经排查引起此错误的原因是当自定义导航栏且使用图标时，在某些情况下会报出错误并且导航栏消失，我的情况是当退出登录跳转至登录页面后再登录并且跳转至当前页面时会出现这种错误。
## 解决方法
-  在`fontSrc`这个属性要特别注意路径最前面需要添加**反斜杠/**，不然就会出现上述错误。
## 示例：
```
"app-plus": {  
        "titleNView": {  
            "buttons": [{  
                "text": "\ue534",  
                "fontSrc": "/static/uni.ttf",  
                "fontSize": "22px"  
            }]  
        }  
    }  
```
