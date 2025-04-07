<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>配对食物名称游戏</title>
  <style>
    body {
      font-family: sans-serif;
      text-align: center;
      padding: 2em;
      background: #fffbe6;
    }
    h1 {
      font-size: 2em;
      color: #d2691e;
    }
    .container {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 1em;
      margin-top: 2em;
    }
    .food-item, .name-box {
      border: 2px dashed #ccc;
      padding: 1em;
      min-width: 120px;
      min-height: 120px;
      background: #fff;
      border-radius: 12px;
    }
    .food-img {
      width: 100px;
      height: 100px;
      object-fit: cover;
      border-radius: 8px;
    }
    .name-box {
      cursor: move;
      background: #fef2dc;
    }
    .matched {
      border-color: green;
      background-color: #e0ffe0;
    }
    button {
      margin-top: 2em;
      padding: 0.7em 2em;
      font-size: 1em;
      background: #ffb347;
      border: none;
      border-radius: 8px;
      color: white;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <h1>配对食物和名称</h1>
  <p>把食物名称拖到正确的食物图片上</p>

  <div class="container" id="food-container">
    <div class="food-item" data-name="饺子" ondrop="drop(event)" ondragover="allowDrop(event)">
      <img src="https://upload.wikimedia.org/wikipedia/commons/6/6f/Jiaozi-Dumplings.jpg" class="food-img" alt="饺子" />
    </div>
    <div class="food-item" data-name="寿司" ondrop="drop(event)" ondragover="allowDrop(event)">
      <img src="https://upload.wikimedia.org/wikipedia/commons/6/60/Sushi_platter.jpg" class="food-img" alt="寿司" />
    </div>
    <div class="food-item" data-name="披萨" ondrop="drop(event)" ondragover="allowDrop(event)">
      <img src="https://upload.wikimedia.org/wikipedia/commons/d/d3/Supreme_pizza.jpg" class="food-img" alt="披萨" />
    </div>
  </div>

  <div class="container" id="names-container">
    <div class="name-box" draggable="true" ondragstart="drag(event)" id="寿司">寿司</div>
    <div class="name-box" draggable="true" ondragstart="drag(event)" id="披萨">披萨</div>
    <div class="name-box" draggable="true" ondragstart="drag(event)" id="饺子">饺子</div>
  </div>

  <button onclick="checkAnswers()">提交答案</button>

  <script>
    function allowDrop(ev) {
      ev.preventDefault();
    }

    function drag(ev) {
      ev.dataTransfer.setData("text", ev.target.id);
    }

    function drop(ev) {
      ev.preventDefault();
      var data = ev.dataTransfer.getData("text");
      const draggedEl = document.getElementById(data);
      if (!ev.target.querySelector('.name-box')) {
        ev.target.appendChild(draggedEl);
      }
    }

    function checkAnswers() {
      const items = document.querySelectorAll('.food-item');
      items.forEach(item => {
        const expected = item.getAttribute('data-name');
        const actual = item.querySelector('.name-box')?.id;
        if (expected === actual) {
          item.classList.add('matched');
        } else {
          item.classList.remove('matched');
        }
      });
    }
  </script>
</body>
</html>
