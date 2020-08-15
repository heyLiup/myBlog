# three.js记录

## 入门

1. three.js中完成3D绘图的三大要素

> 有一个场景(scene)，通过相机(carmer)各种拍摄，最后通过渲染器(render)转化为用户所见的图像

2. 场景
>场景是所有物体的容器，场景只有一种
```js
let scene = new THREE.Scene()
```

3. 相机
>透视相机(perspectiveCamera)  

|透视相机参数|介绍|
|:-|:-|
|fov|表示视场，即摄像机能看到的视野。推荐默认值50|
|aspect|指定渲染结果横向尺寸和纵向尺寸的比值，推荐默认值为窗口的长宽比，即window.innerWidth/window.innerHeight|
|near|指定从距离摄像机多近的位置开始渲染，推荐默认值0.1|
|far|指定摄像机从它所在的位置最远能看到多远，太小场景中的远处不会被渲染，太大会浪费资源影响性能，推荐默认值1000|


>正交投影相机(OrthographicCamera) : 在这种投影模式下，无论物体距离相机距离远或者近，在最终渲染的图片中物体的大小都保持不变

4. 坐标轴
```js

var axisHelper = new THREE.AxisHelper(250);
scene.add(axisHelper)

//坐标轴的颜色 rgb 分别代表 xyz轴
```


5. 时间THREE.Clock

```js
requestAnimationFrame 执行的时间间隔不一致，可使用 Clock来准确计算时间

```


!!!include(docs/blog/three/tips.md)!!!
!!!include(docs/blog/three/question.md)!!!
!!!include(docs/blog/three/plugins.md)!!!

