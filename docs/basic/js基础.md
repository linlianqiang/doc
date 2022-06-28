
## var、 let、const
* var存在变量提升，let，const没有
```js
    console.log(a) //undefined . 如果是let报错。
    var a = 100; 
    等价：
    var a ;
    console.log(a)
    a = 100;
```
* var、let定义变量，const定义常量
* let，const有块级作用域。var没有。## 数组

* filter是过滤器，可以return符合条件的集合集合。无匹配则返回空数组
* find是返回满足条件的第一个值，无则undefind
* map 必须return原数组长度的内容
* foreach可以有相对复杂操作。 return 不会得到一个数组结果

## 请求标头

* 常见 Content-Type

  * text/html ： HTML格式

  * text/plain ：纯文本格式

  * application/x-www-form-urlencoded

    <form encType="">中默认的encType，form表单数据被编码为key/value格式发送到服务器（表单默认的提交数据的格式）
    或者：qs.stringify()

    ```js
    /数据格式：
    grant_type=password&client_id=myjszl&client_secret=123&password=43&username=43
    ```
  
  * application/json;chatset=utf-8
  
    json数据格式
  
  * multipart/form-data;  boundary=----WebKitFormBoundarysE9cfzN0VuLxDQho
  
    需要在表单中进行  文件上传  时，就需要使用该格式。 new formData();  

## Blob

`Blob` 对象表示一个不可变、原始数据的类文件对象，类似文件对象的二进制数据。

因此可以像操作File对象一样操作Blob对象，实际上，File继承自Blob。

Binary Large Object缩写。

```js
	Blob(blobParts[, options])
    参数说明：
    blobParts： 数组类型， 数组中的每一项连接起来构成Blob对象的数据，数组中的每项元素可以是ArrayBuffer(二进制数据缓冲区), 		ArrayBufferView,Blob,DOMString。或其他类似对象的混合体。


	var data1 = "a";
    var data2 = "b";
    var data3 = "<div style='color:red;'>This is a blob</div>";
    var data4 = { "name": "abc" };

    var blob1 = new Blob([data1]);
    var blob2 = new Blob([data1, data2]);
    var blob3 = new Blob([data3]);
    var blob4 = new Blob([JSON.stringify(data4)]);
    var blob5 = new Blob([data4]);
    var blob6 = new Blob([data3, data4]);

    console.log(blob1);  //输出：Blob {size: 1, type: ""}
    console.log(blob2);  //输出：Blob {size: 2, type: ""}
    console.log(blob3);  //输出：Blob {size: 44, type: ""}
    console.log(blob4);  //输出：Blob {size: 14, type: ""}
    console.log(blob5);  //输出：Blob {size: 15, type: ""}
    console.log(blob6);  //输出：Blob {size: 59, type: ""}
```

* size代表`Blob` 对象中所包含数据的字节数 ( B )

* slice 方法 - file也有

  ```js
  	var data = "abcdef";
      var blob1 = new Blob([data]);
      var blob2 = blob1.slice(0,3);
      
      console.log(blob1);  //输出：Blob {size: 6, type: ""}
      console.log(blob2);  //输出：Blob {size: 3, type: ""}
  ```

* #### Blob对象能够添加到表单中，作为上传数据（文件）使用

  ```js
  const content = '<a id="a"><b id="b">hey!</b></a>';
  const blob = new Blob([content], {type: 'text/xml'});
  
  formData.append('webmasterfile', blob);

* Blob URL

  Blob URL是blob协议的url: 格式：blob:http://xxx。 Blob URL可以通过`URL.createObjectURL(blob)`创建。在绝大部分场景下，我们可以像使用Http协议得URL一样使用Blob URL。常见得场景有： 作为文件得下载地址和作为图片资源地址。

  ```js
  function createDownloadFile() {
      var content = "Blob Data";
      var blob = new Blob([content]);
      var link = document.getElementByTageName('a')[0];
      link.download = "file";
      link.href = URL.createObjectURL(blob);
  }
  window.onload = createDownloadFile;
  ```

* 使用 Data URL加载图片资源。小图片用base64编码直接嵌入到HTML文件中，实际就是利用了Data URL来获取图片数据。

  ```js
  function handleFile(e) {
      var file = e.files[0];
      var fileReader = new FileReader();
      var img = document.getElementByTagName("img")[0];
      fileReader.onload = function(e) {
        
          img.src = e.target.result;
      }
      //  blob 和 base64之间相互转换.
      fileReader.readAsDataURL(file);
  }
  ```

  Blob URL得长度一般比较短，但Data URL因为直接存储图片base64编码后得数据，往往很长。当显示大图片时，使用Blob URL更优。

  Blob URL可以方便的使用XMLHttpRequest获取源数据

  ```js
  var blobUrl = URL.createObkectURL(new Blob(['Test'], {type: 'text/plain'}));
  var xhr = new XMLHttpRequest();
  //如果是指xhr.responseType = 'blob',将返回一个Blob对象，而不是文本；
  //xhr.responseType = 'blob';
  xhr.onload = function() {
    alert(xhr.responseText);
  }
  xhr.open('get', blobUrl);
  xhr.send();
  ```

* 除了可以用作图片资源的网络地址，Blob URL也可以用作其他资源的网络地址，例如html文件、json文件等，为了保证浏览器能正确的解析Blob URL返回的文件类型，需要在创建Blob对象时指定相应的type

  ```js
  //创建HTML文件的Blob URL
  var data = "<div style='color:red;'This is a blob</div>";
  var blob = new Blob([data], {type: 'text/html'}); // 'application/json'
  var blobUrl = URL.createObjectURL(blob);
  ```

  

## ArrayBuffer & 二进制流

**`ArrayBuffer`** 对象用来表示通用的、固定长度的原始二进制数据缓冲区。

* **Base64**是一种基于`64个可打印字符`来表示[二进制数据](https://zh.wikipedia.org/wiki/二进制)的表示方法。在Base64中的可打印字符包括 字母`A-Z`、`a-z`、数字`0-9`，这样共有62个字符，此外两个可打印符号在不同的系统中而不同。
* file.size指的是字节。arrayBuffer的长度就是指的字节长度：byteLength
* 操作ArrayBuffer必须使用试图：Uint8Array、Uint32Array。
* 二进制是二进制，与二进制流不同。

https://zh.javascript.info/arraybuffer-binary-arrays

https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/TypedArray

```js
(() => {
        const fileReader = new FileReader();
        fileReader.readAsArrayBuffer(file);
        fileReader.onload = function (e: any) {
          const arrayBuffer = e.target.result;
          const length = arrayBuffer.byteLength;
          const chunkSize = 131072; // 128kb
          const chunks = Math.ceil(length / chunkSize);
          const uint8Array = new Uint8Array(arrayBuffer);
          console.log('uint8Array', uint8Array);
          const uint8ArrayServe = new Uint8Array(length);

          for (let i = 0; i < chunks; i++) {
            const start = i * chunkSize;
            const end = Math.min(length, start + chunkSize);
            // 前端切片
            const sliceBuffer = arrayBuffer.slice(start, end);
            // 后端合并 ： 计算偏移量
            const slice8Array = new Uint8Array(sliceBuffer);
            uint8ArrayServe.set(slice8Array, start);
          }
          console.log('uint8ArrayServe', uint8ArrayServe);
        };
 })();
```

```js
const fileReader = new FileReader();
    fileReader.readAsArrayBuffer(file);
    fileReader.onload = function (e: any) {
        const arrayBuffer = e.target.result;
        const length = arrayBuffer.byteLength; // 与 file.length一致
        const chunkSize = 131072; // 128kb
        const chunks = Math.ceil(length / chunkSize);

        for (let i = 0; i < chunks; i++) {
            const start = i * chunkSize;
            const end = Math.min(length, start + chunkSize);
            // 前端切片
            const sliceBuffer = arrayBuffer.slice(start, end);
            const sliceBufferUint8 = new Uint8Array(sliceBuffer);
            // 创建新对象，存储切片序号等信息
            const sliceNewArrayBuffer = new ArrayBuffer(sliceBuffer.byteLength + 2);
            const sliceNew8Array = new Uint8Array(sliceNewArrayBuffer);
            // 切片信息
            sliceNew8Array.set(sliceBufferUint8, 0);
            // 切片顺序 ：start太大，存序号，后端 需要 * chunkSize
            // 可以在字符串上，存取字符串等信息。
            // for (let j = 0; j < stringTxt.length; j++) {
            //     dv.setUint8(2 + j, imageInfo[j].charCodeAt(0));
            // };
            sliceNew8Array.set([i], sliceBuffer.byteLength);
   }
```



## Uint8Array、Uint32Array...

一个**类型化数组**（**TypedArray）**对象描述了一个底层的[二进制数据缓冲区](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer)（binary data buffer）的一个类数组视图（view）。事实上，没有名为 `TypedArray` 的全局属性，也没有一个名为 `TypedArray` 的构造函数。相反，有许多不同的全局属性，它们的值是特定元素类型的类型化数组构造函数

## DataView

data view 视图是一个可以从 二进制[`ArrayBuffer`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer) 对象中读写多种数值类型的底层接口，使用它时，不用考虑不同平台的[字节序](https://developer.mozilla.org/zh-CN/docs/Glossary/Endianness)问题。

## fileReader

`**FileReader**` 对象允许Web应用程序异步读取存储在用户计算机上的文件（或原始数据缓冲区）的内容，使用 [`File`](https://developer.mozilla.org/zh-CN/docs/Web/API/File) 或 [`Blob`](https://developer.mozilla.org/zh-CN/docs/Web/API/Blob) 对象指定要读取的文件或数据。

[`FileReader.abort()`](https://developer.mozilla.org/zh-CN/docs/Web/API/FileReader/abort)

中止读取操作。在返回时，`readyState`属性为`DONE`。

[`FileReader.readAsArrayBuffer()`](https://developer.mozilla.org/zh-CN/docs/Web/API/FileReader/readAsArrayBuffer)

开始读取指定的 [`Blob`](https://developer.mozilla.org/zh-CN/docs/Web/API/Blob)中的内容, 一旦完成, result 属性中保存的将是被读取文件的 [`ArrayBuffer`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer) 数据对象.

[`FileReader.readAsBinaryString()`](https://developer.mozilla.org/zh-CN/docs/Web/API/FileReader/readAsBinaryString) 

开始读取指定的[`Blob`](https://developer.mozilla.org/zh-CN/docs/Web/API/Blob)中的内容。一旦完成，`result`属性中将包含所读取文件的原始二进制数据。

[`FileReader.readAsDataURL()`](https://developer.mozilla.org/zh-CN/docs/Web/API/FileReader/readAsDataURL)

开始读取指定的[`Blob`](https://developer.mozilla.org/zh-CN/docs/Web/API/Blob)中的内容。一旦完成，`result`属性中将包含一个`data:` URL格式的Base64字符串以表示所读取文件的内容。

[`FileReader.readAsText()`](https://developer.mozilla.org/zh-CN/docs/Web/API/FileReader/readAsText)

开始读取指定的[`Blob`](https://developer.mozilla.org/zh-CN/docs/Web/API/Blob)中的内容。一旦完成，`result`属性中将包含一个字符串以表示所读取的文件内容。

## 前端模块化

* https://juejin.cn/post/6844903576309858318

### CommonJS

* 语法：exports、require。 node语法中使用

  ```js
  module.exports = {}
  ```

### AMD

* AMD规范采用异步方式加载模块，模块的加载不影响它后面语句的运行。所有依赖这个模块的语句，都定义在一个回调函数中，等到加载完成之后，这个回调函数才会运行。这里介绍用require.js实现AMD规范的模块化：用`require.config()`指定引用路径等，用`define()`定义模块，用`require()`加载模块。
* AMD规范在2010由requireJS提出，CommonJS规范主要是弥补服务端的模块化机制，不像服务器加载速度很快，客户端加载时需要等待，可能存在假死情况

### CMD

CMD规范在2011年由seaJS提出，CMD规范和AMD规范类似，主要区别是CMD规范是就近加载依赖，延迟执行，只有到require时依赖才执行。

### ES6 Module

export 、export

