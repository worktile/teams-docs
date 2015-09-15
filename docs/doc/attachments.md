纷云支持在消息中添加格式更为丰富的内容，以支持各种第三方服务的集成，所以我们为消息设计了attachment属性，该属性可以用在任何往纷云中发消息的场景。

### 结构说明
attachment属性有很多的字段组成，每个字段都有特定的代表意义，一个完整的attachment结构如下：
```
{
	"attachment": {
	    "fallback"   : "用于移动端将提示信息显示在首页上",
	    "color"      : "#f1867e",
	    "pretext"    : "在显示消息正文之前显示的文本内容",
	    "author_name": "Terry Lee",
    	"author_link": "https://github.com/terrylee",
    	"author_icon": "https://avatars1.githubusercontent.com/u/694592?v=3&s=400",
	    "title"      : "消息正文标题",
	    "title_link" : "http://lesschat.com",
	    "text"       : "这里是普通消息的内容，可以很长，也支持换行。",
	    "img"      : "http://static.lesschat.com/example.png",
	    "fields"     : [
	        {
	            "title": "分配者",
	            "value": "Terry",
	            "short": 1
	        },
	        {
	            "title": "优先级",
	            "value": "高",
	            "short": 1
	        }
	    ]
	}
}
```
在接下来的部分会详细介绍每一个字段的意义和使用方式。

### fallback
fallback是一段纯文字的消息说明，描述当前attachment包含的内容，用于在一些不支持丰富格式的客户端或设备中显示，如IRC频道、移动客户端推送的消息等。fallback中应该只包含纯文本，不能包括任何格式化的标记。

是否必须：**是**

### color
color是一个可选的属性，用于在显示attachment属性的内容时，左边框的颜色值。你可以赋予该颜色更多的含义，如用于显示日志信息时表示错误、警告、信息、成功等，或者表示Issue信息时的高优先级、中优先级、低优先级等。color取值为标准的十六进制颜色值，如#fafb03。

![pic](/img/doc_attachment_01.png)

发送的代码为：
```
{
	"attachment": {
	    "fallback"   : "这是一条Success消息",
	    "color"      : "#5cb85c",
	    "text"       : "这是一条Success消息"
	}
}
```

是否必须：**否**

### pretext
pretext是一个可选的属性，用于显示在attachment的内容上方，即不包含在颜色框中的文字显示，该字段支持一些基本的Markdown标记。

![pic](/img/doc_attachment_02.png)

发送的代码为：
```
{
	"attachment": {
	    "fallback"   : "用于不支持富文本格式的客户端显示",
	    "color"      : "#51bcb6",
	    "text"       : "这里是text属性，显示在attachment的内部",
	    "pretext"       : "这里是pretext属性，显示在attachment的顶部"
	}
}
```

是否必须：**否**

### author
author是三个可选的属性，用于在attachment消息中显示作者信息，如发送的消息内容为一篇文章或者微博，想在消息中显示文章作者，可以使用author系列字段，它由以下三个字段构成：

**author_name**：显示作者的名字。

**author_link**：作者的链接地址，该链接会加在author_name上，如果没有指定，则会显示为纯文本。

**author_icon**：作者的头像地址，指定一个图片地址，该图片将会以24*24的尺寸显示在author_name前面。

![pic](/img/doc_attachment_03.png)

发送的代码为：
```
{
	"attachment": {
	    "fallback"   : "用于不支持富文本格式的客户端显示",
	    "color"      : "#51bcb6",
	    "text"    : "这条消息主要展示author的展示效果",
	    "author_name": "Terry Lee",
    	"author_link": "https://github.com/terrylee",
    	"author_icon": "https://avatars1.githubusercontent.com/u/694592?v=3&s=400"
	}
}
```

是否必须：**否**

### title
title是两个可选的属性，用于在attachment中显示标题信息，如发送的消息内容为一篇文章，可以用title显示文章的标题，它由以下两个字段构成：

**title**：显示标题文字信息

**title_link**：标题链接地址，该链接会加在title上。

![pic](/img/doc_attachment_04.png)

发送的代码为：
```
{
	"attachment": {
	    "fallback"   : "用于不支持富文本格式的客户端显示",
	    "color"      : "#51bcb6",
	    "title"      : "这里是attachment中的标题，可以加链接",
	    "title_link" : "http://lesschat.com",
	    "text"       : "这条消息主要展示title的展示效果"
	}
}
```

是否必须：**否**

### text
text属性是attachment中显示主要内容的字段，用于显示大段的文本内容，可以在text属性中使用格式化的标记，请参考[消息格式化](/doc/formatting)。

![pic](/img/doc_attachment_05.png)

发送的代码为：
```
{
	"attachment": {
	    "fallback"   : "用于不支持富文本格式的客户端显示",
	    "color"      : "#51bcb6",
	    "text"       : "纷云是一个 IM 协作平台，以信息流的方式聚合中小团队每天所需服务与工具的消息。团队成员可以在这个平台上创建频道、群聊私聊、进行交流和沟通，还可以进行文件共享、搜索等，同时能针对共享文件发表评论。纷云最大的特点在于，平台上集成了丰富的第三方服务。"
	}
}

```

是否必须：**是**

### fields
fields属性是设计为一个数组，可以包含多个字段，在attachment显示中会使用表格的方式，主要以下三个字段组成：

**title**：字段的标题，通常用于简单明了的说明该title对应的value是什么。

**value**：字段的内容，文本内容，用于显示上面title的详细内容。

**short**：可选属性，表示当前title/value是否需要完整一行显示。

![pic](/img/doc_attachment_06.png)

发送的代码为：
```
{
	"attachment": {
	    "fallback"   : "用于不支持富文本格式的客户端显示",
	    "color"      : "#51bcb6",
	    "text"       : "这条消息主要用于展示fields的展示效果",
	    "fields"     : [
	    	{
	            "title": "任务描述",
	            "value": "这里是非常非常长的一段关于任务描述的说明性文本，所以用一行来显示",
	            "short": 0
	        },
	        {
	            "title": "分配者",
	            "value": "Terry",
	            "short": 1
	        },
	        {
	            "title": "优先级",
	            "value": "高",
	            "short": 1
	        }
	    ]
	}
}
```

是否必须：**否**

### img
img是一个可选属性，用来表示在attachment中要显示的图片信息URL地址，如显示文章的题图信息，或者微博的配图，人员照片等。

![pic](/img/doc_attachment_07.png)

发送的代码为：
```
{
	"attachment": {
	    "fallback"   : "用于不支持富文本格式的客户端显示",
	    "color"      : "#51bcb6",
	    "text"       : "这条消息主要展示img的展示效果",
	    "img"      : "http://static.lesschat.com/3aeac.jpg"
	}
}
```

是否必须：**否**

