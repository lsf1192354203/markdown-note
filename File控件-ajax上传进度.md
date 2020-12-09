#### File控件中选择的文件列表对象

```js
//<input type='file' id='myFile'/><input type='button'value='click'/>
oBtn.onclick=function(){
    alert(myFile.value);
    alert(myFile.files);
    /*
    for(var attr in myFile.files[0]){
    	console.log(attr+':'+myFile.files[0][attr]);
    }
    for(var attr in myFile.files){
    	console.log(attr+':'+myFile.files[attr]);
    }
    */
    var xhr= new XMLHttpRequest();
    xhr.onload=function(){
        alert(1);//监听上传成功
        //alert(this.responseText);
        var d=JSON.parse(this.responseText);
        alert(d.msg+':'+d.url)
        alert('ok,上传完成')
    }
    //监听进度 
    var oUpload=xhr.upload;//提供很多方法
    alert(oUpload);
    oUpload.onprogress=function(ev){
         console.log(ev.total +':'+ev.loaded);
        var iScale=ev.loaded/ev.total;
        oDiv2.style.width=300*iScale+'px';
    }
    
    xhr.open('post','url',true)
    xhr.setRequestHeader('X-Request-With','XMLHttpRequest');
    //xhr.send('file='+myFile.files[0]);
    var oFormData=new FormData();//通过formdata来构建提交数据
    oFormData.append('file',myFile.files[0]);
    alert(oFormData)
    xhr.send(oFormData);
}

```

```html
<div class='progress div1'>
    
    <div class='div2'></div>
    <div class='div3'>0%</div>
</div>
```



