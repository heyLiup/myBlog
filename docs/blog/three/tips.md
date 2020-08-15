

### 经验

1. sence坐标中心点(0, 0, 0)为容器中心，所以创建的物体默认居中

2. 向量的`.copy`(复制)与`.clone`(克隆)  

对象执行`.clone()`方法，返回一个新的对象，与原对象一致
```js
var a = new THREE.Vector3(1,1,1);
var copyA = a.clone();

//源码

function clone = function () {
    return new this.constructor(this.x, this.y, this.z)
}
```

执行`b.copy(a)`方法，向量a三个分量的xyz将覆盖b三个分量
```js
var a = new THREE.Vector3(1,1,1);
var b = new THREE.Vector3();
a.copy(b);      // a = b = THREE.Vector3 {x: 0, y: 0, z: 0}
```

3. 向量加减

```js
var a = new THREE.Vector3(1,1,1);

var b = new THREE.Vector3(3,3,3);

//计算b点到坐标原点的距离
b.length();    //5.196152422706632

//向量相减 (a的值会改变，如果不期望改变a值，计算前先clone一份)
a.sub(b).length()  //THREE.Vector3 {x: -2, y: -2, z: -2}

//计算a和b之间的距离  (结果为绝对值)
a.clone().sub(b).length()   //3.4641016151377544

```

3.点积(点乘) .dot()

<img :src="$withBase('./three/images/dot.png')" alt="dock">

```js
已知三角形的三个顶点，求其中一个顶点对应角度的余弦值。


var a = new THREE.Vector3(0, 0, 0);
var b = new THREE.Vector3(20, 0, 0);
var c = new THREE.Vector3(0, 40, 0);

//求a点对应角度的余弦值

// a, b两点确定向量x
var x = a.clone().sub(b);  //THREE.Vector3 {x: -20, y: 0, z: 0}
var y = a.clone().sub(c);  //THREE.Vector3 {x: 0, y: -40, z: 0}

// dot = function (v) {
//     return this.x * v.x + this.y + v.y + this.z + v.z;
// }

var cosValue = x.dot(y) / (x.length() * y.length())

console.log('三角形余弦值' + cosValue);   // 三角形余弦值0

//Math.acos(cosValue)*180 为弧度
console.log('a顶点两边夹角为' + Math.acos(cosValue)*180 / Math.PI);  //a顶点两边夹角为90

```

4. 叉乘

```js
//1.计算两个向量的叉乘
var a = new THREE.Vector3(0, 0, 0);
var b = new THREE.Vector3(20, 0, 0);
var c = new THREE.Vector3();

c.crossVectors(a, b)  //c: THREE.Vector3 {x: 0, y: 0, z: 0}

//2.根据三个点求出三角形的面积
function AreaOfrange (x, y, z) {

    //声明两个空的向量
    var p1 = new THREE.Vector3();

    //根据两个顶点坐标坐标算出两个向量
    var v1 = x.clone().sub(y);
    var v2 = x.clone().sub(z);

    p1.crossVectors(v1, v2)
    return p1.length() / 2
}

var d = new THREE.Vector3(10,10,10);

console.log(AreaOfrange(a, b, d));


//3.多面体都是由三角形构成，可通过三角形的数量乘以三角形的表面积，得出不规则物体的表面积

//长宽高为10 的立方体
// var box = new THREE.BoxGeometry(10, 10, 10);

//球体 
//radius(半径), widthSegments(水平分段数（沿着经线分段），最小值为3，默认值为8
var box = new THREE.SphereGeometry(10, 10); 8)

var area = 0;

for (var i = 0, len = box.faces.length; i < len; i++) {
    //三角形对应顶点索引
    var pointA = box.faces[i].a;
    var pointB = box.faces[i].b;
    var pointC = box.faces[i].c;

    //获得三角形三个顶点的坐标
    var p1 = box.vertices[pointA];
    var p2 = box.vertices[pointB];
    var p3 = box.vertices[pointC];

    area += AreaOfrange(p1, p2, p3)
}

console.log(area);

```

5. 获得顶点坐标几种方式

```js

1.获得曲线的顶点坐标

//创建椭圆曲线
var curve = new THREE.EllipseCurve(
    0,  0,            // ax, aY
    10, 10,           // xRadius, yRadius
    0,  2 * Math.PI,  // aStartAngle, aEndAngle
    false,            // aClockwise
    0                 // aRotation
);

//划分成100份，得到101个坐标
curve.getPoints(100)  

//创建三维样条曲线
new THREE.CatmullRomCurve3([])

```

6. 修复出现锯齿的情况

```js

let renderer = new THREE.WebGLRenderer({
    antialias: true,
    //precision:"lowp"  //着色器的精度。可以是"highp", "mediump" 或 "lowp". 默认为"highp"，如果设备支持的话。
});


```

7. 查看THREE.js版本

```
THREE.REVISION // '113'
```

8. 给缓冲类型集合体设置属性

```
var positions = new Float32Array( length * 3 );
geometry.setAttribute( 'position', new THREE.BufferAttribute( positions, 3 ) );
```

9. 渲染点 片元坐标gl_PointCoord

```
//在片元着色器总将小方块变成小圆球
//比如方形区域的左上角坐标是(0.0,0.0),每个方形区域几何中心坐标是(0.5,0.5)，右下角坐标是(1.0,1.0)
if ( length( gl_PointCoord - vec2( 0.5, 0.5 ) ) > 0.5 ) discard;

```

10. 片元坐标gl_FragCoord

```
内置变量gl_FragCoord表示WebGL在canvas画布上渲染的所有片元或者说像素的坐标，坐标原点是canvas画布的左上角，x轴水平向右，y竖直向下，
gl_FragCoord坐标的单位是像素，gl_FragCoord的值是vec2(x,y),通过gl_FragCoord.x、gl_FragCoord.y方式可以分别访问片元坐标的纵横坐标

```