# Babo-bear-order
<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8" />
  <title>สั่งเมนู</title>
  <style>
    body { font-family: sans-serif; padding: 20px; background-color: #f2f2f2; }
    .menu-button {
      margin: 5px; padding: 10px 15px;
      background-color: #007bff; color: white;
      border: none; border-radius: 5px; cursor: pointer;
    }
    .menu-button:hover { background-color: #0056b3; }
    table {
      margin-top: 15px; border-collapse: collapse;
      width: 100%; background-color: white;
    }
    th, td {
      border: 1px solid #ccc; padding: 8px;
      text-align: center;
    }
    .action-btn {
      background-color: #28a745; color: white;
      border: none; padding: 5px 10px;
      border-radius: 3px; cursor: pointer;
    }
    .action-btn:hover { background-color: #218838; }

    .clear-button {
      margin-top: 10px;
      background-color: #dc3545;
      color: white;
      border: none;
      padding: 8px 12px;
      border-radius: 5px;
      cursor: pointer;
    }

    .summary-button {
      margin-top: 10px;
      background-color: orange;
      color: white;
      border: none;
      padding: 8px 12px;
      border-radius: 5px;
      cursor: pointer;
    }

    .total { margin-top: 10px; font-weight: bold; }
  </style>
</head>
<body>

  <h2>เมนูทั้งหมด</h2>
  <div id="menuList">
    <button class="menu-button" onclick="addMenu('หมีคำราม', 60)">หมีคำราม (60฿)</button>
    <button class="menu-button" onclick="addMenu('นมหมีคำราม', 60)">นมหมีคำราม (60฿)</button>
    <button class="menu-button" onclick="addMenu('โกโก้ชีส', 60)">โกโก้ชีส (60฿)</button>
    <button class="menu-button" onclick="addMenu('ไมโลชีส', 60)">ไมโลชีส (60฿)</button>
  </div>

  <h2>เมนูที่เลือก (กำลังทำ)</h2>
  <table id="selectedTable">
    <thead>
      <tr>
        <th>ลำดับ</th>
        <th>ชื่อเมนู</th>
        <th>ราคา (฿)</th>
        <th>จัดการ</th>
      </tr>
    </thead>
    <tbody></tbody>
  </table>
  <div class="total" id="totalPrice">รวมทั้งหมด: 0 บาท</div>
  <button class="clear-button" onclick="clearSelected()">ล้างทั้งหมด</button>

  <h2>เมนูที่เสร็จแล้ว (วันนี้)</h2>
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
  <div class="total" id="doneTotal">รวมทั้งหมด: 0 บาท</div>
  <button class="summary-button" onclick="summarizeDone()">สรุปยอด</button>

  <script>
    const selectedKey = "menus_selected";
    const doneKey = "menus_done_" + new Date().toISOString().split("T")[0];

    let selectedMenus = [];
    let doneMenus = [];

    window.onload = () => {
      const storedSelected = localStorage.getItem(selectedKey);
      const storedDone = localStorage.getItem(doneKey);
      if (storedSelected) selectedMenus = JSON.parse(storedSelected);
      if (storedDone) doneMenus = JSON.parse(storedDone);
      renderTables();
    };

    function addMenu(name, price) {
      const topping = prompt(`เพิ่ม Topping ให้กับ "${name}" (เช่น ไข่มุก +10)\nถ้าไม่มี topping ให้กด Cancel หรือปล่อยว่าง`, "");
      let fullName = name;
      let toppingPrice = 0;

      if (topping && topping.trim() !== "") {
        const match = topping.match(/(.+)\s*\+?(\d+)/);
        if (match) {
          const toppingName = match[1].trim();
          toppingPrice = parseInt(match[2]);
          fullName = `${name} + ${toppingName}`;
        } else {
          alert("รูปแบบ topping ไม่ถูกต้อง เช่น: ไข่มุก +10");
          return;
        }
      }

      selectedMenus.push({ name: fullName, price: price + toppingPrice });
      saveData();
      renderTables();
    }

    function removeSelected(index) {
      selectedMenus.splice(index, 1);
      saveData();
      renderTables();
    }

    function markAsDone(index) {
      const item = selectedMenus.splice(index, 1)[0];
      doneMenus.push(item);
      saveData();
      renderTables();
    }

    function clearSelected() {
      if (confirm("ล้างรายการทั้งหมดในกำลังทำ?")) {
        selectedMenus = [];
        saveData();
        renderTables();
      }
    }

    function summarizeDone() {
      let total = doneMenus.reduce((sum, item) => sum + item.price, 0);
      alert(`สรุปยอดวันนี้: ${total} บาท`);
      doneMenus = [];
      saveData();
      renderTables();
    }

    function saveData() {
      localStorage.setItem(selectedKey, JSON.stringify(selectedMenus));
      localStorage.setItem(doneKey, JSON.stringify(doneMenus));
    }

    function renderTables() {
      // Render selected table
      const selectedBody = document.querySelector("#selectedTable tbody");
      selectedBody.innerHTML = "";
      let selectedTotal = 0;

      selectedMenus.forEach((item, i) => {
        const row = document.createElement("tr");
        row.innerHTML = `
          <td>${i + 1}</td>
          <td>${item.name}</td>
          <td>${item.price}</td>
          <td>
            <button class="action-btn" onclick="markAsDone(${i})">เสร็จ</button>
            <button class="clear-button" style="padding: 3px 6px;" onclick="removeSelected(${i})">ลบ</button>
          </td>
        `;
        selectedBody.appendChild(row);
        selectedTotal += item.price;
      });
      document.getElementById("totalPrice").textContent = `รวมทั้งหมด: ${selectedTotal} บาท`;

      // Render done table
      const doneBody = document.querySelector("#doneTable tbody");
      doneBody.innerHTML = "";
      let doneTotal = 0;

      doneMenus.forEach((item, i) => {
        const row = document.createElement("tr");
        row.innerHTML = `
          <td>${i + 1}</td>
          <td>${item.name}</td>
          <td>${item.price}</td>
        `;
        doneBody.appendChild(row);
        doneTotal += item.price;
      });
      document.getElementById("doneTotal").textContent = `รวมทั้งหมด: ${doneTotal} บาท`;
    }
  </script>
</body>
</html>
