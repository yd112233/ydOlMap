## 添加通过拖放处理向量数据的输入

> 用户可使用openlayers内置方式进行添加

* 手动添加，在创建地图完成后你可以获取一个地图对象，先实例化
  你的交互，然后调用 ``addInteraction()`` 方法添加交互。此添加方式也适合用户
  自定义交互添加。
  
```javascript
  var Map = new HMap({
    target: 'map',
    view: {
      center: [113.53450137499999, 34.44104525],
      projection: 'EPSG:4326',
      zoom: 5
    },
    baseLayers: [
      {
        layerName: 'ArcGIS',
        isDefault: true,
        layerType: 'TileXYZ',
        tileGrid: {
          tileSize: 256,
          extent: [62.21838746752366, 2.0954232465376195, 145.98013922632043, 54.99084140614476],
          origin: [-400, 399.9999999999998],
          resolutions: [
            0.07883072696803219,
            0.04394531353227711,
            0.021972656766138556,
            0.010986328383069278,
            0.005493164191534639,
            0.0027465809060368165,
            0.0013732916427489112,
            6.866458213744556E-4,
            3.433229106872278E-4,
            1.716614553436139E-4,
            8.582953794130404E-5,
            4.291595870115493E-5,
            2.1457979350577466E-5,
            1.0728989675288733E-5,
            5.363305107141452E-6,
            2.681652553570726E-6
          ]
        },
        layerUrl: 'http://211.101.37.251:6080/arcgis/rest/services/HNmapQg/MapServer/tile/{z}/{y}/{x}'
      }
    ]
  });

  var interactionDragAndDrag = new ol.interaction.DragAndDrop({
    formatConstructors: [
      ol.format.GPX,
      ol.format.GeoJSON,
      ol.format.IGC,
      ol.format.KML,
      ol.format.TopoJSON
    ]
  })
  interactionDragAndDrag.on('addfeatures', function (event) {
    var vectorSource = new ol.source.Vector({
      features: event.features,
      projection: event.projection
    });
    var vectorStyle = new ol.style.Style({
      fill: new ol.style.Fill({
        color: 'rgba(0,0,0,0.2)'
      })
    });
    Map.addLayer(new ol.layer.Vector({
      source: vectorSource,
      style: vectorStyle
    }));
    var view = Map.getView();
    view.fit(vectorSource.getExtent(), Map.getSize());
  });
  Map.addInteraction(interactionDragAndDrag)
```  

#### 尝试编辑它
---
<iframe width="100%" height="430"></iframe>

ol.interaction.DragAndDrop 配置项说明

| 配置项 | 简介 | 类型 | 备注 |
| --- | --- |--- | --- |
| formatConstructors | 处理文件的格式 | `Array` | 非必传 |
| source | 数据源 | `ol.source.Vector` | 非必传 |
| projection | 投影坐标系 | `ol.projection` | 非必传 |
| target | 放置目标的元素 | `Element` | 非必传 |
