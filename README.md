
        }
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
