---
title: Cookie操作
date: 2017-04-15 09:56:12
tags: 
- 前端
- Cookie
categories: 
- 前端
---
在PC项目实战中，需要进行对站点的选择，将用户选择的站点保存在Cookie当中，设置cookie时一直没能成功。

下面来说重点！如何设置，获取，删除cookie

<!-- more -->

##### 保存Cookie

```
 
//参数 name: 自定义Cookie名字  value：给Cookie设置值  expired: 设置Cookie保存多长时间  path: 将Cookie保存的位置（根据项目的文件目录，asp.net默认为/，就是根目录）  domain: 表示的是cookie所在的域，默认为请求的地址，如网址为www.cookie.com/cookie/cookie.aspx，那么domain默认为www.test.com

function setCookie(name, value, expired, path, domain) {
  var d = new Date();
  d.setTime(d.getTime() + (expired * 24 * 60 * 60 * 1000));
  var expires = "expires=" + d.toUTCString();
  document.cookie = name + "=" + value + "; " + expires + ";path=/;domain=" + location.hostname;
};

```

##### 获取Cookie

参数 name : 自定义Cookie名字
```
function getCookie(objName) {//获取指定名称的cookie的值 
  var name = objName + "=";
  var value = document.cookie.split(';');
  for (var i = 0; i < value.length; i++) {
    var key = value[i];
    while (key.charAt(0) == ' ') key = key.substring(1);
    if (key.indexOf(name) != -1) return key.substring(name.length, key.length);
  }
  return "";
};

```

##### 删除Cookie

```
function delCookie(name) {//为了删除指定名称的cookie，可以将其过期时间设定为一个过去的时间，或者将Cookie值设置为空 
  setCookie(name, "", -1);
}

```

好了，Cookie的基本的方法基本就是这样。当然在项目中运用这些方法之前，我也是踩了许多坑，比如，保存不成功，在做登陆的时候，获取Cookie值时，就遇到登陆后返回的token值保存在浏览器，获取保存在浏览器的token值时，值发生变化。好了，去搬砖了。