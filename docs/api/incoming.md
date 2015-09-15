使用Incoming Webhook可以非常方便的把外部服务的数据实时发送到纷云指定的频道中，同时你也可以自定义消息发送者的名称和头像。如你想把公司内部的办公系统，或者项目管理系统中团队成员产生的消息发送到纷云，或者自定义实现服务器的监控，定时把服务器的状态发送到纷云。

### 发送普通消息
在发送消息时，需要在POST Body中发送JSON字符串作为参数，并且设置Content-Type为`application/json`，发送的JSON字符串中至少需要包含`text`属性作为消息内容，如发送的消息内容为：
```
{
    "text": "这是一条来自于Incoming Webhook的消息。\n并且消息还可以换行。"
}
```
在频道中将会展示为：

![pic](/img/api_incoming_01.png)

### 发送带链接消息
如果要在发送的消息中带有链接，可以使用`[]`把URL封装起来，这样发送的消息中的链接会变为可点击，如果要使用文字代替URL显示，使用`|`符号，如下面的示例代码：
```
{
    "text": "[http://lesschat.com|点击查看]任务详细内容。"
}
```
在频道中将会展示为：

![pic](/img/api_incoming_02.png)

### 自定义名称和图标
在添加完Incoming Webhook服务后，可以自己定义Incoming Webhook的显示名称和头像，如下面的截图中自定义了一个名为部署机器人的Webhook：

![pic](/img/api_incoming_03.png)

### 定义复杂消息格式
你可以使用纷云提供的消息格式规则，发送更为丰富的消息格式，具体的消息格式化规则请参考[消息格式化](/doc/formatting)，同时还可以使用附加消息内容的方式，为纷云消息中提供更多内容，详细描述请参考[附加消息内容](/doc/attachments)。下面是一个带有附加内容的消息格式：

![pic](/img/api_incoming_04.png)

在发起的POST请求中，Body中发送的数据格式为：
```
{
	"attachment": {
	    "fallback"   : "用于移动端将提示信息显示在首页上",
	    "color"      : "#f1867e",
	    "pretext"    : "在显示消息正文之前显示的文本内容",
	    "title"      : "消息正文标题",
	    "title_link" : "http://lesschat.com",
	    "text"       : "这里是普通消息的内容，可以很长，也支持换行。",
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
