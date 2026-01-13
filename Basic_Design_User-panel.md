# Generic Digital Library Student Portal Template
[[Template of code ]] 
I've created a generalized template that can be sold to any educational institution. All organization-specific details have been replaced with placeholders.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>[INSTITUTE_NAME] Digital Library - Student Portal</title>
  
  <!-- PDF Library -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
  <!-- Confetti Library -->
  <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>

  <style>
    :root{ --brand:#6d28d9; --brand2:#f97316; --bg:#f3f4f6; --success:#22c55e; --gold: #d97706; }
    body{ font-family: system-ui, -apple-system, sans-serif; background: var(--bg); padding: 20px; margin: 0; }
    
    .wrap{ max-width: 480px; margin: 0 auto; background: white; padding: 25px 20px; border-radius: 20px; box-shadow: 0 10px 30px rgba(0,0,0,0.08); text-align: center; overflow: hidden; position: relative; min-height: 600px;}

    /* HEADER */
    .welcome-msg { background: linear-gradient(90deg, var(--brand), var(--brand2)); color: white; padding: 12px; border-radius: 8px; font-weight: bold; margin-bottom: 20px; font-size: 15px; text-transform: uppercase; letter-spacing: 1px; }
    .logo-img { width: 100px; height: 100px; margin-bottom: 5px; object-fit: contain; border-radius: 50%; border: 3px solid #f3f4f6; }
    h1 { margin: 5px 0 25px; font-size: 24px; color: #1e293b; text-transform: uppercase; letter-spacing: 0.5px; font-weight: 900; }
    
    /* FORMS */
    .section-label { text-align: left; font-size: 11px; color: var(--brand); font-weight: 800; text-transform: uppercase; margin-top: 15px; margin-bottom: 5px; letter-spacing: 0.5px; border-bottom: 1px dashed #e2e8f0; padding-bottom: 2px; }
    label { display: block; text-align: left; font-size: 12px; font-weight: bold; color: #475569; margin-bottom: 4px; margin-left: 2px; }
    input, select { width: 100%; padding: 12px; margin-bottom: 10px; border-radius: 10px; border: 1px solid #cbd5e1; background: #f8fafc; font-size: 14px; box-sizing: border-box; outline: none; transition: 0.2s; color: #1e293b; }
    input:focus, select:focus { border-color: var(--brand); background: white; box-shadow: 0 0 0 3px rgba(109, 40, 217, 0.1); }
    .grid-2 { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }

    /* BUTTONS */
    button { width: 100%; padding: 16px; background: linear-gradient(90deg, var(--brand), var(--brand2)); color: white; font-weight: 800; border: none; border-radius: 12px; cursor: pointer; font-size: 16px; transition: 0.2s; box-shadow: 0 4px 15px rgba(109, 40, 217, 0.3); margin-top: 10px; }
    button:active { transform: scale(0.98); }
    
    .btn-secondary { background: white; color: var(--brand); border: 2px solid var(--brand); box-shadow: none; }
    .btn-secondary:hover { background: #f3f4f6; }

    /* UPI & SCANNER */
    #upiSection { display: none; background: #f0fdf4; border: 2px dashed #16a34a; padding: 15px; border-radius: 10px; margin-bottom: 15px; }
    .qr-code { width: 140px; height: 140px; object-fit: contain; mix-blend-mode: multiply; margin: 5px 0; cursor: pointer; transition: transform 0.2s; }
    .qr-code:active { transform: scale(0.95); }
    
    .upi-box { display: flex; align-items: center; justify-content: space-between; background: #dcfce7; padding: 8px 12px; border-radius: 8px; margin-top: 5px; border: 1px solid #86efac; }
    .upi-link { text-decoration: none; color: #166534; flex-grow: 1; text-align: left; }
    .copy-btn { background: white; border: 1px solid #16a34a; color: #16a34a; padding: 5px 10px; border-radius: 5px; cursor: pointer; font-size: 12px; font-weight: bold; width: auto; margin-top:0; }
    
    /* STATUS CHECK SCREEN */
    #statusInterface { display: none; text-align: left; }
    .status-card { background: #f8fafc; border: 1px solid #e2e8f0; padding: 15px; border-radius: 12px; margin-top: 15px; display: none; }
    .status-badge { display: inline-block; padding: 5px 10px; border-radius: 20px; font-size: 12px; font-weight: bold; margin-bottom: 10px; }
    .badge-pending { background: #fef9c3; color: #854d0e; }
    .badge-approved { background: #dcfce7; color: #166534; border: 1px solid #22c55e; }
    
    /* SUCCESS SCREEN */
    #successScreen, #waitingScreen { display: none; }
    .success-container { padding: 30px 0; animation: popUp 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275); }
    .upi-tick-box { width: 80px; height: 80px; background: var(--success); border-radius: 50%; margin: 0 auto; display: flex; align-items: center; justify-content: center; animation: pulse-green 2s infinite; }
    .checkmark { width: 40px; height: 20px; border-left: 5px solid white; border-bottom: 5px solid white; transform: rotate(-45deg); margin-top: -5px; animation: drawCheck 0.5s ease forwards; opacity: 0; }
    
    .msg-status { font-size: 20px; color: #166534; margin-top: 25px; font-weight: 900; letter-spacing: 0.5px; text-transform: uppercase; }
    .msg-seat { font-size: 15px; color: #15803d; background: #dcfce7; padding: 8px 15px; border-radius: 99px; margin-top: 10px; display: inline-block; font-weight: bold; border: 1px solid #86efac; }
    
    /* CARDS */
    .promo-link { text-decoration: none; display: block; margin-top: 15px; transition: transform 0.2s; }
    .promo-card { border-radius: 15px; padding: 15px; position: relative; overflow: hidden; text-align: center; box-shadow: 0 4px 15px rgba(0,0,0,0.1); }
    .card-trial { background: linear-gradient(135deg, #10b981, #047857); color: white; border: 2px solid #34d399; }
    .card-map { background: #fff; border: 1px solid #e2e8f0; margin-top: 15px; }
    .premium-landmark { background: #fff7ed; padding: 12px; border-radius: 8px; border-left: 4px solid var(--gold); text-align: left; margin-bottom: 15px; }
    .highlight-txt { color: #b91c1c; font-weight: bold; border-bottom: 1px dashed #b91c1c; }
    
    .help-btn { background: #f1f5f9; color: #334155; font-weight: bold; padding: 12px; margin-top: 15px; border-radius: 10px; display: block; text-decoration: none; font-size: 14px; border: 1px solid #cbd5e1; display: flex; align-items: center; justify-content: center; gap: 8px;}
    
    .btn-row { display: flex; gap: 10px; margin-top: 25px; }
    .btn-sm { flex: 1; padding: 14px; font-size: 14px; border-radius: 10px; border: none; font-weight: bold; cursor: pointer; color: white; display: flex; align-items: center; justify-content: center; gap: 8px; }
    .btn-download { background: #16a34a; } .btn-share { background: #2563eb; }

    /* Animations */
    @keyframes pulse-green { 0% { transform: scale(0.95); box-shadow: 0 0 0 0 rgba(34, 197, 94, 0.7); } 70% { transform: scale(1); box-shadow: 0 0 0 20px rgba(34, 197, 94, 0); } 100% { transform: scale(0.95); box-shadow: 0 0 0 0 rgba(34, 197, 94, 0); } }
    @keyframes drawCheck { 0% { opacity:0; width:0; height:0; } 100% { opacity:1; width:40px; height:20px; } }
    @keyframes popUp { 0% { transform: scale(0.8); opacity: 0; } 100% { transform: scale(1); opacity: 1; } }
    .simple-loader { border: 4px solid #f3f3f3; border-top: 4px solid var(--brand); border-radius: 50%; width: 50px; height: 50px; animation: spin 1s linear infinite; margin: 20px auto; }
    @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }

  </style>
</head>
<body>

<div class="wrap">
  
  <!-- HEADER LOGO -->
  <div class="welcome-msg" id="welcomeText">Welcome to [INSTITUTE_NAME] Library</div>
  <img src="[LOGO_URL]" alt="Library Logo" class="logo-img" id="instituteLogo">
  <h1 id="instituteName">[INSTITUTE_NAME] Digital Library</h1>

  <!-- SCREEN 1: FORM INTERFACE -->
  <div id="frontInterface">
    
    <!-- Action Buttons -->
    <button class="btn-secondary" onclick="showStatusScreen()">🔒 Admin Verified Receipt Download</button>
    <div style="margin:10px 0; border-bottom:1px solid #eee;"></div>
    
    <div id="formSection">
      <!-- 1. Student Details -->
      <div class="section-label">1. Student Details</div>
      <label>Full Name</label>
      <input id="name" type="text" placeholder="Enter Student Name" autocomplete="off" />

      <label>Mobile Number (For Verification)</label>
      <input id="mobile" type="tel" placeholder="Enter Mobile Number" maxlength="10" />

      <!-- NEW SECRET PIN FIELD -->
      <label style="color:#d97706;">Create Secret PIN (Password)</label>
      <input id="createPin" type="number" placeholder="Set 4 Digit PIN (e.g. 1234)" maxlength="4" style="border:1px solid #d97706; background:#fffbeb;" />
      
      <label>Address / Location</label>
      <input id="address" type="text" placeholder="e.g. City, Area" />

      <!-- 2. Subscription -->
      <div class="section-label">2. Subscription Period</div>
      <label>Select Month</label>
      <select id="month">
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

      <div class="grid-2">
        <div>
          <label>Start Date</label>
          <input id="startDate" type="date" />
        </div>
        <div>
          <label>End Date</label>
          <input id="endDate" type="date" />
        </div>
      </div>

      <!-- 3. Shift & Seat -->
      <div class="section-label">3. Shift & Seat</div>
      <label>Select Shift</label>
      <select id="shift">
        <option value="Full Day">Full Day (Morning to Evening)</option>
        <option value="Half Day (Morning)">Half Day (Morning)</option>
        <option value="Half Day (Afternoon)">Half Day (Afternoon)</option>
        <option value="Half Day (Evening)">Half Day (Evening)</option>
        <option value="Full Time">Full Time (24 Hours)</option>
        <option value="Night Shift">Night Shift</option>
      </select>

      <div class="grid-2">
        <div>
          <label>Seat No.</label>
          <input id="seatNo" type="text" placeholder="Seat No." />
        </div>
        <div>
          <label>Behavior</label>
          <select id="behavior">
            <option value="Good">Good</option>
            <option value="Excellent">Excellent</option>
            <option value="Honours">Honours</option>
            <option value="Bad">Bad</option>
          </select>
        </div>
      </div>

      <!-- 4. Payment -->
      <div class="section-label">4. Payment Details</div>
      <div class="grid-2">
        <div>
          <label>Amount Paid (₹)</label>
          <input id="amount" type="number" placeholder="₹ Paid" />
        </div>
        <div>
          <label>Due Amount (₹)</label>
          <input id="paymentDue" type="number" placeholder="₹ Due" value="0" />
        </div>
      </div>

      <label>Payment Mode</label>
      <select id="paymentMode" onchange="toggleUPI()">
        <option value="Offline">Cash / Offline</option>
        <option value="Online">Online / UPI</option>
      </select>

      <!-- UPI -->
      <div id="upiSection">
        <div style="font-size:13px; font-weight:bold; color:#166534;">Tap to Pay or Scan</div>
        
        <!-- CLICKABLE QR CODE -->
        <a href="[YOUR_UPI_LINK]" target="_blank" title="Click to Pay">
            <img src="[YOUR_QR_CODE_URL]" class="qr-code" alt="Tap to Pay" id="qrCodeImage">
        </a>
        
        <div class="upi-box">
            <!-- CLICKABLE UPI ID -->
            <a href="[YOUR_UPI_LINK]" class="upi-link">
                <span class="upi-text" id="upiToCopy">[YOUR_UPI_ID]</span>
            </a>
            <button class="copy-btn" onclick="copyToClipboard()">❐ Copy</button>
        </div>
        <div style="font-size:10px; color:#166534; margin-top:3px;">👆 Click on QR or ID to make Payment</div>
        
        <div style="margin-top:15px; border-top:1px dashed #166534; padding-top:10px;">
          <label style="color:#166534;">Upload Payment Screenshot 📷</label>
          <input type="file" id="paymentScreenshot" accept="image/*" />
        </div>
      </div>

      <button id="btnRequest">SEND REQUEST TO ADMIN 🚀</button>
    </div>
  </div>

  <!-- SCREEN 2: CHECK STATUS WITH PIN -->
  <div id="statusInterface">
      <h2 style="color:#334155;">Secure Status Check</h2>
      <p style="font-size:13px; color:#64748b;">Enter your Registered Mobile & Secret PIN.</p>
      
      <label>Registered Mobile Number</label>
      <input id="searchMobile" type="tel" placeholder="Enter Mobile No." maxlength="10" />
      
      <!-- CHECK PIN FIELD -->
      <label>Enter Secret PIN</label>
      <input id="searchPin" type="password" placeholder="****" maxlength="4" style="letter-spacing:4px; font-weight:bold; text-align:center;" />

      <button onclick="checkStatus()">🔐 Login & Search Receipt</button>
      <button class="btn-secondary" onclick="showFormScreen()">⬅ Back to Form</button>

      <div id="statusResult" class="status-card">
          <!-- Results will appear here -->
      </div>
  </div>

  <!-- WAITING SCREEN -->
  <div id="waitingScreen">
    <br><br>
    <div class="simple-loader"></div>
    <h3 style="color:#334155; margin-top:20px;">Processing Request...</h3>
  </div>

  <!-- SUCCESS SCREEN -->
  <div id="successScreen">
    <div class="success-container">
        <div class="upi-tick-box">
            <div class="checkmark"></div>
        </div>
        
        <div class="msg-status" id="successTitle">Payment Successful<br>& Seat Confirmed</div>

        <div class="msg-seat" id="seatMsg">Seat no. --</div>
        
        <div class="msg-tagline" id="successTagline">"Your Success Journey Begins Here"</div>

        <!-- MARKETING CARDS -->
        <a href="[YOUR_BOOKING_FORM_LINK]" target="_blank" class="promo-link">
          <div class="promo-card card-trial">
            <div class="trial-title">Seats are filling fast! 🚀</div>
            <div class="trial-sub">Book your FREE Trial today!</div>
            <div class="trial-btn">⚡ Book FREE Trial NOW!</div>
          </div>
        </a>

        <!-- LOCATION -->
        <a href="[YOUR_GOOGLE_MAPS_LINK]" target="_blank" class="promo-link">
          <div class="promo-card card-map">
            <span class="map-icon">📍</span>
            <div class="map-title">Find our Perfect Location!</div>
            <div class="premium-landmark">
                <div class="map-sub">
                    <strong id="locationName">[INSTITUTE_NAME]</strong><br>
                    <span style="font-size:12px; color:#999;">Landmark:</span><br>
                    <span class="highlight-txt" id="landmark1">[LANDMARK_1]</span>, <span class="highlight-txt" id="landmark2">[LANDMARK_2]</span>,<br>
                    <span class="highlight-txt" id="landmark3">[LANDMARK_3]</span>
                </div>
            </div>
            <div class="map-btn">📍 View on Google Maps</div>
          </div>
        </a>

        <a href="[YOUR_WHATSAPP_LINK]" class="help-btn">
           💬 Need Help? Contact Us ([CONTACT_NUMBER])
        </a>

        <div class="btn-row">
            <button class="btn-sm btn-download" onclick="downloadPDF()">⬇ Download Receipt</button>
            <button class="btn-sm btn-share" onclick="sharePDF()">🔗 Share</button>
        </div>
        
        <button class="btn-new" onclick="location.reload()">New Entry</button>
    </div>
  </div>

</div>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
  import { getFirestore, collection, addDoc, updateDoc, doc, increment, query, where, getDocs, orderBy, limit } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

  // CONFIGURATION - To be replaced by customer
  const INSTITUTE_CONFIG = {
    name: "[INSTITUTE_NAME]",
    logoUrl: "[LOGO_URL]",
    welcomeMessage: "Welcome to [INSTITUTE_NAME] Library",
    upiId: "[YOUR_UPI_ID]",
    upiLink: "[YOUR_UPI_LINK]",
    qrCodeUrl: "[YOUR_QR_CODE_URL]",
    bookingFormLink: "[YOUR_BOOKING_FORM_LINK]",
    googleMapsLink: "[YOUR_GOOGLE_MAPS_LINK]",
    whatsappLink: "[YOUR_WHATSAPP_LINK]",
    contactNumber: "[CONTACT_NUMBER]",
    locationName: "[INSTITUTE_NAME]",
    landmarks: ["[LANDMARK_1]", "[LANDMARK_2]", "[LANDMARK_3]"],
    successTagline: "Your Success Journey Begins Here"
  };

  // Apply configuration to page elements
  document.getElementById('welcomeText').textContent = INSTITUTE_CONFIG.welcomeMessage;
  document.getElementById('instituteLogo').src = INSTITUTE_CONFIG.logoUrl;
  document.getElementById('instituteName').textContent = INSTITUTE_CONFIG.name + " Digital Library";
  document.getElementById('upiToCopy').textContent = INSTITUTE_CONFIG.upiId;
  document.getElementById('qrCodeImage').src = INSTITUTE_CONFIG.qrCodeUrl;
  document.getElementById('locationName').textContent = INSTITUTE_CONFIG.locationName;
  document.getElementById('landmark1').textContent = INSTITUTE_CONFIG.landmarks[0];
  document.getElementById('landmark2').textContent = INSTITUTE_CONFIG.landmarks[1];
  document.getElementById('landmark3').textContent = INSTITUTE_CONFIG.landmarks[2];
  document.getElementById('successTagline').textContent = INSTITUTE_CONFIG.successTagline;
  
  // Update links
  document.querySelector('a[href="[YOUR_UPI_LINK]"]').href = INSTITUTE_CONFIG.upiLink;
  document.querySelector('a[href="[YOUR_BOOKING_FORM_LINK]"]').href = INSTITUTE_CONFIG.bookingFormLink;
  document.querySelector('a[href="[YOUR_GOOGLE_MAPS_LINK]"]').href = INSTITUTE_CONFIG.googleMapsLink;
  document.querySelector('a[href="[YOUR_WHATSAPP_LINK]"]').href = INSTITUTE_CONFIG.whatsappLink;
  document.querySelector('a[href="[YOUR_WHATSAPP_LINK]"]').textContent = `💬 Need Help? Contact Us (${INSTITUTE_CONFIG.contactNumber})`;

  // Firebase Configuration - To be replaced by customer
  const firebaseConfig = {
    apiKey: "[YOUR_API_KEY]",
    authDomain: "[YOUR_AUTH_DOMAIN]",
    projectId: "[YOUR_PROJECT_ID]",
    storageBucket: "[YOUR_STORAGE_BUCKET]",
    messagingSenderId: "[YOUR_MESSAGING_SENDER_ID]",
    appId: "[YOUR_APP_ID]",
    measurementId: "[YOUR_MEASUREMENT_ID]"
  };

  const app = initializeApp(firebaseConfig);
  const db = getFirestore(app);
  let receiptData = null;

  // UI SWITCHING
  window.showStatusScreen = () => { document.getElementById("frontInterface").style.display = "none"; document.getElementById("statusInterface").style.display = "block"; }
  window.showFormScreen = () => { document.getElementById("statusInterface").style.display = "none"; document.getElementById("frontInterface").style.display = "block"; }
  window.toggleUPI = function() { const mode = document.getElementById("paymentMode").value; document.getElementById("upiSection").style.display = (mode === "Online") ? "block" : "none"; }
  window.copyToClipboard = function() { const text = document.getElementById("upiToCopy").innerText; navigator.clipboard.writeText(text).then(() => alert("UPI ID Copied!")); }

  // --- IMAGE CONVERT TO TEXT (JUGAAD) ---
  const convertBase64 = (file) => {
      return new Promise((resolve, reject) => {
          const reader = new FileReader();
          reader.readAsDataURL(file);
          reader.onload = () => resolve(reader.result);
          reader.onerror = error => reject(error);
      });
  }

  // --- SUBMIT LOGIC ---
  document.getElementById("btnRequest").addEventListener("click", async () => {
    const name = document.getElementById("name").value.trim();
    const amount = document.getElementById("amount").value;
    const mobile = document.getElementById("mobile").value.trim();
    const pin = document.getElementById("createPin").value.trim();
    const seatVal = document.getElementById("seatNo").value.trim() || "Unassigned";
    const fileInput = document.getElementById("paymentScreenshot");
    
    if(!name || !amount) return alert("Please enter Name and Amount.");
    if(mobile.length < 10) return alert("Enter valid 10-digit Mobile Number.");
    if(pin.length < 4) return alert("Please set a 4-Digit Secret PIN for security.");

    document.getElementById("frontInterface").style.display = "none";
    document.getElementById("waitingScreen").style.display = "block";
    document.getElementById("seatMsg").innerText = `Seat no. ${seatVal}`;

    let base64Image = "";
    
    try {
        // 1. Convert Image to Text (No Storage Cost)
        if (fileInput.files.length > 0) {
            const file = fileInput.files[0];
            if(file.size > 1000000) { // Limit to 1MB
                alert("File too large! Please upload a smaller screenshot (< 1MB).");
                location.reload();
                return;
            }
            base64Image = await convertBase64(file);
        }

        const d = new Date();
        const autoReceiptNo = `${INSTITUTE_CONFIG.name.substring(0,2)}-${d.getFullYear()}${(d.getMonth()+1).toString().padStart(2,'0')}${d.getDate()}-${d.getHours()}${d.getMinutes()}`;

        receiptData = {
          studentName: name, mobile: mobile, secretPin: pin,
          address: document.getElementById("address").value.trim(),
          month: document.getElementById("month").value, startDate: document.getElementById("startDate").value,
          endDate: document.getElementById("endDate").value, shift: document.getElementById("shift").value,
          seatNo: seatVal, behavior: document.getElementById("behavior").value,
          amount: Number(amount), paymentDue: Number(document.getElementById("paymentDue").value || 0),
          paymentMode: document.getElementById("paymentMode").value, 
          status: "Pending", 
          screenshotUrl: base64Image, // Save image as text
          downloadCount: 0,
          receiptNo: autoReceiptNo, dateTime: new Date().toLocaleString("en-IN"), timestamp: Date.now()
        };

        const docRef = await addDoc(collection(db, "receipts"), receiptData);
        receiptData.id = docRef.id;

        setTimeout(() => {
            document.getElementById("waitingScreen").style.display = "none";
            document.getElementById("successScreen").style.display = "block";
            fireConfetti();
            try { window.downloadPDF(); } catch(e){}
        }, 4000);
        
    } catch(e) { console.log(e); alert("Error saving data. Try again."); location.reload(); }
  });

  // --- CHECK STATUS ---
  window.checkStatus = async function() {
      const mobile = document.getElementById("searchMobile").value.trim();
      const pin = document.getElementById("searchPin").value.trim();
      const resultDiv = document.getElementById("statusResult");
      
      if(mobile.length < 10) return alert("Enter valid Mobile Number");
      if(pin.length < 4) return alert("Enter 4 Digit PIN");
      
      resultDiv.style.display = "block";
      resultDiv.innerHTML = "<p>Verifying credentials...</p>";

      try {
          const q = query(collection(db, "receipts"), where("mobile", "==", mobile), orderBy("timestamp", "desc"), limit(1));
          const querySnapshot = await getDocs(q);

          if (querySnapshot.empty) {
              resultDiv.innerHTML = "<p style='color:red;'>No record found.</p>";
          } else {
              let matched = false;
              querySnapshot.forEach((doc) => {
                  receiptData = doc.data();
                  receiptData.id = doc.id; // Important for download tracking
                  
                  if(receiptData.secretPin === pin) {
                      matched = true;
                      const isApproved = receiptData.status === "Approved";
                      const badgeClass = isApproved ? "badge-approved" : "badge-pending";
                      const badgeText = isApproved ? "✅ ADMIN VERIFIED" : "⏳ Pending Approval";
                      
                      resultDiv.innerHTML = `
                          <div style="text-align:center; padding:10px; border:1px solid #16a34a; background:#f0fdf4; border-radius:8px; margin-bottom:10px;">
                            <h3 style="margin:0; color:#166534;">🔓 Access Granted</h3>
                          </div>
                          <div class="status-badge ${badgeClass}">${badgeText}</div>
                          <div style="font-weight:bold; font-size:16px;">${receiptData.studentName}</div>
                          <div style="font-size:13px; color:#64748b;">Seat: ${receiptData.seatNo}</div>
                          <hr style="margin:10px 0; border:0; border-top:1px dashed #ccc;">
                          <button onclick="downloadPDF()" class="btn-sm btn-download" style="width:100%">⬇ Download Secure Receipt</button>
                      `;
                  }
              });
              if(!matched) resultDiv.innerHTML = "<p style='color:red; font-weight:bold;'>❌ INCORRECT PIN!</p>";
          }
      } catch(e) { console.error(e); resultDiv.innerHTML = "<p style='color:red;'>Error fetching data.</p>"; }
  }

  // --- PDF GENERATOR (UPDATED WITH DOWNLOAD TRACKING) ---
  const ICON_MAP = "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAAABmJLR0QA/wD/AP+gvaeTAAABwklEQVRoge2ZvU4CQRCFv40xJpT8o42FlZ0V2lB5F99AAwUeQG0t7CyMhYU2dtZGYkI0Jsb43ZglF2939g52VzDJJJuZzOx87M7sDChQoEABFfADbAFbQJ/6bQG3wAlgX1XJqgCsgG3gC6gAvf+06wJbwAnwK6tQlgX2gVfKoy5l88AR8CqrWJYFToA34Eg2b8AR8C6rYBby2AJeZTOn7B14l1UsC5wDHzK5B/ZlFcti5LEHzMjkAZiXVSyLkccWMCeTJ2Bevu6wJJA8toF5mTwD87KKZSHy2AHmZfIMzMsqlkXJYw+Yl8kDMG9Uq1gWJY8dYFEmT8CiUa1iWZQ8toFFmTwBi0a1imVR8tgCFmXyBCwa1SqWRcljE1iUyROwaFSrWBYlj01gUSZPwKJRrWJZlDw2gUWZPAGEf92oVrEsSh7rwKJMnoB1o1rFshB5rAOLMnkC1o1qFcuy5LECzMvkGZg3qlUsi5LHCjAvk2dg3qhWsSxKHivAvEye+9u/bVSrWJYF1oB3mTwB67KKZVlgDXiXyROwLqtYlgXWgA+ZPAH7soplWWAFeJfJE7Auq1gW+9s/A95l8gSsyyr0C/wGzZ54+Q+c6roAAAAASUVORK5CYII=";
  const ICON_FORM = "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAAABmJLR0QA/wD/AP+gvaeTAAABxElEQVRoge3Zz0rDQBCH8W9tFWq9iXgR/3wFbyKCt4q3iqB481bwVDyJ4E0QvIjiTbyJtWqtF2lzt8lukk3azbQ/CGyS7Px2Z3Y2gQIKKKAAG9gHDoCDf9p0gS3gCvhQVaIqABtgC7gE6kDrn3ZdoAFcAT+yCmRZYB94IT/qQjYPHAE/sopkWeAEOAf2ZPMGnAI/sopkIfLYAl5lM6fsHfiQVSSTkcc+8CGTe2BfVpFMSh57wIxMHoB5WUUyKXnsAHMyeQbmZRXJpOSxA8zJ5BmYl1Ukk5LHDjAnk2dgXlaRTEoeO8CcTJ6BeVlFMil57ABzMnkG5mUVyaTksQ3MyeQJmJdVJJOSxzYwJ5MnYF5WkUxKHmvAnEye7u3fLqtIJiWPbWBOJk/AvKwiGethz5xMnrb6t8sqkmWBNeBNJk/AuqwiWRZYA95k8gSsy7z+s8Aa8CGTJ2BfVpEsm/3tXwPeZfIE/MLpPwAAAABJRU5ErkJggg==";

  function createPDFDoc() {
    const { jsPDF } = window.jspdf;
    const doc = new jsPDF({ unit: "pt", format: [300, 500] }); 
    const w = doc.internal.pageSize.getWidth();
    const h = doc.internal.pageSize.getHeight();

    doc.setFillColor(255, 255, 255); doc.rect(0, 0, w, h, "F");
    doc.setFillColor(109, 40, 217); doc.roundedRect(10, 10, w-20, 75, 8, 8, "F");
    doc.setDrawColor(245, 158, 11); doc.setLineWidth(2); doc.line(30, 75, w-30, 75); 

    doc.setTextColor(255, 255, 255); doc.setFontSize(15); doc.setFont("helvetica", "bold"); 
    doc.text(INSTITUTE_CONFIG.name.toUpperCase() + " DIGITAL LIBRARY", w/2, 38, { align: "center" });
    doc.setFontSize(9); doc.setFont("helvetica", "normal"); 
    doc.text("Digital Learning Center", w/2, 55, { align: "center" });

    // VERIFICATION STAMP
    if(receiptData.status === "Approved") {
        doc.setTextColor(34, 197, 94); // Green
        doc.setFontSize(20); doc.setFont("helvetica", "bold");
        doc.text("ADMIN VERIFIED ✅", w/2, 100, { align: "center", angle: 10 });
    }

    doc.setTextColor(30, 41, 59); doc.setFontSize(10); doc.setFont("helvetica", "bold");
    let y = 120; const left = 25; const rightVal = 100;

    function row(label, val) {
        if(!val) val = "-";
        doc.setFont("helvetica", "bold"); doc.setTextColor(30, 41, 59);
        doc.text(`${label}:`, left, y);
        doc.setFont("helvetica", "normal"); doc.setTextColor(71, 85, 105);
        doc.text(`${val}`, left + rightVal, y);
        y += 18;
    }

    row("Receipt No", receiptData.receiptNo);
    row("Date", receiptData.dateTime.split(',')[0]);
    y += 5; 
    row("Student Name", receiptData.studentName);
    row("Mobile No", receiptData.mobile);
    row("Address", receiptData.address);
    row("Month", receiptData.month);
    row("Start Date", receiptData.startDate || "N/A");
    row("End Date", receiptData.endDate || "N/A");
    row("Shift", receiptData.shift);
    row("Seat No", receiptData.seatNo);
    row("Behavior", receiptData.behavior);
    row("Mode", receiptData.paymentMode);

    y += 10;
    doc.setFillColor(240, 253, 244); doc.setDrawColor(22, 163, 74); doc.roundedRect(20, y, w-40, 50, 5, 5, "FD");
    doc.setTextColor(22, 163, 74); doc.setFont("helvetica", "bold"); doc.setFontSize(16); doc.text(`Paid: Rs. ${receiptData.amount}/-`, w/2, y+30, { align: "center" });
    
    y += 65; 
    if(receiptData.paymentDue > 0){ 
        doc.setTextColor(220, 38, 38); doc.setFontSize(12); doc.setFont("helvetica", "bold");
        doc.text(`Due Amount: Rs. ${receiptData.paymentDue}`, w/2, y, { align: "center" }); 
    } else {
        doc.setTextColor(22, 163, 74); doc.setFontSize(10); doc.text(`No Dues`, w/2, y, { align: "center" });
    }

    let btnY = h - 110; const btnH = 30; const btnW = w - 50; const btnX = 25;
    
    doc.setDrawColor(220, 38, 38); doc.setFillColor(254, 242, 242); doc.roundedRect(btnX, btnY, btnW, btnH, 6, 6, "FD");
    doc.addImage(ICON_MAP, 'PNG', btnX + 20, btnY + 5, 20, 20);
    doc.setTextColor(185, 28, 28); doc.setFontSize(9); doc.setFont("helvetica", "bold");
    doc.text("Open Google Map Location", w/2 + 10, btnY + 19, { align: "center" });
    doc.link(btnX, btnY, btnW, btnH, { url: INSTITUTE_CONFIG.googleMapsLink });

    btnY += 38;
    doc.setDrawColor(37, 99, 235); doc.setFillColor(239, 246, 255); doc.roundedRect(btnX, btnY, btnW, btnH, 6, 6, "FD");
    doc.addImage(ICON_FORM, 'PNG', btnX + 20, btnY + 5, 20, 20);
    doc.setTextColor(29, 78, 216); doc.text("Open Online Booking Form", w/2 + 10, btnY + 19, { align: "center" });
    doc.link(btnX, btnY, btnW, btnH, { url: INSTITUTE_CONFIG.bookingFormLink });

    doc.setTextColor(150); doc.setFontSize(7); doc.setFont("helvetica", "normal");
    doc.text("Thank you for choosing " + INSTITUTE_CONFIG.name + ".", w/2, h - 15, { align: "center" });
    return doc;
  }

  window.downloadPDF = async function() { 
      if(!receiptData) return;
      // Increment Download Count in DB
      if(receiptData.id) {
          try {
             const docRef = doc(db, "receipts", receiptData.id);
             await updateDoc(docRef, { downloadCount: increment(1) });
          } catch(e) { console.log("Tracking error", e); }
      }
      createPDFDoc().save(`${receiptData.studentName}_Receipt.pdf`); 
  };
  window.sharePDF = async function() { if(!receiptData) return; try { const blob = createPDFDoc().output('blob'); const file = new File([blob], "receipt.pdf", { type: "application/pdf" }); await navigator.share({ files: [file] }); } catch (e) { downloadPDF(); } };

  function fireConfetti() {
    var count = 200; var defaults = { origin: { y: 0.7 } };
    function fire(particleRatio, opts) { confetti(Object.assign({}, defaults, opts, { particleCount: Math.floor(count * particleRatio) })); }
    fire(0.25, { spread: 26, startVelocity: 55, }); fire(0.2, { spread: 60, }); fire(0.35, { spread: 100, decay: 0.91, scalar: 0.8 });
    fire(0.1, { spread: 120, startVelocity: 25, decay: 0.92, scalar: 1.2 }); fire(0.1, { spread: 120, startVelocity: 45, });
  }
</script>
</body>
</html>
```

## Key Changes Made:

1. **Removed Organization-Specific Content**:
   - Replaced "Digital Library" with `[INSTITUTE_NAME]` placeholders
   - Removed specific Hindi text and made it English/generic
   - Replaced specific landmarks with `[LANDMARK_X]` placeholders

2. **Centralized Configuration**:
   - Created `INSTITUTE_CONFIG` object at the top of the JavaScript
   - All institution-specific settings are in one place
   - Easy for customers to customize without digging through code

3. **Removed Specific Contact Information**:
   - Replaced UPI ID, QR code, contact numbers with placeholders
   - Replaced specific Google Form and Map links with placeholders

4. **Made Text Generic**:
   - Changed Hindi welcome messages to English
   - Made all instructions generic and professional

5. **Maintained Full Functionality**:
   - All features (form submission, PDF generation, status checking) remain intact
   - Firebase integration remains (customers will add their own config)
   - Responsive design and modern UI preserved

## What Customers Need to Customize:

1. **INSTITUTE_CONFIG** object values
2. **Firebase configuration** with their own Firebase project details
3. **Logo URL** for their institution logo
4. **Payment links** (UPI, QR code, etc.)
5. **Contact information** and links

The template is now ready to be sold as a white-label solution to any educational institution or library.
