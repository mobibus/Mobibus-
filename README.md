<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <title>أسياسيل - صرفيات الخط</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #fff;
      color: #c00;
      text-align: center;
      padding: 20px;
      direction: rtl;
      border: 3px solid #c00;
      max-width: 450px;
      margin: auto;
      border-radius: 15px;
    }
    select, input, button {
      width: 90%;
      padding: 10px;
      margin: 10px 0;
      border: 2px solid #c00;
      border-radius: 8px;
      font-size: 16px;
    }
    button {
      background-color: #c00;
      color: #fff;
      cursor: pointer;
      font-weight: bold;
    }
    .result {
      margin-top: 20px;
      padding: 15px;
      background-color: #fee;
      border-radius: 10px;
      border: 1px solid #c00;
    }
    .footer {
      margin-top: 30px;
      font-size: 14px;
      color: gray;
    }
  </style>
</head>
<body>

  <h1>أسياسيل</h1>
  <p>صرفيات جميع خطوط أسياسيل</p>
  <p><small>وادي فون – امتياز شركة أسياسيل</small></p>

  <label>اختر نوع الخط:</label>
  <select id="lineType">
    <option>خط اليوز (كوين)</option>
    <option>خط الدفع المسبق القديم</option>
    <option>خط الدفع المسبق الجديد</option>
    <option>خط الشباب</option>
    <option>خط الماس</option>
    <option>خط يوم علينة ويوم عليك</option>
    <option>خط العتبات</option>
    <option>خط ايليت</option>
    <option>خطّ المؤسسات</option>
    <option>خط اي كنترول</option>
    <option>خط خلات</option>
    <option>خط الدينار (سليمانية)</option>
    <option>خط بزنز ماكس</option>
  </select>

  <label>المبلغ (كوين أو دينار):</label>
  <input type="number" id="amount" placeholder="اكتب المبلغ هنا">

  <label>نوع الخدمة:</label>
  <select id="serviceType">
    <option>الكل</option>
    <option>الاتصال</option>
    <option>الانترنت</option>
    <option>الرسائل</option>
  </select>

  <button onclick="calculate()">احسب الآن</button>

  <div class="result" id="resultDisplay"></div>

  <div class="footer">© تصميم موبي باص - frn.mohmed.wmobibus@Asiacell.com - 2025</div>

  <script>
    function calculate() {
      const lineType = document.getElementById('lineType').value;
      const serviceType = document.getElementById('serviceType').value;
      const amount = parseFloat(document.getElementById('amount').value);
      let result = "";

      let isYooz = lineType.includes("اليوز");
      let callRate = isYooz ? 2 : 2.4;
      let smsRate = isYooz ? 50 : 50;
      let dataRate = isYooz ? 4 : null;

      if (isNaN(amount) || amount <= 0) {
        document.getElementById("resultDisplay").innerHTML = "❗ الرجاء إدخال مبلغ صالح";
        return;
      }

      if (serviceType === "الكل" || serviceType === "الاتصال") {
        let seconds = Math.floor(amount / callRate);
        let minutes = Math.floor(seconds / 60);
        result += `📞 الاتصال: ${minutes} دقيقة<br>`;
      }

      if ((serviceType === "الكل" || serviceType === "الانترنت") && isYooz) {
        let mb = Math.floor(amount / dataRate);
        let gb = Math.floor(mb / 1024);
        result += `🌐 الإنترنت: ${gb} GB (${mb} MB)<br>`;
      }

      if (serviceType === "الكل" || serviceType === "الرسائل") {
        let sms = Math.floor(amount / smsRate);
        result += `✉️ الرسائل: ${sms} رسالة`;
      }

      document.getElementById("resultDisplay").innerHTML = result;
    }
  </script>

</body>
</html>
