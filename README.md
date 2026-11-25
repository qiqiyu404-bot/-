<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>線上服務申請</title>
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: -apple-system, BlinkMacSystemFont, "PingFang TC", "Microsoft JhengHei", "Segoe UI", Roboto, sans-serif;
    }

    body {
      background-color: #f3f7f4;
      color: #2b332e;
      display: flex;
      flex-direction: column;
      align-items: center;
      min-height: 100vh;
      padding: 20px 16px 36px;
    }

    .container {
      width: 100%;
      max-width: 420px;
    }

    /* 頂部深綠色主卡片 */
    .header-card {
      background-color: #367250;
      color: #ffffff;
      border-radius: 16px;
      padding: 34px 24px 30px;
      text-align: center;
      box-shadow: 0 6px 16px rgba(54, 114, 80, 0.14);
      margin-bottom: 16px;
    }

    .icon-circle {
      width: 52px;
      height: 52px;
      background-color: rgba(255, 255, 255, 0.16);
      border-radius: 50%;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      margin-bottom: 14px;
    }

    .header-card h1 {
      font-size: 22px;
      font-weight: 700;
      margin-bottom: 10px;
      letter-spacing: 0.5px;
    }

    .header-card p {
      font-size: 14px;
      line-height: 1.65;
      color: rgba(255, 255, 255, 0.92);
    }

    /* 白色表單卡片 */
    .form-card {
      background-color: #ffffff;
      border-radius: 16px;
      padding: 24px 22px;
      box-shadow: 0 2px 12px rgba(0, 0, 0, 0.04);
      margin-bottom: 24px;
    }

    .form-group {
      margin-bottom: 18px;
    }

    .form-group label {
      display: block;
      font-size: 14px;
      font-weight: 600;
      color: #262b28;
      margin-bottom: 8px;
    }

    .form-group label .required {
      color: #e04848;
      margin-left: 2px;
    }

    .input-box {
      position: relative;
      display: flex;
      align-items: center;
    }

    .input-box svg {
      position: absolute;
      left: 14px;
      width: 18px;
      height: 18px;
      color: #9ba59f;
      pointer-events: none;
    }

    .input-box input {
      width: 100%;
      height: 48px;
      padding: 0 14px 0 40px;
      border: 1px solid #e2e6e4;
      border-radius: 10px;
      font-size: 15px;
      color: #262b28;
      background-color: #ffffff;
      transition: border-color 0.2s, box-shadow 0.2s;
      outline: none;
    }

    .input-box input::placeholder {
      color: #9ba59f;
    }

    .input-box input:focus {
      border-color: #367250;
      box-shadow: 0 0 0 3px rgba(54, 114, 80, 0.1);
    }

    /* 隱私提示灰底區塊 */
    .privacy-box {
      background-color: #f7f9f8;
      border-radius: 10px;
      padding: 12px 14px;
      display: flex;
      align-items: flex-start;
      gap: 8px;
      margin-bottom: 20px;
      font-size: 12.5px;
      line-height: 1.5;
      color: #6b756f;
    }

    .privacy-box svg {
      flex-shrink: 0;
      width: 15px;
      height: 15px;
      color: #6b756f;
      margin-top: 2px;
    }

    /* 送出申請按鈕 */
    .submit-btn {
      width: 100%;
      height: 50px;
      background-color: #367250;
      color: #ffffff;
      border: none;
      border-radius: 10px;
      font-size: 16px;
      font-weight: 600;
      letter-spacing: 0.5px;
      cursor: pointer;
      transition: background-color 0.2s, transform 0.1s;
    }

    .submit-btn:hover {
      background-color: #2d6043;
    }

    .submit-btn:active {
      transform: scale(0.99);
    }

    /* 底部安全標章 */
    .trust-badges {
      display: flex;
      justify-content: center;
      align-items: center;
      gap: 16px;
      margin-top: 16px;
      font-size: 12px;
      color: #77827c;
    }

    .trust-badges span {
      display: inline-flex;
      align-items: center;
      gap: 4px;
    }

    .trust-badges svg {
      width: 13px;
      height: 13px;
      color: #367250;
    }

    /* 頁尾連結區 */
    .footer {
      text-align: center;
      font-size: 12px;
      color: #8c9690;
    }

    .footer-links {
      display: flex;
      justify-content: center;
      align-items: center;
      gap: 16px;
      margin-bottom: 10px;
    }

    .footer-links a {
      color: #6b756f;
      text-decoration: none;
    }

    .footer-links a.line-link {
      color: #367250;
      font-weight: 600;
      display: inline-flex;
      align-items: center;
      gap: 4px;
    }

    /* 提示小視窗 (Modal) */
    .modal-overlay {
      position: fixed;
      inset: 0;
      background-color: rgba(0, 0, 0, 0.45);
      display: none;
      align-items: center;
      justify-content: center;
      padding: 20px;
      z-index: 9999;
    }

    .modal-overlay.show {
      display: flex;
    }

    .modal-box {
      background-color: #ffffff;
      width: 100%;
      max-width: 300px;
      border-radius: 14px;
      padding: 24px 20px 18px;
      text-align: center;
      box-shadow: 0 10px 28px rgba(0, 0, 0, 0.18);
      animation: popIn 0.18s ease-out;
    }

    @keyframes popIn {
      from {
        transform: scale(0.92);
        opacity: 0;
      }
      to {
        transform: scale(1);
        opacity: 1;
      }
    }

    .modal-title {
      font-size: 16px;
      font-weight: 700;
      color: #262b28;
      margin-bottom: 8px;
    }

    .modal-desc {
      font-size: 14px;
      color: #555e59;
      margin-bottom: 20px;
    }

    .modal-btn {
      width: 100%;
      height: 40px;
      background-color: #367250;
      color: #ffffff;
      border: none;
      border-radius: 8px;
      font-size: 14px;
      font-weight: 600;
      cursor: pointer;
    }

    .modal-btn:hover {
      background-color: #2d6043;
    }
  </style>
</head>
<body>
  <div class="container">
    <!-- 頂部卡片 -->
    <div class="header-card">
      <div class="icon-circle">
        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"></path>
          <polyline points="14 2 14 8 20 8"></polyline>
          <line x1="16" y1="13" x2="8" y2="13"></line>
          <line x1="16" y1="17" x2="8" y2="17"></line>
        </svg>
      </div>
      <h1>線上服務申請</h1>
      <p>填寫您的聯絡資料，我們將儘速與您聯繫，協助您完成訂單流程。</p>
    </div>

    <!-- 表單卡片 -->
    <div class="form-card">
      <form id="applyForm" novalidate>
        <div class="form-group">
          <label for="contactName">聯絡人 <span class="required">*</span></label>
          <div class="input-box">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"></path>
              <circle cx="12" cy="7" r="4"></circle>
            </svg>
            <input type="text" id="contactName" placeholder="請輸入聯絡人姓名" />
          </div>
        </div>

        <div class="form-group">
          <label for="contactPhone">聯絡電話 <span class="required">*</span></label>
          <div class="input-box">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72c.127.96.361 1.903.7 2.81a2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45c.907.339 1.85.573 2.81.7A2 2 0 0 1 22 16.92z"></path>
            </svg>
            <input type="tel" id="contactPhone" placeholder="請輸入聯絡電話" />
          </div>
        </div>

        <div class="privacy-box">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <rect x="3" y="11" width="18" height="11" rx="2" ry="2"></rect>
            <path d="M7 11V7a5 5 0 0 1 10 0v4"></path>
          </svg>
          <span>送出即表示同意提供以上資料供客服聯繫，我們承諾妥善保管您的個資。</span>
        </div>
<button type="submit" class="submit-btn" id="submitBtn">送出申請</button>

        <div class="trust-badges">
          <span>
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5">
              <polyline points="20 6 9 17 4 12"></polyline>
            </svg>
            SSL 加密
          </span>
          <span>
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5">
              <polyline points="20 6 9 17 4 12"></polyline>
            </svg>
            個資保護
          </span>
          <span>
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5">
              <polyline points="20 6 9 17 4 12"></polyline>
            </svg>
            快速回應
          </span>
        </div>
      </form>
    </div>

    <!-- 頁尾 -->
    <div class="footer">
      <div class="footer-links">
        <a href="#terms">服務條款</a>
        <a href="#privacy">隱私政策</a>
        <a href="#faq">常見問題</a>
        <a href="https://line.me/ti/p/您的LINE_ID" target="_blank" class="line-link">
          <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M21 11.5a8.38 8.38 0 0 1-.9 3.8 8.5 8.5 0 0 1-7.6 4.7 8.38 8.38 0 0 1-3.8-.9L3 21l1.9-5.7a8.38 8.38 0 0 1-.9-3.8 8.5 8.5 0 0 1 4.7-7.6 8.38 8.38 0 0 1 3.8-.9h.5a8.48 8.48 0 0 1 8 8v.5z"></path>
          </svg>
          LINE 客服
        </a>
      </div>
      <p>© 2026 All Rights Reserved.</p>
    </div>
  </div>

  <!-- 提示小視窗 -->
  <div class="modal-overlay" id="alertModal">
    <div class="modal-box">
      <div class="modal-title">提示</div>
      <div class="modal-desc">請先填入訊息</div>
      <button type="button" class="modal-btn" id="closeModalBtn">確定</button>
    </div>
  </div>

  <script>
    // 請將下方網址替換為您實際要跳轉的 LINE 連結
    const LINE_URL = "https://line.me/ti/p/您的LINE_ID";

    const form = document.getElementById("applyForm");
    const nameInput = document.getElementById("contactName");
    const phoneInput = document.getElementById("contactPhone");
    const alertModal = document.getElementById("alertModal");
    const closeModalBtn = document.getElementById("closeModalBtn");

    form.addEventListener("submit", function (e) {
      e.preventDefault();

      const nameVal = nameInput.value.trim();
      const phoneVal = phoneInput.value.trim();

      // 只要有任一欄位未填入，彈出提示小視窗
      if (!nameVal || !phoneVal) {
        alertModal.classList.add("show");
        return;
      }

      // 兩個欄位皆已填入，跳轉至 LINE
      window.location.href = LINE_URL;
    });

    // 關閉提示視窗並自動聚焦到未填寫的欄位
    closeModalBtn.addEventListener("click", function () {
      alertModal.classList.remove("show");
      if (!nameInput.value.trim()) {
        nameInput.focus();
      } else if (!phoneInput.value.trim()) {
        phoneInput.focus();
      }
    });

    // 點擊遮罩背景也能關閉提示視窗
    alertModal.addEventListener("click", function (e) {
      if (e.target === alertModal) {
        alertModal.classList.remove("show");
      }
    });
  </script>
</body>
</html>