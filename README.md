基于 WebGL 的 Leaflet 热力图插件
============================

![MIT 许可证](http://img.shields.io/badge/license-MIT-lightgrey.svg)
&nbsp;
![Leaflet](http://img.shields.io/badge/leaflet-1.0.1-green.svg?style=flat)
&nbsp;
[![构建状态](https://travis-ci.org/ursudio/leaflet-webgl-heatmap.svg?branch=master)](https://travis-ci.org/ursudio/leaflet-webgl-heatmap)

一个 Leaflet 插件，基于 [@pyalot](https://github.com/pyalot) 的 [webgl 热力图库](https://github.com/pyalot/webgl-heatmap).

就像 [@pyalot](https://github.com/pyalot) 在他的文章中指出的， [高性能的 JS 热力图](http://codeflow.org/entries/2013/feb/04/high-performance-js-heatmaps/)，有时需要能够将数十万个数据点绘制到地图上（并且由于滞后而导致浏览器崩溃）。

我们使用他的 WebGL 热力图库替换 leaflet 现有的热力图插件。

本插件使用了以下在他的库中存在的参数：

* gradientTexture （使用PNG，而不是默认的绿色到红色）
* alphaRange （显示透明度）

详见 [在线示例](http://ursudio.github.io/leaflet-webgl-heatmap/)

[![Screenshot](http://i.imgur.com/VGXbWpx.png)](http://ursudio.github.io/leaflet-webgl-heatmap/)

## 安装

通过 npm:
```bash
npm install leaflet-webgl-heatmap --save 
```
## 依赖关系

当前版本依赖最新的leaflet库，之前版本对应leaflet版本也不相同。

  * leaflet 1.0.3版本（包括js、css文件）
  * webgl-heatmap.js
  
## 用法

### 创建你的地图

```javascript
var base = L.tileLayer( tileURL );
var map = L.map('mapid', {
	layers : [base],
	center : [44.65, -63.57],
	zoom: 12 
});
```

### 初始化热力图

```javascript
var heatmap = new L.webGLHeatmap({
    size: diameter-in-meters
});
```

**或**以像素为单位（不随地图尺度缩放）：

```javascript
var heatmap = new L.webGLHeatmap({
    size: diameter-in-pixels,
    units: 'px'
});
```

### 添加数据

数据格式为二维数组： `[[lat, lng]...]` ，或者明确每个点的强度： `[[lat, lng, intensity]...]`

```javascript
var dataPoints = [[44.6674, -63.5703, 37], [44.6826, -63.7552, 34], [44.6325, -63.5852, 41], [44.6467, -63.4696, 67], [44.6804, -63.487, 64], [44.6622, -63.5364, 40], [44.603, - 63.743, 52]];
```

得到这样格式的数据后，你就可以使用 `heatmap.setData(dataPoints)`来添加数据集了。

### 将热力图添加到地图

```javascript
map.addLayer( heatmap );
```

## 选项

* size （以 米 为单位或者以 像素 为单位的大小）
* units （m 或者 px）
* opacity （canvas元素的透明度）
* gradientTexture （图片路径或者图片）
* alphaRange （通过改变0到1之间的值来调整透明度）

## 方法

* multiply （将所有点的强度值乘以一个给定的数字）

## 许可

* MIT: 详见 mit-license
