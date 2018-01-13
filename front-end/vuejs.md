# Properties

props

data

computed

watch

# Life Cycle

image

hook

mounted, beforeDestroy

# Vue Router

# Vuex

states

getters

mutations

actions

modules

mapGetters

mapMutattions

mapActions

use function as getters



# 权限控制

1. 路由权限
2. 资源权限

路由权限控制，主要采用动态路由的方法

首先我们有一套完整的路由表，然后根据用户的路由权限对完整路由进行筛选

```js
let hashMenus = {
    '/route1': true,
    '/route1/route1-1':true,
    '/route1/route1-2':true,
    '/route2':true,
    ...
}
```

然后根据筛选情况，生成路由



视图控制

通过设置Meta data实现



请求控制

利用axios拦截器即可实现

# 

# Optimization

Debounce UI updates

Global cache race condition

# Case Analysis

![](/assets/Pasted image at 2018_01_04 08_38 PM.png)

add a queue to avoid race condition

![](/assets/Pasted image at 2018_01_04 08_38 PM %281%29.png)

implement user cache

![](/assets/Pasted image at 2018_01_04 08_06 PM.png)

debounce

