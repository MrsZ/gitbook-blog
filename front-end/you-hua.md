懒加载

* 减少无效资源的加载
* 并发加载的资源过多会阻塞js的加载，影响网站的正常使用
  * 浏览器并发的线程是有限的

原理：

在浏览器进入可视区域之前，img的src指向占位图片，只有在进入可视区域之后，替换src为真正的图片位置

做法

监听scroll事件，在scroll事件的回调中，去判断我们的懒加载图片是否进入可视区域

判断图片是否进入可视区域： 图片的上边缘是否小于设备的Height

注意：在图片加载之前，需要占位，即设置好原本的高度

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

预加载

图片等静态资源在使用之前的提前请求

* 资源使用到时能从缓存中加载，提升用户体验
* 页面展示的依赖关系维护

![](/assets/preload.png)

