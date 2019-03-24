# 移动Web相关知识 #

## Pixel移动开发像素知识 ##
- **px**:CSS pixels逻辑像素，浏览器使用的抽象单位
- **dp,pt**:device independent设备无关像素
- **dpr**:devicePixelRatio设备像素缩放比
计算公式： $$ 1px = (dpr)^2 * dp $$
- **dpi**:打印机每英寸可以喷的墨汁点（印刷行业）
- **ppi**:屏幕每英寸的像素数量，即单位英寸的像素密度
目前，在计算机显示设备参数描述上，dpi和ppi表达的意思是一样的。
计算公式：$$ ppi = {\sqrt{x^2+y^2} \over 英寸} $$
其中，x，y为物理像素。
## Viewport ##
自动缩放匹配设备界面。
```
<meta name = "viewport" 
	content = "width = device-width",
	initial-scale = 1,
	user-scalable = no">
```
## Flex弹性布局 ##
> 参考阮一峰博客资料，作者配图很棒

任何一个容器都可以指定为Flex布局：
```
.box{
	display: flex;
	display: -webkit-flex; //webkit内核浏览器必须加-webkit-flex
}
```
行内元素也可以使用:
```
.box{
	display: inline-flex;
}
```
> 注意：设为flex布局后，子元素的float、clear和vertical-align属性将失效

采用 Flex 布局的元素，称为 Flex 容器（flex container），简称"容器"。它的所有子元素自动成为容器成员，称为 Flex 项目（flex item），简称"项目"。
![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071004.png)


- 容器默认存在两根轴：水平的主轴（*main axis*）和垂直的交叉轴（*cross axis*）;
- 主轴的开始位置（与边框的交叉点）叫做 *main start*,结束位置叫做 *main end*;
- 交叉轴的开始位置叫做 *cross start* ，结束位置叫做 *cross end* ；
- 项目默认沿主轴排列。单个项目占据的空间叫做 *main size* ,占据的交叉空间叫做 *cross size* 。

- 容器的属性：
```
	1. flex-direction
	2. flex-wrap
	3. flex-flow
	4. justify-content
	5. align-items
	6. align-content
```
1. flex-direction属性
flex-direction属性决定主轴的方向（即项目的排列方向）


