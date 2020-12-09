### 关于HTML <form> 标签的 enctype 属性

enctype就是encodetype就是编码类bai型的意思

**默认情况下**，enctype的值是application/x-www-form-urlencoded，不能用于文件上传，只有使用了multipart/form-data，才能完整的传递文件数据。

application/x-www-form-urlencoded不是不能上传文件，是只能上传文本格式的文件，multipart/form-data是将文件以二进制的形式上传，这样可以实现多种类型的文件上传。

+ application/x-www-form-urlencoded。默认的编码方式。但是在用文本的传输和MP3等大型文件的时候，使用这种编码就显得 效率低下
+ multipart/form-data 。 指定传输数据为二进制类型，比如图片、mp3、文件。 
+ text/plain。纯文体的传输。空格转换为 “+” 加号，但不对特殊字符编码。

