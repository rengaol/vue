<template>
  <canvas id="can"></canvas>
</template>

<script>
export default {
  mounted() {
    function ran(n, m) {
      return parseInt(Math.random() * (m - n) + n);
    }
    window.onload = function () {
      var oC = document.querySelector("#can");
      var gd = oC.getContext("2d"); //创建2D画笔
      var winW = document.documentElement.clientWidth;
      var winH = document.documentElement.clientHeight;
      oC.width = winW;
      oC.height = winH;
      var Len = 15; //尾巴个数
      var N = 5; //转折点个数
      var arr = []; //存每个转折点的xy坐标和x轴y轴运动速度
      for (var i = 0; i < N; i++) {
        arr[i] = {
          x: ran(0, winW),
          y: ran(0, winH),
          iSpeedX: ran(-10, 10),
          iSpeedY: ran(-10, 10),
        };
      }
      var pw = 1; //每个转折点的宽
      var ph = 1; //每个转折点的高
      var oldArr = []; //存第一个线条

      function draw(json) {
        gd.fillStyle = "#fff";
        gd.fillRect(json.x - pw / 2, json.y - ph / 2, pw, ph);
      }

      setInterval(function () {
        //先准备五个点
        gd.clearRect(0, 0, oC.width, oC.height);
        for (var i = 0; i < arr.length; i++) {
          //边界 碰到边界反向掉头继续运动
          if (arr[i].x <= 100) {
            arr[i].x = 100;
            arr[i].iSpeedX *= -1;
          } else if (arr[i].x >= oC.width - 100) {
            arr[i].x = oC.width - 100;
            arr[i].iSpeedX *= -1;
          }
          if (arr[i].y <= 100) {
            arr[i].y = 100;
            arr[i].iSpeedY *= -1;
          } else if (arr[i].y >= oC.height - 100) {
            arr[i].y = oC.height - 100;
            arr[i].iSpeedY *= -1;
          }
          arr[i].x += arr[i].iSpeedX;
          arr[i].y += arr[i].iSpeedY;
          draw(arr[i]);
        }

        //开始沿着五个点画线
        gd.beginPath(); //重新开启画笔
        gd.moveTo(arr[0].x, arr[0].y); //起始位置
        for (var i = 1; i < arr.length; i++) {
          gd.lineTo(arr[i].x, arr[i].y);
        } //路径
        gd.closePath(); //闭合路径
        gd.strokeStyle =
          "rgb(" + ran(0, 255) + "," + ran(0, 255) + "," + ran(0, 255) + ")";
        gd.stroke(); //描边

        //画剩下的几条线
        var arr2 = []; //存新的点
        for (var i = 0; i < arr.length; i++) {
          arr2[i] = {
            x: arr[i].x,
            y: arr[i].y,
          };
        }

        oldArr.push(arr2); //****存上次的数据
        if (oldArr.length > Len) {
          oldArr.shift();
        } //保证只有十五条数据就够了
        for (var i = 0; i < oldArr.length; i++) {
          gd.beginPath();
          gd.moveTo(oldArr[i][0].x, oldArr[i][0].y);
          for (var j = 1; j < oldArr[i].length; j++) {
            gd.lineTo(oldArr[i][j].x, oldArr[i][j].y);
          }
          gd.closePath();
          gd.strokeStyle =
            "rgb(" + ran(0, 255) + "," + ran(0, 255) + "," + ran(0, 255) + ")";
          gd.stroke();
        }
      }, 200);
    };
  },
};
</script>

<style  scoped>
* {
  margin: 0;
  padding: 0;
  list-style: none;
}

canvas {
 height: 700px;
}
</style>