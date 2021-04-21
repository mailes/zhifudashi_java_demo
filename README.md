# zhifudashi_java_demo
支付大师java_demo版本
# 支付大师 https://www.zhifudashi.com
## 是真正的个人免签约第三方h5支付通道聚合支付接口，云端免挂机监控，即时到账，支持小程序、网站二维码扫码收款。只需个人微信支付宝账号即可自动化收款，超稳定不漏单

## 接口文档  https://docs.zhifudashi.com

### 对接简单，异步回调，安全高效，不限行业

``` java
String uid = "xxxxxxxxx";// 商户号 在商户后台查看
		String order_id = "20210729023137U97661109";// 商户订单号
		String order_price = "1.00";// 支付金额
		String redirect_url = "https://xxxdomain/api/paySuccessNoticeTest";// 填写您的接收支付成功的异步通知地址
		String returnUrl = "";// 同步通知地址
		String order_type = "alipay";// 请求支付类型
		String extension = ""; // 附加参数
		String secretKey = "xxxxxxxxxxxxxxx";//商户密钥APPKEY 在商户后台查看

        // sign 签名是order_id+order_price MD5加密之后 再次+secretKey 然后再次MD5
		String sign = MD5Utils.md5(order_id+order_price)+secretKey;
		sign = MD5Utils.md5(sign);// md5签名
	    System.out.println(sign);
		String url = "https://www.zhifudashi/ApiOrders/createorder"; //"http://www.zhifudashi/ApiOrders/createorder";// 发起订单地址
		Map<String, String> paramMap = new HashMap<>();// post请求的参数
		paramMap.put("order_id", order_id);
		paramMap.put("order_price", order_price);
		paramMap.put("redirect_url", redirect_url);
		paramMap.put("returnUrl", returnUrl);
		paramMap.put("order_type", order_type);
		paramMap.put("extension", extension);
		paramMap.put("sign", sign);
		paramMap.put("order_name", "测试商品name");
        paramMap.put("uid", uid);
		System.out.println(JSONObject.toJSON(paramMap));
//		String result = HttpUtil.post(url, paramMap); //JDK11
//		System.out.println(result);
        String result;
        JSONObject ret = new JSONObject();
        String parameters=map2Json(paramMap);
        System.out.println("parameters=="+parameters);

        try {
            CloseableHttpClient httpclient = HttpClientBuilder.create().build();
            HttpPost httpost = new HttpPost(url); // 设置响应头信息
            String userAgent = "Mozilla/5.0 (Windows NT 6.2; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/54.0.2840.87 Safari/537.36";
            httpost.setHeader("User-Agent",userAgent); //防止被防火墙拦截 Apache httpclient

            httpost.addHeader("Content-type","application/json; charset=utf-8");
            httpost.setHeader("Accept", "application/json");

            httpost.setEntity(new StringEntity(parameters, Charset.forName("UTF-8")));
            
            RequestConfig requestConfig = RequestConfig.custom()  
                .setConnectTimeout(5000).setConnectionRequestTimeout(1000)  
                .setSocketTimeout(5000).build();  
            httpost.setConfig(requestConfig);

            
            HttpResponse retResp = httpclient.execute(httpost);
            result = EntityUtils.toString(retResp.getEntity(), "UTF-8");
            System.out.println(result);
        }
        catch (ClientProtocolException e1) {
            e1.printStackTrace();
        }
        catch (IOException e1) {
            e1.printStackTrace();
        }catch (ParseException e1) {
            e1.printStackTrace();
        }
        

```

### 更多demo
php:  
ios:  
android:  


