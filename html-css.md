# css



### 盒子模型

`box-sizing`: border-box | content-box;

#### BFC

https://segmentfault.com/a/1190000013647777

Block Format Context：块级格式化上下⽂。⼀块独⽴的渲染区域，内部元素的渲染不会影响边界以外的元素 

相关

+ IFC（⾏级格式化上下⽂）- inline 内联 
+ GFC（⽹格布局格式化上下⽂）- display: grid 
+ FFC（⾃适应格式化上下⽂）- display: flex或display: inline-flex

形成 BFC 的条件： 

float 不设置成 none 

position 是 absolute 或者 fixed 

overflow 不是 visible 

display 是 flex 或者 inline-block 等 

应⽤：清除浮动

#### margin

纵向重叠，负值问题

#### float

浮动元素不在⽂档流中

清除浮动 

1. ⽗级div定义height 
2. 最后⼀个浮动元素加空div标签，添加样式clear:both（不推荐） 
3. ⽗级div定义zoom 
4. ⽗级添加overflow：hidden/auto（不推荐） 
5. 浮动元素的容器添加浮动（不推荐，会使整体浮动，影响布局） 
6. after伪元素清除浮动，尾部添加⼀个看不见的块元素清理浮动，设置clear:both （推荐） 
7. before和after双伪元素清除浮动

圣杯布局，双飞翼布局

#### 元素居中

行内

```css
text-align: center		⽔平
line-height：盒⼦⾼度	 垂直
```

块级

```css
display: inline-block;

margin: 0 auto;			水平

position: absolute;		正中
top: 50%;
left: 50%;
transform: translate(-50%，-50%) 

display：flex;			弹性盒子
justify-content: center;
align-items: center; 

display: table-cell;
text-align: center;
vertical-align: middle; 
```

#### 样式单位

em：相对于⾃⾝字体⼤⼩的单位 

rem：相对于 html 标签字体⼤⼩的单位 

vh：相对于视口⾼度⼤⼩的单位

#### 溢出

单行溢出

```css
overflow:hidden
white-space:nowrap
text-overflow: ellipsis
```

多行溢出

+ 基于高度截断
+ 伪元素定位

#### background-size

100%：整个图⽚铺满div 

cover：整个图⽚铺满div，缩放背景图⽚以完全覆盖背景区，可能背景图⽚部分看不见。和 contain 相反，cover 尽可能⼤地缩放背景图像并保持图像的宽⾼⽐例（图像不会被压 扁）。背景图以它的全部宽或者⾼覆盖所在容器。当容器和背景图⼤⼩不同时，背景图的 左/右 或者 上/下 部分会被裁剪 

contain：不能铺满整个div，缩放背景图⽚以完全装⼊背景区，可能背景区部分空⽩。 contain 尽可能地缩放背景并保持图像的宽⾼⽐例（图像不会被压缩）。背景图会填充所在 容器。当背景图和容器的⼤⼩的不同时，容器的空⽩区域（上/下或者左/右）显⽰由 background-color 设置的背景颜⾊ 

auto：不能铺满整个div，以背景图⽚⽐例缩放背景图⽚

#### z-index

⼀个层叠上下⽂可能出现7个层叠等级，从低到⾼排列为 

1. 背景和边框 
2. z-index为负数 
3. block盒模型(位于正常⽂档流，块级，⾮定位) 
4. float盒模型(浮动，⾮定位) 
5. 盒模型(位于正常⽂档流，内联，⾮定位) 
6. z-index=0 
7. z-index为正数(数值越⼤越靠上⽅)

### client、offset&scroll

client 主要与可视区有关 

客户区⼤⼩指的是元素内容及其内边距所占据空间⼤⼩。

offset 主要与⾃⾝有关 

偏移量，可动态得到元素的位置（偏移），⼤⼩。元素在屏幕上占⽤的所有可见空间。元素 ⾼度宽度包括内边距，滚动条和边框。 

offsetParent是⼀个只读属性，返回⼀个指向最近的（closest，指包含层级上的最近）包含 该元素的定位元素。如果没有定位的元素，则 offsetParent 为最近的 table, td, th或body元 素。当元素的 style.display 设置为 “none” 时，offsetParent 返回 null。 

+ element.clientWidth 获取元素可视区的宽度，不包括垂直滚动条 element.offsetWidth 获取元素的宽度= boder + padding + content element.clientHeight 获取元素可视区的⾼度，不包括⽔平滚动条 element.offsetHeight 获取元素的⾼度= boder + padding + content 
+ clientWidth 和 clientHeight 获取的值不包含边框 
+ offsetWidth 和 offsetHeight 获取的值包含左右边框 
+ element.clientTop获取元素的上边框宽度，不包括顶部外边距和内边距 
+ element.clientLeft获取元素的左边框宽度 
+ element.offsetTop获取元素到有定位的⽗盒⼦的顶部距离 
+ element.offsetLeft获取元素到有定位的⽗盒⼦的左侧距离 
+ e.clientX ⿏标距离可视区的左侧距离 
+ e.clientY ⿏标距离可视区的顶部距离 

scroll 滚动系列 

动态获得元素⼤⼩，滚动距离等。具有兼容问题。 

+ scrollWidth 和 scrollHeight 主要⽤于确定元素内容的实际⼤⼩ 
+ scrollLeft 和 scrollTop 属性既可以确定元素当前滚动的状态，也可以设置元素的滚动位置 
+ 垂直滚动 scrollTop > 0 
+ ⽔平滚动 scrollLeft > 0 
+ 将元素的 scrollLeft 和 scrollTop 设置为 0，可以重置元素的滚动位置 

共同点： 返回数字时，均不带单位。 只读。

#### 隐藏元素

display: none：渲染树不会包含该渲染对象，因此该元素不会在页⾯中占据位置， 也不会响应绑定的监听事件。 

visibility: hidden：元素在页⾯中仍占据空间，但是不会响应绑定的监听事件。 

opacity: 0：将元素的透明度设置为0，以此来实现元素的隐藏。元素在页⾯中仍然 占据空间，并且能够响应元素绑定的监听事件。 

position: absolute：通过使⽤绝对定位将元素移除可视区域内，以此来实现元素 的隐藏。 

z-index: 负值：来使其他元素遮盖住该元素，以此来实现隐藏。 

clip/clip-path：使⽤元素裁剪的⽅法来实现元素的隐藏，这种⽅法下，元素仍在 页⾯中占据位置，但是不会响应绑定的监听事件。 

transform: scale(0,0)：将元素缩放为0，来实现元素的隐藏。这种⽅法下，元素仍 在页⾯中占据位置，但是不会响应绑定的监听事件



### 重排、重绘和合成

重排（回流）⼀定触发重绘，重绘不⼀定触发重排。重绘开销⼩，重排代价⾼。

#### 重排

渲染树中部分或全部元素的尺⼨、结构或属性变化，浏览器会重新渲染部分或全部⽂档

触发重排的操作：

+ 初次渲染 
+ 窗⼜⼤⼩改变
+ 元素属性、尺⼨、位置、内容改变 
+ 元素字体⼤⼩变化 
+ 添加或者删除可见 dom 元素 
+ 激活 CSS 伪类(如 :hover) 
+ 查询某些属性或调⽤某些⽅法 
  + clientWidth、clientHeight、clientTop、clientLeft 
  + offsetWidth、offsetHeight、offsetTop、offsetLeft 
  + scrollWidth、scrollHeight、scrollTop、scrollLeft 
  + getComputedStyle() 
  + getBoundingClientRect() 
  + scrollTo()

#### 重绘

某些元素的样式如颜⾊改变，但不影响其在⽂档流中的位置，浏览器会对元素重新绘制 不再执⾏布局阶段，直接进⼊绘制阶段

#### 合成

利⽤transform、opacity和filter可实现合成效果，即GPU加速 避开布局 分块和绘制阶段

#### 优化 

+ 最⼩化重绘和重排：样式集中改变，使⽤添加新样式类名 
+ 使⽤ absolute或 fixed使元素脱离⽂档流(制作复杂动画时对性能有影响) 
+ 开启GPU加速。利⽤css属性transform opacity will-change等，⽐如改变元素位 置，使⽤translate会⽐使⽤绝对定位改变其left或top更⾼效，因为它不会触发重 排或重绘，transform使浏览器为元素创建⼀个GPU图层，这使得动画元素在⼀个 独⽴的层中进⾏渲染，当元素内容没有改变就没必要进⾏渲染。 
+ 使⽤ visibility替换 display: none ，因为前者只会引起重绘，后者会引发回流（改 变了布局） 
+ DOM 离线后修改，如：先把 DOM 设为display:none(有⼀次 Reflow)，然后修改 再显⽰，只会触发⼀次回流 
+ 不要把 DOM 结点属性值放在⼀个循环当成循环⾥的变量 
+ 不要使⽤ table 布局，可能很⼩的⼀个⼩改动会造成整个 table 重新布局 
+ 动画实现速度的选择，动画速度越快，回流次数越多，也可以选择使⽤ requestAnimationFrame 
+ CSS 选择符从右往左匹配查找，避免节点层级过多 
+ 频繁运⾏的动画变为图层，图层能够阻⽌该节点回流影响别的元素。⽐如对于 video 标签，浏览器会⾃动将该节点变为图层 
+ 通过documentFragment创建⼀个DOM⽂档⽚段，在它上⾯批量操作DOM，完成 后再添加到⽂档中，只触发⼀次回流 。documentFragment不是真实DOM的⼀部分，它的变化不会触发DOM树的重新渲 染，不会导致性能问题 效果不甚明显，因为现代浏览器会使⽤队列存储储存多次修改进⾏优化



### 布局

#### 两栏布局

左边宽度固定，右边宽度⾃适应。 

+ 利⽤flex布局，将左边元素设置为固定宽度200px，将右边的元素设置为flex:1 

+ 利⽤浮动。左边元素宽度设置为200px，且设置向左浮动。右边元素的margin-left 设置为200px，宽度设置为auto（默认为auto，撑满整个⽗元素）marginleft/padding-left/calc 
+ 利⽤浮动。左边元素宽度固定 ，设置向左浮动。右侧元素设置 overflow: hidden; 这样右边就触发了 BFC ，BFC 的区域不会与浮动元素发⽣重叠，所以两侧就不会 发⽣重叠。 float + overflow:hidden 
+ 使⽤ calc 计算
+ grid

#### 三栏布局

+ 两边float，中间自适应 overflow：auto
+ flex：左右两栏设置固定⼤⼩，中间⼀栏设置为flex:1
+ 圣杯，双飞翼布局
+ 定位实现



#### flex布局

##### 父容器

```css
flex-direction: row | column | row-reverse;
flex-wrap: wrap;		// 换行
justify-content: space-between | space-around;
align-items: center | flex-start;	// 交叉轴
align-content: space-between;
```

##### 子容器

```css
order: 0				// 定义排列顺序，默认0
flex-grow: 0			// 放大比例
flex-shrink: 1 			// 缩小比例
flex-basis: auto		// 初始尺寸
flex: 0 1 auto
```

#### 响应式布局

页⾯的设计和开发根据⽤户⾏为和设备环境进⾏调整和响应

```css
<meta name="viewport" content="width=device-width, initial-scale=1,
maximum-scale=1, user-scalable=no”>
```

+ width=device-width: ⾃适应⼿机屏幕的尺⼨宽度
+ maximum-scale:缩放⽐例的最⼤值
+ inital-scale:缩放的初始化
+ user-scalable:⽤户可以缩放

实现响应式布局的⽅式 

1. 媒体查询 
2. 百分⽐ 
3. vw/vh 
4. rem

响应式设计实现通常会从以下⼏⽅⾯思考： 

1. 弹性盒⼦和媒体查询等 
2. 百分⽐布局创建流式布局的弹性UI，同时使⽤媒体查询限制元素的尺⼨和内容变 更范围
3.  相对单位使得内容⾃适应调节

缺点： 1. 仅适⽤布局、信息、框架并不复杂的部门类型⽹站 2. 兼容各种设备⼯作量⼤，效率低下 3. 代码累赘，出现隐藏⽆⽤的元素，加载时间加长 4. ⼀定程度上改变了⽹站原有的布局结构



### 过渡与动画

#### SVG 

1. 控制动画延时 
2. 控制属性的连续改变 
3. 控制颜⾊变化 
4. 控制如缩放,旋转等⼏何变化 
5. 控制SVG内元素的移动路径

SVG是对图形的渲染，HTML是对DOM的渲染

#### transition

transition是过度动画。但transition不能实现独⽴的动画，只能在某个标签元素样式或状态 改变时进⾏平滑的动画效果过渡，⽽不是马上改变

在移动端开发中，直接使⽤transition动画会让页⾯变慢甚⾄卡顿。所以我们通常添加 transform:translate3D(0,0,0)或transform:translateZ(0)来开启移动端动画的GPU加速，让 动画过程更加流畅

```css
transition:transform 1s ease;
style="transform: translate(304px, 256px);"
```

#### animation

animation 算是真正意义上的CSS3动画。通过对关键帧和循环次数的控制，页⾯标签元素 会根据设定好的样式改变进⾏平滑过渡 

⽐较CSS3最⼤的优势是摆脱了js的控制，并且能利⽤硬件加速以及实现复杂动画效果

### requestAnimationFrame

requestAnimationFrame是另⼀种Web API，执⾏动画的效果，会在⼀帧(⼀般是16ms)间隔 内根据选择浏览器情况执⾏相关动作 raf按照系统刷新的节奏调⽤！！ 在性能上⽐另两者要好。 通常，我们将执⾏动画的每⼀步传到requestAnimationFrame中，在每次执⾏完后进⾏异步 回调来连续触发动画效果。

### Canvas

canvas作为H5新增元素，借助Web API来实现动画 只有width和height两个属性





### JavaScript 动画 和 CSS动画

#### js动画

JavaScript 动画就是通过对元素样式进⾏渐进式变化编程完成的。这种变化通过⼀个计数器来调 ⽤。当计数器间隔很⼩时，动画看上去就是连贯的。

#### css动画

@keyframes：规则中指定了 CSS 样式，动画将在特定时间逐渐从当前样式更改为新样式。 

animation-name：⽤来绑定动画规则 

animation-duration：定义需要多长时间才能完成动画 

animation-delay：规定动画开始的延迟时间。也就是多久后才开始动画 

animation-iteration-count：指定动画应运⾏的次数。 

animation-direction：指定是向前播放、向后播放还是交替播放动画。 

animation-timing-function：规定动画的速度曲线。 

animation-fill-mode：SS 动画不会在第⼀个关键帧播放之前或在最后⼀个关键帧播放之 后影响元素。animation-fill-mode 属性能够覆盖这种⾏为。 

animation：实现与上例相同的动画效果，也就是类似我们的 font 可以包含所有的相关属 性

```css
@keyframes bluetored {
    from {
        background-color: blue;
        width: 100px;
    }
    to {
        width: 200px;
        background-color: red;
    }
}
.left {
    width: 100px;
    height: 100px;
    background-color: blue;
    animation-name: bluetored;
    animation-duration: 5s;
}
```

#### 优缺点

JS动画 

优点： 

1. 过程可控，在动画中可以实现任何效果，暂停，返回，加速等等

2. 动画效果丰富，可以根据绘图函数实现任意效果，跳跳球，变速等 
2. 兼容性好，使⽤ CSS3 存在兼容问题，但是 JavaScript ⼏乎没有 

缺点： 

1. JavaScript 在浏览器的主线程中运⾏，⽽主线程中还有其它需要运⾏的JavaScript 脚本、样式计算、布局、绘制任务等,对其⼲扰导致线程可能出现阻塞，从⽽造成 丢帧的情况。 
2. 代码的复杂度⾼于CSS动画。 

CSS动画 

优点（浏览器可以对动画进⾏优化）： 

1. 集中所有DOM，⼀次重绘重排，刷新频率和浏览器刷新频率相同。 
2. 代码简单，⽅便调试 
3. 不可见元素不参与重排，节约CPU 
4. 可以使⽤硬件加速（通过 GPU 来提⾼动画性能）。 

缺点： 

1. 运⾏过程控制较弱，⽆法附加事件绑定回调函数。 
2. 代码冗长。





### 选择器权重

内联（1000）> id（100）> 类=属性=伪类 （10）> 标签(类型、元素选择器h1)=伪元素（1）

有!important的权值最⼤，优先级最⾼

:link ：选择未被访问的链接 

:visited：选取已被访问的链接 

:active：选择活动链接 

:hover ：⿏标指针浮动在上⾯的元素 

:focus ：选择具有焦点的 

:first-child：⽗元素的⾸个⼦元素

伪元素选择器 ::before、::after 

::first-letter ：⽤于选取指定选择器的⾸字母

 ::first-line ：选取指定选择器的⾸⾏

 ::before : 选择器在被选元素的内容前⾯插⼊内容 

::after : 选择器在被选元素的内容后⾯插⼊内容



### CSS3 新特性 

1. 新增选择器： p:nth-child（n）{color: rgba（255, 0, 0, 0.75）} 

2.  弹性盒模型： 

   弹性布局： display: flex;

   栅格布局： display: grid; 

3. 渐变 线性渐变： linear-gradient（red, green, blue）； 径向渐变：radial-gradient（red, green, blue） 

4. 边框 border-radius：创建圆⾓边框 box-shadow：为元素添加阴影 border-image：使⽤图⽚来绘制边框 

1. 阴影 box-shadow:3px 3px 3px rgba（0, 64, 128, 0.3）； 
2. 背景 ⽤于确定背景画区：background-clip 设置背景图⽚对齐：background-origin 调整背景图⽚的⼤⼩background-size 控制背景怎样在这些不同的盒⼦中显⽰：background-break 多列布局： column-count: 5; 
3. text-overflow ⽂字溢出时修剪：text-overflow：clip ⽂字溢出时省略符号来代表：text-overflow：ellipsis 
4. transform 转换 transform: translate(120px, 50%)：位移， transform: scale(2, 0.5)：缩放， transform: rotate(0.5turn)：旋转， transform: skew(30deg, 20deg)：倾斜 
5. animation 动画 animation-name：动画名称， animation-duration：动画持续时间， animation-timing-function：动画时间函数， animation-delay：动画延迟时间， animation-iteration-count：动画执⾏次数，可以设置为⼀个整数，也可以设置为 infinite，意思是⽆限循环 animation-direction：动画执⾏⽅向， animation-paly-state：动画播放状态 animation-fill-mode：动画填充模式 

还有多列布局、媒体查询（@media）、混合模式等等，⽽CSS3如今有很多是我们⽇常使 ⽤到的，⽐如我们在处理⽂字溢出时会使⽤ text-overflow ，⽐如我们需要⽂字突破限制12 像素就可以使⽤ transform: scale（0.5）来调整。



### HTML5特性

新增 

新的选择器 document.querySelector、document.querySelectorAll 

媒体播放的 video 和 audio 标签 以前⽤的flash实现 

本地存储 localStorage 和 sessionStorage 

浏览器通知 Notifications 

语义化标签，例如 header，nav，footer，section，article 等标签。 

地理位置 Geolocation 

鉴于隐私性，除⾮⽤户统⼀，否则不可获取⽤户地理位置信息 

离线应⽤ manifest 

全双⼯通信协议 websocket 

浏览器历史对象 history 

多任务处理 webworker 运⾏在后台的JS，独⽴于其他脚本，不影响性能 

拖拽相关API 

增强表单控件 url，date，time，email，calendar，search 

页⾯可见性改变事件 visibilitychange 

跨窗⼜通信 PostMessage 

表单 FormData 对象 

canvas+SVG



### HTML5语义化

优点 

+ 增加代码可读性，结构清晰，便于开发和维护 
+ 对机器友好，⽂字表现⼒丰富，有利于SEO。SEO(Search Engine Optimization)是 搜索引擎优化，为了让⽤户在搜索和⽹站相关的关键词的时候，可以使⽹站在搜索 引擎的排名尽量靠前，从⽽增加流量。 
+ ⽅便设备解析（如盲⼈阅读器等），可⽤于智能分析 
+ 在没有 CSS 样式下，页⾯也能呈现出很好地内容结构、代码结构 

常见的语义化标签 

+ title ：页⾯主体内容 
+ header ： 页眉通常包括⽹站标志、主导航、全站链接以及搜索框。 
+ nav ： 标记导航，仅对⽂档中重要的链接群使⽤。 
+ section ： 定义⽂档中的节（section、区段）。⽐如章节、页眉、页脚或⽂档中的 其他部分。 
+ main，帮助到搜索引擎以及搜索⼯程师找到⽹站的主要内容，本⾝并不承载特殊 的功能和意义。 
+ article： 定义外部的内容，其中的内容独⽴于⽂档的其余部分。 
+ aside ： 定义其所处内容之外的内容。如侧栏、⽂章的⼀组链接、⼴告、友情链 接、相关产品列表等。 
+ footer：页脚，只有当⽗级是body时，才是整个页⾯的页脚。 
+ address： 作者、相关⼈⼠或组织的联系信息（电⼦邮件地址、指向联系信息页的 链接）。

### defer 和 async

defer和async是script标签的两个属性，⽤于在不阻塞页⾯⽂档解析的前提下，控制脚本 的下载和执⾏。 

先了解⼀下页⾯的加载和渲染过程： 

1. 浏览器发送请求，获取HTML⽂档开始从上到下解析并构建DOM 
2. 构建DOM过程中，若遇到外联样式声明和脚本声明，会暂停⽂档解析，并开始下 载样式脚本和⽂件 
3.  样式⽂件下载完成后，构建CSSDOM；脚本⽂件下载完成后，解析并执⾏，再继 续解析⽂档构建DOM 
4. ⽂档解析完成后，将DOM和CSSDOM进⾏关联和映射，最后将视图渲染到浏览器 窗⼜ 

注意，在上述过程中，脚本⽂件的下载和执⾏是和⽂档解析同步的，即它会阻塞⽂档的解 析，若控制的不好，会影响⽤户体验，造成页⾯卡顿。 

因此我们可以在script中声明defer和async这两个属性。 

defer：⽤于开启新的线程下载脚本⽂件，并使脚本在⽂档解析完成后执⾏。 

async： HTML5新增属性，⽤于异步下载脚本⽂件，下载完毕⽴即解释执⾏代码。 

共同点 都是异步加载外部脚本⽂件 不会阻塞页⾯的解析 

区别 

async表⽰异步加载，表后续⽂档的加载和渲染与JS脚本加载和执⾏并⾏进⾏,脚本 ⽂件⼀旦加载完成，会⽴即执⾏，我们⽆法预测每个脚本的下载和执⾏时间顺序， 谁先下载好谁执⾏。 

defer表⽰延迟加载，加载后续⽂档和JS脚本加载（仅加载不执⾏)并⾏进⾏，JS脚 本的执⾏需要等待⽂档所有元素解析完之后，load和DOMContentLoaded事件之 前执⾏，有顺序⽽⾔。



### iframe

将另一个 HTML 页面嵌入到当前页面中。

优点 

1. 实现⼀个窗⼜同时加载多个第三⽅域名下内容 
2. 增加代码复⽤性 

缺点： 

1. 搜索引擎⽆法识别 
2. 影响⾸页⾸屏加载时间 
3. 兼容性差 

限制iframe访问另⼀个页⾯ 设置X-Frame-Options 响应头 ——是否允许⽹页通过iframe 嵌套 

1. deny：完全禁⽌任何⽹页嵌套 
2. sameorigin：只允许同源域名访问 
3. allow-from url：允许url的域名可嵌套 

设置Content-Security-Policy CSP，内容安全策略，限定⽹页允许加载的资源，防范XSS攻击 判断 window.top 页⾯顶级窗⼜和 ⾃⾝窗⼜ window.self 是否相等，若不等则是嵌⼊了 iframe





浏览器,

字符编码,

常用标签,

列表,

路径,

table,

选择器,
文本,

背景

浮动,

盒子模型,

overflow,

定位,

表单,

音频,

视频,

input,

阴影,
响应式布局,

em,rem,vw,

渐变,

动画,

平移,

缩放,

旋转,

关键帧动画,

animate动画库,

3d,

网格布局,