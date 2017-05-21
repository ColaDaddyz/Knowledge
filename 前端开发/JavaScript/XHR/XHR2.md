# XHR2
## FormData

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

## 超时

```
xhr.timeout = 1000
xhr.ontimeout = function(){
	console.log('timeout')
}
```

## overrideMimeType
重写`xhr`的mime类型，让浏览器用别的方式处理返回值，很少用，了解

## 进度
目前有6个进度事件：

1. loadstart：在接收到响应数据的第一个字节时触发
2. progress：在接收响应期间不断触发
3. error：请求发生错误时触发
4. abort：因为调用 abort 终止时触发
5. load：在接收到完整的响应数据时触发
6. loadend：在通信完成或者触发error，abort，load事件后触发

### load
为了简化异步交互模型，ff添加了一个load事件，响应接收完毕后将处罚load事件，但是并非所有浏览器都实现了，因此需要注意

### progress

必须在 open 之前调用 onprogress 处理事件
```
xhr.onprogress = function(event){
	event.lengthComputable; 进度信息是否可用
	event.position; 已经接收的字节数
	event.totalSize; 根据Content-Length确定的预期字节数
}
```

