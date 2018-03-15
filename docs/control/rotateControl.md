## 添加旋转控件

> 为用户提供了单独的旋转控件，可配置开启，也可手动添加，也可单独配合openlayers使用

### 如何使用

> 旋转控件(具体代码实现：[rotate](https://github.com/sakitam-fdd/ol-extent/blob/master/src/control/RotateControl.js))。
  此控件以实现并包含在HMap内部。所以你可以按照以下代码添加控件。

* 配置中开启, 直接在controls设置rotate为true。
* 注：旋转控件默认即开启

```javascript
  var Map = new HMap('map', {
    controls: {
      rotate: true
    },
    view: {
      center: [12118909.300259633, 4086043.1061670054],
      zoom: 5,
    },
    baseLayers: [
      {
        layerName: 'firstLayer',
        layerType: 'OSM',
        isDefault: true,
        layerUrl: 'https://{a-c}.tile.openstreetmap.org/{z}/{x}/{y}.png'
      }
    ]
  });
```

#### 尝试编辑它
---
<iframe width="100%" height="430"></iframe>

* 手动添加，在创建地图完成后你可以获取一个地图对象，先实例化
  你的控件，然后调用 ``addControl()`` 方法添加控件。此添加方式也适合用户
  自定义的控件添加。

```javascript
  var Map = new HMap('map', {
    view: {
      center: [12118909.300259633, 4086043.1061670054],
      zoom: 5,
    },
    baseLayers: [
      {
        layerName: 'firstLayer',
        layerType: 'OSM',
        isDefault: true,
        layerUrl: 'https://{a-c}.tile.openstreetmap.org/{z}/{x}/{y}.png'
      }
    ]
  });

  var olControlRotateControl = new ol.control.RotateControl()
  Map.addControl(olControlRotateControl)
```

#### 尝试编辑它
---
<iframe width="100%" height="430"></iframe>

> rotate控件配置

配置项说明

| 配置项 | 简介 | 类型 | 备注 |
| --- | --- |--- | --- |
| className | CSS类名，可自定义样式 | `String` | 非必传 默认 ```hmap-rotate-control```  |
| render | 当控件重新呈现时调用的函数 | `Function` | 非必传 |
| resetNorth | 回调函数 | `Function` | 非必传 |
| duration | 动画持续时间 | `Number` | 非必传 单位毫秒 默认250毫秒 |
| autoHide | 是否自动隐藏 | `Boolean` | 非必传 默认 true |
| target | 控件的目标对象 | `Element` | 非必传 |
