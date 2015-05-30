#CSS编码规范
===
##目的

本文档定义了CSS的编码规范，旨在推进代码的可维护性和可读性，方便后期的管理和维护。

##编码

所有CSS文件均采用 **`UTF-8`** 编码

##引入方式
* 外联

		<link rel="stylesheet" href="css/commom.css">

* 内联

		<style>...</style>
		
* **注意**
   * 原则上，不允许在html 上直接写样式
   * 内外联方式的类型声明type="text/css" 都可以省略
   * link 和style 标签都应该放入head 中
   * `禁止`在css文件内部采用 @import 方式引入其它css文件
   * 如遇修改线上css 文件内引用的背景图，需要在相应url 后添加版本号，如：
   
   			background: url(images/sprite.png?v=20150307);
   
##命名、规则书写规范
* 规则命名采用小写加中划线 `-` 的方式，不允许使用大写字母或下划线* 命名推荐采用更简明有语义的英文单词进行组合。应尽量避免使用中文拼音，尤其是首字母简拼* 命名应注意缩写，但是不能盲目缩写，具体请参见[常用css命名](#cssName)* DOM 一律不准使用 `id ` 挂载css，且要避免id 与class 重名* 规则名称中不应该包含颜色（red/blue） 、定位（left/right） 、大小（width/height/300px）等与具体显示效果相关的信息。应该使用其意义或功能命名，而不是样式显示结果* `禁止`直接为html tag 添加css 样式（全局的reset 除外），如：
		div { color: red; }

* `禁止`直接为全局类名设置属性
* `禁止`类名中出现 **`ad`** 字样，防止被广告插件屏蔽
* 尽量避免使用!important
* 具体命名规则规定如下：  * 全局(globals)级别模块/组件如：头、尾、迷你购物车、主导航，类名以“g-” 开始；  * 低耦合的通用模块/组件(module)，类名以“m-”开始，如： m-dialog / m-floatbar /m-page，组件库适合采用此类方式命名；  * 其它css命名按照功能划分，可采用一级或多级加中划线方式表示，但不能采用前几条中已经指定的内容；* **如果全局已经使用 `g-` 开头，其他地方请勿用此前缀*** 属性值  	* 属性值采用小写形式，以下情况例外：      * 16 进制色值，必须大写；      * 滤镜等必须使用驼峰式写法的值；    * 属性值可缩写的必须缩写，如：
	  * 如果可以，颜色尽量用三位字符表示，例如#AABBCC 写成#ABC；
	  * 0 后面不需要单位，比如0px 可以省略成0，0.8px 可以省略成.8px；
	  * 如果没有边框时，不要写成border: 0，应该写成border: 0 none；
	  * background、font 等可以缩写的属性，尽量使用缩写形式，但一定要遵循W3C 的顺序规范如：
			selector {				border: 5px solid red;				background: #0F0 url(bgimage.gif) no-repeat fixed top;				font: italic bold 14px/20px 'Microsoft YaHei';			}
* 性能
  * 选择器应该在满足功能的基础上尽量简短，减少嵌套选择器的查询消耗。同时要务必避免覆盖全局样式的设置；  * 注意选择器的性能，不要使用低性能的选择器，例如：

		div > * { ... }		ul > li > a { ... }		body.profile ul.tabs.nav li a { ... }    * 禁止在 css 中使用 * 选择符；  * 除非必须，一般有class 或id 的，不需要再写上元素对应的tag，如：
  		span.important-text { color: red; }	
  	应写成：
		
		.important-text { color: red; }
		  * 合并margin、padding、border 的-left/-top/-right/-bottom 设置，尽量使用缩写；
  * 在保持代码解耦的前提下，尽量合并重复的样式，例如：
  
  		h1 { color: red; }		P { color: red; }  	应写成：
  		h1, p { color: red; }
  * css 背景图要使用sprite 技术。可按照相关度（是否首屏、模块、页面等）合并，并存储为web所用格式。图片优先使用png8 格式保存，并适当压缩体积。在存在透明通道的情况下可使用png24 位图片。在色值较多的情况下，可使用jpg 格式保存。

##规则书写顺序
* 显示、位置属性

		display, position, left, top, float, clear, list-style
		
* 自身属性（盒模型）

		width, height, margin, padding, border

* 背景、行高
	
		background,line-height

* 文本属性

		color, font, text-decoration, text-align, text-indent, vertical-align, white-space,word-wrap,word-break

* 其它

		cursor, z-index, zoom，opacity

* css3

		transform, transition, animation, box-shadow, border-radius

* hack

##CSS取值规范
* font-family
  * font-family 不允许在业务代码中随意设置，需严格遵守视觉给出的规范；
  * css 中的字体不能出现中文，中文字体优先使用别名表示。遇别名中存在空格的情况，必须用引号引起来。如遇某些特殊版本浏览器无效，可使用unicode 编码表示。
  * 常见的中文字体对应unicode 编码及英文名称如下：

	名  称   |  unicode编码         |    别名
  :-------- | :------------------: | :---------:  宋体		|  \5B8B\4F53	        | SimSun  微软雅黑   |  \5FAE\8F6F\96C5\9ED1 | Microsoft YaHei  黑体		|  Microsoft YaHei      | SimHei  仿宋		|  \4EFF\5B8B           | FangSong  楷体		|  \6977\4F53           | KaiTi
* font-size
  * font-size 必须以px 或pt 为单位，推荐用px（注：pt 为打印版字体大小设置）；  * 不允许使用xx-small/x-small/small/medium/large/x-large/xx-large 等值；  * 中文字体大小不允许出现奇数的像素值，如：13px；
* text-indent
  * 使用text-indent 时要避免使用一个很大的值来达到隐藏文字的效果，例如： text-indent:-9999px; 因为使用此规则时，浏览器需要生成一个9999px 宽度的盒模型，这会引起性能问题。推荐使用以下方式达到相同的效果：
		.hide-text { text-indent: 100%; white-space: nowrap; overflow: hidden; }

##注释
* 文件顶部注释(多行)

		/**		 * @description: 文件中文说明		 * @author: yourname		 * @update: yourname (2015-05-29 18:32)		 */
* 模块注释（单行）	

		/* module: 模块中文名称by yourname */
		* 特殊注释
	
		用于标注代办、修改等信息		/* TODO: xxxx by yourname 2015-05-29 18:32 */		/* BUGFIX: xxxx by yourname 2015-05-29 18:32 */
* 长度要求	*注释中的每一行长度不超过40 个汉字，或者80 个英文字符。*
	**为避免极端情况下出现乱码字符导致注释范围意外扩大，注释的星号与内容之间有一个空格。**
	
##排版规范
* 缩进统一使用四个空格缩进
* 规则可以写成单行，或者多行，但是整个文件内的规则排版必须统一
* 单行书写风格
	1. 多个selector 共用一个样式集时，多个selector 之间作为分隔标识的逗号后需要一个空格
	2. 每一条规则的大括号`{ `前后都添加空格
	3. 属性名与值的冒号前不加空格，冒号之后加空格
	4. 每一个属性值后必须添加分号，并且分号后空格
	
			selector, selector2, selector3 { display: block; width: 100px; border: 1px solid #F00; }
			
* 多行的书写风格
	1. 多个selector 共用一个样式集时，多个selector 单独成行：	2. 每一条规则的大括号`{ `前添加空格；	3. 属性名与值的冒号前不加空格，冒号之后加空格；	4. 每一个属性值后必须添加分号；
			selector1,			selector2,			selector3 {				display: block;				width: 100px;				border: 1px solid #F00;			}
* 其他
	1. 在可以不使用引号的情况下尽量不使用引号，如背景图片路径；	2. 使用单引号，不建议使用双引号；	3. 开发阶段的css 文件（非单条样式集），为了能够对开发人员友好，不要求压缩为单行。发布生产的css 文件，外联文件或内联片段都需要压缩为单行，且删除注释与非属性值内空格。
* sublime可以安装[CSS Format插件](https://packagecontrol.io/packages/CSS%20Format)	
##hack
hack 是一把双刃剑，原则上是：最大程度减少hack的使用

	color:red\9;     /* ie6+ */
	color:yellow\0;  /* ie8+ */
	color:yellow\9\0;  /* ie9+ */
	color:#333 !important;   /* 非ie6 */
	*color:green;  /* ie7,ie6 */
	+color:pink;  /* ie7 */
	_color:orange;  /* ie6 */
	
<h2 id="cssName">常用CSS命名</h2>

中文名	  |	 建议类名	    |	中文名	  |		建议类名
:------- | :---------- | :---------- | :--------
头部		| 	header 		|	外围容器		|	wrapper
尾部		|	footer 		|	容器			|	container内容		|	content 	|	页面主体		|	main导航		|	nav			|	栏目/列		|	column顶导航	|	topnav 		|	菜单			|	menu子导航	|	subnav 		|	侧栏			|	sidebar子菜单	|	submenu 	|	模块			|	module标题		|	title 		|	标签页		|	tab小技巧	|	tips 		|	状态			|	status提示信息	|	msg 		|	按钮			|	btn摘要		|	summary 	|	购物车/收银台	|	shop注释		|	note 		|	搜索			|	search结果		|	result 		|	排序			|	sort价格		|	price 		|	滚动			|	scroll下拉		|	drop-down 	|	当前			|	current团购		|	group-buy 	|	母婴			|	redbaby

##常见bug
* [IE6]float时双倍边距，解决方法：
  * 将display属性设置为inline[建议]
  * 使用hack方式，对IE6特殊对待
* [IE6]列表 li 的楼梯 Bug，当在 li 中设置一些浮动但是 li 本身不浮动时，在 ie6 中就会出现楼梯效果。解决方法:
  * 为 li 设置浮动属性.
  * 为 li 设置 inline 属性
* [IE6]小于10px,解决方法：
  * 增加_overflow:hidden;
* [IE6]绝对定位元素消失的问题，解决方法：
  * 不要跟在浮动元素后面
  * 也可以在中间加个清除浮动
* [IE6]overflow:hidden 失效的bug，解决方法：
  * 父元素中设置position:relative
* [IE6]浮动出现3pxbug，解决方法：
  * margin-right:-3px 
* [IE6]重复字符，解决方法：
  * \<!-- --\>注释的影响，试着去掉注释
  * 减小第二个容器的宽度，使得父元素减去子元素大于3px 
  * 加一个或多个clear元素
* [IE6/7] z-index 失效的问题，解决方法：
  * 父元素或者祖元素这是z-index
* [IE6/7] 空\<a\>标签在 ie6，ie7下无法点击的bug，解决方法：
  * 给\<a\>标签设置一个background，然后设置透明度为0
* [chrome] chrome字体不能小于12px,解决方法：
  * -webkit-text-size-adjust:none;
  
##兼容性写法小技巧
* min-height

		min-height:50px;height:auto !important;height:50px;
	
* max-height

		max-height:45px;_height:expression(this.scrollHeight > 45 ? "45px" : "auto");
		
* 背景色透明(子元素不透明)
 		
 		/* AA指透明度，为十六进制正整数，取值范围为 00 – FF，00是完全透明，FF是完全不透明*/
 		filter:progid:DXImageTransform.Microsoft.gradient(enabled='true',
 		startColorstr='#AARRGGBB', endColorstr='#AARRGGBB');
 			