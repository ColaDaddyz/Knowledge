# Ajax
Ajax (Asynchronous JavaScript and XML、异步 JavaScript 与 XML) 是用于描述利用 XMLHttpRequest 对象所实现的客户与服务器之间的异步通信。

Ajax 的核心规则之一就是：不能存在域外链接。这是通过使用跨域资源共享 (Cross-Origin Resource Sharing CORS) 标准强制实施的

## HTTP请求
#### 建立连接

建立连接的步骤
1. 创建 XMLHttpRequest 实例
2. 对该对象进行适当的配置
3. 通过特定的 HTTP 动词和目的地址打开请求
4. 发送请求


```  JavaScript
	//创建请求
	var xml = new XMLHttpRequest();
	
	//设置Header
	xml.setRequestHeader('Content-type','application/x-www-form-urlencoded')

	//打开套接字
	xml.open('GET','/some/api',true)
	
	//建立连接
	xhr.open();
```
#### 数据序列化
向服务器发送一组数据的第一步就是对其进行格式化，这个过程称作 *序列化*(serialization)，在序列化之前要考虑这么几个问题
1. 要发送什么数据，发送的是键值对么？数据量大么？是文件么？
2. 打算怎样发送数据，GET？POST？还是其他HTTP动词
3. 要使用什么样的数据格式，目前有两种：`application/x-www-form-urlencoded` 和 `multipart/form-data`，前者叫做查询字符串编码 (`query string encoding`)，采用的是 `var1=1&var2=2` 这种形式

对于 `multipart/form-data` ，现代浏览器中可以使用 `FormData` 对象来处理，注意并非所有浏览器都支持。

##### FormData
`FormData` 是 `HTML5` 中的一个提案。它可以初始化为空或者和表单元素联系在一起，如果要用表单初始化需要一个指向表单DOM元素的引用 (使用getElementById())，并将其传入 `FormData` 构造器。


``` JavaScript
var formDataObj = new FormData();

//追加数据
formDataObj.append('first','Yakkp');
formDataObj.append('second','hahaha');

var xml = new XMLHttpRequest();

xml.open('POST','/some/api');

xml.send(formDataObj);
```

目前，W3C的规范中只有 `append()` 函数，意味着 `FormData` 对象是单向的，可以添加数据，但是只能在 HTTP 请求的另一端访问。

#### HTTP 响应
TODO 读取相应数据 监听请求进度，超时检查，跨域

``` JavaScript
```
##### 超时检查

``` JavaScript
//设置超时时间
xml.timeout = 5000;
//监听超时事件
xml.addEventListener('timeout',onTimeOut,false);
```

##### 跨域
默认情况下浏览器不允许应用程序向站点所在服务器之外的其他服务器发出请求，如果需要跨域，服务器需要修改 `Header`


```
Access-Control-Allow-Origin:* 
	//使用通配符表示允许所有用户访问
Access-Control-Allow-Origin:http://spaceappleyoshi.com
	//只允许特定域名访问
```

