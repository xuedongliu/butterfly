# 画布(Canvas)

```
let canvas = new Canvas({
  root: dom,              //canvas的根节点(必传)
  layout: 'ForceLayout'   //布局设置(可传)
  zoomable: true,         //可缩放(可传)
  moveable: true,         //可平移(可传)
  draggable: true,        //节点可拖动(可传)
  linkable: true,         //节点可连接(可传)
  disLinkable: true,      //节点可取消连接(可传)
  theme: {                //主题定制(可传) 
    edge: {
      type: 'Bezier',     //线条类型：贝塞尔曲线，折线，直线
      Class: XXClass,     //自己拓展的class
      isExpandWidth: false //增加线条交互区域
    },
    endpoint: {
      position: []        //限制锚点位置['Top', 'Bottom', 'Left', 'Right']
    }
  },
  global: {               //自定义配置，会贯穿所有canvas，group，node，edge，endpoint对象
    isStrict: false       //scope是否为严格模式(默认为false)
  }
});
```

### 属性：

| key | 说明 | 类型 | 默认值 
| :------ | :------ | :------ | :------ 
| root | 渲染画布的跟节点 | Dom (Require) | `*这个dom必须设置position:relative`
| layout | 自动布局 | string (Option) | null 
| zoomable | 画布是否可缩放 | boolean (Option) | false 
| moveable | 画布是否可移动 | boolean (Option) | false 
| draggable | 画布节点是否可拖动 | boolean (Option) | false 
| linkable | 画布节点是否可连接 | boolean (Option) | false 
| disLinkable | 画布节点是否可取消连接 | boolean (Option) | false 
| theme | 画布主题 | object (Option) | undefined
| global | 全局属性 | object (Option) | undefined


### API：
```
/**
  * 渲染方法
  * @param {data} data  - 里面包含分组，节点，连线
  * @param {function} callback  - `*渲染过程是异步的过程，需要的用户请留意回调`
  */
draw = (data, calllback) => {}

/**
  * 添加分组
  * @param {object|Group} object  - 分组的信息；Group － 分组的基类
  */
addGroup = (object|Group) => {}

/**
  * 根据id获取node
  * @param {string} id  - node id
  * @return {Node} - 节点对象
  */
getNode = (string) => {}

/**
  * 根据id获取group
  * @param {string} id  - group id
  * @return {Group} - 分组对象
  */
getGroup = (string) => {}

/**
  * 根据id获取相邻的edge
  * @param {string} id  - node id
  * @return {Edges} - 相邻的连线
  */
getNeighborEdges = (string) => {}

/**
  * 添加节点
  * @param {object|Node} object  - 节点的信息；Node － 节点的基类
  */
addNode = (object|Node) => {}

/**
  * 添加连线
  * @param {object|Edge} object  - 连线的信息；Edge － 连线的基类
  */
addEdge = (object|Edge) => {}

/**
  * 设置放大缩小
  * @param {true|false} boolean  - 是否支持放大缩小
  */
removeNode = (string) => {}

/**
  * 根据id删除节点
  * @param {string} id  - node id
  * @return {Node} - 删除的对象
  */
removeGroup = (string) => {}

/**
  * 根据id或者Edge对象来删除线
  * @param {string or Edge} id or Edge  - 线的id或者Edge对象
  * @return {Edge} - 删除的线
  */
removeEdge = (param) => {}

/**
  * 根据id或者Edge对象来批量删除线
  * @param {array} string or Edge  - 线的id或者Edge对象的数组
  * @return {array} Edge - 删除的线
  */
removeEdges = (param) => {}

/**
  * 根据id删除分组
  * @param {string} id  - group id
  * @return {Node} - 删除的对象
  */
setZoomable = (boolean) => {}

/**
  * 设置画布平移
  * @param {true|false} boolean  - 是否支持画布平移
  */
setMoveable = (boolean) => {}

/**
  * 聚焦某个节点/节点组
  * @param {string/function} nodeId/groupId or filter  - 节点的id或者过滤器
  * @param {string} type  - 节点的类型(node or group)
  * @param {function} callback  - 聚焦后的回调
  */
focusNodeWithAnimate = (string, type) => {}

/**
  * 聚焦某多个节点/节点组
  * @param {object} {nodes: [], groups: []}  - 节点和节点组的id数组
  * @param {array} type  - 节点的类型(node or group)
  * @param {function} callback  - 聚焦后的回调
  */
focusNodesWithAnimate = (objs, type) => {}

/**
  * 聚焦整个画布，会自动调整画布位置和缩放
  * @param {function} callback  - 聚焦后的回调
  */
focusCenterWithAnimate = () => {}

/**
  * 设置框选模式
  * @param {true|false} boolean  - 是否开启框选功能
  * @param {array} type - 可接受框选的内容(node/endpoint/edge,默认node)
  */
setSelectMode = (boolean, type) => {}

/**
  * 获取画布的数据模型
  * @return {data} - 画布的数据
  */
getDataMap = (string) => {}

/**
  * 手动设置画布偏移
  * @param {[x, y]} array  - x,y坐标
  */
move = (postion) => {}

/**
  * 手动设置画布缩放
  * @param {scale} float  - 0-1之间的缩放值
  * @param {function} callback  - 缩放后的回调
  */
zoom = (postion) => {}

/**
  * 发送事件
  */
emit = (string, obj) => {}

/**
  * 接受事件
  */
on = (string, callback) => {}

/**
  * 设置网格布局
  * @param {true|false} boolean  - 是否开启网格布局功能
  * @param {array} options - 网格布局的定制化参数
  */
setGirdMode = (show, options) => {}

/**
  * 把画布上的节点，节点组自动对齐(必须在网格布局下才生效)
  */
justifyCoordinate = () => {}


/**
  * 设置辅助线
  * @param {true|false} boolean  - 是否开启辅助线功能
  * @param {array} options - 辅助线的定制化参数
  */
setGuideLine = (show, options) => {}


/**
  * 画布转换为屏幕的坐标
  * @param {array[number]} coordinates - 需要换算的坐标([x,y])
  * @return {number} - 转换后的坐标
  */
canvas2terminal = (coordinates) => {}

/**
  * 屏幕转换为画布的坐标
  * @param {array[number]} coordinates - 需要换算的坐标([x,y])
  * @return {number} - 转换后的坐标
  */
terminal2canvas = (coordinates) => {}

```


### 事件

```
let canvas = new Canvas({...});
canvas.on('type', (data) => {
  //data 数据
});
```

| key | 说明 | 返回 
| :------ | :------ | :------
| system.canvas.click | 点击画布空白处 | -
| system.node.delete | 删除节点 | -
| system.node.move | 移动节点 | -
| system.link.delete | 删除连线 | -
| system.link.connect | 连线成功 | -
| system.group.delete | 删除节点组 | -
| system.group.move | 移动节点组 | -
| system.group.addMembers | 节点组添加节点 | -
| system.group.removeMembers | 节点组删除节点 | -
| system.multiple.select | 框选结果 | -
| system.drag.start | 拖动开始 | -
| system.drag.move | 拖动 | -
| system.drag.end | 拖动结束 | -


### 详细说明