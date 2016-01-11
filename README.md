# Scratch-GuaGuaLe-Demo
刮刮乐Demo
```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>刮刮乐</title>
    <style media="screen">
      #scratch {
        /*background: url('http://pic.baike.soso.com/p/20090711/bki-20090711100323-24213954.jpg');*/
        background-size: 100% 100%;
      }
    </style>
  </head>
  <body>
    <canvas id="scratch" width="300" height="300"></canvas>
    <script type="text/javascript">
      var scratch = document.getElementById('scratch'); // 获取刮刮乐Dom
      var ctx = scratch.getContext('2d'), // 访问绘画上下文
          isDown = false, // 按下状态
          radius = 15, // 定义半径
          pi2 = Math.PI * 2, // 定义绘制圆终点
          img = new Image; // 声明图片
      img.onload = start; // 图片加载完执行绘制遮罩图片函数
      img.src = 'http://pic.baike.soso.com/p/20090711/bki-20090711100310-2024468547.jpg';
      // 绘制遮罩图片函数
      function start() {
        ctx.drawImage(this, 0, 0, scratch.width, scratch.height); // 绘制遮罩图片
        ctx.globalCompositeOperation = 'destination-out'; // canvas设置全局绘制方式
        scratch.onmousedown = handleMouseDown; // 监听鼠标按下
        scratch.onmousemove = handleMouseMove; // 监听鼠标移动
        window.onmouseup = handleMouseUp; // 监听鼠标抬起
      }
      // 处理鼠标按下
      function handleMouseDown(e) {
        isDown = true;
        var pos = getXY(e);
        erase(pos.x, pos.y);
      }
      // 处理鼠标移动
      function handleMouseMove(e) {
        if(!isDown) return;
        var pos = getXY(e);
        erase(pos.x, pos.y);
      }
      // 处理鼠标抬起
      function handleMouseUp(e) {
        isDown = false;
      }
      // 获取圆心
      function getXY(e) {
        var rect = scratch.getBoundingClientRect();
        return {
          x: e.clientX - rect.left,
          y: e.clientY - rect.top
        }
      }
      // 绘制圆形(即"橡皮擦")
      function erase(x, y) {
        ctx.beginPath(); // 新建一条路径，生成之后，图形绘制命令被指向到路径上生成路径。
        ctx.arc(x, y, radius, 0, pi2); // 画一个以（x,y）为圆心的以radius为半径的圆弧（圆），从0开始到2*PI*R结束
        ctx.fill(); // 通过填充路径的内容区域生成实心的图形。
      }
      // 延迟函数，若背景图片放在css中，则会被提前显示出来
      setTimeout(function() {
        scratch.style.backgroundImage = 'url(http://pic.baike.soso.com/p/20090711/bki-20090711100323-24213954.jpg)';
      }, 100);
    </script>
  </body>
</html>
```
