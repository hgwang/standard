#JavaScript编码规范
===

##目的

本文档定义了JavaScript的编码规范，旨在推进代码的可维护性和可读性，方便后期的管理和维护。

##编码

所有JavaScript文件均采用**`UTF-8`**编码

##命名规范
* 命名要有意义，可读性强
* 私有变量名用下划线`_`开头
* 一般变量命名用下划线分隔方式或者驼峰方式

		var className = "suning";

* 常量必须使用大写字符,并用下划线分隔

		var ID_USER;

* 为全局代码使用命名空间

		var SN = {}


		function Class(){
		
##变量声明、语句约定
* 声明变量必须加上**`var`**关键字
* 如非必要，javascript代码不应该被包含在HTML文件中
* 即使只有一条语句也不能省略`{}`
    
    	if(boolean){
			return;
    	}

* 每个语句结束必须使用分号
* 使用`{}`代替`new Object()`，使用`[]`代替`new Array()`

		var arr=[],obj={};
	
* 避免使用eval（只用于解析序列化串）

	    $.get(url, function(sn_data_json){




		//在语句的行长度超过 120 时，根据逻辑条件合理缩进。
		if (user.isAuthenticated()
    		&& user.isInRole('admin')
    		&& user.hasAuthority('add-admin')
    		|| user.hasAuthority('delete-admin')
		) {
    		// Code
		}

* 一个函数应该返回统一的数据类型

		//错误示例，bad bad，应该返回同样的数据类型
* 遍历数组不使用 `for in`
	*数组对象可能存在数字以外的属性, 这种情况下 for in 不会得到正确结果*

##空格、缩进、空行

* 语句中的必要空格和缩进，缩进的单位为四个空格，sublime的可以如下设置

		"tab_size": 4,



* for 循环条件中, 分号后留一空格;

		for( var i = 0; i < 10; i++){



* 空对象和数组不要填入空格;
* 不要吝啬空行. 尽量使用空行将逻辑相关的代码块分割开, 以提高程序的可读性.
* 合理的格式化和缩进

		var obj = {

			doSomething(1);
			doSomething(2);
			doSomething(3);

			case '1':
        		// do...
        		break;
    		case '2':
        		// do...
        		break;
    		default:
        		// do...
		}

##类型转换
* [建议]转换成 string 时，使用 `+ ''`

		// good
		num + '';

		// bad
		new String(num);
		num.toString();
		String(num);

* [建议]转换成 number 时，使用`+`

		// good
		+str;

		// bad
		Number(str);
		
* 使用 parseInt 时，必须指定`进制`

##注释

* 参照 [jsDoc](http://usejsdoc.org/)
* 单行注释

		//名称

* 多行注释

		   /**
 			* 函数描述
 			*
 			* @param {string} p1 参数1的说明
 			* @param {string} p2 参数2的说明，比较长
 			*     那就换行了.
			* @param {number=} p3 参数3的说明（可选）
 			* @return {Object} 返回值描述
 			* @
 			*/




	1. 输入单引号不需要按住 shift，方便输入。
	
	2. 实际使用中，字符串经常用来拼接 HTML。为方便 HTML 中包含双引号而不需要转义写法。


	2. 在现代浏览器下，使用 + 拼接字符串，性能较数组的方式要高。
	3. 如需要兼顾老旧浏览器，应尽量使用数组拼接字符串。

		
		
			// 使用数组拼接字符串
			var str = [
    			// 推荐换行开始并缩进开始第一个字符串, 对齐代码, 方便阅读.
    			'<ul>',
        		'<li>第一项</li>',
        		'<li>第二项</li>',
    			'</ul>'
			].join('');

			// 使用 + 拼接字符串
			var str2 = '' 	// 建议第一个为空字符串, 第二个换行开始并缩进开始, 对齐代码, 方便阅读
    		+ '<ul>',
    		+    '<li>第一项</li>',
    		+    '<li>第二项</li>',
    		+ '</ul>';
    		
* 清空数组使用 `.length = 0`	
* 避免 `==` 、`!=` 的使用， 用严格比较条件 `===`、`!==`
* 可以省略script标签的`type`