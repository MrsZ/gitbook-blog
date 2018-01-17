主要考虑地图上的定位问题

# Requirements

1. 作为rider,需要找到当前位置附近所有的driver
2. How to design a real time system： driver update location, speed and direction per 4 seconds.

# Solution

GeoHash可以解决点的问题，R Tree可以解决线的问题

首先GeoHash用四边型切分地图，以当前位置为圆心，距离为半径可以生成一个圆，可以查询圆形覆盖到的四边形内的所有driver。GeoHash的精度，即hash长度，应该根据日常区域内的流量和系统的负载能力来决定。

```js
class Util {

    getHash(lat, lng) {
        // 获取当前区块geohash值
        return hash;
    }

    getAroundHash(hash, radius) {
        // return 被radius覆盖到的区域
        return [];
    }

    getDrivers(hash) {
        // query database or cache
        // return an array of driver
        return [];
    }

}

class Point {
    constructor(lat, lng) {
        this.lat = lat;
        this.lng = lng;
    }
}

class Customer {
    constructor(lat, lng, radius) {
        this.lat = lat;
        this.lng = lng;
        this.radius = radius;
        this.geoHash = getHash(lat, lng);
    }

    getNearDrivers(lat, lng, radius) {
        let areas = getAroundHash(this.geoHash).concat(this.geoHash);
        let drivers = areas.map(hash => {
                return getDrivers(hash)
            }).reduce((arr1, arr2) => {
                return arr1.concat(arr2);
            });

         return drivers.filter(driver => {
            let distance = getDistance(this.lat, this.lng, driver.lat, driver.lng);
            return distance <= this.radius;
        });
    }
}
```

Real-time system:

Driver每4秒update一次位置和速度方向信息，怎么样保证他们都被收到并且存下来呢。我们可以用一个distrubuted message Queue，类似kafka，producer把内容写到messageQueue来，我们的server有很多worker从message Queue里面拿到数据并且分析数据，然后记录下来，供rider来使用。有一个问题是如果我们把所有的这些都放在同一个地方，就会很拥挤，而大部分的Uber的ride都是在同一个城市里的，而且我们要求实时计算，所以delay可能会很严重，所以我们可以把这些数据都分成不同的shard，相同的城市可以用一个shard，这样的好处就是大部分的Uber Ride应该是同城市的，而down side是如果是cross city的话就会比较expensive，还有一点就是小城市和大城市的traffic差距很多，所以我们可以把很多小城市组合在一起。



GeoHash的感性认识

1. GeoHash将二维的经纬度转换成字符串，比如下图展示了北京9个区域的GeoHash字符串，分别是WX4ER，WX4G2、WX4G3等等，每一个字符串代表了某一矩形区域。
2. 字符串越长，表示的范围越精确
3. 字符串相似的表示距离相近

![](/assets/GeoHash.png)

# Ref

GeoHash核心原理解析: [http://www.cnblogs.com/LBSer/p/3310455.html](http://www.cnblogs.com/LBSer/p/3310455.html)

