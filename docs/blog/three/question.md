### 问题

1. 创建点、线条、面

```js

//声明顶点坐标
var vertices = new Float32Array([
    0, 0, 0,    //顶点1坐标
    50, 0, 0,
    0, 100, 0,
    0, 0, 0,
    50, 0, 0,
    0, 0, 100
])



//创建空的缓存立方体
var geometry = new THREE.BufferGeometry()

//3个数字为一组
var attribute = new THREE.BufferAttribute(vertices, 3);

//添加顶点数据
geometry.attributes.position = attribute;


//创建面
var material = new THREE.MeshBasicMaterial({
    color: 0xfffff,
    side: THREE.DoubleSide   //两面可见
})

var mesh = new THREE.Mesh(geometry, material)
scene.add(mesh)


//创建线
var material = new THREE.LineBasicMaterial({
    color: 0x0000ff,
})
var Line = new THREE.Line(geometry, material)
scene.add(Line)

//创建点
var material = new THREE.PointsMaterial({
    color: 0x0000ff,
    size: 50
})

var points = new THREE.Points(geometry, material)
scene.add(points)
```

2. 材质颜色

```js

//声明各顶点颜色
var colors = new Float32Array([
    1, 0, 0,    //顶点1颜色
    0, 1, 0,
    0, 1, 0,

    0, 0, 1,
    1, 0, 0,
    0, 0, 1
])


// THREE.NoColors
// THREE.FaceColors
// THREE.VertexColors

geometry.attributes.color = new THREE.BufferAttribute(colors, 3);

//线
var material = new THREE.LineBasicMaterial({
    vertexColors: THREE.VertexColors    //选择VertexColors进行颜色的插值计算，可画出有颜色渐变的线条
})
var Line = new THREE.Line(geometry, material)
scene.add(Line)

```


3. 投影

```js

//渲染器，允许使用阴影贴图
renderer.shadowMap.enabled = true;

//开启光源产生投影
light.castShadow = true; 

//产生投影
mesh.castShadow = true; //default is false

//底座接受投影
planeMesh.receiveShadow = true 

//开启投影辅助线
var helper = new THREE.CameraHelper( light.shadow.camera );

```

4. ExtrudeGeometry 拉伸