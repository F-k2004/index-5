<!-- index.html -->
<!DOCTYPE html>
<html lang="fa">
<head>
  <meta charset="UTF-8">
  <title>🎨 پالت‌ساز رنگ</title>
  <style>
    body {
      font-family: sans-serif;
      text-align: center;
      background: #f3f3f3;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      padding: 20px;
    }
    h1 {
      margin-bottom: 20px;
    }
    #colorDisplay {
      width: 150px;
      height: 150px;
      border-radius: 12px;
      margin-bottom: 15px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.2);
      transition: background 0.3s;
    }
    #colorCode {
      font-size: 20px;
      background: #fff;
      padding: 8px 15px;
      border-radius: 8px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
      margin-bottom: 15px;
    }
    button {
      padding: 10px 20px;
      border: none;
      border-radius: 8px;
      background: #333;
      color: #fff;
      font-size: 16px;
      margin: 5px;
      cursor: pointer;
      transition: 0.3s;
    }
    button:hover {
      background: #555;
    }
    #palette {
      margin-top: 30px;
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      justify-content: center;
    }
    .colorBox {
      width: 80px;
      height: 80px;
      border-radius: 10px;
      cursor: pointer;
      position: relative;
    }
    .colorBox span {
      position: absolute;
      bottom: 5px;
      left: 5px;
      font-size: 12px;
      color: #fff;
      text-shadow: 0 0 3px #000;
    }
  </style>
</head>
<body>
  <h1>🎨 سازنده پالت رنگ</h1>
  <div id="colorDisplay"></div>
  <div id="colorCode">#ffffff</div>
  <button onclick="generateColor()">🔄 رنگ جدید</button>
  <button onclick="saveColor()">💾 ذخیره رنگ</button>
  <h2>🎨 پالت من</h2>
  <div id="palette"></div>

  <script>
    let currentColor = "#ffffff";
    let palette = JSON.parse(localStorage.getItem("palette")) || [];

    function generateColor() {
      currentColor = "#" + Math.floor(Math.random() * 16777215).toString(16).padStart(6, '0');
      document.getElementById("colorDisplay").style.backgroundColor = currentColor;
      document.getElementById("colorCode").textContent = currentColor;
    }

    function saveColor() {
      if (!palette.includes(currentColor)) {
        palette.push(currentColor);
        localStorage.setItem("palette", JSON.stringify(palette));
        renderPalette();
      }
    }

    function renderPalette() {
      const container = document.getElementById("palette");
      container.innerHTML = "";
      palette.forEach(color => {
        const div = document.createElement("div");
        div.className = "colorBox";
        div.style.backgroundColor = color;
        div.innerHTML = `<span>${color}</span>`;
        div.onclick = () => copyColor(color);
        container.appendChild(div);
      });
    }

    function copyColor(color) {
      navigator.clipboard.writeText(color);
      alert(`✅ رنگ ${color} کپی شد!`);
    }

    // نمایش پالت هنگام بارگذاری
    renderPalette();
    generateColor();
  </script>
</body>
</html>
