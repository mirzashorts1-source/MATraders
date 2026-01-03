<!DOCTYPE html>
<html lang="en">
<head><script type="module">
  // Import the functions you need from the SDKs you need
  import { initializeApp } from "https://www.gstatic.com/firebasejs/12.7.0/firebase-app.js";
  import { getAnalytics } from "https://www.gstatic.com/firebasejs/12.7.0/firebase-analytics.js";
  // TODO: Add SDKs for Firebase products that you want to use
  // https://firebase.google.com/docs/web/setup#available-libraries

  // Your web app's Firebase configuration
  // For Firebase JS SDK v7.20.0 and later, measurementId is optional
  const firebaseConfig = {
    apiKey: "AIzaSyBN7JWmQjaSwn4f6_DB4Ecejl271iPfYo8",
    authDomain: "matraders3.firebaseapp.com",
    projectId: "matraders3",
    storageBucket: "matraders3.firebasestorage.app",
    messagingSenderId: "441825754184",
    appId: "1:441825754184:web:f31a8b6141bee79effec7d",
    measurementId: "G-MVS8EYVVGS"
  };

  // Initialize Firebase
  const app = initializeApp(firebaseConfig);
  const analytics = getAnalytics(app);
</script>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>M.A Traders - Sahiwal | v18.8</title>
    <style>
        :root { --primary: #1a3a5f; --secondary: #2980b9; --success: #27ae60; --danger: #e74c3c; --warning: #f39c12; --bg: #ebf0f3; --white: #ffffff; }
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background-color: var(--bg); margin: 0; padding-bottom: 50px; color: #333; }
        
        /* Login Screen Styling */
        #login-screen {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: var(--primary); display: flex; justify-content: center;
            align-items: center; z-index: 10000; color: white; flex-direction: column;
        }
        .login-box { background: white; padding: 30px; border-radius: 8px; text-align: center; color: #333; box-shadow: 0 4px 15px rgba(0,0,0,0.3); }
        .login-box input { padding: 10px; font-size: 1.2rem; width: 150px; text-align: center; margin-bottom: 15px; border: 2px solid #ddd; border-radius: 4px; }
        
        /* Original UI Components */
        .top-bar { background: var(--primary); color: white; padding: 15px 40px; display: flex; justify-content: space-between; align-items: center; box-shadow: 0 2px 5px rgba(0,0,0,0.1); }
        .container { max-width: 1400px; margin: 20px auto; padding: 0 20px; display: grid; grid-template-columns: 1.8fr 1fr; gap: 25px; }
        @media (max-width: 950px) { .container { grid-template-columns: 1fr; } }
        
        .card { background: var(--white); border-radius: 8px; padding: 20px; box-shadow: 0 2px 10px rgba(0,0,0,0.05); margin-bottom: 20px; }
        .tab-header { font-size: 1.4rem; font-weight: bold; color: #444; margin-bottom: 15px; border-bottom: 2px solid #eee; padding-bottom: 10px; }
        .dash-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(130px, 1fr)); gap: 10px; margin-bottom: 25px; }
        .stat-card { padding: 12px; border-radius: 6px; color: white; text-align: center; }
        .bg-sales { background: #34495e; } .bg-profit { background: #16a085; } .bg-stock { background: #2980b9; } 
        .bg-c-credit { background: #d35400; } .bg-v-credit { background: #8e44ad; }
        .stat-val { font-size: 0.95rem; font-weight: bold; background: rgba(255,255,255,0.9); color: #333; padding: 4px; border-radius: 4px; margin-top: 8px; }
        
        label { display: block; font-size: 0.75rem; font-weight: 600; margin: 8px 0 2px; color: #666; }
        input, select { width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 4px; box-sizing: border-box; }
        .grid-row { display: grid; grid-template-columns: repeat(auto-fit, minmax(100px, 1fr)); gap: 10px; }
        
        .btn { cursor: pointer; border: none; border-radius: 4px; font-weight: bold; padding: 10px 15px; transition: 0.2s; }
        .btn-save { background: var(--primary); color: white; width: 100%; margin-top: 20px; }
        .btn-stock { background: var(--success); color: white; margin-top: 10px; width: 100%; }
        .btn-add-item { background: #e67e22; color: white; margin-top: 22px; width: 100%; }
        .btn-view { background: var(--secondary); color: white; font-size: 0.65rem; padding: 4px 6px; border-radius: 3px; }
        .btn-del { background: var(--danger); color: white; font-size: 0.65rem; padding: 4px 6px; border-radius: 3px; }
        .btn-edit { background: var(--secondary); color: white; font-size: 0.65rem; padding: 4px 6px; border-radius: 3px; }
        .btn-ret { background: var(--warning); color: white; font-size: 0.65rem; padding: 4px 6px; border-radius: 3px; }
        .btn-pay { background: var(--success); color: white; font-size: 0.65rem; padding: 4px 6px; border-radius: 3px; }
        .btn-hist { background: #7f8c8d; color: white; font-size: 0.65rem; padding: 4px 6px; border-radius: 3px; }

        table { width: 100%; border-collapse: collapse; margin-top: 10px; font-size: 0.82rem; }
        th { text-align: left; padding: 8px; border-bottom: 2px solid #eee; background: #f8f9fa; }
        td { padding: 8px; border-bottom: 1px solid #eee; }

        .overlay { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.85); z-index: 9999; overflow-y: auto; padding: 40px 0; }
        
        #print-area { 
            background: white; width: 210mm; min-height: 297mm; padding: 20mm; margin: 0 auto;
            box-shadow: 0 0 20px rgba(0,0,0,0.5); box-sizing: border-box; color: #000; position: relative;
        }

        @media print { 
            body * { visibility: hidden; } 
            #invoiceOverlay, #invoiceOverlay * { visibility: visible; } 
            #invoiceOverlay { position: absolute; left: 0; top: 0; width: 100%; background: white; padding: 0; margin: 0; } 
            #print-area { border: none; box-shadow: none; margin: 0; width: 100%; padding: 10mm; }
            .no-print { display: none !important; } 
            @page { size: A4; margin: 0; }
        }
    </style>
</head>
<body onload="checkAuth()">

    <div id="login-screen">
        <div class="login-box">
            <h2>M.A TRADERS</h2>
            <p>Enter Access Code</p>
            <input type="password" id="login-code" maxlength="4" placeholder="****">
            <br>
            <button class="btn btn-save" onclick="login()">Login</button>
        </div>
    </div>

    <div id="main-app" style="display:none;">
        <div class="top-bar">
            <div><strong style="font-size:1.5rem;">M.A TRADERS</strong> | Faisalabad Road Sahiwal</div>
            <div style="display: flex; gap: 10px; align-items: center;">
                <button onclick="manualSave()" class="btn" style="background: var(--success); color: white; padding: 5px 10px;">SAVE ALL</button>
                <button onclick="logout()" class="btn" style="background: var(--danger); color: white; padding: 5px 10px;">LOGOUT</button>
                <div id="clock"></div>
            </div>
        </div>

        <div class="container">
            <div>
                <div class="dash-grid">
                    <div class="stat-card bg-stock"><div>STOCK VALUE</div><div class="stat-val" id="d-stock">0</div></div>
                    <div class="stat-card bg-sales"><div>TOTAL SALES</div><div class="stat-val" id="d-sales">0</div></div>
                    <div class="stat-card bg-profit"><div>NET PROFIT</div><div class="stat-val" id="d-profit">0</div></div>
                    <div class="stat-card bg-c-credit"><div>CUST. CREDIT</div><div class="stat-val" id="d-cc">0</div></div>
                    <div class="stat-card bg-v-credit"><div>VEND. CREDIT</div><div class="stat-val" id="d-vc">0</div></div>
                </div>

                <div class="card">
                    <div class="tab-header">Update Stock</div>
                    <input type="hidden" id="edit-id">
                    <div class="grid-row">
                        <div><label>Quick Select</label>
                            <select onchange="document.getElementById('s-name').value = this.value">
                                <option value="">-- Choose --</option>
                                <option>Vicryl 1 40mm 90cm Demetech</option><option>Vicryl 1 40mm 90cm Ethicon</option><option>Vicryl 2/0 30mm 75cm Demetech</option><option>Vicryl 3/0 24mm 75cm Demetech</option><option>Vicryl 4/0 20mm 75cm Demetech</option><option>Vicryl 0 40mm 90cm Demetech </option>
                                <option>Prolene 0 30mm 75cm Demetech </option><option>Prolene 1 30mm 75cm Demetech</option><option>Prolene 2/0 RB 30mm 75cm Demetech </option><option>Prolene 2/0 ST 60mm 75cm </option>
                                <option>Orange Syringe 5ml Auto Disable </option><option>BM Syringe 3ml Auto Disable</option><option>BM Syringe 5ml Auto Disable</option><option>BM Syringe 10ml Auto Disable</option>
                                <option>Trow IV Infusion Set Single</option><option>Trow IV Infusion Set With Y Pot</option>
                                <option>Trow Tape 1/2"</option><option>Trow Tape 1"</option><option>Trow Tape 2"</option><option>Orange IV Infusion Set Single</option>
                            </select>
                        </div>
                        <div><label>Product Name</label><input type="text" id="s-name"></div>
                        <div><label>Vendor Name</label><input type="text" id="s-vendor"></div>
                    </div>
                    <div class="grid-row">
                        <div><label>Pack Size</label><input type="text" id="s-pack"></div>
                        <div><label>Batch #</label><input type="text" id="s-batch"></div>
                        <div><label>Expiry</label><input type="text" id="s-exp" placeholder="MM/YY"></div>
                    </div>
                    <div class="grid-row">
                        <div><label>Qty</label><input type="number" id="s-qty" value="0"></div>
                        <div><label>Buy Price</label><input type="number" id="s-buy" value="0"></div>
                        <div><label>Sale Price</label><input type="number" id="s-sell" value="0"></div>
                        <div><label>Paid to Vendor</label><input type="number" id="s-vpaid" value="0"></div>
                    </div>
                    <button class="btn btn-stock" id="stock-btn" onclick="addStock()">SAVE TO STOCK</button>
                </div>

                <div class="card">
                    <div class="tab-header">Sale Entry</div>
                    <div class="grid-row">
                        <div><label>Customer Name</label><input type="text" id="c-name" placeholder="Name"></div>
                        <div><label>Address</label><input type="text" id="c-addr" placeholder="City"></div>
                        <div><label>Amount Received</label><input type="number" id="c-received" value="0"></div>
                    </div>
                    <div class="grid-row" style="margin-top:15px; border-top:1px solid #eee; padding-top:10px;">
                        <div style="grid-column: span 2;"><label>Select Item</label><select id="c-prod" onchange="loadProductInfo()"></select></div>
                        <div><label>Rate</label><input type="number" id="c-price"></div>
                        <div><label>Qty</label><input type="number" id="c-qty" value="1"></div>
                        <div><label>Disc %</label><input type="number" id="c-disc" value="0"></div>
                        <div><button class="btn btn-add-item" onclick="addToCart()">+ ADD</button></div>
                    </div>
                    <table style="background:#fffcf0; border: 1px solid #ffd32a; margin-top:15px;">
                        <thead><tr><th>Item</th><th>Qty</th><th>Total</th><th>X</th></tr></thead>
                        <tbody id="cart-body"></tbody>
                    </table>
                    <button class="btn btn-save" onclick="saveSale()">GENERATE INVOICE</button>
                </div>
            </div>

            <div>
                <div class="card">
                    <div class="tab-header">Ledgers</div>
                    <div style="font-weight:bold; color:var(--primary); margin-bottom:5px;">Customer Credit</div>
                    <div style="max-height: 150px; overflow-y:auto;"><table id="cc-table"><thead><tr><th>Name</th><th>Due</th><th>Action</th></tr></thead><tbody id="cc-body"></tbody></table></div>
                    <div style="font-weight:bold; color:var(--primary); margin:15px 0 5px;">Vendor Credit</div>
                    <div style="max-height: 150px; overflow-y:auto;"><table id="vc-table"><thead><tr><th>Name</th><th>Due</th><th>Action</th></tr></thead><tbody id="vc-body"></tbody></table></div>
                </div>
                
                <div class="card">
                    <div class="tab-header">Inventory</div>
                    <div style="max-height: 300px; overflow-y:auto;"><table><thead><tr><th>Item</th><th>Qty</th><th>Action</th></tr></thead><tbody id="stk-body"></tbody></table></div>
                </div>

                <div class="card">
                    <div class="tab-header">Recent Bills</div>
                    <div style="max-height: 250px; overflow-y:auto;">
                        <table id="h-table">
                            <thead><tr><th>Client</th><th>Total</th><th>Action</th></tr></thead>
                            <tbody id="h-body"></tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <div id="invoiceOverlay" class="overlay">
        <div style="max-width: 210mm; margin: 0 auto;">
            <div id="print-area">
                <div style="text-align:center; border-bottom: 3px double #000; padding-bottom: 10px; margin-bottom: 20px;">
                    <div style="font-size: 42px; font-weight: 900; letter-spacing: 2px; margin: 0; color: #000;">M.A TRADERS</div>
                    <div style="font-size: 18px; font-weight: bold; margin: 5px 0; color: #000;">Surgical Disposable & Sutures</div>
                    <div style="font-size: 16px; color: #000;">Faisalabad Road Sahiwal</div>
                </div>
                <div style="display: flex; justify-content: space-between; margin-bottom: 20px;">
                    <div style="width: 60%;">
                        <div style="background: #fff; color: #000000; display: padding: 4px 12px; font-weight: 800; font-size: 15px; margin-bottom: 10px;">Customer Name:</div>
                        <div style="font-size: 15px; font-weight: 900; color: #000;" id="p-client"></div>
                        <div style="font-size: 16px; color: #000;" id="p-addr"></div>
                    </div>
                    <div style="text-align: right; font-size: 14px; line-height: 1.6; color: #000;">
                        <div style="font-size: 20px; font-weight: bold; border-bottom: 2px solid #000; margin-bottom: 5px;">INVOICE</div>
                        <b>Invoice #:</b> <span id="p-id" style="font-weight:bold;"></span><br>
                        <b>Date:</b> <span id="p-date" style="font-weight:bold;"></span><br>
                        <b>Time:</b> <span id="p-time" style="font-weight:bold;"></span>
                    </div>
                </div>
                <table style="width: 100%; border: 1.5px solid #000; border-collapse: collapse;">
                    <thead><tr style="background: #f0f0f0;">
                        <th style="border:1.5px solid #000; padding:8px; text-align:center; color:#000;">Qty</th>
                        <th style="border:1.5px solid #000; padding:8px; width:40%; color:#000;">Description</th>
                        <th style="border:1.5px solid #000; padding:8px; text-align:center; color:#000;">Pack</th>
                        <th style="border:1.5px solid #000; padding:8px; text-align:center; color:#000;">Batch</th>
                        <th style="border:1.5px solid #000; padding:8px; text-align:center; color:#000;">Expiry</th>
                        <th style="border:1.5px solid #000; padding:8px; text-align:right; color:#000;">Rate</th>
                        <th style="border:1.5px solid #000; padding:8px; text-align:center; color:#000;">Disc%</th>
                        <th style="border:1.5px solid #000; padding:8px; text-align:right; color:#000;">Total</th>
                    </tr></thead>
                    <tbody id="p-items" style="font-weight: bold; color: #000;"></tbody>
                </table>
                <div style="margin-top: 30px; display: flex; justify-content: space-between; color: #000;">
                    <div style="width: 50%; font-size: 13px; line-height: 1.5;">
                        <p><b>Terms & Conditions:</b><br>1. Goods once sold are not returnable.<br>2. Please check expiry before leaving.</p>
                        <br><br>
                        <div style="display: flex; justify-content: space-between; align-items: flex-end; width: 100%; margin-top: 20px;">
                            <div style="text-align: center;">
                                <div style="border-top: 1.5px solid #000; width: 150px; font-weight:bold; padding-top: 5px;">Received By</div>
                            </div>
                            <div style="text-align: center;">
                                <div style="border-top: 1.5px solid #000; width: 150px; font-weight:bold; padding-top: 5px;">Authorized Signature</div>
                            </div>
                        </div>
                    </div>
                    <div style="width: 40%; line-height: 2.2;">
                        <div style="display:flex; justify-content:space-between; border-bottom: 1px dashed #000; font-weight:bold;"><span>Total:</span><span>Rs. <span id="p-total"></span></span></div>
                        <div style="display:flex; justify-content:space-between; border-bottom: 1px dashed #000; font-weight:bold;"><span>Received:</span><span>Rs. <span id="p-rec"></span></span></div>
                        <div style="display:flex; justify-content:space-between; font-weight: 900; font-size: 24px; border-top: 2.5px solid #000;"><span>Balance:</span><span>Rs. <span id="p-due"></span></span></div>
                    </div>
                </div>
                <div style="position: absolute; bottom: 15mm; left: 0; right: 0; text-align: center; font-size: 14px; border-top: 1.5px solid #000; padding-top: 10px; margin: 0 20mm; font-weight:bold; color:#000;">Thanks For Trust!</div>
            </div>
            <div class="no-print" style="text-align: center; margin-top: 30px;">
                <button class="btn" style="background: #555; color: #fff; padding: 60px 60px;" onclick="document.getElementById('invoiceOverlay').style.display='none'">Close</button>
                <button class="btn btn-save" style="width: auto; padding: 60px 60px; margin-center: 10px; background:var(--success);" onclick="window.print()">PRINT</button>
            </div>
        </div>
    </div>

    <div id="historyOverlay" class="overlay">
        <div class="card" style="max-width:800px; margin:20px auto;">
            <div style="display:flex; justify-content:space-between; align-items:center;">
                <h2 id="hist-title" style="margin:0;">History</h2>
                <div id="hist-balance" style="font-weight:bold; color:var(--danger);"></div>
            </div>
            <hr>
            <div style="max-height: 400px; overflow-y: auto;">
                <table>
                    <thead><tr><th>Date</th><th>Time</th><th>Paid</th><th>Credit</th></tr></thead>
                    <tbody id="hist-content"></tbody>
                </table>
            </div>
            <div style="text-align: right; margin-top: 20px;">
                <button class="btn" style="background: var(--primary); color: #fff;" onclick="document.getElementById('historyOverlay').style.display='none'">CLOSE</button>
            </div>
        </div>
    </div>

<script>
    // System Variables
    let currentPass = "";
    let stock = [], sales = [], vendorCredit = {}, customerCredit = {}, paymentHistory = [], cart = [];

    function checkAuth() {
        let savedPass = sessionStorage.getItem('ma_pass');
        if (savedPass) {
            currentPass = savedPass;
            document.getElementById('login-screen').style.display = 'none';
            document.getElementById('main-app').style.display = 'block';
            loadData();
        }
    }

    function login() {
        const code = document.getElementById('login-code').value;
        if (code === '1234' || code === '1122' || code === '1133') {
            currentPass = code;
            sessionStorage.setItem('ma_pass', code);
            document.getElementById('login-screen').style.display = 'none';
            document.getElementById('main-app').style.display = 'block';
            loadData();
        } else {
            alert("Incorrect Code!");
            document.getElementById('login-code').value = "";
        }
    }

    function logout() {
        if(confirm("Are you sure you want to logout?")) {
            sessionStorage.removeItem('ma_pass');
            location.reload();
        }
    }

    function loadData() {
        let key = "ma_data_" + currentPass;
        let data = JSON.parse(localStorage.getItem(key)) || {};
        stock = data.stock || [];
        sales = data.sales || [];
        vendorCredit = data.vc || {};
        customerCredit = data.cc || {};
        paymentHistory = data.pay || [];
        render();
    }

    function manualSave() {
        let key = "ma_data_" + currentPass;
        let dataToSave = { stock, sales, vc: vendorCredit, cc: customerCredit, pay: paymentHistory };
        localStorage.setItem(key, JSON.stringify(dataToSave));
        alert("All Items Saved Successfully! (OK)");
    }

    function saveAndRender() {
        let key = "ma_data_" + currentPass;
        let dataToSave = { stock, sales, vc: vendorCredit, cc: customerCredit, pay: paymentHistory };
        localStorage.setItem(key, JSON.stringify(dataToSave));
        render();
    }

    window.history.pushState(null, null, window.location.href);
    window.onpopstate = function() {
        if (confirm("Do you want to Save data? (Press OK to Save)")) {
            manualSave();
        }
        window.history.pushState(null, null, window.location.href);
    };

    function confirmDelete(callback) {
        if(confirm("Are you sure you want to delete this permanently?")) {
            callback();
        }
    }

    function addStock() {
        const name = document.getElementById('s-name').value;
        const qty = parseInt(document.getElementById('s-qty').value) || 0;
        const buy = parseFloat(document.getElementById('s-buy').value) || 0;
        const paid = parseFloat(document.getElementById('s-vpaid').value) || 0;
        const vendor = document.getElementById('s-vendor').value || "General";
        const editId = document.getElementById('edit-id').value;

        if(name && qty > 0) {
            if(editId) {
                const idx = stock.findIndex(x => x.id == editId);
                stock[idx] = { ...stock[idx], name, vendor, pack: document.getElementById('s-pack').value, batch: document.getElementById('s-batch').value, exp: document.getElementById('s-exp').value, qty, buy, sell: parseFloat(document.getElementById('s-sell').value) || 0 };
                document.getElementById('edit-id').value = "";
                document.getElementById('stock-btn').innerText = "SAVE TO STOCK";
            } else {
                const totalBill = qty * buy;
                const due = totalBill - paid;
                stock.push({ name, pack: document.getElementById('s-pack').value, batch: document.getElementById('s-batch').value, exp: document.getElementById('s-exp').value, qty, buy, sell: parseFloat(document.getElementById('s-sell').value) || 0, id: Date.now(), vendor, totalBill, paid });
                if(due > 0) vendorCredit[vendor] = (vendorCredit[vendor] || 0) + due;
                if(paid > 0) paymentHistory.push({ id: Date.now(), type: 'vend', name: vendor, amount: paid, date: new Date().toLocaleDateString(), time: new Date().toLocaleTimeString() });
            }
            saveAndRender(); clearStockForm();
        }
    }

    function clearStockForm() {
        ['s-name','s-vendor','s-pack','s-batch','s-exp','s-qty','s-buy','s-sell','s-vpaid'].forEach(f => document.getElementById(f).value = (f==='s-qty'||f==='s-buy'||f==='s-sell'||f==='s-vpaid') ? 0 : "");
    }

    function editStock(id) {
        const item = stock.find(x => x.id == id);
        if(item) {
            ['s-name','s-vendor','s-pack','s-batch','s-exp','s-qty','s-buy','s-sell'].forEach(f => document.getElementById(f).value = item[f.split('-')[1]]);
            document.getElementById('edit-id').value = id;
            document.getElementById('stock-btn').innerText = "UPDATE ITEM";
            window.scrollTo(0,0);
        }
    }

    function returnToVendor(id) {
        const item = stock.find(x => x.id == id);
        if(!item) return;
        const q = parseInt(prompt(`Quantity to return to vendor for ${item.name}? (Max: ${item.qty})`));
        if(q > 0 && q <= item.qty) {
            item.qty -= q;
            saveAndRender();
            alert("Stock returned to vendor.");
        }
    }

    function loadProductInfo() {
        const item = stock.find(x => x.id == document.getElementById('c-prod').value);
        if(item) document.getElementById('c-price').value = item.sell;
    }

    function addToCart() {
        const item = stock.find(x => x.id == document.getElementById('c-prod').value);
        const q = parseInt(document.getElementById('c-qty').value) || 0;
        if(!item || item.qty < q) return alert("Insufficient Stock!");
        const p = parseFloat(document.getElementById('c-price').value) || 0;
        const d = parseFloat(document.getElementById('c-disc').value) || 0;
        const total = (q * p) - ((q * p * d)/100);
        cart.push({ itemId: item.id, name: item.name, pack: item.pack, batch: item.batch, exp: item.exp, qty: q, price: p, buy: item.buy, disc: d, total });
        item.qty -= q; renderCart();
    }

    function renderCart() {
        document.getElementById('cart-body').innerHTML = cart.map((i, idx) => `<tr><td>${i.name}</td><td>${i.qty}</td><td>${Math.round(i.total)}</td><td onclick="cart.splice(${idx},1); renderCart();" style="color:red; cursor:pointer;">X</td></tr>`).join('');
    }

    function saveSale() {
        if(cart.length === 0) return alert("Cart empty!");
        const client = document.getElementById('c-name').value || "Cash Customer";
        const received = parseFloat(document.getElementById('c-received').value) || 0;
        const total = cart.reduce((a,b) => a + b.total, 0);
        const due = total - received;
        const saleObj = { id: Date.now(), client, addr: document.getElementById('c-addr').value || "Sahiwal", items: [...cart], total, received, due, date: new Date().toLocaleDateString(), time: new Date().toLocaleTimeString() };
        if(due > 0) customerCredit[client] = (customerCredit[client] || 0) + due;
        if(received > 0) paymentHistory.push({ id: Date.now(), type: 'cust', name: client, amount: received, date: new Date().toLocaleDateString(), time: new Date().toLocaleTimeString() });
        sales.push(saleObj);
        saveAndRender(); showInvoice(saleObj);
        cart = []; renderCart();
    }

    function deleteBill(id) {
        confirmDelete(() => {
            sales = sales.filter(s => s.id !== id);
            saveAndRender();
        });
    }

    function viewBill(id) {
        const sale = sales.find(s => s.id === id);
        if(sale) showInvoice(sale);
    }

    function showInvoice(sale) {
        document.getElementById('p-client').innerText = sale.client;
        document.getElementById('p-addr').innerText = sale.addr;
        document.getElementById('p-date').innerText = sale.date;
        document.getElementById('p-time').innerText = sale.time;
        document.getElementById('p-id').innerText = sale.id.toString().slice(-6);
        document.getElementById('p-items').innerHTML = sale.items.map(i => `<tr><td style="border:1px solid #000; padding:8px; text-align:center;">${i.qty}</td><td style="border:1px solid #000; padding:8px;">${i.name}</td><td style="border:1px solid #000; padding:8px; text-align:center;">${i.pack || ''}</td><td style="border:1px solid #000; padding:8px; text-align:center;">${i.batch || ''}</td><td style="border:1px solid #000; padding:8px; text-align:center;">${i.exp || ''}</td><td style="border:1px solid #000; padding:8px; text-align:right;">${i.price}</td><td style="border:1px solid #000; padding:8px; text-align:center;">${i.disc}%</td><td style="border:1px solid #000; padding:8px; text-align:right;">${Math.round(i.total)}</td></tr>`).join('');
        document.getElementById('p-total').innerText = Math.round(sale.total).toLocaleString();
        document.getElementById('p-rec').innerText = Math.round(sale.received).toLocaleString();
        document.getElementById('p-due').innerText = Math.round(sale.due).toLocaleString();
        document.getElementById('invoiceOverlay').style.display = 'block';
    }

    function payCredit(type, name) {
        const amount = parseFloat(prompt(`Payment Amount for ${name}:`));
        if(amount > 0) {
            if(type==='cust') { customerCredit[name] -= amount; if(customerCredit[name]<=0) delete customerCredit[name]; } 
            else { vendorCredit[name] -= amount; if(vendorCredit[name]<=0) delete vendorCredit[name]; }
            paymentHistory.push({ id: Date.now(), type, name, amount, date: new Date().toLocaleDateString(), time: new Date().toLocaleTimeString() });
            saveAndRender();
        }
    }

    function showHistory(type, name) {
        document.getElementById('hist-title').innerText = `History: ${name}`;
        let balance = (type === 'cust') ? (customerCredit[name] || 0) : (vendorCredit[name] || 0);
        document.getElementById('hist-balance').innerText = `Total Pending: Rs ${Math.round(balance).toLocaleString()}`;
        let allRecs = [];
        if(type === 'cust') {
            sales.filter(s => s.client === name && s.due > 0).forEach(s => {
                allRecs.push({ ts: s.id, date: s.date, time: s.time, paid: 0, credit: s.due });
            });
        } else {
            stock.filter(s => s.vendor === name && (s.totalBill - s.paid) > 0).forEach(s => {
                allRecs.push({ ts: s.id, date: new Date(s.id).toLocaleDateString(), time: new Date(s.id).toLocaleTimeString(), paid: 0, credit: (s.totalBill - s.paid) });
            });
        }
        paymentHistory.filter(p => p.type === type && p.name === name).forEach(p => {
            let ts = p.id || new Date(p.date).getTime();
            allRecs.push({ ts: ts, date: p.date, time: p.time, paid: p.amount, credit: 0 });
        });
        allRecs.sort((a,b) => b.ts - a.ts);
        const rows = allRecs.map(r => {
            const dObj = new Date(r.ts);
            const day = dObj.toLocaleDateString('en-US', { weekday: 'long' });
            return `<tr><td>${r.date}<br><small>${day}</small></td><td>${r.time}</td><td style="color:green;">${r.paid > 0 ? r.paid.toLocaleString() : '-'}</td><td style="color:red;">${r.credit > 0 ? r.credit.toLocaleString() : '-'}</td></tr>`;
        }).join('');
        document.getElementById('hist-content').innerHTML = rows || '<tr><td colspan="4">No records found</td></tr>';
        document.getElementById('historyOverlay').style.display = 'block';
    }

    // Function to Return Bill Stock
    function returnBillStock(saleId) {
        const sale = sales.find(s => s.id === saleId);
        if(!sale) return;
        if(confirm(`Return all items from bill of ${sale.client} to stock?`)) {
            sale.items.forEach(soldItem => {
                const stockItem = stock.find(si => si.id === soldItem.itemId);
                if(stockItem) {
                    stockItem.qty += soldItem.qty;
                }
            });
            // Adjust Credit if balance was pending
            if(sale.due > 0) {
                customerCredit[sale.client] -= sale.due;
                if(customerCredit[sale.client] <= 0) delete customerCredit[sale.client];
            }
            sales = sales.filter(s => s.id !== saleId);
            alert("Items returned to stock and bill removed.");
            saveAndRender();
        }
    }

    // Function to Delete Ledger Entry
    function deleteLedger(type, name) {
        if(confirm(`Are you sure you want to delete ledger for ${name}?`)) {
            if(type === 'cust') delete customerCredit[name];
            else delete vendorCredit[name];
            saveAndRender();
        }
    }

    function render() {
        let ts = 0, sc = 0, tp = 0, stkH = "", hH = "", ccH = "", vcH = "";
        
        // Render Stock
        stock.forEach(s => { 
            if(s.qty > 0) {
                sc += (s.qty * s.buy); 
                stkH += `<tr><td>${s.name}</td><td>${s.qty}</td><td><button class="btn-edit" onclick="editStock(${s.id})">E</button><button class="btn-ret" onclick="returnToVendor(${s.id})">R</button><button class="btn-del" onclick="confirmDelete(() => { stock=stock.filter(x=>x.id!=${s.id});saveAndRender(); })">X</button></td></tr>`;
            }
        });

        // Render Recent Bills (Sales)
        sales.slice().reverse().forEach(s => {
            ts += s.total; 
            s.items.forEach(i => { tp += (i.total - (i.qty * i.buy)); });
            hH += `<tr><td>${s.client}</td><td>${Math.round(s.total)}</td><td><button class="btn-view" onclick="viewBill(${s.id})">View</button><button class="btn-ret" onclick="returnBillStock(${s.id})">Return</button><button class="btn-del" onclick="deleteBill(${s.id})">X</button></td></tr>`;
        });

        // Render Ledgers
        Object.entries(customerCredit).forEach(([n, v]) => {
            ccH += `<tr><td>${n}</td><td style="color:red; font-weight:bold;">${Math.round(v).toLocaleString()}</td><td><button class="btn-pay" onclick="payCredit('cust','${n}')">Pay</button><button class="btn-hist" onclick="showHistory('cust','${n}')">H</button><button class="btn-del" onclick="deleteLedger('cust','${n}')">X</button></td></tr>`;
        });
        Object.entries(vendorCredit).forEach(([n, v]) => {
            vcH += `<tr><td>${n}</td><td style="color:red; font-weight:bold;">${Math.round(v).toLocaleString()}</td><td><button class="btn-pay" onclick="payCredit('vend','${n}')">Pay</button><button class="btn-hist" onclick="showHistory('vend','${n}')">H</button><button class="btn-del" onclick="deleteLedger('vend','${n}')">X</button></td></tr>`;
        });

        document.getElementById('stk-body').innerHTML = stkH;
        document.getElementById('h-body').innerHTML = hH;
        document.getElementById('cc-body').innerHTML = ccH;
        document.getElementById('vc-body').innerHTML = vcH;
        
        document.getElementById('d-stock').innerText = Math.round(sc).toLocaleString();
        document.getElementById('d-sales').innerText = Math.round(ts).toLocaleString();
        document.getElementById('d-profit').innerText = Math.round(tp).toLocaleString();
        document.getElementById('d-cc').innerText = Math.round(Object.values(customerCredit).reduce((a,b)=>a+b,0)).toLocaleString();
        document.getElementById('d-vc').innerText = Math.round(Object.values(vendorCredit).reduce((a,b)=>a+b,0)).toLocaleString();

        const sel = document.getElementById('c-prod');
        const cur = sel.value;
        sel.innerHTML = '<option value="">-- Select Product --</option>' + stock.filter(s => s.qty > 0).map(s => `<option value="${s.id}">${s.name} (Qty: ${s.qty})</option>`).join('');
        sel.value = cur;
    }

    setInterval(() => { document.getElementById('clock').innerText = new Date().toLocaleString(); }, 1000);
</script>
</body>
</html>
