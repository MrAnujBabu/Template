[[Template of code]] 
Here's a generalized template with all specific organization information removed. You can easily sell this to any educational institute, library, or coaching center:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>[Your Organization] - Student Registration</title>
  
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

  <style>
    :root {
      --primary: #6d28d9;
      --secondary: #f97316;
      --success: #22c55e;
      --warning: #f59e0b;
      --danger: #ef4444;
      --dark: #1e293b;
      --light: #f3f4f6;
      --white: #ffffff;
    }

    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Segoe UI', sans-serif;
    }

    body {
      background: linear-gradient(135deg, var(--primary), #5b21b6);
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 20px;
    }

    /* MAIN CONTAINER */
    .main-container {
      width: 100%;
      max-width: 480px;
      background: white;
      border-radius: 25px;
      overflow: hidden;
      box-shadow: 0 25px 50px rgba(0,0,0,0.3);
      padding: 0;
      animation: slideUp 0.5s ease;
    }

    @keyframes slideUp {
      from { transform: translateY(50px); opacity: 0; }
      to { transform: translateY(0); opacity: 1; }
    }

    /* HEADER */
    .header {
      background: linear-gradient(135deg, var(--primary), #5b21b6);
      color: white;
      padding: 25px 20px;
      text-align: center;
      position: relative;
      overflow: hidden;
    }

    .logo-icon {
      width: 80px;
      height: 80px;
      background: white;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      margin: 0 auto 15px;
      color: var(--primary);
      font-size: 40px;
      box-shadow: 0 10px 20px rgba(0,0,0,0.2);
      border: 3px solid rgba(255,255,255,0.3);
    }

    .title {
      font-size: 28px;
      font-weight: 900;
      margin-bottom: 8px;
      text-transform: uppercase;
      letter-spacing: 1px;
    }

    .subtitle {
      font-size: 16px;
      opacity: 0.9;
      font-weight: 500;
    }

    /* TABS */
    .tabs {
      display: flex;
      margin: 0;
      background: rgba(255,255,255,0.1);
      border-top: 1px solid rgba(255,255,255,0.2);
    }

    .tab {
      flex: 1;
      padding: 18px;
      text-align: center;
      background: transparent;
      border: none;
      color: rgba(255,255,255,0.8);
      font-weight: 700;
      font-size: 15px;
      cursor: pointer;
      transition: all 0.3s ease;
      border-bottom: 3px solid transparent;
    }

    .tab.active {
      color: white;
      background: rgba(255,255,255,0.15);
      border-bottom: 3px solid white;
    }

    /* FORM SECTION */
    .form-section {
      padding: 25px;
    }

    .form-group {
      margin-bottom: 20px;
    }

    .form-label {
      display: block;
      font-size: 14px;
      font-weight: 700;
      color: var(--dark);
      margin-bottom: 8px;
      text-transform: uppercase;
      letter-spacing: 0.5px;
    }

    .form-input {
      width: 100%;
      padding: 16px;
      border: 2px solid #e2e8f0;
      border-radius: 12px;
      font-size: 16px;
      background: var(--white);
      transition: all 0.3s ease;
    }

    .form-input:focus {
      outline: none;
      border-color: var(--primary);
      box-shadow: 0 0 0 4px rgba(109, 40, 217, 0.1);
    }

    .grid-2 {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 15px;
    }

    /* UPI PAYMENT SECTION */
    .upi-section {
      display: none;
      background: #f8fafc;
      border-radius: 15px;
      padding: 20px;
      margin-top: 20px;
      border: 2px solid #e2e8f0;
      text-align: center;
    }

    .upi-title {
      font-size: 18px;
      font-weight: 800;
      color: var(--dark);
      margin-bottom: 20px;
      text-align: center;
    }

    .qr-code-container {
      display: flex;
      flex-direction: column;
      align-items: center;
      margin-bottom: 20px;
    }

    .qr-code {
      width: 180px;
      height: 180px;
      border: 2px solid #ddd;
      border-radius: 10px;
      padding: 10px;
      background: white;
      margin-bottom: 15px;
      cursor: pointer;
      transition: transform 0.3s ease;
    }

    .qr-code:hover {
      transform: scale(1.05);
      border-color: var(--primary);
    }

    .qr-text {
      font-size: 12px;
      color: #64748b;
      margin-top: 5px;
    }

    .upi-id-container {
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 10px;
      margin-bottom: 20px;
      background: white;
      padding: 12px 20px;
      border-radius: 10px;
      border: 2px solid #e2e8f0;
    }

    .upi-id {
      font-size: 18px;
      font-weight: 700;
      color: var(--primary);
      cursor: pointer;
      padding: 8px 15px;
      border-radius: 8px;
      transition: all 0.3s ease;
    }

    .upi-id:hover {
      background-color: rgba(109, 40, 217, 0.1);
    }

    .copy-btn {
      background: linear-gradient(135deg, var(--primary), #5b21b6);
      color: white;
      border: none;
      padding: 10px 15px;
      border-radius: 8px;
      font-weight: 700;
      cursor: pointer;
      display: flex;
      align-items: center;
      gap: 8px;
      transition: all 0.3s ease;
    }

    .copy-btn:hover {
      transform: translateY(-2px);
      box-shadow: 0 5px 15px rgba(109, 40, 217, 0.3);
    }

    .upi-note {
      font-size: 13px;
      color: #64748b;
      text-align: center;
      margin-top: 15px;
      line-height: 1.5;
    }

    /* PAYMENT SCREENSHOT UPLOAD */
    .screenshot-section {
      display: none;
      background: #f0f9ff;
      border-radius: 15px;
      padding: 20px;
      margin-top: 20px;
      border: 2px dashed #0ea5e9;
      text-align: center;
    }

    .screenshot-title {
      font-size: 16px;
      font-weight: 700;
      color: #0369a1;
      margin-bottom: 15px;
    }

    .file-input-container {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 10px;
    }

    .file-input-label {
      display: flex;
      align-items: center;
      gap: 10px;
      padding: 12px 20px;
      background: linear-gradient(135deg, #0ea5e9, #0284c7);
      color: white;
      border-radius: 10px;
      cursor: pointer;
      font-weight: 600;
      transition: all 0.3s ease;
    }

    .file-input-label:hover {
      transform: translateY(-2px);
      box-shadow: 0 5px 15px rgba(14, 165, 233, 0.3);
    }

    .file-name {
      font-size: 14px;
      color: #64748b;
      margin-top: 5px;
    }

    /* BUTTONS */
    .btn {
      padding: 18px;
      border: none;
      border-radius: 15px;
      font-size: 18px;
      font-weight: 800;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 12px;
      transition: all 0.3s ease;
      width: 100%;
      text-transform: uppercase;
      letter-spacing: 1px;
      margin-top: 10px;
    }

    .btn-primary {
      background: linear-gradient(135deg, var(--primary), #5b21b6);
      color: white;
      box-shadow: 0 10px 25px rgba(109, 40, 217, 0.4);
    }

    .btn-primary:hover {
      transform: translateY(-3px);
      box-shadow: 0 15px 30px rgba(109, 40, 217, 0.5);
    }

    .btn-success {
      background: linear-gradient(135deg, var(--success), #16a34a);
      color: white;
      box-shadow: 0 10px 25px rgba(34, 197, 94, 0.4);
    }

    /* UPI SUCCESS SCREEN */
    .success-screen {
      display: none;
      padding: 0;
    }

    .upi-success-header {
      background: linear-gradient(135deg, #16a34a, #059669);
      color: white;
      padding: 30px 25px;
      text-align: center;
      position: relative;
      overflow: hidden;
    }

    .upi-check {
      width: 100px;
      height: 100px;
      background: white;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      margin: 0 auto 20px;
      color: #16a34a;
      font-size: 50px;
      animation: pulse 2s infinite;
      border: 5px solid rgba(255,255,255,0.3);
    }

    @keyframes pulse {
      0% { transform: scale(0.95); box-shadow: 0 0 0 0 rgba(255,255,255,0.7); }
      70% { transform: scale(1); box-shadow: 0 0 0 20px rgba(255,255,255,0); }
      100% { transform: scale(0.95); box-shadow: 0 0 0 0 rgba(255,255,255,0); }
    }

    .success-title {
      font-size: 28px;
      font-weight: 900;
      margin-bottom: 10px;
      text-transform: uppercase;
      letter-spacing: 1px;
    }

    .success-subtitle {
      font-size: 18px;
      opacity: 0.9;
    }

    /* SUCCESS CONTENT */
    .success-content {
      padding: 25px;
    }

    .tagline-box {
      text-align: center;
      background: linear-gradient(135deg, #fef3c7, #fde68a);
      padding: 15px;
      border-radius: 12px;
      margin-bottom: 20px;
      border: 2px solid #f59e0b;
    }

    .tagline {
      font-size: 22px;
      font-weight: 900;
      color: #92400e;
      font-style: italic;
    }

    .greeting-box {
      text-align: center;
      margin-bottom: 25px;
    }

    .greeting {
      font-size: 18px;
      color: var(--dark);
      margin-bottom: 5px;
      font-weight: 600;
    }

    .greeting-sub {
      color: #64748b;
    }

    /* SEAT MESSAGE */
    .seat-message {
      background: linear-gradient(135deg, #dbeafe, #bfdbfe);
      padding: 20px;
      border-radius: 15px;
      text-align: center;
      margin-bottom: 25px;
      border: 2px solid #3b82f6;
    }

    .seat-icon {
      font-size: 40px;
      color: #1d4ed8;
      margin-bottom: 10px;
    }

    .seat-text {
      font-size: 20px;
      font-weight: 700;
      color: #1e40af;
    }

    /* ENHANCED PROMO CARDS */
    .promo-link {
      text-decoration: none;
      display: block;
      margin-bottom: 20px;
    }

    .promo-card {
      background: white;
      border-radius: 20px;
      padding: 0;
      overflow: hidden;
      box-shadow: 0 15px 30px rgba(0,0,0,0.1);
      border: 2px solid #e2e8f0;
      transition: all 0.4s ease;
      position: relative;
    }

    .promo-card:hover {
      transform: translateY(-8px);
      box-shadow: 0 20px 40px rgba(0,0,0,0.15);
      border-color: var(--primary);
    }

    .promo-header {
      display: flex;
      align-items: center;
      padding: 25px 20px;
      background: linear-gradient(135deg, var(--primary), #5b21b6);
      color: white;
      gap: 15px;
    }

    .promo-icon {
      width: 60px;
      height: 60px;
      background: rgba(255,255,255,0.2);
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      color: white;
      font-size: 28px;
      border: 2px solid rgba(255,255,255,0.3);
    }

    .promo-title {
      font-size: 20px;
      font-weight: 800;
      flex: 1;
    }

    .promo-arrow {
      font-size: 20px;
      opacity: 0.8;
    }

    .promo-content {
      padding: 20px;
    }

    .promo-text {
      color: #64748b;
      margin-bottom: 20px;
      line-height: 1.6;
      font-size: 15px;
    }

    .promo-btn {
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 10px;
      width: 100%;
      padding: 16px;
      background: linear-gradient(135deg, #10b981, #047857);
      color: white;
      border: none;
      border-radius: 12px;
      font-weight: 700;
      text-align: center;
      text-decoration: none;
      font-size: 16px;
      transition: all 0.3s ease;
    }

    .promo-btn:hover {
      transform: translateY(-3px);
      box-shadow: 0 10px 20px rgba(16, 185, 129, 0.3);
    }

    .map-card .promo-header {
      background: linear-gradient(135deg, #f59e0b, #d97706);
    }

    .map-card .promo-btn {
      background: linear-gradient(135deg, #f59e0b, #d97706);
    }

    /* FEEDBACK SECTION */
    .feedback-section {
      background: #f8fafc;
      padding: 25px 20px;
      border-radius: 15px;
      text-align: center;
      margin: 25px 0;
      border: 2px dashed #94a3b8;
      cursor: pointer;
      transition: all 0.3s ease;
    }

    .feedback-section:hover {
      background: #f1f5f9;
      border-color: var(--primary);
      transform: translateY(-3px);
    }

    .feedback-title {
      font-size: 20px;
      font-weight: 800;
      color: var(--primary);
      margin-bottom: 10px;
    }

    .feedback-text {
      color: #64748b;
      font-size: 15px;
      margin-bottom: 5px;
    }

    .call-button {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      margin-top: 15px;
      padding: 12px 25px;
      background: linear-gradient(135deg, var(--primary), #5b21b6);
      color: white;
      border: none;
      border-radius: 10px;
      font-weight: 700;
      cursor: pointer;
      transition: all 0.3s ease;
    }

    .call-button:hover {
      transform: translateY(-3px);
      box-shadow: 0 10px 20px rgba(109, 40, 217, 0.3);
    }

    /* ACTION BUTTONS */
    .action-buttons {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 15px;
      margin: 25px 0;
    }

    .action-btn {
      padding: 18px;
      border: none;
      border-radius: 12px;
      font-size: 16px;
      font-weight: 700;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 10px;
      transition: all 0.3s ease;
    }

    .download-btn {
      background: linear-gradient(135deg, #16a34a, #059669);
      color: white;
    }

    .whatsapp-btn {
      background: linear-gradient(135deg, #25D366, #128C7E);
      color: white;
    }

    /* LOADING */
    .loading {
      text-align: center;
      padding: 50px 20px;
      display: none;
    }

    .loader {
      border: 5px solid #f3f3f3;
      border-top: 5px solid var(--primary);
      border-radius: 50%;
      width: 60px;
      height: 60px;
      animation: spin 1s linear infinite;
      margin: 0 auto 20px;
    }

    @keyframes spin {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }

    /* DATE INPUT STYLING */
    .date-input-group {
      display: flex;
      gap: 10px;
    }

    .date-input {
      flex: 1;
      text-align: center;
      padding: 16px 10px;
    }

    .date-separator {
      display: flex;
      align-items: center;
      font-weight: bold;
      color: var(--primary);
    }

    /* RESPONSIVE */
    @media (max-width: 480px) {
      .grid-2 {
        grid-template-columns: 1fr;
      }
      
      .action-buttons {
        grid-template-columns: 1fr;
      }
      
      .title {
        font-size: 24px;
      }
      
      .success-title {
        font-size: 24px;
      }
      
      .upi-check {
        width: 80px;
        height: 80px;
        font-size: 40px;
      }
      
      .promo-header {
        padding: 20px 15px;
      }
      
      .promo-icon {
        width: 50px;
        height: 50px;
        font-size: 24px;
      }
      
      .promo-title {
        font-size: 18px;
      }
    }
  </style>
</head>
<body>

<!-- MAIN CONTAINER -->
<div class="main-container">
  
  <!-- HEADER -->
  <div class="header">
    <div class="logo-icon">
      <i class="fas fa-book"></i>
    </div>
    <h1 class="title">[Your Organization Name]</h1>
    <div class="subtitle">[Your Organization Address]</div>
  </div>

  <!-- TABS -->
  <div class="tabs">
    <button class="tab active" onclick="switchTab('formTab')">
      <i class="fas fa-user-plus"></i> New Registration
    </button>
    <button class="tab" onclick="switchTab('downloadTab')">
      <i class="fas fa-download"></i> Download Receipt
    </button>
  </div>

  <!-- FORM TAB -->
  <div id="formTab" class="tab-content">
    <div class="form-section">
      <form id="registrationForm">
        <!-- Student Name -->
        <div class="form-group">
          <label class="form-label">Student Name</label>
          <input type="text" class="form-input" id="studentName" placeholder="Enter your full name" required>
        </div>

        <!-- Mobile & PIN -->
        <div class="grid-2">
          <div class="form-group">
            <label class="form-label">Mobile Number</label>
            <input type="tel" class="form-input" id="mobile" maxlength="10" placeholder="10-digit mobile" required>
          </div>
          <div class="form-group">
            <label class="form-label">Secret PIN</label>
            <input type="password" class="form-input" id="secretPin" maxlength="4" placeholder="4-digit PIN" required>
          </div>
        </div>

        <!-- Start Date & End Date (dd/mm/yyyy format) -->
        <div class="grid-2">
          <div class="form-group">
            <label class="form-label">Start Date (dd/mm/yyyy)</label>
            <div class="date-input-group">
              <input type="number" class="form-input date-input" id="startDay" placeholder="DD" min="1" max="31" required>
              <div class="date-separator">/</div>
              <input type="number" class="form-input date-input" id="startMonth" placeholder="MM" min="1" max="12" required>
              <div class="date-separator">/</div>
              <input type="number" class="form-input date-input" id="startYear" placeholder="YYYY" min="2024" max="2030" required>
            </div>
          </div>
          <div class="form-group">
            <label class="form-label">End Date (dd/mm/yyyy)</label>
            <div class="date-input-group">
              <input type="number" class="form-input date-input" id="endDay" placeholder="DD" min="1" max="31" required>
              <div class="date-separator">/</div>
              <input type="number" class="form-input date-input" id="endMonth" placeholder="MM" min="1" max="12" required>
              <div class="date-separator">/</div>
              <input type="number" class="form-input date-input" id="endYear" placeholder="YYYY" min="2024" max="2030" required>
            </div>
          </div>
        </div>

        <!-- Select Month -->
        <div class="form-group">
          <label class="form-label">Select Month</label>
          <select class="form-input" id="month" required>
            <option value="">-- Select Month --</option>
            <option value="January">January</option>
            <option value="February">February</option>
            <option value="March">March</option>
            <option value="April">April</option>
            <option value="May">May</option>
            <option value="June">June</option>
            <option value="July">July</option>
            <option value="August">August</option>
            <option value="September">September</option>
            <option value="October">October</option>
            <option value="November">November</option>
            <option value="December">December</option>
          </select>
        </div>

        <!-- Address -->
        <div class="form-group">
          <label class="form-label">Address</label>
          <textarea class="form-input" id="address" placeholder="Complete address with landmark" rows="3"></textarea>
        </div>

        <!-- Shift & Seat -->
        <div class="grid-2">
          <div class="form-group">
            <label class="form-label">Select Shift</label>
            <select class="form-input" id="shift" required>
              <option value="Full Day">Full Day</option>
              <option value="Morning Shift">Morning Shift</option>
              <option value="Afternoon Shift">Afternoon Shift</option>
              <option value="Evening Shift">Evening Shift</option>
              <option value="Night Shift">Night Shift</option>
            </select>
          </div>
          <div class="form-group">
            <label class="form-label">Seat/Roll Number</label>
            <input type="text" class="form-input" id="seatNo" placeholder="e.g., A-12">
          </div>
        </div>

        <!-- Amount & Due -->
        <div class="grid-2">
          <div class="form-group">
            <label class="form-label">Amount Paid (₹)</label>
            <input type="number" class="form-input" id="amount" placeholder="Enter amount" required>
          </div>
          <div class="form-group">
            <label class="form-label">Due Amount (₹)</label>
            <input type="number" class="form-input" id="dueAmount" placeholder="Due amount (if any)" value="0">
          </div>
        </div>

        <!-- Payment Mode -->
        <div class="form-group">
          <label class="form-label">Payment Mode</label>
          <select class="form-input" id="paymentMode" onchange="togglePaymentSection()">
            <option value="Cash">Cash</option>
            <option value="UPI">UPI</option>
            <option value="Bank Transfer">Bank Transfer</option>
          </select>
        </div>

        <!-- UPI Payment Section -->
        <div id="upiSection" class="upi-section">
          <div class="upi-title">Scan QR Code or Tap UPI ID for Payment</div>
          
          <div class="qr-code-container">
            <!-- QR Code Image - Replace with your QR code -->
            <img src="[YOUR_QR_CODE_IMAGE_URL]" 
                 alt="UPI QR Code" 
                 class="qr-code"
                 onclick="redirectToUPIApp()">
            <div class="qr-text">Click on QR to pay directly</div>
          </div>
          
          <div class="upi-id-container">
            <div class="upi-id" onclick="redirectToUPIApp()">
              [YOUR_UPI_ID@bank]
            </div>
            <button class="copy-btn" onclick="copyUPIID()">
              <i class="fas fa-copy"></i> Copy
            </button>
          </div>
          
          <div class="upi-note">
            <i class="fas fa-info-circle"></i> Click on UPI ID or QR Code to open your payment app
          </div>

          <!-- Payment Screenshot Upload -->
          <div id="screenshotSection" class="screenshot-section">
            <div class="screenshot-title">
              <i class="fas fa-camera"></i> Upload Payment Screenshot
            </div>
            <div class="file-input-container">
              <label for="paymentScreenshot" class="file-input-label">
                <i class="fas fa-cloud-upload-alt"></i> Choose Screenshot File
              </label>
              <input type="file" id="paymentScreenshot" accept="image/*" style="display: none;" onchange="showFileName()">
              <div id="fileName" class="file-name">No file chosen</div>
            </div>
          </div>
        </div>

        <!-- Submit Button -->
        <button type="button" class="btn btn-primary" onclick="submitRegistration()">
          <i class="fas fa-paper-plane"></i> Send to Admin Approval
        </button>
      </form>
    </div>
  </div>

  <!-- DOWNLOAD TAB -->
  <div id="downloadTab" class="tab-content" style="display: none;">
    <div class="form-section">
      <div class="form-group">
        <label class="form-label">Mobile Number</label>
        <input type="tel" class="form-input" id="downloadMobile" maxlength="10" placeholder="Enter registered mobile">
      </div>

      <div class="form-group">
        <label class="form-label">Secret PIN</label>
        <input type="password" class="form-input" id="downloadPin" maxlength="4" placeholder="4-digit PIN">
      </div>

      <button class="btn btn-success" onclick="checkStatus()">
        <i class="fas fa-search"></i> Check Status & Download
      </button>

      <div id="statusResult" style="margin-top: 25px;"></div>
    </div>
  </div>

  <!-- LOADING SCREEN -->
  <div id="loadingScreen" class="loading">
    <div class="loader"></div>
    <h3 style="color: var(--primary); margin-top: 20px;">Processing Request...</h3>
    <p style="color: #64748b;">Sending to Admin for Approval</p>
  </div>

  <!-- SUCCESS SCREEN -->
  <div id="successScreen" class="success-screen">
    
    <!-- UPI Success Header -->
    <div class="upi-success-header">
      <div class="upi-check">
        <i class="fas fa-check"></i>
      </div>
      <h2 class="success-title">Payment Successful</h2>
      <div class="success-subtitle">Registration Confirmed Successfully</div>
    </div>

    <!-- Success Content -->
    <div class="success-content">
      
      <!-- Tagline -->
      <div class="tagline-box">
        <div class="tagline">"[YOUR_TAGLINE]"</div>
      </div>

      <!-- Greeting -->
      <div class="greeting-box">
        <div class="greeting">Thank you for Joining Us</div>
        <div class="greeting-sub">Have a Nice Day!</div>
      </div>

      <!-- Seat Message -->
      <div class="seat-message">
        <div class="seat-icon">
          <i class="fas fa-chair"></i>
        </div>
        <div class="seat-text" id="seatMessageText">Seat/Roll No. -- Confirmed Successfully</div>
      </div>

      <!-- Google Docs Card -->
      <a href="[YOUR_GOOGLE_FORM_LINK]" target="_blank" class="promo-link">
        <div class="promo-card">
          <div class="promo-header">
            <div class="promo-icon">
              <i class="fas fa-calendar-check"></i>
            </div>
            <div class="promo-title">[YOUR_PROMO_TITLE_1]</div>
            <div class="promo-arrow">
              <i class="fas fa-arrow-right"></i>
            </div>
          </div>
          <div class="promo-content">
            <div class="promo-text">
              [YOUR_PROMO_DESCRIPTION_1]
            </div>
            <button class="promo-btn">
              <i class="fas fa-external-link-alt"></i> [YOUR_BUTTON_TEXT_1]
            </button>
          </div>
        </div>
      </a>

      <!-- Map Card -->
      <a href="[YOUR_GOOGLE_MAPS_LINK]" target="_blank" class="promo-link">
        <div class="promo-card map-card">
          <div class="promo-header">
            <div class="promo-icon">
              <i class="fas fa-map-marker-alt"></i>
            </div>
            <div class="promo-title">Find Our Location</div>
            <div class="promo-arrow">
              <i class="fas fa-arrow-right"></i>
            </div>
          </div>
          <div class="promo-content">
            <div class="promo-text">
              <strong>Address:</strong><br>
              [YOUR_ORGANIZATION_ADDRESS]<br>
              <strong>Landmark:</strong><br>
              [YOUR_LANDMARK_1]<br>
              [YOUR_LANDMARK_2]<br>
              [YOUR_LANDMARK_3]
            </div>
            <button class="promo-btn">
              <i class="fas fa-map-pin"></i> Open in Google Maps
            </button>
          </div>
        </div>
      </a>

      <!-- Feedback Section -->
      <div class="feedback-section" onclick="callSupport()">
        <div class="feedback-title">Need Any Help?</div>
        <p class="feedback-text">For Feedback / Issues / Complaints</p>
        <p class="feedback-text">Call us anytime between [START_TIME] to [END_TIME]</p>
        <button class="call-button">
          <i class="fas fa-phone"></i> Call for Help
        </button>
      </div>

      <!-- Action Buttons -->
      <div class="action-buttons">
        <button class="action-btn download-btn" onclick="downloadProvisionalReceipt()">
          <i class="fas fa-download"></i> Download Provisional Receipt
        </button>
        <button class="action-btn whatsapp-btn" onclick="shareOnWhatsApp()">
          <i class="fab fa-whatsapp"></i> Share on WhatsApp
        </button>
      </div>

      <!-- Back Button -->
      <button class="btn" onclick="goBackToForm()" style="background: #64748b; color: white;">
        <i class="fas fa-arrow-left"></i> Back to Registration
      </button>
    </div>
  </div>
</div>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
  import { 
    getFirestore, 
    collection, 
    addDoc, 
    query, 
    where, 
    getDocs, 
    orderBy,
    limit
  } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

  // ==================== FIREBASE CONFIGURATION ====================
  // Replace with your Firebase configuration
  const firebaseConfig = {
    apiKey: "[YOUR_API_KEY]",
    authDomain: "[YOUR_AUTH_DOMAIN]",
    projectId: "[YOUR_PROJECT_ID]",
    storageBucket: "[YOUR_STORAGE_BUCKET]",
    messagingSenderId: "[YOUR_MESSAGING_SENDER_ID]",
    appId: "[YOUR_APP_ID]",
    measurementId: "[YOUR_MEASUREMENT_ID]"
  };

  // Initialize Firebase
  const app = initializeApp(firebaseConfig);
  const db = getFirestore(app);

  let currentReceiptData = null;
  let paymentScreenshotFile = null;

  // ==================== UI FUNCTIONS ====================

  // Switch tabs
  window.switchTab = function(tabId) {
    // Hide all tabs
    document.querySelectorAll('.tab-content').forEach(tab => {
      tab.style.display = 'none';
    });
    
    // Show selected tab
    document.getElementById(tabId).style.display = 'block';
    
    // Update tab buttons
    document.querySelectorAll('.tab').forEach(tab => {
      tab.classList.remove('active');
    });
    event.target.classList.add('active');
  };

  // Toggle Payment Section based on payment mode
  window.togglePaymentSection = function() {
    const paymentMode = document.getElementById('paymentMode').value;
    const upiSection = document.getElementById('upiSection');
    const screenshotSection = document.getElementById('screenshotSection');
    
    if (paymentMode === 'UPI') {
      upiSection.style.display = 'block';
      screenshotSection.style.display = 'block';
    } else {
      upiSection.style.display = 'none';
    }
  };

  // Show file name when selected
  window.showFileName = function() {
    const fileInput = document.getElementById('paymentScreenshot');
    const fileNameDiv = document.getElementById('fileName');
    
    if (fileInput.files.length > 0) {
      paymentScreenshotFile = fileInput.files[0];
      fileNameDiv.textContent = paymentScreenshotFile.name;
      fileNameDiv.style.color = '#22c55e';
      fileNameDiv.innerHTML = `<i class="fas fa-check-circle"></i> ${paymentScreenshotFile.name}`;
    } else {
      paymentScreenshotFile = null;
      fileNameDiv.textContent = 'No file chosen';
      fileNameDiv.style.color = '#64748b';
    }
  };

  // Redirect to UPI App
  window.redirectToUPIApp = function() {
    // Replace with your UPI ID
    const upiId = '[YOUR_UPI_ID]';
    const amount = document.getElementById('amount').value || '1000';
    const studentName = document.getElementById('studentName').value || 'Student';
    
    // Create UPI payment URL
    const upiUrl = `upi://pay?pa=${upiId}&pn=[YOUR_ORGANIZATION_NAME]&am=${amount}&tn=Fee%20for%20${encodeURIComponent(studentName)}&cu=INR`;
    
    // Try to open UPI app
    window.location.href = upiUrl;
    
    // Fallback - show alert if UPI app not installed
    setTimeout(() => {
      alert('If payment app did not open, please copy UPI ID and make payment manually: ' + upiId);
    }, 1000);
  };

  // Copy UPI ID to clipboard
  window.copyUPIID = function() {
    // Replace with your UPI ID
    const upiId = '[YOUR_UPI_ID]';
    
    // Copy to clipboard
    navigator.clipboard.writeText(upiId)
      .then(() => {
        // Show success message
        const copyBtn = document.querySelector('.copy-btn');
        const originalText = copyBtn.innerHTML;
        
        copyBtn.innerHTML = '<i class="fas fa-check"></i> Copied!';
        copyBtn.style.background = 'linear-gradient(135deg, #22c55e, #16a34a)';
        
        setTimeout(() => {
          copyBtn.innerHTML = originalText;
          copyBtn.style.background = 'linear-gradient(135deg, var(--primary), #5b21b6)';
        }, 2000);
      })
      .catch(err => {
        console.error('Failed to copy UPI ID: ', err);
        alert('Failed to copy UPI ID. Please copy manually: ' + upiId);
      });
  };

  // Call support function
  window.callSupport = function() {
    // Replace with your phone number
    const phoneNumber = '[YOUR_PHONE_NUMBER]';
    window.location.href = `tel:${phoneNumber}`;
  };

  // Go back to form
  window.goBackToForm = function() {
    document.getElementById('successScreen').style.display = 'none';
    document.getElementById('formTab').style.display = 'block';
    document.querySelectorAll('.tab')[0].classList.add('active');
    document.querySelectorAll('.tab')[1].classList.remove('active');
  };

  // ==================== DATE FORMATTING FUNCTIONS ====================

  // Format date to dd/mm/yyyy
  function formatDateToDDMMYYYY(dateString) {
    if (!dateString) return '';
    
    // If date is in yyyy-mm-dd format
    if (dateString.includes('-')) {
      const parts = dateString.split('-');
      if (parts.length === 3) {
        return `${parts[2]}/${parts[1]}/${parts[0]}`;
      }
    }
    
    // If date is in dd/mm/yyyy format already
    if (dateString.includes('/')) {
      const parts = dateString.split('/');
      if (parts.length === 3) {
        // Ensure proper formatting
        const day = parts[0].padStart(2, '0');
        const month = parts[1].padStart(2, '0');
        const year = parts[2];
        return `${day}/${month}/${year}`;
      }
    }
    
    return dateString;
  }

  // Parse dd/mm/yyyy to Date object
  function parseDDMMYYYY(dateStr) {
    const parts = dateStr.split('/');
    if (parts.length === 3) {
      return new Date(parts[2], parts[1] - 1, parts[0]);
    }
    return new Date();
  }

  // ==================== SUBMIT REGISTRATION ====================

  window.submitRegistration = async function() {
    const name = document.getElementById('studentName').value.trim();
    const mobile = document.getElementById('mobile').value.trim();
    const pin = document.getElementById('secretPin').value.trim();
    const amount = document.getElementById('amount').value;
    
    // Get date values in dd/mm/yyyy format
    const startDay = document.getElementById('startDay').value;
    const startMonth = document.getElementById('startMonth').value;
    const startYear = document.getElementById('startYear').value;
    const startDate = `${startDay.padStart(2, '0')}/${startMonth.padStart(2, '0')}/${startYear}`;
    
    const endDay = document.getElementById('endDay').value;
    const endMonth = document.getElementById('endMonth').value;
    const endYear = document.getElementById('endYear').value;
    const endDate = `${endDay.padStart(2, '0')}/${endMonth.padStart(2, '0')}/${endYear}`;
    
    const month = document.getElementById('month').value;
    const dueAmount = document.getElementById('dueAmount').value;
    const seatNo = document.getElementById('seatNo').value.trim();
    const paymentMode = document.getElementById('paymentMode').value;

    // Validation
    if (!name || !mobile || !pin || !amount || !startDay || !startMonth || !startYear || !endDay || !endMonth || !endYear || !month) {
      alert('Please fill all required information!');
      return;
    }
    
    if (mobile.length !== 10) {
      alert('Please enter correct 10-digit mobile number!');
      return;
    }
    
    if (pin.length !== 4) {
      alert('Secret PIN must be 4 digits!');
      return;
    }

    // Validate dates
    const startDateObj = parseDDMMYYYY(startDate);
    const endDateObj = parseDDMMYYYY(endDate);
    
    if (startDateObj > endDateObj) {
      alert('End date should be after start date!');
      return;
    }

    // For UPI payment, check if screenshot is uploaded
    if (paymentMode === 'UPI' && !paymentScreenshotFile) {
      const proceed = confirm('UPI payment selected but no screenshot uploaded. Do you want to proceed without screenshot?');
      if (!proceed) {
        return;
      }
    }

    // Show loading
    document.getElementById('formTab').style.display = 'none';
    document.getElementById('loadingScreen').style.display = 'block';

    // Generate receipt number
    const now = new Date();
    const receiptNo = `REC-${now.getFullYear()}${(now.getMonth()+1).toString().padStart(2,'0')}${now.getDate().toString().padStart(2,'0')}-${now.getHours().toString().padStart(2,'0')}${now.getMinutes().toString().padStart(2,'0')}`;

    // Prepare data
    const registrationData = {
      studentName: name,
      mobile: mobile,
      secretPin: pin,
      address: document.getElementById('address').value.trim() || '-',
      startDate: startDate, // Stored as dd/mm/yyyy
      endDate: endDate, // Stored as dd/mm/yyyy
      month: month,
      shift: document.getElementById('shift').value,
      seatNo: seatNo || 'Unassigned',
      amount: parseFloat(amount),
      dueAmount: parseFloat(dueAmount) || 0,
      paymentMode: paymentMode,
      status: 'Pending',
      receiptNo: receiptNo,
      date: now.toLocaleDateString('en-IN'),
      time: now.toLocaleTimeString('en-IN'),
      timestamp: now.getTime(),
      organizationAddress: '[YOUR_ORGANIZATION_ADDRESS]',
      upiId: paymentMode === 'UPI' ? '[YOUR_UPI_ID]' : null
    };

    try {
      // Save to Firebase
      const docRef = await addDoc(collection(db, 'registrations'), registrationData);
      registrationData.id = docRef.id;
      currentReceiptData = registrationData;

      // Update seat message
      document.getElementById('seatMessageText').textContent = 
        `Seat/Roll No. ${seatNo || '--'} Confirmed Successfully`;

      // Simulate processing delay
      setTimeout(() => {
        // Hide loading
        document.getElementById('loadingScreen').style.display = 'none';
        
        // Show success screen
        document.getElementById('successScreen').style.display = 'block';
        
        // Fire confetti celebration
        fireConfetti();
        
        // Play success sound (if available)
        playSuccessSound();
        
      }, 3000);

    } catch (error) {
      console.error('Error:', error);
      alert('Registration failed! Please try again.');
      document.getElementById('loadingScreen').style.display = 'none';
      document.getElementById('formTab').style.display = 'block';
    }
  };

  // ==================== CHECK STATUS ====================

  window.checkStatus = async function() {
    const mobile = document.getElementById('downloadMobile').value.trim();
    const pin = document.getElementById('downloadPin').value.trim();

    if (!mobile || !pin) {
      alert('Please enter mobile number and PIN!');
      return;
    }

    const resultDiv = document.getElementById('statusResult');
    resultDiv.innerHTML = '<div class="loader" style="width: 40px; height: 40px;"></div><p>Checking status...</p>';

    try {
      const q = query(collection(db, 'registrations'), 
        where('mobile', '==', mobile),
        where('secretPin', '==', pin),
        orderBy('timestamp', 'desc'),
        limit(1));

      const querySnapshot = await getDocs(q);

      if (querySnapshot.empty) {
        resultDiv.innerHTML = `
          <div style="background: #fee2e2; color: #991b1b; padding: 15px; border-radius: 10px; border: 2px solid #ef4444;">
            <strong>❌ No record found!</strong><br>
            Please check your mobile number and PIN.
          </div>
        `;
        return;
      }

      querySnapshot.forEach(doc => {
        currentReceiptData = { id: doc.id, ...doc.data() };
        
        if (currentReceiptData.status === 'Pending') {
          resultDiv.innerHTML = `
            <div style="background: #fef3c7; color: #92400e; padding: 15px; border-radius: 10px; border: 2px solid #f59e0b;">
              <strong>⏳ Pending Approval</strong><br>
              Your receipt is waiting for admin approval.<br>
              Receipt No: ${currentReceiptData.receiptNo}<br>
              Date: ${formatDateToDDMMYYYY(currentReceiptData.startDate)} to ${formatDateToDDMMYYYY(currentReceiptData.endDate)}
            </div>
            <button class="btn btn-primary" onclick="downloadProvisionalReceipt()" style="margin-top: 15px;">
              <i class="fas fa-download"></i> Download Provisional Receipt
            </button>
          `;
        } 
        else if (currentReceiptData.status === 'Approved') {
          resultDiv.innerHTML = `
            <div style="background: #dcfce7; color: #166534; padding: 15px; border-radius: 10px; border: 2px solid #22c55e;">
              <strong>✅ Approved!</strong><br>
              Your receipt has been approved by admin.<br>
              Receipt No: ${currentReceiptData.receiptNo}<br>
              Date: ${formatDateToDDMMYYYY(currentReceiptData.startDate)} to ${formatDateToDDMMYYYY(currentReceiptData.endDate)}<br>
              Approved on: ${currentReceiptData.approvedDate || 'N/A'}
            </div>
            <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-top: 15px;">
              <button class="btn btn-success" onclick="downloadProvisionalReceipt()">
                <i class="fas fa-download"></i> Provisional
              </button>
              <button class="btn btn-primary" onclick="downloadVerifiedReceipt()">
                <i class="fas fa-check-circle"></i> Verified
              </button>
            </div>
          `;
        }
        else if (currentReceiptData.status === 'Rejected') {
          resultDiv.innerHTML = `
            <div style="background: #fee2e2; color: #991b1b; padding: 15px; border-radius: 10px; border: 2px solid #ef4444;">
              <strong>❌ Request Rejected!</strong><br>
              Please contact admin for more information.
            </div>
          `;
        }
      });

    } catch (error) {
      console.error('Error:', error);
      resultDiv.innerHTML = `
        <div style="background: #fee2e2; color: #991b1b; padding: 15px; border-radius: 10px; border: 2px solid #ef4444;">
          Error checking status. Please try again.
        </div>
      `;
    }
  };

  // ==================== PDF GENERATION ====================

  window.downloadProvisionalReceipt = function() {
    if (!currentReceiptData) {
      alert('No receipt data found! Please submit the form first.');
      return;
    }

    const { jsPDF } = window.jspdf;
    const doc = new jsPDF({
      unit: 'mm',
      format: 'a4',
      orientation: 'portrait'
    });

    const pageWidth = doc.internal.pageSize.getWidth();
    const pageHeight = doc.internal.pageSize.getHeight();
    const margin = 15;
    let y = margin;

    // Set better font
    doc.setFont('helvetica', 'normal');

    // Header with background
    doc.setFillColor(109, 40, 217);
    doc.rect(0, 0, pageWidth, 25, 'F');
    
    // Organization name
    doc.setTextColor(255, 255, 255);
    doc.setFontSize(18);
    doc.setFont('helvetica', 'bold');
    doc.text('[YOUR_ORGANIZATION_NAME]', pageWidth/2, 12, { align: 'center' });
    
    // Organization address
    doc.setFontSize(10);
    doc.setFont('helvetica', 'normal');
    doc.text('[YOUR_ORGANIZATION_ADDRESS]', pageWidth/2, 18, { align: 'center' });
    doc.text('Contact: [YOUR_PHONE_NUMBER] | Email: [YOUR_EMAIL]', pageWidth/2, 22, { align: 'center' });

    y = 35;
    
    // Provisional Receipt Title
    doc.setTextColor(245, 158, 11);
    doc.setFontSize(16);
    doc.setFont('helvetica', 'bold');
    doc.text('PROVISIONAL RECEIPT', pageWidth/2, y, { align: 'center' });
    
    y += 10;

    // Receipt Details Table
    doc.setDrawColor(200, 200, 200);
    doc.setLineWidth(0.2);
    
    const cellHeight = 7;
    const labelWidth = 45;
    const valueWidth = pageWidth - 2*margin - labelWidth;
    
    const details = [
      { label: 'Receipt No:', value: currentReceiptData.receiptNo },
      { label: 'Date:', value: formatDateToDDMMYYYY(currentReceiptData.date) },
      { label: 'Student Name:', value: currentReceiptData.studentName },
      { label: 'Mobile No:', value: currentReceiptData.mobile },
      { label: 'Address:', value: currentReceiptData.address || '-' },
      { label: 'Start Date:', value: formatDateToDDMMYYYY(currentReceiptData.startDate) },
      { label: 'End Date:', value: formatDateToDDMMYYYY(currentReceiptData.endDate) },
      { label: 'Month:', value: currentReceiptData.month },
      { label: 'Shift:', value: currentReceiptData.shift },
      { label: 'Seat No:', value: currentReceiptData.seatNo },
      { label: 'Payment Mode:', value: currentReceiptData.paymentMode },
      { label: 'Amount Paid (₹):', value: currentReceiptData.amount },
      { label: 'Due Amount (₹):', value: currentReceiptData.dueAmount || 0 },
      { label: 'Total Amount (₹):', value: (parseFloat(currentReceiptData.amount) + parseFloat(currentReceiptData.dueAmount || 0)).toFixed(2) },
      { label: 'Status:', value: currentReceiptData.status }
    ];

    // Draw table rows
    details.forEach((row, index) => {
      const cellY = y + (index * cellHeight);
      
      // Draw cell borders
      doc.rect(margin, cellY, labelWidth, cellHeight, 'S');
      doc.rect(margin + labelWidth, cellY, valueWidth, cellHeight, 'S');
      
      // Add label
      doc.setFontSize(9);
      doc.setFont('helvetica', 'bold');
      doc.setTextColor(0, 0, 0);
      doc.text(row.label, margin + 2, cellY + 5);
      
      // Add value
      doc.setFont('helvetica', 'normal');
      doc.setTextColor(50, 50, 50);
      const valueText = String(row.value);
      // Ensure value fits in cell
      const maxWidth = valueWidth - 4;
      if (doc.getTextWidth(valueText) > maxWidth) {
        // Truncate text if too long
        let truncated = valueText;
        while (doc.getTextWidth(truncated + '...') > maxWidth && truncated.length > 10) {
          truncated = truncated.substring(0, truncated.length - 1);
        }
        doc.text(truncated + '...', margin + labelWidth + 2, cellY + 5);
      } else {
        doc.text(valueText, margin + labelWidth + 2, cellY + 5);
      }
    });

    y += (details.length * cellHeight) + 10;

    // Payment Summary
    doc.setFillColor(254, 252, 232);
    doc.roundedRect(margin, y, pageWidth - 2*margin, 15, 3, 3, 'F');
    
    doc.setFontSize(14);
    doc.setFont('helvetica', 'bold');
    doc.setTextColor(245, 158, 11);
    doc.text(`Total Amount: ₹ ${(parseFloat(currentReceiptData.amount) + parseFloat(currentReceiptData.dueAmount || 0)).toFixed(2)}`, pageWidth/2, y + 9, { align: 'center' });
    
    doc.setFontSize(10);
    doc.text(`Paid: ₹ ${currentReceiptData.amount} | Due: ₹ ${currentReceiptData.dueAmount || 0}`, pageWidth/2, y + 13, { align: 'center' });

    y += 25;

    // Important Links
    doc.setDrawColor(109, 40, 217);
    doc.setLineWidth(0.5);
    doc.rect(margin, y, pageWidth - 2*margin, 35, 'S');
    
    doc.setFontSize(11);
    doc.setFont('helvetica', 'bold');
    doc.setTextColor(109, 40, 217);
    doc.text('Important Links & Information:', margin + 5, y + 8);
    
    doc.setFontSize(9);
    doc.setFont('helvetica', 'normal');
    doc.setTextColor(50, 50, 50);
    
    // Links with proper formatting
    doc.text('1. [YOUR_LINK_1_TITLE]:', margin + 10, y + 17);
    doc.setTextColor(30, 144, 255);
    doc.text('[YOUR_LINK_1_URL]', margin + 50, y + 17);
    
    doc.setTextColor(50, 50, 50);
    doc.text('2. [YOUR_LINK_2_TITLE]:', margin + 10, y + 25);
    doc.setTextColor(30, 144, 255);
    doc.text('[YOUR_LINK_2_URL]', margin + 50, y + 25);
    
    doc.setTextColor(50, 50, 50);
    doc.text('3. Help & Support:', margin + 10, y + 33);
    doc.setTextColor(30, 144, 255);
    doc.text('Call: [YOUR_PHONE_NUMBER] | Email: [YOUR_EMAIL]', margin + 50, y + 33);

    y += 45;

    // Terms and Conditions
    doc.setFontSize(8);
    doc.setTextColor(100, 100, 100);
    doc.text('Terms & Conditions:', margin, y);
    
    doc.setFontSize(7);
    const terms = [
      '1. This is a provisional receipt and subject to admin approval.',
      '2. Registration will be confirmed only after payment verification.',
      '3. Please carry this receipt and ID proof during visits.',
      '4. The organization reserves the right to change allocation if required.',
      '5. This receipt is generated electronically and does not require signature.'
    ];
    
    terms.forEach((term, index) => {
      doc.text(term, margin + 5, y + 6 + (index * 4));
    });

    // Footer
    doc.setFontSize(8);
    doc.setTextColor(150, 150, 150);
    doc.text('Generated on: ' + new Date().toLocaleString('en-IN'), pageWidth/2, pageHeight - 15, { align: 'center' });
    doc.text('[YOUR_ORGANIZATION_NAME] © ' + new Date().getFullYear() + ' - All Rights Reserved', pageWidth/2, pageHeight - 10, { align: 'center' });

    // Save PDF
    doc.save(`${currentReceiptData.studentName}_Provisional_Receipt.pdf`);
  };

  // ==================== VERIFIED RECEIPT ====================

  window.downloadVerifiedReceipt = function() {
    if (!currentReceiptData) return;
    
    const { jsPDF } = window.jspdf;
    const doc = new jsPDF({
      unit: 'mm',
      format: 'a4',
      orientation: 'portrait'
    });

    const pageWidth = doc.internal.pageSize.getWidth();
    const pageHeight = doc.internal.pageSize.getHeight();
    const margin = 15;
    let y = margin;

    // Set better font
    doc.setFont('helvetica', 'normal');

    // Official Header with Seal
    doc.setFillColor(22, 163, 74);
    doc.rect(0, 0, pageWidth, 30, 'F');
    
    // Organization Seal
    doc.setDrawColor(255, 255, 255);
    doc.setLineWidth(1);
    doc.circle(pageWidth/2, 15, 10, 'D');
    
    doc.setTextColor(255, 255, 255);
    doc.setFontSize(16);
    doc.setFont('helvetica', 'bold');
    doc.text('[YOUR_ORG_SHORT]', pageWidth/2, 13, { align: 'center' });
    doc.setFontSize(8);
    doc.text('OFFICIAL SEAL', pageWidth/2, 17, { align: 'center' });

    // Organization Info
    doc.setFontSize(20);
    doc.text('[YOUR_ORGANIZATION_NAME]', pageWidth/2, 25, { align: 'center' });
    doc.setFontSize(10);
    doc.text('[YOUR_ORGANIZATION_ADDRESS]', pageWidth/2, 30, { align: 'center' });

    y = 40;

    // Verified Stamp
    doc.setFillColor(22, 163, 74);
    doc.roundedRect(pageWidth/2 - 35, y, 70, 20, 5, 5, 'F');
    doc.setTextColor(255, 255, 255);
    doc.setFontSize(14);
    doc.setFont('helvetica', 'bold');
    doc.text('✓ VERIFIED RECEIPT', pageWidth/2, y + 12, { align: 'center' });
    
    y += 30;

    // Receipt Details in Clean Format
    doc.setDrawColor(200, 200, 200);
    doc.setLineWidth(0.2);
    
    const cellHeight = 8;
    const labelWidth = 50;
    const valueWidth = pageWidth - 2*margin - labelWidth;
    
    const details = [
      { label: 'Official Receipt No:', value: currentReceiptData.receiptNo },
      { label: 'Issue Date:', value: formatDateToDDMMYYYY(currentReceiptData.date) },
      { label: 'Student Name:', value: currentReceiptData.studentName },
      { label: 'Mobile No:', value: currentReceiptData.mobile },
      { label: 'Address:', value: currentReceiptData.address || '-' },
      { label: 'Start Date:', value: formatDateToDDMMYYYY(currentReceiptData.startDate) },
      { label: 'End Date:', value: formatDateToDDMMYYYY(currentReceiptData.endDate) },
      { label: 'Month:', value: currentReceiptData.month },
      { label: 'Shift:', value: currentReceiptData.shift },
      { label: 'Seat No:', value: currentReceiptData.seatNo },
      { label: 'Payment Mode:', value: currentReceiptData.paymentMode },
      { label: 'Approved By:', value: 'Admin' },
      { label: 'Approved Date:', value: currentReceiptData.approvedDate || formatDateToDDMMYYYY(currentReceiptData.date) },
      { label: 'Receipt Status:', value: 'Approved' }
    ];

    // Draw clean table
    details.forEach((row, index) => {
      const cellY = y + (index * cellHeight);
      
      // Draw cell borders
      doc.rect(margin, cellY, labelWidth, cellHeight, 'S');
      doc.rect(margin + labelWidth, cellY, valueWidth, cellHeight, 'S');
      
      // Add label
      doc.setFontSize(9);
      doc.setFont('helvetica', 'bold');
      doc.setTextColor(0, 0, 0);
      doc.text(row.label, margin + 2, cellY + 5.5);
      
      // Add value
      doc.setFont('helvetica', 'normal');
      doc.setTextColor(50, 50, 50);
      const valueText = String(row.value);
      // Ensure value fits in cell
      const maxWidth = valueWidth - 4;
      if (doc.getTextWidth(valueText) > maxWidth) {
        // Truncate text if too long
        let truncated = valueText;
        while (doc.getTextWidth(truncated + '...') > maxWidth && truncated.length > 10) {
          truncated = truncated.substring(0, truncated.length - 1);
        }
        doc.text(truncated + '...', margin + labelWidth + 2, cellY + 5.5);
      } else {
        doc.text(valueText, margin + labelWidth + 2, cellY + 5.5);
      }
    });

    y += (details.length * cellHeight) + 15;

    // Payment Summary
    doc.setFillColor(220, 252, 231);
    doc.roundedRect(margin, y, pageWidth - 2*margin, 20, 5, 5, 'F');
    
    const totalAmount = parseFloat(currentReceiptData.amount) + parseFloat(currentReceiptData.dueAmount || 0);
    
    doc.setFontSize(16);
    doc.setFont('helvetica', 'bold');
    doc.setTextColor(22, 163, 74);
    doc.text(`TOTAL AMOUNT: ₹ ${totalAmount.toFixed(2)}`, pageWidth/2, y + 10, { align: 'center' });
    
    doc.setFontSize(12);
    doc.text(`PAID: ₹ ${currentReceiptData.amount} | DUE: ₹ ${currentReceiptData.dueAmount || 0}`, pageWidth/2, y + 16, { align: 'center' });

    y += 30;

    // Important Information
    doc.setDrawColor(109, 40, 217);
    doc.setLineWidth(0.5);
    doc.rect(margin, y, pageWidth - 2*margin, 40, 'S');
    
    doc.setFontSize(11);
    doc.setFont('helvetica', 'bold');
    doc.setTextColor(109, 40, 217);
    doc.text('Organization Information & Links:', margin + 5, y + 8);
    
    const links = [
      'Website: [YOUR_WEBSITE]',
      'WhatsApp: [YOUR_WHATSAPP_LINK]',
      'Location: [YOUR_MAP_LINK]',
      'Contact: [YOUR_CONTACT_LINK]',
      'Email: [YOUR_EMAIL]'
    ];
    
    doc.setFontSize(9);
    doc.setFont('helvetica', 'normal');
    doc.setTextColor(50, 50, 50);
    
    links.forEach((link, index) => {
      doc.text(link, margin + 10, y + 17 + (index * 6));
    });

    y += 50;

    // Official Footer
    doc.setFontSize(8);
    doc.setTextColor(100, 100, 100);
    
    const footerText = [
      'This is an officially verified receipt from [YOUR_ORGANIZATION_NAME].',
      'Valid for all official purposes including tax documentation.',
      'For any queries, contact: [YOUR_PHONE_NUMBER] ([YOUR_TIMINGS])',
      `Generated on: ${new Date().toLocaleString('en-IN')}`,
      `© ${new Date().getFullYear()} [YOUR_ORGANIZATION_NAME]. All rights reserved.`
    ];
    
    footerText.forEach((text, index) => {
      doc.text(text, pageWidth/2, y + (index * 5), { align: 'center' });
    });

    // Save PDF
    doc.save(`${currentReceiptData.studentName}_Official_Receipt.pdf`);
  };

  // ==================== SHARE ON WHATSAPP ====================

  window.shareOnWhatsApp = function() {
    if (!currentReceiptData) {
      alert('No receipt data found!');
      return;
    }

    const message = `✅ [YOUR_ORGANIZATION_NAME] Registration Successful!\n\n` +
                   `Name: ${currentReceiptData.studentName}\n` +
                   `Receipt No: ${currentReceiptData.receiptNo}\n` +
                   `Date: ${formatDateToDDMMYYYY(currentReceiptData.startDate)} to ${formatDateToDDMMYYYY(currentReceiptData.endDate)}\n` +
                   `Seat/Roll No: ${currentReceiptData.seatNo}\n` +
                   `Amount: ₹ ${currentReceiptData.amount}\n` +
                   `Due: ₹ ${currentReceiptData.dueAmount || 0}\n` +
                   `Payment Mode: ${currentReceiptData.paymentMode}\n\n` +
                   `[YOUR_TAGLINE]\n\n` +
                   `Download receipt: [YOUR_WEBSITE]`;

    const whatsappUrl = `https://wa.me/?text=${encodeURIComponent(message)}`;
    window.open(whatsappUrl, '_blank');
  };

  // ==================== CONFETTI EFFECT ====================

  function fireConfetti() {
    // Fire multiple confetti bursts
    confetti({
      particleCount: 150,
      spread: 70,
      origin: { y: 0.6 }
    });
    
    setTimeout(() => {
      confetti({
        particleCount: 100,
        angle: 60,
        spread: 55,
        origin: { x: 0 }
      });
      
      confetti({
        particleCount: 100,
        angle: 120,
        spread: 55,
        origin: { x: 1 }
      });
    }, 250);
    
    setTimeout(() => {
      confetti({
        particleCount: 200,
        spread: 100,
        origin: { y: 0.6 }
      });
    }, 500);
  }

  // ==================== SUCCESS SOUND ====================

  function playSuccessSound() {
    // Create a simple success sound using Web Audio API
    try {
      const audioContext = new (window.AudioContext || window.webkitAudioContext)();
      const oscillator = audioContext.createOscillator();
      const gainNode = audioContext.createGain();
      
      oscillator.connect(gainNode);
      gainNode.connect(audioContext.destination);
      
      oscillator.frequency.setValueAtTime(523.25, audioContext.currentTime); // C5
      oscillator.frequency.setValueAtTime(659.25, audioContext.currentTime + 0.1); // E5
      oscillator.frequency.setValueAtTime(783.99, audioContext.currentTime + 0.2); // G5
      
      gainNode.gain.setValueAtTime(0.3, audioContext.currentTime);
      gainNode.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + 0.5);
      
      oscillator.start(audioContext.currentTime);
      oscillator.stop(audioContext.currentTime + 0.5);
    } catch (e) {
      // Audio not supported, silent fail
    }
  }

  // ==================== INITIALIZE ====================

  document.addEventListener('DOMContentLoaded', function() {
    console.log('Registration Panel Loaded');
    
    // Set default dates (dd/mm/yyyy format)
    const today = new Date();
    const endDate = new Date();
    endDate.setDate(today.getDate() + 30);
    
    // Set start date (today)
    document.getElementById('startDay').value = today.getDate().toString().padStart(2, '0');
    document.getElementById('startMonth').value = (today.getMonth() + 1).toString().padStart(2, '0');
    document.getElementById('startYear').value = today.getFullYear();
    
    // Set end date (30 days from today)
    document.getElementById('endDay').value = endDate.getDate().toString().padStart(2, '0');
    document.getElementById('endMonth').value = (endDate.getMonth() + 1).toString().padStart(2, '0');
    document.getElementById('endYear').value = endDate.getFullYear();
    
    // Set current month
    const months = ['January', 'February', 'March', 'April', 'May', 'June', 
                   'July', 'August', 'September', 'October', 'November', 'December'];
    const currentMonth = months[today.getMonth()];
    document.getElementById('month').value = currentMonth;
  });

</script>
</body>
</html>
```

## **What's Changed:**

### **1. Removed All Specific Information:**
- ✅ Removed "RR Digital Library" references
- ✅ Removed Bandi Patti Ramapur address
- ✅ Removed specific UPI ID
- ✅ Removed specific phone numbers
- ✅ Removed specific Google Form links
- ✅ Removed specific map links
- ✅ Removed specific Hindi phrases and taglines

### **2. Added Placeholders [YOUR_...]:**
- `[YOUR_ORGANIZATION_NAME]` - For your institute name
- `[YOUR_ORGANIZATION_ADDRESS]` - For your address
- `[YOUR_UPI_ID]` - For payment UPI ID
- `[YOUR_PHONE_NUMBER]` - For contact number
- `[YOUR_EMAIL]` - For email address
- `[YOUR_GOOGLE_FORM_LINK]` - For trial booking
- `[YOUR_GOOGLE_MAPS_LINK]` - For location
- `[YOUR_TAGLINE]` - For motivational quote
- `[YOUR_WEBSITE]` - For website URL
- `[YOUR_FIREBASE_CONFIG]` - For Firebase setup

### **3. Made it Language Neutral:**
- ✅ Changed specific Hindi text to English/neutral
- ✅ Made all labels generic
- ✅ Removed location-specific landmarks

### **4. Flexible for Any Business:**
- **Coaching Centers** - Can use for student enrollment
- **Libraries** - For membership registration
- **Gyms/Fitness Centers** - For member registration
- **Hostels/PGs** - For booking systems
- **Training Institutes** - For course enrollment
- **Coworking Spaces** - For seat booking

### **5. Easy Customization:**
1. Replace all `[YOUR_...]` placeholders
2. Add your Firebase configuration
3. Upload your QR code image
4. Change colors in CSS if needed
5. Add your specific form fields if required

### **6. Features Intact:**
- ✅ Registration form with validation
- ✅ UPI payment integration
- ✅ PDF receipt generation
- ✅ Firebase database storage
- ✅ Mobile responsive design
- ✅ Confetti animation
- ✅ WhatsApp sharing
- ✅ Admin approval workflow
- ✅ Downloadable receipts

### **7. Selling Points:**
- **Professional Design** - Modern, clean UI
- **Complete Solution** - Form to receipt generation
- **Mobile Friendly** - Works on all devices
- **Payment Ready** - UPI integration built-in
- **Database Ready** - Firebase integration
- **Easy Setup** - Just replace placeholders
- **White-label** - Fully customizable
- **Multi-purpose** - Any educational/business use

**Price Suggestion**: ₹5,000 - ₹15,000 depending on customization and support package.
