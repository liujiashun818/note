```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>html元素转canvas并一键生成png图片(支持img图片元素)</title>
	<!-- html2canvas将Dom节点在Canvas里边画出来 -->
	<script src="js/html2canvas.min.js"></script>
 
	<!-- 将canvas图片保存成图片 -->
	<script src="js/canvas2image.js"></script>
	<script src="js/base64.js"></script>
	<style>
		p{
			font-size: 15px;
			font-family: 'Microsoft YaHei', 'Lantinghei SC', 'Open Sans', Arial, 'Hiragino Sans GB', 'STHeiti', 'WenQuanYi Micro Hei', 'SimSun', sans-serif;
		}
		#content{
			border-radius: 3px;
		}
		#btnSave,#Download{
		    position: absolute;
		    left: 180px;
		    top: 540px;
		    width: 78px;
		    height: 30px;
		    background-color: #22b4f6;
		    color: #fff;
		    text-align: center;
		    border-radius: 3px;
		    border: none;
		}
		#Download{
		    margin-left: 560px;
		}
		.tx,.bt{
			border: 1px solid #999;
			width: 100px;
			height: 20px;
			border-radius: 3px;
		}
		.bt{
			background-color: #22b4f6;
			color: #fff;
			text-align: center;
			border: none;
		}
	</style>
</head>
<body>
<div>注意：html2canvas 只能在服务器中抓取img ????????????????</div>
	<div id="content" style="width:500px;height:500px;border:1px solid #22b4f6;float:left;text-align:center; background: #fff;">
		<p><img width="80" height="100" src="images/pic.jpg" alt="头像"></p>
	    <p>昵称：马云云</p>
	    <p>技能：前端 + 后端 + 小程序 + webapp</p>
	    <p>语言：html5、php、mysql</p>
	    <p>脚本：javascript</p>
	    <p>框架：vue.js、smarty、thinkphp、MUI、WeUI、Bootstrap</p>
	    <p><input type="text" class="tx" placeholder="微信公众号开发"></p>
	    <p><input type="button" class="bt" value="网站微站开发"></p>
	</div>
	<div style="width:60px;height:302px;float:left;text-align:center;line-height:302px;font-size:30px;color:#22b4f6;">==></div>
	<div id="images" style="width:190px;height:302px;float:left;text-align:center;line-height:302px">图片预览区</div>
	<button id="btnSave">抓取图片</button><button id="Download">下载图片</button>
</body>
<script>
/*生成canvas图形*/
 
// 获取按钮id
var btnSave = document.getElementById("btnSave");
// 获取内容id
var content = document.getElementById("content");
// 进行canvas生成
btnSave.onclick = function(){
	html2canvas(content, {
        onrendered: function(canvas) {
        	//添加属性
        	canvas.setAttribute('id','thecanvas');
			//读取属性值
			// var value= canvas.getAttribute('id');
            document.getElementById('images').innerHTML = '';
            document.getElementById('images').appendChild(canvas);
        }
	});
}
</script>
<script>
/*
 * 说明
 * 不支持跨域图片
 * 不能在浏览器插件中使用
 * 部分浏览器上不支持SVG图片
 * 不支持Flash
 */
var Download = document.getElementById("Download");
Download.onclick = function(){
	var oCanvas = document.getElementById("thecanvas");
 
	/*自动保存为png*/
	// 获取图片资源
	var img_data1 = Canvas2Image.saveAsPNG(oCanvas, true).getAttribute('src');
	saveFile(img_data1, 'richer.png');
 
 
	/*下面的为原生的保存，不带格式名*/
	// 这将会提示用户保存PNG图片
	// Canvas2Image.saveAsPNG(oCanvas);
}
// 保存文件函数
var saveFile = function(data, filename){
    var save_link = document.createElementNS('http://www.w3.org/1999/xhtml', 'a');
    save_link.href = data;
    save_link.download = filename;
   
    var event = document.createEvent('MouseEvents');
    event.initMouseEvent('click', true, false, window, 0, 0, 0, 0, 0, false, false, false, false, 0, null);
    save_link.dispatchEvent(event);
};
</script>
</html>

```
