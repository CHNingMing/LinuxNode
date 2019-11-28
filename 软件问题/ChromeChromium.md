## Chromium

### 不能登录Google账号：

管理员身份打开com，执行：

```
setx GOOGLE_API_KEY "AIzaSyAUoSnO_8k-3D4-fOp-CFopA_NQAkoVCLw"
setx GOOGLE_DEFAULT_CLIENT_ID "6307505647-6knmr84r2pj2leudg3pp1j0h1licd6b9.apps.googleusercontent.com"
setx GOOGLE_DEFAULT_CLIENT_SECRET "rbeWhXTLgU8oLiUeefPsEL9c"
```

## Chrome

###  http网站需要使用录音时：

Chrome启动参数添加:

```http
--no-sandbox --unsafely-treat-insecure-origin-as-secure="http://网站:端口"
```

--no-sandbox --unsafely-treat-insecure-origin-as-secure="http://192.168.1.100:9999"