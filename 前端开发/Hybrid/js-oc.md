#JavaScript-Objective-C 交互
##关键类：

类 | 作用
---+---
JSBridge（js） | 全局对象，js端负责和native进行通讯的桥梁
JSValue（iOS） | 保存js对象，可以是对象、方法
JSContext（iOS） | OC中js的执行环境
JSExport（iOS） | 约定js调用的方法名对应native的实现（js注入的一种方式）


##js调用native方式：

* 注入API (js注入)
* 拦截URL Scheme（目前hybrid使用此方案）


方式 | 原理
---+---
注入API   |   如果webView提供的接口，向JavaScript的context（window）中注入对象或方法，让JavaScript调用时，直接执行native代码
拦截scheme   |  约定特别的protocol和host，从而达到native拦截JavaScript发出特定请求的目的

###注入API示例：

* native代码：

```objective-c
JSContext *context = [UIWebView valueForKeyPath:@"documentView.webView.mainFrame.javaScriptContext"];
context[@"jsInvokeNative"] = ^(NSString *str) {
	/// Native 逻辑
	NSLog(@"%@", str);
	/// 输出： Hello word!
};
```

* js调用native：

~~~css
<input type="button" value="addSubView" onclick="jsInvokeNative('Hello word!');" />
~~~

##HYbrid Plugin调用流程：

1、native自定义protocol并进行注入，拦截前端request;

2、组装数据，塞入data（调桥需要的参数）和callBack（native返回后需要执行的function）；

3、为jsCallBack生成唯一的ID（此ID十分关键，native回调js的关键），并挂载到window；

4、使用约定好的Scheme，发送head请求；

5、native拦截request后，根据handlerName找到对应的实现，将来自js的参数和nativeCallback（闭包）重新包装后传入native桥，最终执行native逻辑；

6、native逻辑执行完成后，调用nativeCallback；

7、组装回调数据，塞入native将执行结果和jsCallBackID；

8、调用js全局对象WebViewJavascriptBridge中的_handleMessageFromObjC方法通知js；

9、根据jsCallBackID取出callBack并执行，完成这次桥的调用；


##类型对照表：

Objective-C type | JavaScript type
---+---
nil | undefined
NSNull | null
NSString | string
NSNumber |   number, boolean
NSDictionary | Object object
NSArray | Array object
NSDate | Date object
NSBlock  |  Function object
id  | Wrapper object
Class  | Constructor object




