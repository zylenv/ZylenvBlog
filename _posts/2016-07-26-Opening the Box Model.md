---
layout: post
title:  "Opening the Box Model"
date:   2016-07-26 19:14:19 +0800
categories: jekyll update
---

##Opening the Box Model
####1、display

浏览器会依据element的display属性来决定这个element如何渲染，display的取值有以下几种：   

-	`block`	A value of block will make that element a block-level element.   

-	`inline` A value of inline will make that element an inline-level element.   

-	`inline-block` Using this value will allow an element to behave as a block-level element, accepting all box model properties. However, the element will be displayed in line with other elements, and it will not begin on a new line by default.   

-	`none` Using a value of `none` will completely hide an element and render the page as if that element doesn't exist. Any elements nested within this element will also be hidden.

####2、Box Model
每一个页面上的元素都是rectangular box，都符合box model。CSS中有一些属性决定着box的大小：`width`,`height`,`padding`,`border`,`margin`。`width`和`height`指定element的内容的大小，`padding`,`border`,`margin`扩大box的外围。


CSS:
		
	div {
		border: 6px solid #949599;
		height: 100px;
		margin: 20px;
		padding: 20px;
		width: 400px;
	}		

div的宽度为：
	
	margin-right + border-right + padding-right + width + padding-left + border-left + margin-left   

div的高度为：

	margin-top + border-top + padding-top + height + padding-bottom + border-bottom + margin-bottom
	
如下图：   

<img src="./images/box-model.png" width="80%" max-width="600px">

当我们设置一个元素的width为 400px 时，它实际的width可能是 492px，我们需要将`padding`,`border`,`margin`考虑进去。实际的width并不仅仅包括width属性，也包含`padding-left`,`padding-right`,`border-left`,`border-right`,`marin-left`,`margin-right`。   


####3、Box Model的相关属性
#####（1）Width & Height
每一个element都有默认的width和height，默认的width和height是由element的display属性决定的。    

-	width   
	`Block-level` element的默认width是100%，独占整个水平空间。`inline`和`inline-block`的width是由element本身内容所需要占用的宽度决定的，`inline-level`的元素没有固定的大小，它的宽高与`non-inline` element相关。    
	指定`non-inline` element的高度使用width属性

-	height
	element默认的height是由它的内容决定的，内容需要多高，它的高度就会扩展多大。
	指定`non-inline` element的高度使用height属性

注: `inline-level` element 不接受`width`、`height`的约束。但是`block`或者`inline-block` element会受`width`、`height`的约束。	

#####（2）Margin & Padding
对于不同type的element，每个浏览器默认的margin和padding都不一样。我们可以使用CSS reset去将这些默认的margin和padding的设为0。   

CSS Reset:
		
	/* http://meyerweb.com/eric/tools/css/reset/ 2. v2.0 | 20110126		License: none (public domain)
	*/
	html, body, div, span, applet, object, iframe,
	h1, h2, h3, h4, h5, h6, p, blockquote, pre,
	a, abbr, acronym, address, big, cite, code,
	del, dfn, em, img, ins, kbd, q, s, samp,
	small, strike, strong, sub, sup, tt, var,
	b, u, i, center,
	dl, dt, dd, ol, ul, li,
	fieldset, form, label, legend,
	table, caption, tbody, tfoot, thead, tr, th, td,
	article, aside, canvas, details, embed,
	figure, figcaption, footer, header, hgroup,
	menu, nav, output, ruby, section, summary,
	time, mark, audio, video {
	  margin: 0;
	  padding: 0;
	  border: 0;
	  font-size: 100%;
	  font: inherit;
	  vertical-align: baseline;
	}
	/* HTML5 display-role reset for older browsers */
	article, aside, details, figcaption, figure,
	footer, header, hgroup, menu, nav, section {
	  display: block;
	}
	body {
	  line-height: 1;
	}
	ol, ul {
	  list-style: none;
	}
	blockquote, q {
	  quotes: none;
	}
	blockquote:before, blockquote:after,
	q:before, q:after {
	  content: '';
	  content: none;
	}
	table {
	  border-collapse: collapse;
	  border-spacing: 0;
	}
margin和padding能帮助用户更好的理清页面上的逻辑。从文字的段落上我们能很好的看到这一点。   

-	Margin `margin`属性允许我们设置围绕一个element的空间。`margin`是一个元素`border`之外的空间，而且完全透明。
-	Padding `padding`是与`margin`非常相似的一个属性。但是它是一个element的`border`之内的
空间。   

注: 	

-	`margin`和`padding`对`inline-level`element 的影响与它对`block`和`inline-block`的影响是不一样的。   
-	`margin`对于`inline-level`element只在水平方向起作用（也就是说margin只有left和right起作用）。   
-	`padding`对`inline-level`element在四个方向上都起作用。但是竖直方向上的`top`、`bottom`可能会导致element侵入它所在行的上方或下方。   
-	`padding`和`margin`对于`block`、`inline-block`element的影响则是正常的。

`margin`, `padding`的值的顺序为`top`,`right`,`bottom`,`left`,从上开始顺时针旋转。   
`margin`, `padding`的背景颜色都是透明的，而且不能设置它的颜色。它会把它底部element的颜色透出来。   

#####（3）Border
`border`处于`margin`和`padding`之间。为element提供一个outline。指定一个border至少需要三个值：`width`、`style`、`color`。也可以通过`border-width`、`border-style`、`border-color`分别单独指定这三个元素。   
指定p的border样式：
		
	p {
		border: 6px solid #994532;
	}
这个样式与下面的CSS样式功效是相等的：
	
	p {
		border-width: 6px;
		border-style: solid;
		border-color: #994532;
	}
	
也可以单独指定border某一边的样式：

	p {
		border-bottom: 6px solid #994532;
	}
	p {
		border-bottom-width: 6px;
		border-bottom-style: solid;
		border-bottom-color: #994532;
	}

###### Border Radius
border radius的单位可以是`px`、`%`。指定一个border radius可以通过四个脚指定：`top-left`,`top-right`,`bottom-right`,`bottom-left`。

	div {
		border-radius: 5px;
	}
	
上面的CSS样式相当于同时指定`top-left`,`top-right`,`bottom-right`,`bottom-left`为5px。单独指定如下：

	div {
		border-top-right-radius: 5px;
	}
	
#####（4）Box Sizing
一般我们要计算一个element的实际大小，需要通过它的`border`、`padding`、`margin`、`width`、`height`等属性计算得到。`box-sizing`是CSS3引进的属性。它允许我们指定element如何计算其大小。`box-sizing`有三个基础的取值`content-box`、`padding-box`、`border-box`,每一个取值对于box的size的计算方式都是不一样的。

-	Content Box	`content-box`是`box-sizing`的默认值。如果你不指定element的box-sizing属性，那么它的box-sizing属性的值就是`content-box`。element的内容大小为width，height属性的值，element的size大小就是width、height加上padding,border和margin属性的值。
-	Padding Box 如果`box-sizing`的值为`padding-box`，那么如果:

		div {
			box-sizing: padding-box;
			padding: 20px;
			width: 200px;
			border:2px;
			margin: 20px;
		}
	element的实际宽度为 margin-left + border-left + width + border-right + margin-right。而element的内容宽度为width减去padding-left和padding-right的值,高度为height减去padding-left和padding-right的值。也就是说width和height属性将padding属性包含在内。
-	Border Box 如果`box-sizing`属性为`border-box`时，width和height属性将 border 和 padding 都包含在内。也就是说如果 element的width为400px，padding为20px，border为10px，那么element的实际宽度还是400px。

**注：** 不管`box-sizing`为什么值，margin都不会包含到width中，element的实际大小都需要加上margin。

总的来说，一般将`box-sizing`设置为`border-box`最好。设置为`border-box`更能方便我们计算element的位置与大小。下面的css代码能将所有element的`box-sizing`默认设置为`border-box`
		
	*,
	*:before,
	*:after {
		-webkit-box-sizing: border-box;
		   -moz-box-sizing: border-box;
			    box-sizing: border-box;
	}

