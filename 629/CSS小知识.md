## CSS小知识

**去掉浏览器默认滚动条**

```css
/* .box为当前出现滚动条的容器 */
	 .box::-webkit-scrollbar {
	    display: none
	  }
	/*滚动条的宽度*/
.ant-drawer-wrapper-body::-webkit-scrollbar {
    width: 4px;
    height: 105px;
}


/*外层轨道。可以用display:none让其不显示，也可以添加背景图片，颜色改变显示效果*/
.ant-drawer-wrapper-body::-webkit-scrollbar-track {
    width: 4px;
    height: 80%;
    background-color: #E0E6F3;
    -webkit-border-radius: 2em;
    -moz-border-radius: 2em;
    border-radius: 2em;
}

/*滚动条的设置*/
.ant-drawer-wrapper-body::-webkit-scrollbar-thumb {
    background-color: #A4A9C1;
    background-clip: padding-box;
    min-height: 28px;
    max-height: 105px;
    -webkit-border-radius: 2em;
    -moz-border-radius: 2em;
    border-radius: 2em;
    /* display: none; */
}

/*滚动条移上去的背景*/

/* .ant-drawer-wrapper-body::-webkit-scrollbar-thumb:hover {
    background-color: #fff;
} */

```

