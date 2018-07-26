# QRcode_create
Make a QRcode parser case.
`说明：`
> 由于业务需求，需要制作一个移动端的长按识别二维码的功能，同时该功能最本质的也可以解析二维码。后面接触到Google的二维码插件“Anything to QRcode”。后来在根据网上的资料，自己进行了代码整理测试目前能够成功应用到项目中，现在把最初的代码整理进行分享。这里最主要的是利用了llqrcode.js这个插件的qrcode.decode和qrcode.callback,就能对二维码进行解析，同时对解析的结果进行返回。

> 1.解析的图片，这里采用的是上传图片解析，（可以使用图片的地址链接或采用扫一扫输出的图片进行解析）
 ```
 //获取图片路径
 let getObjectURL = function(file){
	    let url = null ; 
	    if (window.createObjectURL!=undefined) { // basic
	        url = window.createObjectURL(file) ;
	    } else if (window.URL!=undefined) { // mozilla(firefox)
	        url = window.URL.createObjectURL(file) ;
	    } else if (window.webkitURL!=undefined) { // webkit or chrome
	        url = window.webkitURL.createObjectURL(file) ;
	    }
	    return url;
	}
```  
 > 2.获取解析图片
  ```
  url = getObjectURL(elem.files[0]);
  ```
 > 3.通过qrcode.decode()方法去解析该图片的内容（该方法解析时需要传入解析图片的路径）
  ```
  qrcode.decode(url);
  ```
 > 4.通过qrcode.callback把解析的结果进行返回（qrcode.callback返回的imgMsg就是解析后获取的信息）
 ```
  qrcode.callback = function(imgMsg){
				fn(imgMsg,url);
			}
```
  `注：`此处，我业务中是进行的重定向操作，所以我的引用变为 window.location.href = imgMsg ，建议我们在使用的时候可以根据自己的需求进行修改。
  
  
  
