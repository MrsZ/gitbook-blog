主要考虑地图上的定位问题

# Requirements

1. 作为rider,需要找到当前位置附近所有的driver
2. How to design a real time system： driver update location, speed and direction per 4 seconds.

# Solution

GeoHash可以解决点的问题，R Tree可以解决线的问题

Real-time system: 



GeoHash的感性认识

1. GeoHash将二维的经纬度转换成字符串，比如下图展示了北京9个区域的GeoHash字符串，分别是WX4ER，WX4G2、WX4G3等等，每一个字符串代表了某一矩形区域。
2. 字符串越长，表示的范围越精确
3. 字符串相似的表示距离相近

![](/assets/GeoHash.png)

