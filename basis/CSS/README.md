### 1. CSS3构建3D的世界
* 淘宝造物节、h5doo、720yun
* html5陀螺仪：
	- 陀螺仪又叫角度传感器，是不同于加速度计（G-sensor）的，它的测量物理量是旋转、倾斜是的转动角速度。在手机上，仅用加速度计没办法测量或重构出完整3d动作，测不到转动的动作的。G-sensor只能检测轴向的线性动作。但陀螺仪可以对转动、偏转的动作做很好的测量。这样就可以精确分析判断出使用者的实际动作。而后根据动作，可以对手机做响应的操作。
	- 垂直于手机屏幕：gamma z轴为轴，alpha的作用域为（0，360）
	- 垂直于耳机口：alpha y轴为轴，gamma的作用域为（-180，180）
	- 垂直于sim卡槽：beta x轴为轴，beta的作用域为（-90，90）
	- deviceorientation：设备的物理方向信息，表示为一系列本地坐标的旋角
	- devicemotion：提供设备的加速信息
	- compassneedscalibration：用于通知web站点使用罗盘信息校准上述事件
	- 重力加速度：是一个物体受重力作用的情况下所具有的加速度。与位置有关（G=mg）（其中g=9.80665m/s^2为标准重力加速度）s = GM/r*r
* css3 3D模型（css3d-engine）
	- 球面投影：在三维空间，每个3d模型都等同于一个多面体（即3d模型只能由不弯曲的平面构成），你只能以一个正多边形表示圆，边越多，圆越完美3200*1600的图切成一片一片的。如果把图切成9份（宽度是210px），拼成一个圆时每个图片之间的夹角是40度，每个图片离圆心的位置是288px（利用tan）
	- 立方体投影：1600*1600的图切成一个正方形一个正方形
* 集合touth事件
* javascript 库：parallax：通过视觉差构建

### 2. CSS高级实用技巧【上】
* 早期的双飞翼布局+css hack
	- position float 负边距 等高(padding-bottom:9999px;margin-bottom:-9999px;在container{overflow:hidden}) 盒子模型(margin不会影响盒子模型) 清除浮动【《css那些事儿》】
	- 垂直居中：
	- 伸缩盒：
	```flexible box：box-orient box-pack box-align box-flex box-flex-group box-ordinal-group box-direction box-lines```
```flexible(新): flex flex-group flex-shrink flex-basis flex-flow flex-direction  flex-wrap align-content align-items align-self justify-content order```
* 基于移动端的px和rem转换兼容方案
	- different size different DPR
	- 目前的设计稿一般是640 750 1125 ，一般要先均分成100份，（兼容vh，vm）750/10 = 75px。div宽是240px*120px css的书写改成3.2rem*1.6rem。配合响应式修改html根的大小
	- 字体不建议使用rem的，data-dpr属性动态设置字体大小。屏幕变大放更多的文字，或者屏幕更大放更多的字。
	- 神奇的padding margin-top等比例缩放间距
* 弹性盒子模型与reset的选择
	- flex模型
	- *的杀伤力太大！！！！
	- reset.css重置 normalize.css修复 Neat.css融合了重置和修复
	- html{box-sizing:border-box;}
	- *,*:before,*:after{box-sizing:inherit;} //继承html
* 自制的icon-font与常用字体排版
	- no-image时代，不要超过纯色为2的图片（http://csscon.space/#/）
	- 宋体非宋体，黑体非黑体 windows下的宋体叫中易宋体simsun，mac是华文宋体STSong。windows下的黑体叫中易黑体simhei，mac是华文黑体STHeiti
	- 不要只写中文字体名，保证西文字体在中文字体前面。mac -> linux -> windows
	- 切记不要直接使用设计师psd的设计font-family，关键时刻再去启动font-fase（typo.css entry.css type.css）
	- font-family：sans-serif；系统默认
* css代码检测与团队项目规范（css lint）
* css绘制特殊图形 高级技巧
	- border border-radius造就万千可能
	- after、before任何一个html元素都可以创造3个可以供我们操作的视觉元素，即三个矩形
	- box-shadow是可以定义为任何颜色的，并且同一个元素可以投影出不同的box-shabow
	- 神奇borders构建的三角形
	- 矩形的四条border，不一定永远是一个长条矩形的形状。它在正常情况下是一个梯形的形状，在我们改变这条边相邻的另外两条边的参数时，它的形状会相应得到改变。当我们在这条边的两个顶点加一些borber-radius圆角值的时候，这个形状还会有更奇异不可预知的形变。
* BFC IFC GFC FFC
	- BFC:(就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素)
        box:是css布局的对象和基本单位，直观点来说，就是一个页面是由很多个同类型的box，会参与不同的formatting context（一个决定如何渲染文档的容器），因此box内的元素会以不同的方式渲染。让我们看看有哪些盒子：
        block-level box:display属性为block，list-item，table的元素，会生成block-level box。并且参与block formatting context
        inline-level box:display属性为inline，inline-block，inline-table的元素，会生成inline-level box。并且参与inline formatting context
        formatting context是w3c css2.1 规范中的一个概念，它是页面中的一块渲染区域，并且有一套渲染规则，它决定了其子元素将如何定位，以及和其他元素的关系和相互作用。最常见的formatting context有block formatting context（简称BFC）和inline formatting context（简称IFC）
        哪些元素会生成BFC：根元素（html）、float属性不为none、position为absolute或fixed、display为inline-block，table-cell，table-caption，flex，inline-flex、overflow不为visible(两个元素相互独立)
        例子：自适应两栏布局、清除内部浮动、防止垂直margin重叠
	- IFC:直译为“内联格式化上下文”，它的line box（线框）高度由其包括行内元素中最高的实际高度计算而来（不受到竖直方向的padding/margin影响）
	- GFC:（GirdLayout formatting context）直译为“网络布局格式化上下文”，当为一个元素设置display值为grid的时候，此元素将会获得一个独立的渲染区域，我们可以通过在网络容器上定义网络定义行（grid definition rows）和网络定义列（grid definition columns）属性各在网络项目（grid item）上定义网络行（grid row）和网络列（grid columns）为每个网络项目定义位置和空间。
	- FFC:（flex formatting context）直译为“自适应格式上下文”，display值为flex或者inline-flex的元素会自动自适应容器
* CSS Grid Layout
* CSS分层与面向对象
	- 为什么分层
	- SMACSS:(scalable and modular architecture for css可扩展的模块化架构的css)像oocss一样以减少重复样式为基础，然而SMACSS使用一套五个层次来划分css给项目带来更结构化的方法
		+ base:设定标签元素的预设值（html{} input[type=text]{}）
		+ layout：整个网站的【大架构】的外观（#header{margin:30px}）
		+ module:应用在不同页面公共模块（button{}）
		+ state:定义元素不同的状态（nav--main{.active{}}）
		+ theme:画面上所有【主视觉】的定义（border-color\background-image）
		+ 修饰符使用的是--，子模块使用_符号
	- BEM
	- SUIT
	- ACSS:原子（atoms）是创建一个区块的最基本的特质，比如说表单按钮。分子（molecules）是很多原子的组合，比如说一个表单中包括了一个标签，输入框和按钮。生物（organisms）是众多分子的组合物，比如一个网站的顶部区域，它包括了网站的标题，导航等。面板膜（template）又是众多生物的组合体，比如一个网站页面的布局，而最后的页面就是特殊的模版```.m-10{margin:10px} .w-50{width:50px;}```
	- ITCSS
* 面向对象的css
