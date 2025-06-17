<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>أسياسيل - حاسبة الصرف</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #fff;
      color: #c00;
      text-align: center;
      padding: 20px;
      border: 4px solid #c00;
      margin: 10px;
      border-radius: 12px;
    }
    select, input {
      width: 90%;
      padding: 10px;
      margin: 10px auto;
      border: 2px solid #c00;
      border-radius: 6px;
      font-size: 16px;
    }
    button {
      padding: 12px 20px;
      font-size: 18px;
      background-color: #c00;
      color: #fff;
      border: none;
      border-radius: 8px;
      cursor: pointer;
    }
    .result {
      margin-top: 20px;
      background: #fee;
      padding: 15px;
      border-radius: 10px;
      border: 1px solid #f99;
    }
    footer {
      margin-top: 30px;
      font-size: 14px;
      color: #777;
    }
  </style>
</head>
<body>
  <h2 style="color: red;">أسياسيل</h2>
  <p>صرفيات جميع خطوط أسياسيل<br>وادي فون – امتياز شركة أسياسيل</p>

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
  <input type="number" id="amount" placeholder="اكتب المبلغ هنا" />

  <label>نوع الخدمة:</label>
  <select id="serviceType">
    <option value="all">الكل</option>
    <option value="call">📞 الاتصال</option>
    <option value="data">🌐 الإنترنت</option>
    <option value="sms">✉️ الرسائل</option>
  </select>

  <button onclick="calculate()">احسب الآن</button>

  <div class="result" id="resultBox"></div>

  <footer>
    تصميم موبي باص ©<br>
    frn.mohmed.wmobibus@Asiacell.com - 2025
  </footer>

  <script>
    function calculate() {
      const line = document.getElementById("lineType").value;
      const amount = parseFloat(document.getElementById("amount").value);
      const service = document.getElementById("serviceType").value;
      const isYooz = line.includes("يوز");

      let callRate = isYooz ? 2 : 2.4; // كوين أو دينار
      let dataRate = isYooz ? 4 : 4;    // نفس السعر
      let smsRate = isYooz ? 50 : 50;

      let result = "";

      if (service === "call" || service === "all") {
        const callSeconds = amount / callRate;
        const callMinutes = Math.floor(callSeconds / 60);
        result += `📞 الاتصال: ${callMinutes} دقيقة<br>`;
      }

      if (service === "data" || service === "all") {
        const mb = amount / dataRate;
        if (mb >= 1024) {
          const gb = (mb / 1024).toFixed(2);
          result += `🌐 الإنترنت: ${gb} GB (${Math.floor(mb)} MB)<br>`;
        } else {
          result += `🌐 الإنترنت: ${Math.floor(mb)} MB<br>`;
        }
      }

      if (service === "sms" || service === "all") {
        const smsCount = Math.floor(amount / smsRate);
        result += `✉️ الرسائل: ${smsCount} رسالة<br>`;
      }

      document.getElementById("resultBox").innerHTML = result || "يرجى إدخال المبلغ!";
    }
  </script>
</body>
</html>
