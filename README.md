# arcgis-popup-control

基于ArcGis For JavaScript 4.x的自定义弹窗控制

![20230531\_155823.gif](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4eaf838088a04ff48a6911386ee262d9~tplv-k3u1fbpfcp-watermark.image?)

## Features
*  纯JS实现，兼容性强

## Install

    npm install --save arcgis-popup-control
    or
    pnpm install --save arcgis-popup-control

## Usage

Vue3使用示例:

核心代码
```js
<template>
  <Map>
    <MyPopup v-show="popupVisible" :style="{ position: 'absolute', top: popupPosition.top, left: popupPosition.left }" />
  </Map>
</template>

<script setup>
  import { reactive, ref } from 'vue';
  import PopupControl from 'arcgis-popup-control'
  
  const popupPosition = reactive({left: '0px', top: '0px'})
  let popupVisible = ref(false)
  
  // PopupControl 的部分配置参数
  const options = {
      // 强制性必填
    view, 
      // open的回调返回 { left: 100, top: 100, attributes: {} } 结构的对象
    open: (obj) => { 
      // 更新定位并打开弹窗等逻辑
      popupPosition.left = obj.left + 'px'
      popupPosition.top = obj.top + 'px'
      popupVisible.value = true
    },
    close: () => {
      // popupVisible = false等一些操作逻辑
      popupVisible.value = false
    }
  }
  
  // 创建 PopupControl
  const popupControl = new PopupControl(options)
</script>
```

## Options 参数
| 参数      | 说明    | 类型      | 可选值       | 默认值   |
|---------- |-------- |---------- |-------------  |-------- |
| view | View实例 | View | 必填 | - |
| open | 打开的回调方法, 接收{ left: 100, top: 100, attributes: {} } 结构的对象 | Function | - | - |
| close | 关闭的回调方法 | Function | - | - |
| include | 要包含在hitTest中的图层和图形列表。如果未指定include，则将包括所有图层和图形 | 参照[ArcGis MapView hitTest](https://developers.arcgis.com/javascript/latest/api-reference/esri-views-MapView.html#hitTest) | - | undefined |
| exclude | 要从hitTest中排除的图层和图形列表。如果未指定exclude，则不排除任何图层或图形。 | 参照[ArcGis MapView hitTest](https://developers.arcgis.com/javascript/latest/api-reference/esri-views-MapView.html#hitTest)  | - | undefined |
| emptyClose | 点击空白处弹窗是否自动关闭 | Boolean | false | true |
| dragCloseType | 地图移动时弹窗动作 'close': 关闭弹窗、'hide': 暂时隐藏,停止移动后显示、'never': 不关闭 | Sting | 'close'  'never' | 'hide' |
| positionType | 定位坐标来源, 'click': 点击位置的坐标, 'geometry': Graphic geometry的中心点 | Sting | 'click' | 'geometry' |
| goto | 是否开启view\.goto | Boolean | true | false |
| transition | goTo持续时长（毫秒） | Number | - | 800 |

### 方法
| 方法名 | 说明 | 类型      | 参数 |
| ---- | ---- | ---- | ---- | 
| destroy | 销毁方法 | -  |- |

## Related

*   [`arcgis-popup-example`](https://github.com/1103442828/arcgis-popup) – 示例项目

## License

MIT © [Matheus Fernandes](http://matheus.top)
