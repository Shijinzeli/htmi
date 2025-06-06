<!DOCTYPE html>
<html lang="zh">
<head>
  <meta charset="UTF-8">
  <title>主食转盘</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      background-color: #f8f8f8;
    }
    h1 {
      margin-top: 30px;
    }
    #wheel {
      margin: 20px auto;
      width: 300px;
      height: 300px;
      border: 8px solid #333;
      border-radius: 50%;
      position: relative;
      overflow: hidden;
    }
    .segment {
      position: absolute;
      width: 50%;
      height: 50%;
      top: 50%;
      left: 50%;
      transform-origin: 0% 0%;
      background-color: #f0c674;
      color: #333;
      text-align: right;
      padding-right: 10px;
      font-weight: bold;
    }
    #pointer {
      width: 0;
      height: 0;
      border-left: 20px solid transparent;
      border-right: 20px solid transparent;
      border-bottom: 30px solid red;
      margin: 20px auto;
    }
    #startBtn {
      padding: 10px 20px;
      font-size: 16px;
      cursor: pointer;
    }
    #result {
      margin-top: 20px;
      font-size: 20px;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <h1>🍜 主食转盘</h1>
  <div id="pointer"></div>
  <div id="wheel"></div>
  <button id="startBtn">开始转盘</button>
  <div id="result"></div>

  <script>
    const foods = [
      "牛肉面", "炸酱面", "热干面", "刀削面", "酸辣粉", "米饭", "炒饭", "盖浇饭",
      "卤肉饭", "煲仔饭", "扬州炒饭", "腊味饭", "砂锅米线", "螺蛳粉", "饺子", "馄饨",
      "炒米粉", "年糕", "馒头", "烧麦"
    ];

    const wheel = document.getElementById("wheel");

    function drawWheel() {
      const count = foods.length;
      const angle = 360 / count;
      wheel.innerHTML = "";
      for (let i = 0; i < count; i++) {
        const div = document.createElement("div");
        div.className = "segment";
        div.style.transform = `rotate(${i * angle}deg) skewY(${90 - angle}deg)`;
        div.style.backgroundColor = `hsl(${i * (360 / count)}, 70%, 75%)`;
        div.innerText = foods[i];
        wheel.appendChild(div);
      }
    }

    drawWheel();

    document.getElementById("startBtn").addEventListener("click", () => {
      const randomIndex = Math.floor(Math.random() * foods.length);
      const angle = 360 / foods.length;
      const rotateDeg = 360 * 5 + (360 - randomIndex * angle - angle / 2);
      wheel.style.transition = "transform 5s ease-out";
      wheel.style.transform = `rotate(${rotateDeg}deg)`;
      setTimeout(() => {
        document.getElementById("result").innerText = "今晚吃：" + foods[randomIndex];
      }, 5200);
    });
  </script>
</body>
</html>
