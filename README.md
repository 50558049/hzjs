<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>韩折计算器</title>
<style>
  /* 基础样式 */
  body { font-family: Arial, sans-serif; padding: 20px; }
  .input-group { margin-bottom: 10px; }
  .input-group label { margin-right: 10px; display: block; }
  .input-group input, .input-group select, button {
    width: 100%; /* 使输入框和按钮宽度适应容器宽度 */
    margin-right: 0; margin-bottom: 10px;
    font-size: 16px; padding: 10px;
  }
  button {
    cursor: pointer; font-weight: bold;
    background-color: #4CAF50; color: white; /* 添加按钮背景色和文字颜色 */
    border: none; border-radius: 5px; /* 圆角按钮 */
  }
  .result { margin-top: 20px; }

  /* 响应式设计：针对屏幕宽度小于600px的设备 */
  @media (max-width: 600px) {
    body { padding: 5px; }
    .input-group label, .input-group input, .input-group select, button {
      font-size: 14px; padding: 8px; /* 调整字体大小和内边距 */
    }
  }
</style>
</head>
<body>
<h2>韩折计算器</h2>
<div class="input-group">
  <label for="windowWidth">窗宽（cm）:</label>
  <input type="number" id="windowWidth" required>
</div>
<div class="input-group">
  <label for="fabricWidth">布料宽（cm）:</label>
  <input type="number" id="fabricWidth" required>
</div>
<div class="input-group">
  <label for="curtainType">窗帘类型:</label>
  <select id="curtainType">
    <option value="split">对开</option>
    <option value="single">单块</option>
  </select>
</div>
<div class="input-group">
  <label for="addWidth">增加宽度:</label>
  <select id="addWidth">
    <option value="20">+20</option>
    <option value="15">+15</option>
  </select>
</div>
<button onclick="calculate()">计算</button>

<div class="result" id="result"></div>

<script>
  function calculate() {
    const windowWidth = parseFloat(document.getElementById('windowWidth').value);
    const fabricWidth = parseFloat(document.getElementById('fabricWidth').value);
    const curtainType = document.getElementById('curtainType').value;
    const addWidth = parseInt(document.getElementById('addWidth').value, 10);

    let finishedCurtainWidth;
    if (curtainType === 'split') {
      finishedCurtainWidth = windowWidth / 2 + addWidth;
    } else {
      finishedCurtainWidth = windowWidth + addWidth;
    }
    
    const foldMaterial = fabricWidth - finishedCurtainWidth;
    const numberOfFolds = Math.floor(finishedCurtainWidth * 0.07);
    const sizeOfFold = numberOfFolds > 0 ? foldMaterial / numberOfFolds : 0;
    const spacingBetweenFolds = numberOfFolds > 1 ? finishedCurtainWidth / (numberOfFolds - 1) : 0;

    document.getElementById('result').innerHTML = `成品帘宽: ${finishedCurtainWidth.toFixed(2)} cm<br>折用料: ${foldMaterial.toFixed(2)} cm<br>折个数: ${numberOfFolds}<br>折大小: ${sizeOfFold.toFixed(2)} cm<br>折间距: ${spacingBetweenFolds.toFixed(2)} cm`;
  }
</script>
</body>
</html>
