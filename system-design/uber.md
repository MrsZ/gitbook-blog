主要考虑地图上的定位问题

# Requirements

1. 作为rider,需要找到当前位置附近所有的driver
2. How to design a real time system： driver update location, speed and direction per 4 seconds.

# Solution

GeoHash可以解决点的问题，R Tree可以解决线的问题

首先GeoHash用四边型切分地图，以当前位置为圆心，距离为半径可以生成一个圆，可以查询圆形覆盖到的四边形内的所有driver. 由于GeoHash的字符串的长度与精度挂钩，所以我们可以根据当前经纬度和查询半径的精度得到当前所在的四边形的索引和周围的8个区域的索引。最后只用计算在这9个区域所有的driver的经纬度即可。

```js

class Util {

    getHash(lat, lng) {
        // 获取当前区块geohash值
        return hash;
    }
    
    getAroundHash() {
        // return an array, 8 around hash
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

GeoHash的感性认识

1. GeoHash将二维的经纬度转换成字符串，比如下图展示了北京9个区域的GeoHash字符串，分别是WX4ER，WX4G2、WX4G3等等，每一个字符串代表了某一矩形区域。
2. 字符串越长，表示的范围越精确
3. 字符串相似的表示距离相近

![](/assets/GeoHash.png)

# Ref

GeoHash核心原理解析: [http://www.cnblogs.com/LBSer/p/3310455.html](http://www.cnblogs.com/LBSer/p/3310455.html)

