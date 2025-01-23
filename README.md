<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>لیست اطلاعات راننده و مالک</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 20px;
        }
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        .datetime {
            font-size: 16px;
            color: #555;
        }
        .stats {
            font-size: 14px;
            color: #333;
            text-align: right;
        }
        .footer {
            margin-top: 20px;
            text-align: center;
            font-size: 14px;
            color: #333;
        }
        h1 {
            text-align: center;
            font-size: 24px;
            font-weight: bold;
        }
        .logo-container {
            text-align: center;
            margin: 20px 0;
        }
        .logo {
            width: 150px;
            height: auto;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
            font-size: 18px;
            text-align: center;
            background: #fff;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        }
        table thead tr {
            background-color: #4CAF50;
            color: white;
        }
        table th, table td {
            padding: 12px 15px;
            border: 1px solid #ddd;
        }
        table tbody tr:nth-child(even) {
            background-color: #f9f9f9;
        }
        table tbody tr:hover {
            background-color: #f1f1f1;
            cursor: pointer;
        }
        .actions {
            text-align: center;
            margin: 20px 0;
        }
        button, input[type="file"], input[type="text"] {
            padding: 10px 20px;
            font-size: 16px;
            color: black;
            border: 1px solid #ddd;
            border-radius: 5px;
            margin: 5px;
        }
        input[type="text"] {
            width: 300px;
        }
    </style>
    <script>
        function updateDateTime() {
            const now = new Date();
            const daysOfWeek = ['یکشنبه', 'دوشنبه', 'سه‌شنبه', 'چهارشنبه', 'پنجشنبه', 'جمعه', 'شنبه'];
            const day = daysOfWeek[now.getDay()];
            const date = now.toLocaleDateString('fa-IR');
            const time = now.toLocaleTimeString('fa-IR');
            document.getElementById("datetime").textContent = `تاریخ: ${date} (${day}) | ساعت: ${time}`;
        }

        function updateStats() {
            const rows = document.querySelectorAll("#infoTable tbody tr");
            const totalEntries = rows.length;
            const paidCount = Array.from(rows).filter(row => {
                const checkbox = row.querySelector("input[type='checkbox']");
                return checkbox && checkbox.checked;
            }).length;

            document.getElementById("stats").textContent = `تعداد ورودی‌ها: ${totalEntries} | تعداد پرداختی‌ها: ${paidCount}`;
        }

        function saveChanges() {
            const table = document.querySelector("#infoTable");
            const rows = table.querySelectorAll("tbody tr");
            const data = [];
            rows.forEach(row => {
                const cells = row.querySelectorAll("td");
                const rowData = Array.from(cells).map((cell, index) => 
                    index === 7 
                    ? (cell.querySelector("input[type='checkbox']").checked ? "true" : "false")
                    : cell.textContent.trim()
                );
                data.push(rowData);
            });

            // ذخیره داده‌ها در LocalStorage
            localStorage.setItem("tableData", JSON.stringify(data));
            updateStats();
            alert("داده‌ها ذخیره شدند!");
        }

        function loadSavedData() {
            const savedData = localStorage.getItem("tableData");
            if (savedData) {
                const data = JSON.parse(savedData);
                const tableBody = document.querySelector("#infoTable tbody");
                tableBody.innerHTML = "";
                data.forEach(rowData => {
                    const tr = document.createElement("tr");
                    tr.innerHTML = rowData.map((cell, index) => 
                        index === 7 
                        ? `<td><input type="checkbox" ${cell === "true" ? "checked" : ""}></td>` 
                        : `<td contenteditable="true">${cell}</td>`
                    ).join("");
                    tableBody.appendChild(tr);
                });
            }
            updateStats();
        }

        function addRow() {
            const tableBody = document.querySelector("#infoTable tbody");
            const tr = document.createElement("tr");
            for (let i = 0; i < 9; i++) {
                if (i === 7) {
                    tr.innerHTML += `<td><input type="checkbox" onclick="updateStats()"></td>`;
                } else {
                    tr.innerHTML += `<td contenteditable="true"></td>`;
                }
            }
            tableBody.appendChild(tr);
            updateStats();
        }

        document.addEventListener("DOMContentLoaded", () => {
            loadSavedData();
            setInterval(updateDateTime, 1000);
        });
    </script>
</head>
<body>
    <div class="header">
        <div class="datetime" id="datetime"></div>
        <div class="stats" id="stats"></div>
    </div>
    <h1>شرکت حمل و نقل ایرانجوان</h1>
    <div class="actions">
        <input type="text" id="searchInput" placeholder="جستجو در جدول..." onkeyup="searchTable()">
        <button onclick="addRow()">افزودن سطر جدید</button>
        <button onclick="saveChanges()">ذخیره داده‌ها</button>
    </div>
    <table id="infoTable">
        <thead>
            <tr>
                <th>کد مشتری</th>
                <th>نام و نام خانوادگی</th>
                <th>کد ملی</th>
                <th>شماره ثبت اکانت</th>
                <th>نام مالک</th>
                <th>کد ملی مالک</th>
                <th>شماره پلاک</th>
                <th>تیک پرداخت</th>
                <th>تاریخ و ساعت ثبت</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td contenteditable="true">1</td>
                <td contenteditable="true">نام نمونه</td>
                <td contenteditable="true">1234567890</td>
                <td contenteditable="true">1001</td>
                <td contenteditable="true">مالک نمونه</td>
                <td contenteditable="true">0987654321</td>
                <td contenteditable="true">12الف345</td>
                <td><input type="checkbox" onclick="updateStats()"></td>
                <td contenteditable="true">1402/10/01</td>
            </tr>
        </tbody>
    </table>
    <div class="footer">
        ادمین: <span id="stats"></span> | کاربری مدیریت: ***** ایمانی
    </div>
</body>
</html>
