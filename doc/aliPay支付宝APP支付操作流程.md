## aliPay支付宝APP支付操作流程  





## 1 注册帐号&官方文档解析    

在支付宝商家中心注册帐号,已经拥有支付宝帐号的用户，直接登录商家中心即可(同一个支付宝帐号,可以既是买家也是商家)  

支付宝商户中心: [https://b.alipay.com/](https://b.alipay.com/)  

支付宝APP支付接入流程官方文档: [https://b.alipay.com/signing/productDetail.htm?productId=I1011000290000001002](https://b.alipay.com/signing/productDetail.htm?productId=I1011000290000001002)  

接入指南已经表达的很清楚、简洁，这里只是把流程走一遍  

支付宝APP支付流程: 

- 第一阶段

>创建或登录支付宝账号
>
>在支付宝网站，根据实际业务注册为个人或企业账号并完成认证。

- 第二阶段

> 申请产品
>
> 根据产品要求提交资料，一个工作日即可通过审核。

- 第三阶段

> 使用产品
>
> 根据产品说明，开始使用或启动开发。

- APP支付「申请条件」

>1. 企业或个体工商户可申请；
>2. 需提供真实有效的营业执照，且支付宝账户名称需与营业执照主体一致；
>3. 提供APP名称或产品说明文档，开发者与支付宝账户名称不一致需提供开发合作协议。



## 2 创建应用  

### 2.1 登录支付宝「开放平台」  

如果在第一步已经登录支付宝「**商家中心**」，在页面最上边一栏找到「**开放平台**」并点击进入  

如果之前没有登录支付宝「开放平台」，则直接在「开放平台」进行登录  

支付宝开放平台地址: [https://open.alipay.com](https://open.alipay.com)  

### 2.2 创建应用  

登录开放平台之后，在页面最上边一栏找到「开发者中心」，选择「第三方开发」下的「第三方应用」即可进行应用创建  

「创建第三方应用」要求:  

- 应用名称: 3-20 个字符  
- 应用图标: 上传应用高清图片，支持.jpg .jpeg .png格式，建议320*320像素，小于3M   
- 业务代理范围: 有(1)小程序;(2)网页/移动应用;(3)生活号 三种,APP支付选择(2)  

### 2.3 生成密钥  

应用创建之后是处于待提交状态的，这个时候需要填写密钥  

关于支付宝密钥,工具以及使用说明都在官方文档: [https://docs.open.alipay.com/291/106097](https://docs.open.alipay.com/291/106097)  

除了密钥,还需要设置「应用网关」和「回调地址」  

「应用网关」以及「回调地址」都是由于接收支付宝通知信息的，其中「回调地址」会在每一笔交易完成/状态改变的时候发起通知，这两个都必须填写公网可以访问的地址(**开发初期也可以不填写这两项,不影响支付,但是会接收不到通知** )  

### 2.4 提交应用  

密钥、网关等信息填写完毕之后,即可提交应用,大概**一个工作日**会有回复  

提交的应用通过之后，即可进行开发测试  



## 3 开发测试  

### 3.1 签约APP支付  

支付宝APP支付功能属于需要签约的功能,支付签约需要以下信息:  

- 经营内容: 选择和经营内容或者网站主营业务相近的行业,如3C数码  
- 应用名称: 和之前申请的应用名称保持一致  
- APP说明: 附件形式,具体要求:  [https://cshall.alipay.com/enterprise/knowledgeDetail.htm?knowledgeId=201602055524](https://cshall.alipay.com/enterprise/knowledgeDetail.htm?knowledgeId=201602055524)  

### 3.2 支付宝APP支付必需参数  

支付宝提供了一个沙箱环境,在应用提交并通过之后，可以先进行沙箱测试(**沙箱测试仅支持Android,不支持iOS** )  

支付宝支付必需参数  

| 字段名       | 值&描述                                                      |
| ------------ | ------------------------------------------------------------ |
| appid        | 向发起请求的应用ID,相当于身份识别,沙箱环境和正式环境不同     |
| 支付宝网关   | 支付宝网关,沙箱环境为: https://openapi.alipaydev.com/gateway.do <br>正式环境为:  https://openapi.alipay.com/gateway.do |
| 支付宝公钥   | 支付宝公钥                                                   |
| 应用公钥     | 开发者APP应用公钥，在提交应用时生成的，测试环境可以和生产环境不一致 |
| 应用私钥     | 开发者APP应用私钥，和「应用公钥」的要求一样，公钥和私钥需要匹配 |
| 应用网关     | 开发者APP应用网关，必需是外网可以直接访问的地址              |
| 授权回调地址 | 开发者APP应用回调地址,用于接收支付宝订单支付通知             |

### 3.3 应用上线  

在使用沙箱环境测试没有问题之后，点击上线即可，上线之后可以使用正式环境参数进行调试(iOS开发只有上线)

### 3.4 支付宝支付aliPay服务端demo示例  

Github 源码: [https://github.com/Flying9001/pay](https://github.com/Flying9001/pay)  

支付宝官方文档: [https://docs.open.alipay.com/54/103419/](https://docs.open.alipay.com/54/103419/)  

### 3.4 开发测试工具  

微信支付/支付宝 支付测试工具推荐:  

NATAPP  

简介: 内网穿透工具,可以免费申请**临时**公网域名并映射到本地,用于接收 微信/支付宝 支付结果通知,  

注册**需要实名认证**  

地址: [https://natapp.cn/](https://natapp.cn/)  



