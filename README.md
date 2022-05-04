
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        *{padding:0;margin:0}
        html{overflow:hidden}
          </style>
</head>
<body>
    <B>2002年的第一场雪比以往时候来的更晚一些停靠在八楼的二路汽车带走了最后一片飘落的黄叶</B>
<canvas id="canvas" style="background:#111"></canvas>
<audio src="http://dx.sc.chinaz.com/Files/DownLoad/sound1/201210/2178.mp3" autoplay loop/>
<audio src="http://dx.sc.chinaz.com/Files/DownLoad/sound1/201205/1430.mp3" autoplay loop/>
<script type="text/javascript">
window.onload = function(){
//获取画布对象
var canvas = document.getElementById("canvas");
//获取画布的上下文
var context =canvas.getContext("2d");
//获取浏览器屏幕的宽度和高度
var w = window.innerWidth;
var h = window.innerHeight;
//设置canvas的宽度和高度
canvas.width = w;
canvas.height = h;
//1：如何产生雪花,一个圆 ,arc(x,y,r,start,end)
//初始化雪花数量
var num = 400;
//雪花数组
var snows = [];
for(var i=0;i<num;i++){
//x,y圆心掉的坐标位置，r代表圆的半径，d每个圆的每个圆之间的间距，c代表的颜色
var r = randColor();
snows.push({
x:Math.random()*w,
y:Math.random()*h,
r:Math.random()*10,
d:Math.random()*num
});
};
//绘画的函数
function draw(){
context.clearRect(0,0,w,h);
context.beginPath();
for(var i=0;i<num;i++){
var snow = snows[i];
context.fillStyle = "rgba(255,255,255,0.9)";
context.moveTo(snow.x,snow.y);
context.arc(snow.x,snow.y,snow.r,0,Math.PI*2);
}
context.fill();
//掉落
drop();
};
var angle = 0;
function drop()
{
angle += 0.01;
for(var i = 0; i < num; i++){
var p = snows[i];
//记住两个公式：Math.sin(弧度)返回是一个0 1 -1 的数字
//math.cos(1 0 -1 ) 自由体，
p.y += Math.cos(angle+p.d) + 1 + p.r*0.625;
p.x += Math.sin(angle) * 8 ;
//如果雪花到了边界，进行边界处理
if(p.x > w+5 || p.x < -5 || p.y > h){
if(i%4 > 0) {
snows[i] = {x: Math.random()*w, y: -10, r: p.r, d: p.d};
}else{
//控制方向
if(Math.sin(angle) > 0){
snows[i] = {x: -5, y: Math.random()*h, r: p.r, d: p.d};
}else{
snows[i] = {x: w+5, y: Math.random()*h, r: p.r, d: p.d};
}
}
}
}
};
//执行和调用函数
draw();
setInterval(draw,10);
//随机颜色
function randColor(){
var r = Math.floor(Math.random() * 256);
var g = Math.floor(Math.random() * 256);
var b = Math.floor(Math.random() * 256);
return "rgb("+r+","+g+","+b+")";
};
};
  
</script>
</body>
</html>
