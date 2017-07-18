# HQWebViewFit
TableViewCell加载WebView高度自适应

#为了让web页面中的元素都适应屏幕的宽度显示，需要对WKWebView进行一下设置，原理是加载js代码，然后通过js来设置webview中的元素大小：

// 自适应屏幕宽度js
NSString *jsStr = @"var meta = document.createElement('meta'); meta.setAttribute('name', 'viewport'); meta.setAttribute('content', 'width=device-width'); document.getElementsByTagName('head')[0].appendChild(meta);";
WKUserScript *wkScript = [[WKUserScript alloc] initWithSource:jsStr injectionTime:WKUserScriptInjectionTimeAtDocumentEnd forMainFrameOnly:YES];

1.在cell上嵌套webview之前，一定要在中间多加一层scrollview。
2.在计算cell高度的时候，不建议直接使用系统webview的代理方法，建议使用kvo。
3.进行减少- (UITableViewCell )tableView:(UITableView )tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath方法中对webview的操作，这样能减少webview的重复加载，提高性能和速度。
