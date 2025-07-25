<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8" />
  <title>BaBo BearRayog</title>
  <link href="https://fonts.googleapis.com/css2?family=Kanit&display=swap" rel="stylesheet">
  <style>
    body {
      font-family: 'Kanit', sans-serif;
      background-color: #fff0f5;
      padding: 20px;
      color: #333;
    }

    h2, h3 {
      color: #6b3e75;
    }

    .menu-button, .topping-button, .done-button, .clear-button {
      margin: 5px;
      padding: 10px 20px;
      background-color: #ffb6c1;
      color: white;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      font-size: 16px;
      box-shadow: 2px 2px 5px rgba(0,0,0,0.1);
      transition: background-color 0.2s ease;
    }

    .menu-button:hover, .topping-button:hover, .done-button:hover {
      background-color: #ff69b4;
    }

    .clear-button {
      background-color: #dc3545;
    }

    .clear-button:hover {
      background-color: #c82333;
    }

    .done-button {
      background-color: #28a745;
    }

    .done-button:hover {
      background-color: #218838;
    }

    table {
      width: 100%;
      margin-top: 15px;
      border-collapse: collapse;
      background-color: #fff;
      box-shadow: 0 0 10px rgba(0,0,0,0.05);
    }

    th, td {
      border: 1px solid #eee;
      padding: 10px;
      text-align: center;
    }

    th {
      background-color: #ffe4e1;
    }

    #toppingSection {
      margin-top: 20px;
      padding: 15px;
      background-color: #fffafc;
      border: 1px dashed #ff69b4;
      border-radius: 10px;
    }

    .section-title {
      margin-top: 40px;
      border-bottom: 2px solid #ff69b4;
      padding-bottom: 5px;
    }

    #totalPrice, #doneTotal {
      margin-top: 10px;
      font-size: 18px;
      font-weight: bold;
      color: #6b3e75;
    }

    #dashboardSection {
      margin-top: 40px;
      padding: 15px;
      background-color: #fffafc;
      border: 1px solid #ff69b4;
      border-radius: 10px;
      max-width: 100%;
    }

    #dashboardSection > div > div {
      margin-bottom: 20px;
    }

    #doneControls {
      margin-top: 10px;
      text-align: right;
    }

    canvas {
      width: 100% !important;
      height: auto !important;
    }
  </style>
</head>
<body>

  <h1 style="text-align:center;">🍹 BaBo Bear Rayong </h1>

  <!-- เมนูต่าง ๆ (เหมือนเดิม) -->
  <h2>เมนูแนะนำ</h2>
  <div>
    <button class="menu-button" onclick="selectBaseMenu('หมีคำราม', 60)">หมีคำราม (60฿)</button>
    <button class="menu-button" onclick="selectBaseMenu('นมหมีคำราม', 60)">นมหมีคำราม (60฿)</button>
    <button class="menu-button" onclick="selectBaseMenu('โกโก้ชีส', 60)">โกโก้ชีส (60฿)</button>
    <button class="menu-button" onclick="selectBaseMenu('ไมโลชีส', 60)">ไมโลชีส (60฿)</button>
  </div>

  <h2>ชานม</h2>
  <div>
    <button class="menu-button" onclick="selectBaseMenu('ชานมไต้หวัน', 40)">ชานมไต้หวัน (40฿)</button>
    <button class="menu-button" onclick="selectBaseMenu('ชานมเผือก', 50)">ชานมเผือก (50฿)</button>
    <button class="menu-button" onclick="selectBaseMenu('ชานมสตอเบอรี่', 50)">ชานมสตอเบอรี่ (50฿)</button>
    <button class="menu-button" onclick="selectBaseMenu('ชาเขียว', 50)">ชาเขียว (50฿)</button>
    <button class="menu-button" onclick="selectBaseMenu('ชานมคาปู', 50)">ชานมคาปู (50฿)</button>
    <button class="menu-button" onclick="selectBaseMenu('ชานมน้ำผึ้ง', 50)">ชานมน้ำผึ้ง (50฿)</button>
  </div>

  <h2>ชาผลไม้</h2>
  <div>
    <button class="menu-button" onclick="selectBaseMenu('ชามะลิ', 40)">ชามะลิ (40฿)</button>
    <button class="menu-button" onclick="selectBaseMenu('ชาสตอเบอรี่', 40)">ชาสตอเบอรี่ (40฿)</button>
    <button class="menu-button" onclick="selectBaseMenu('ชาแอปเปิ้ล', 40)">ชาแอปเปิ้ล (40฿)</button>
    <button class="menu-button" onclick="selectBaseMenu('ชาลิ้นจี่', 40)">ชาลิ้นจี่ (40฿)</button>
    <button class="menu-button" onclick="selectBaseMenu('ชาน้ำผึ้งมะนาว', 50)">ชาน้ำผึ้งมะนาว (50฿)</button>
    <button class="menu-button" onclick="selectBaseMenu('ชาบ๊วย', 50)">ชาบ๊วย (50฿)</button>
  </div>

  <h2>นมสด</h2>
  <div>
    <button class="menu-button" onclick="selectBaseMenu('นมสด', 50)">นมสด (50฿)</button>
    <button class="menu-button" onclick="selectBaseMenu('นมไมโล', 50)">นมไมโล (50฿)</button>
    <button class="menu-button" onclick="selectBaseMenu('นมโกโก้', 50)">นมโกโก้ (50฿)</button>
    <button class="menu-button" onclick="selectBaseMenu('นมสตอเบอรี่', 50)">นมสตอเบอรี่ (50฿)</button>
    <button class="menu-button" onclick="selectBaseMenu('นมเผือก', 50)">นมเผือก (50฿)</button>
  </div>

<h2>ชาไทย</h2>
  <div>
    <button class="menu-button" onclick="selectBaseMenu('ชาไทย', 40)">ชาไทย (40฿)</button>
    <button class="menu-button" onclick="selectBaseMenu('ชาไทยไข่มุก', 50)">ชาไทยไข่มุก (50฿)</button>
    <button class="menu-button" onclick="selectBaseMenu('ชาไทยดับเบิ้ลชีส', 65)">ชาไทยดับเบิ้ลชีส (65฿)</button>
    <button class="menu-button" onclick="selectBaseMenu('ชาไทยดับเบิ้ลชีสไข่มุก', 75)">ชาไทยดับเบิ้ลชีสไข่มุก (75฿)</button>
    </div>

  <!-- Section Topping -->
  <div id="toppingSection" style="display:none;">
    <h3>เลือก Topping สำหรับ <span id="selectedBaseName"></span></h3>
    <button class="topping-button" onclick="confirmMenu('+ ไข่มุก', 0)">ไข่มุก (+0฿)</button>
    <button class="topping-button" onclick="confirmMenu('+ ชีส', 15)">ชีส (+15฿)</button>
    <button class="topping-button" onclick="confirmMenu('', 0)">ไม่ใส่ Topping</button>
  </div>

  <!-- ตารางกำลังทำ -->
  <h2 class="section-title">📋 เมนู "กำลังทำ"</h2>
  <table id="selectedTable">
    <thead>
      <tr>
        <th>ลำดับ</th>
        <th>ชื่อเมนู</th>
        <th>ราคา (฿)</th>
        <th>ดำเนินการ</th>
      </tr>
    </thead>
    <tbody></tbody>
  </table>
  <div id="totalPrice">รวมทั้งหมด: 0 บาท</div>
  <button class="clear-button" onclick="clearAll()">ล้างทั้งหมด</button>

  <!-- ตารางเสร็จแล้ว -->
  <h2 class="section-title">✅ รายการที่เสร็จแล้ว</h2>
  <table id="doneTable">
    <thead>
      <tr>
        <th>ลำดับ</th>
        <th>ชื่อเมนู</th>
        <th>ราคา (฿)</th>
      </tr>
    </thead>
    <tbody></tbody>
  </table>
  <div id="doneTotal">รวมรายวัน: 0 บาท</div>

  <div id="doneControls">
    <button class="clear-button" onclick="clearDoneData()">ล้างข้อมูลสรุปยอด</button>
    <button class="clear-button" onclick="clearDoneAndSummarize()">สรุปยอด</button>
  </div>

  <!-- Dashboard -->
  <div id="dashboardSection" style="display:none;">
    <h2 class="section-title">📊 Dashboard ยอดขายวันนี้</h2>
    <div style="display: flex; flex-wrap: wrap; justify-content: space-between; gap: 20px;">
      <div style="flex: 1; min-width: 300px; max-width: 48%;">
        <h3>เมนูหลัก</h3>
        <canvas id="mainMenuChart"></canvas>
      </div>
      <div style="flex: 1; min-width: 300px; max-width: 48%;">
        <h3>Topping</h3>
        <canvas id="toppingChart"></canvas>
      </div>
    </div>
  </div>

  <!-- Script -->
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <script>
    let selectedMenus = [];
    let doneMenus = [];
    let currentBaseMenu = null;
    let mainMenuChart = null;
    let toppingChart = null;

    const todayKey = 'menus_' + new Date().toISOString().split('T')[0];
    const doneKey = todayKey + '_done';

    window.onload = () => {
      const saved = localStorage.getItem(todayKey);
      if (saved) selectedMenus = JSON.parse(saved);
      const done = localStorage.getItem(doneKey);
      if (done) doneMenus = JSON.parse(done);
      renderTables();
    };

    function selectBaseMenu(name, price) {
      currentBaseMenu = { name, price };
      document.getElementById("selectedBaseName").textContent = name;
      document.getElementById("toppingSection").style.display = "block";
    }

    function confirmMenu(toppingText, toppingPrice) {
      if (!currentBaseMenu) return;
      const fullName = currentBaseMenu.name + (toppingText ? ' ' + toppingText : '');
      const fullPrice = currentBaseMenu.price + toppingPrice;
      selectedMenus.push({ name: fullName, price: fullPrice });
      currentBaseMenu = null;
      document.getElementById("toppingSection").style.display = "none";
      saveToStorage();
      renderTables();
      document.getElementById("selectedTable").scrollIntoView({ behavior: 'smooth' });
    }

    function markAsDone(index) {
      const item = selectedMenus.splice(index, 1)[0];
      doneMenus.push(item);
      saveToStorage();
      renderTables();
    }

    function clearAll() {
      if (confirm("ล้างรายการ 'กำลังทำ' ทั้งหมด?")) {
        selectedMenus = [];
        saveToStorage();
        renderTables();
      }
    }

    function clearDoneAndSummarize() {
      if (doneMenus.length === 0) {
        alert("ยังไม่มีรายการที่เสร็จแล้วสำหรับสรุปยอด");
        return;
      }
      const total = doneMenus.reduce((sum, item) => sum + item.price, 0);
      const today = new Date().toLocaleDateString('th-TH', { day: 'numeric', month: 'long', year: 'numeric' });
      alert("สรุปยอดรายวัน: " + total + " บาท");
      document.querySelector("#dashboardSection h2").textContent = `📊 Dashboard ยอดขายวันที่ ${today}`;
      renderSalesCharts(doneMenus);
      document.getElementById('dashboardSection').style.display = 'block';
    }

    function clearDoneData() {
      if (confirm("ล้างข้อมูลรายการสรุปยอดทั้งหมด?")) {
        doneMenus = [];
        saveToStorage();
        renderTables();
        if (mainMenuChart) {
          mainMenuChart.destroy();
          mainMenuChart = null;
        }
        if (toppingChart) {
          toppingChart.destroy();
          toppingChart = null;
        }
        document.getElementById('dashboardSection').style.display = 'none';
      }
    }

    function saveToStorage() {
      localStorage.setItem(todayKey, JSON.stringify(selectedMenus));
      localStorage.setItem(doneKey, JSON.stringify(doneMenus));
    }

    function renderTables() {
      const tbody = document.querySelector("#selectedTable tbody");
      const tbodyDone = document.querySelector("#doneTable tbody");
      tbody.innerHTML = "";
      tbodyDone.innerHTML = "";

      let total = 0;
      selectedMenus.forEach((item, index) => {
        const row = document.createElement("tr");
        row.innerHTML = `
          <td>${index + 1}</td>
          <td>${item.name}</td>
          <td>${item.price}</td>
          <td><button class="done-button" onclick="markAsDone(${index})">เสร็จ</button></td>`;
        tbody.appendChild(row);
        total += item.price;
      });
      document.getElementById("totalPrice").textContent = `รวมทั้งหมด: ${total} บาท`;

      let doneTotal = 0;
      doneMenus.forEach((item, index) => {
        const row = document.createElement("tr");
        row.innerHTML = `<td>${index + 1}</td><td>${item.name}</td><td>${item.price}</td>`;
        tbodyDone.appendChild(row);
        doneTotal += item.price;
      });
      document.getElementById("doneTotal").textContent = `รวมรายวัน: ${doneTotal} บาท`;
    }

    function renderSalesCharts(data) {
      const mainCounts = {};
      const toppingCounts = {};

      data.forEach(item => {
        let nameParts = item.name.split(' + ');
        let mainName = nameParts[0].trim();
        mainCounts[mainName] = (mainCounts[mainName] || 0) + 1;

        if (nameParts.length > 1) {
          let toppingName = nameParts[1].trim();
          toppingCounts[toppingName] = (toppingCounts[toppingName] || 0) + 1;
        }
      });

      const mainLabels = Object.keys(mainCounts);
      const mainData = Object.values(mainCounts);
      const ctxMain = document.getElementById('mainMenuChart').getContext('2d');

      if (mainMenuChart) mainMenuChart.destroy();
      mainMenuChart = new Chart(ctxMain, {
        type: 'pie',
        data: {
          labels: mainLabels,
          datasets: [{
            label: 'ยอดขายเมนูหลัก',
            data: mainData,
            backgroundColor: generateColors(mainLabels.length),
          }]
        },
        options: {
          responsive: true,
          plugins: {
            legend: { position: 'bottom' },
            title: { display: true, text: 'ยอดขายเมนูหลักวันนี้ (จำนวนรายการ)' }
          }
        }
      });

      const toppingLabels = Object.keys(toppingCounts);
      const toppingData = Object.values(toppingCounts);
      const ctxTopping = document.getElementById('toppingChart').getContext('2d');

      if (toppingChart) toppingChart.destroy();
      toppingChart = new Chart(ctxTopping, {
        type: 'pie',
        data: {
          labels: toppingLabels,
          datasets: [{
            label: 'ยอดขาย Topping',
            data: toppingData,
            backgroundColor: generateColors(toppingLabels.length),
          }]
        },
        options: {
          responsive: true,
          plugins: {
            legend: { position: 'bottom' },
            title: { display: true, text: 'ยอดขาย Topping วันนี้ (จำนวนรายการ)' }
          }
        }
      });
    }

    function generateColors(n) {
      const colors = ['#FF6384', '#36A2EB', '#FFCE56', '#8A2BE2', '#FF4500', '#00CED1', '#9ACD32', '#FF69B4', '#20B2AA', '#FFA500'];
      return Array.from({ length: n }, (_, i) => colors[i % colors.length]);
    }
  </script>
</body>
</html>
