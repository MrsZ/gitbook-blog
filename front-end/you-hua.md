![](/assets/http_process.png)潜在性能优化点

* dns是否可以通过缓存减少查询时间
* 网络请求的过程走最近的网络环境
* 相同的静态资源是否可以缓存
* 能否减少请求http请求大小
* 减少http请求
* 服务端渲染

# 资源的合并和压缩

* 减少http请求数量
* 减少请求资源的大小

html压缩： 去除html中无意义的字符

css压缩

* 无效代码删除
* css语义合并

js压缩与混乱

* 无效字符的删除
* 剔除注释
* 代码语义的缩减和优化
* 代码保护

文件合并存在的问题

* 首屏渲染问题
* 缓存失效问题

做法

* 公共库合并： 公共库一般不会改动，业务代码经常改动，分别打包
* 不同页面的合并：不同页面js单独打包

# 重绘与回流

css如果频繁触发重绘和回流，会导致UI频繁渲染，最终导致JS变慢

回流

* 当render tree中的一部分或全部因为元素的规模尺寸，布局，隐藏等改变而需要重新构建。这就称为回流\(reflow\)
* 当页面布局和几何属性改变时就需要回流

重绘

* 当render tree中的一些元素需要更新属性，而这些属性只是影响元素的外观，风格，而不会影响布局的，比如Background-color。则称为重绘。

# 懒加载

* 减少无效资源的加载
* 并发加载的资源过多会阻塞js的加载，影响网站的正常使用
  * 浏览器并发的线程是有限的

原理：

在浏览器进入可视区域之前，img的src指向占位图片，只有在进入可视区域之后，替换src为真正的图片位置

做法

监听scroll事件，在scroll事件的回调中，去判断我们的懒加载图片是否进入可视区域

判断图片是否进入可视区域： 图片的上边缘是否小于设备的Height

注意：在图片加载之前，需要占位，即设置好原本的高度

```html
<img src="" class="image-item" lazyload="true" data-original="http://image.png">
```

```js
var viewHeight = document.documentElement.clientHeight

function lazyload() {
    var eles = document.querySelectorAll('img[data-original][lazyload]')
    Array.prototype.forEach.call(eles, function(item, index) {
        var ret
        if (item.dataset.original === '')
            return 
        rect = item.getBoundingClientRect()

        if (rect.bottom >= 0 && rect.top < viewHeight) {
            !function() {
                var img = new Image()
                img.src = item.dataset.original
                img.onload = function () {
                    item.src = img.src
                }
                item.removeAttribute('data-original')
                item.removeAttribute('lazyload')
            }()
        }
    })
}

lazyload()


document.addEventListener('scroll', lazyload)
```

预加载（Preload）

preload.js

图片等静态资源在使用之前的提前请求

* 资源使用到时能从缓存中加载，提升用户体验
* 页面展示的依赖关系维护

![](/assets/preload.png)

原理

1. &lt;img&gt;标签
2. js中new一个Image\(\)对象
3. xmlhttprequest



