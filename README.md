# spider-2
## 实例
<pre>
import requests
response = requset.get('https://ww.baidu.com/')
print(type(response))
print(response.status_code)
print(type(response.text))
print(response.text)
print(response.cookise)
</pre>
## 传参
<pre>
import requests
data = {
  'name':'germey',
  'age':'22'
}
response = requests.get('http://httpbin.org/get',params=data)
print(response.text)
</pre>
## json解析
<pre>
import requests
import json
response = requests.get('http://httobin.org/get')
print(type(response.text))
print(response.json())
print(json.loads(response.text))
print(type(response.json()))
</pre>
## 获取二进制数据
<pre>
import requests
response = requests.get("https://github.com/favicon.ico")
print{type(response.text),type(response.content)}
print(response.text)
print(response.content)
</pre>
## 存入二进制数据
<pre>
import requests
response = requests.get("https://github.com/favicon.ico")
with open('favicon.ico','wb') as f:
  f.write(response.content)
  f.close()
</pre>
## 添加headers
<pre>
import requests
response = requests.get('https://www.zhihu.com/explore')
print(response.text)
</pre>
<pre>
import requests
headers = {
  'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; WOW64; rv:63.0) Gecko/20100101 Firefox/63.0'
}
response = requests.get("https://www.zhihu.com/explore",headers=headers)
print(response.text)
</pre>
## POST请求
<pre>
import requests
data = {'name':'germey','age':'22'}
response = reuqests.post('http://httpbin.org/post',data=data)
print(response.text)
</pre>
<pre>
import requests
data = {'name':'germey','age':'22'}
headers = {
  'User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:63.0) Gecko/20100101 Firefox/63.0'
}
response = reuqests.post('http://httpbin.org/post',data=data,headers=headers)
print(response.text)
</pre>
## response属性
<pre>
import requests
response = requests.get('http://www.jianshu.com')
print(type(response.status),response.status)
print(type(response.headers),response.headers)
print(type(response.cookies),response.cookies)
print(type(response.url),response.url)
print(type(response.history),response.history)
</pre>
<pre>
import requests
response = requests.get('http://www,jianshu.com')
exit() if not response.status_code == request.codes.not_found else print('404 Not Found')
</pre>
<pre>
import requests
response = requests.get('http://www.jianshu.com')
exit() if not response.status_code == 200 else print('Request Successfully')
</pre>
## 高级操作
### 文件上传
<pre>
import requests
files = {'file':open('favicon.ico','rb')}
response = requests.post('http://httpbin.org/post',files=files)
print(response.text)
</pre>
### 获取cookie
<pre>
import requests
response = requests.get('https://www.baidu.com')
print(response.cookies)
for key,value in response.cookies.items():
  print(key + '=' + value)
</pre>
## 会话维持
### 模拟登陆思路
<pre>
import requests
requests.get('http://httpbin.org/cookies/set/number/123456789')
response = requests.get('http://httpbin.org/cookies')
print(response.text)
</pre>
### 实例
<pre>
import requests
s = requests.session()
s.get('http://httpbin.org/cookies/set/number/12345678')
response = s.get('http://httpbin.org/cookies')
print(response.text)
</pre>
### 证书解决(使用urllib3库)
<pre>
import requests
from requests.packages import urllib3
urllib3.disable_warnings()
response = requests.get('https://www.12306.cn',verify=False)
print(response.status_code)
</pre>
#### 导入证书
<pre>
import requests
response = requests.get('https://www.12306.cn',cert=('/path/server.crt','/path/key'))
print(response.status_code)
</pre>
### 代理设置(ssl代理)
<pre>
import requests
proxies = {
  "http":"http://127.0.0.1:9743",
  "https":"https://127.0.0.1:9743",
}
response = requests.get("https://www.taobao.com",proxies=proxies)
print(response.status_code)
</pre>
<pre>
import requests
proxies = {
  "http":"http://user:password@127.0.0.1:9743/",
}
response = requests.get("https://www.taobao.com",proxies=proxies)
print(response.status_code)
</pre>
### sock5代理,先安装requests[scoks]
<pre>
pip3 install 'requests[scoks]'
import requests
proxies = {
  'http':'socks5://127.0.0.1:9742',
  'https':'socks5://127.0.0.1:9742'
}
response = requests.get('https://www.taobao.com',proxies=proxies)
print(response.status_code)
</pre>
## 超时设置
<pre>
import requests 
from requests.exceptions import ReadTimeout
try:
    response = requests.get('http://httpbin.org/get',timeout = 1)
    print(response.status_code)
except ReadTimeout:
    print('Timeout')
</pre>
## 认证设置
<pre>
import requests
from requests.auth import HTTPBasicAuth
r = requests.get('http://120.27.34.24:9001',auth=HTTPBasicAuth('user','123'))
print(r.status.code)
### 也可以输入下面的形式
import requests
r = requests.get('http://120.27.34.24:9001',auth=('user','123'))
print(r.status_code)
</pre>
## 异常处理和捕获
<pre>
import requests
from requests.exceptions import ReadTimeout,ConnectionError,HTTPError,RequestException
try:
    response = requests.get('http://httpbin.org/get',timeout=1)
    print(response.status_code)
except ReadTimeout:(子类)
    print('timeout')
except ConnectionError:(子类)
    print('connect error')
except HTTPError:(子类)
    print('http error')
except RequestException:(父类)
    print('Error')
</pre>
