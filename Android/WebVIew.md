# WebView

如果webview指向的是网页,AndroidManifest.xml中添加访问网络权限:

```xml
<uses-permission android:name="android.permission.INTERNET"/>
```

## 启动时设置WebView:

Android调用JS/JS调用Android

```java
webView = findViewById(R.id.webview);
//设置webview
webView.setWebChromeClient(new WebChromeClient());
WebViewClient webViewClient = new WebViewClient(){
            @Override
    		//表示在页面加载完成时触发
            public void onPageFinished(WebView view, String url) {
                //Android动态调用JS方法
                webView.post(new Runnable() {
                    @Override
                    public void run() {
                        //Android调用JS
                        webView.loadUrl("javascript:loadUserInfo('hello!')");
                    }
                });
                super.onPageFinished(view, url);
            }
        };
webView.setWebViewClient(webViewClient);
//打开javascript支持
webView.getSettings().setJavaScriptEnabled(true);
//将指定类下方法映射到JS test对象(this,当前类方法),通过test.当前类方法名() 调用方法
webView.addJavascriptInterface(this,"test");
//加载网页,尽量设置webView后调用加载
webView.loadUrl("http://mall.sinopharmlrt.com/wxweb/login/login");
```

### 类中声明JS调用方法

```java
//声明后,可通过test.saveUserInfo('admin','123456')调用
@JavascriptInterface
public void saveUserInfo(String username,String password){

}
```













