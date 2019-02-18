# ZXRequestBlock
### 拦截全局请求
```
[ZXRequestBlock handleRequest:^NSURLRequest *(NSURLRequest *request) {
        //拦截回调在异步线程
        NSLog(@"拦截到请求-%@",request);
        dispatch_async(dispatch_get_main_queue(), ^{
            self.blockTv.text = [self.blockTv.text stringByAppendingString:[NSString stringWithFormat:@"拦截到请求--%@\n",request]];
        });
        //在这里可以将request赋值给可变的NSURLRequest，进行一些修改（例如根据request的url过滤单独对一些请求的请求体进行修改等）然后再return，达到修改request的目的。
        return request;
}];
```
### 禁止网络代理（若当前处于代理网络下，无论是手机全局VPN还是WiFi代理，都将禁止当前应用的所有网络请求，一般用于防抓包，改包等，有利有弊）
```
[ZXRequestBlock disableHttpProxy];
```
### 启用HTTPDNS（将会直接从本地或http://119.29.29.29 进行DNS解析，是一种避免DNS劫持的措施）
```
[ZXRequestBlock enableHttpDns];
```




