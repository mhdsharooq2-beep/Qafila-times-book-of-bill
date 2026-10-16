# Qafila-times-book-of-bill malayalam

<!DOCTYPE html>
<html lang="ml">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>QafilaTimes Business Manager</title>
<style>
:root{--navy:#17243a;--gold:#c79b45;--bg:#f3f5f9;--green:#16834a;--red:#c0392b}
*{box-sizing:border-box}
body{margin:0;font-family:Arial,"Noto Sans Malayalam",sans-serif;background:var(--bg);color:#202b3c}
header{background:var(--navy);color:white;padding:18px;display:flex;align-items:center;justify-content:space-between;gap:12px;flex-wrap:wrap}
header h1{margin:0;font-size:23px}header p{margin:5px 0 0;color:#e8cc8a;font-size:12px}
nav{background:white;padding:10px;display:flex;gap:7px;flex-wrap:wrap;position:sticky;top:0;z-index:4;box-shadow:0 2px 6px #0001}
button{background:var(--navy);color:white;border:0;border-radius:7px;padding:10px 13px;cursor:pointer;font-weight:bold}
button:hover{opacity:.87}.tab.active{background:var(--gold);color:#171717}
main{max-width:1300px;margin:auto;padding:16px}
.page{display:none}.page.active{display:block}
h2{font-size:22px;margin:5px 0 15px}h3{margin-top:8px}
.panel,.card{background:white;padding:15px;border-radius:11px;box-shadow:0 2px 8px #0000000a;margin-bottom:14px}
.cards{display:grid;grid-template-columns:repeat(auto-fit,minmax(165px,1fr));gap:12px;margin:12px 0}
.card small{color:#6b7485}.amount{font-size:23px;font-weight:bold;margin-top:8px;overflow-wrap:anywhere}
form{display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:12px}
label{display:block;font-size:13px;font-weight:bold;margin-bottom:5px}
input,select,textarea{width:100%;padding:10px;border:1px solid #ccd3de;border-radius:7px;background:white;font:inherit}
.actions{display:flex;gap:8px;flex-wrap:wrap;margin:12px 0}
.green{background:var(--green)}.red{background:var(--red)}.gold{background:var(--gold);color:#111}
.muted{font-size:13px;color:#697487}.notice{background:#fff7e5;padding:12px;border-radius:8px;margin:10px 0}
.table-wrap{overflow-x:auto;margin:12px 0}
table{border-collapse:collapse;width:100%;background:white;min-width:650px}
th,td{padding:10px;border-bottom:1px solid #e5e8ee;text-align:left;font-size:13px}
th{background:#eef1f6}
.hidden{display:none!important}
.bigbtn{padding:14px 18px;font-size:16px}
#presentation{background:#101a2b;color:white;min-height:100vh;padding:25px}
#presentation h1{font-size:clamp(28px,5vw,52px);color:#e5c477}
#presentation .card{color:#202b3c}
#presentation .amount{font-size:clamp(24px,4vw,40px)}
@media(max-width:600px){main{padding:9px}header h1{font-size:19px}nav{position:static}.amount{font-size:20px}}
@media print{header,nav,.no-print,button,form{display:none!important}body{background:white}main{padding:0}.page{display:none!important}#invoicePrint{display:block!important}}
</style>
</head>
<body>
<header>
 <div><h1>⌚ QafilaTimes</h1><p>COMPLETE BUSINESS MANAGEMENT</p></div>
 <div id="dateNow"></div>
 <button class="gold no-print" onclick="showPresentation()">📊 Presentation Mode</button>
</header>

<nav class="no-print">
 <button class="tab active" data-page="dashboard">Dashboard</button>
 <button class="tab" data-page="sales">വിൽപ്പന / Billing</button>
 <button class="tab" data-page="products">Products & Stock</button>
 <button class="tab" data-page="customers">Customers</button>
 <button class="tab" data-page="suppliers">Suppliers</button>
 <button class="tab" data-page="expenses">ചെലവുകൾ</button>
 <button class="tab" data-page="partners">4 Partners</button>
 <button class="tab" data-page="reports">Reports</button>
 <button class="tab" data-page="settings">Settings / Backup</button>
</nav>

<main>
<section id="dashboard" class="page active">
 <h2>Business Dashboard</h2>
 <div class="cards">
  <div class="card"><small>ആകെ ബിൽ തുക</small><div class="amount" id="dSales">₹0</div></div>
  <div class="card"><small>ഉൽപ്പന്ന ലാഭം</small><div class="amount" id="dProfit">₹0</div></div>
  <div class="card"><small>മറ്റ് ചെലവുകൾ</small><div class="amount" id="dExpense">₹0</div></div>
  <div class="card"><small>അറ്റലാഭം</small><div class="amount" id="dNet">₹0</div></div>
  <div class="card"><small>നിക്ഷേപം</small><div class="amount" id="dInvest">₹0</div></div>
  <div class="card"><small>Customer Pending</small><div class="amount" id="dPending">₹0</div></div>
  <div class="card"><small>Supplier Payable</small><div class="amount" id="dPayable">₹0</div></div>
  <div class="card"><small>ആകെ സ്റ്റോക്ക് എണ്ണം</small><div class="amount" id="dStock">0</div></div>
 </div>
 <div class="panel"><h3>ഈ മാസം</h3><div id="monthStats"></div></div>
 <div class="panel"><h3>Recent Sales</h3><div id="recentSales"></div></div>
 <div class="actions"><button onclick="go('reports')">മാസാന്ത റിപ്പോർട്ട് കാണുക</button><button onclick="go('partners')">പാർട്ണർ കണക്കുകൾ കാണുക</button></div>
</section>

<section id="sales" class="page">
 <h2>വിൽപ്പന / പുതിയ ബിൽ</h2>
 <div class="panel">
 <form id="saleForm">
  <div><label>തീയതി</label><input id="sDate" type="date" required></div>
  <div><label>Customer Name</label><input id="sCustomer" required></div>
  <div><label>Phone</label><input id="sPhone"></div>
  <div><label>Address / Location</label><input id="sAddress"></div>
  <div><label>ഉൽപ്പന്നം</label><select id="sProduct" required></select></div>
  <div><label>Qty</label><input id="sQty" type="number" min="1" value="1" required></div>
  <div><label>Cost Price / Unit</label><input id="sCost" type="number" min="0" step=".01" required></div>
  <div><label>MRP / Unit</label><input id="sMrp" type="number" min="0" step=".01"></div>
  <div><label>Selling Price / Unit</label><input id="sPrice" type="number" min="0" step=".01" required></div>
  <div><label>Discount (₹)</label><input id="sDiscount" type="number" min="0" value="0" step=".01"></div>
  <div><label>Delivery Charge (₹)</label><input id="sDelivery" type="number" min="0" value="0" step=".01"></div>
  <div><label>Delivery Cost (₹)</label><input id="sDeliveryCost" type="number" min="0" value="0" step=".01"></div>
  <div><label>Payment Method</label><select id="sPayment"><option>Cash</option><option>Online / UPI</option><option>Bank Transfer</option><option>Credit / Pending</option></select></div>
  <div><label>ഇപ്പോൾ ലഭിച്ച തുക (₹)</label><input id="sPaid" type="number" min="0" step=".01" value="0"></div>
  <div class="card"><small>Bill Total</small><div class="amount" id="billPreview">₹0</div><small id="profitPreview">ലാഭം: ₹0</small></div>
  <div class="full actions"><button class="green" type="submit">വിൽപ്പന സേവ് ചെയ്യുക</button><button type="reset" class="gold">Clear</button></div>
 </form>
 </div>
 <h3>Sales Register</h3>
 <input id="salesSearch" placeholder="ബിൽ നമ്പർ / പേര് / ഫോൺ തിരയുക" style="max-width:400px">
 <div id="salesTable" class="table-wrap"></div>
</section>

<section id="products" class="page">
 <h2>Products & Stock</h2>
 <div class="panel"><h3>ഉൽപ്പന്നം ചേർക്കുക</h3>
 <form id="productForm">
  <div><label>Product Name</label><input id="pName" required></div>
  <div><label>Product Code</label><input id="pCode"></div>
  <div><label>Supplier</label><select id="pSupplier"></select></div>
  <div><label>Cost Price</label><input id="pCost" type="number" min="0" step=".01" required></div>
  <div><label>MRP</label><input id="pMrp" type="number" min="0" step=".01" required></div>
  <div><label>Selling Price</label><input id="pPrice" type="number" min="0" step=".01" required></div>
  <div><label>Opening Stock</label><input id="pStock" type="number" min="0" required></div>
  <div><label>Low Stock Alert At</label><input id="pMin" type="number" min="0" value="3"></div>
  <div class="full"><button class="green">ഉൽപ്പന്നം ചേർക്കുക</button></div>
 </form></div>
 <div id="productsTable" class="table-wrap"></div>
 <div class="panel"><h3>പുതിയ സ്റ്റോക്ക് വാങ്ങുക</h3>
 <form id="stockForm">
  <div><label>Product</label><select id="stProduct" required></select></div>
  <div><label>Qty വാങ്ങിയത്</label><input id="stQty" type="number" min="1" required></div>
  <div><label>Unit Cost</label><input id="stCost" type="number" min="0" step=".01" required></div>
  <div><label>Supplier Invoice / Note</label><input id="stNote"></div>
  <div class="full"><button class="green">സ്റ്റോക്ക് ചേർക്കുക</button></div>
 </form></div>
 <div id="stockHistory" class="table-wrap"></div>
</section>

<section id="customers" class="page">
 <h2>Customers & Receivables</h2>
 <div class="panel"><form id="customerForm">
  <div><label>Customer Name</label><input id="cName" required></div>
  <div><label>Phone</label><input id="cPhone"></div>
  <div><label>Address</label><input id="cAddress"></div>
  <div class="full"><button class="green">Customer ചേർക്കുക</button></div>
 </form></div>
 <div id="customersTable" class="table-wrap"></div>
 <div class="panel"><h3>കുടിശ്ശിക പേയ്മെന്റ് രേഖപ്പെടുത്തുക</h3>
 <form id="customerPaymentForm">
  <div><label>Customer</label><select id="cpCustomer" required></select></div>
  <div><label>ലഭിച്ച തുക (₹)</label><input id="cpAmount" type="number" min=".01" step=".01" required></div>
  <div><label>തീയതി</label><input id="cpDate" type="date" required></div>
  <div><label>Note</label><input id="cpNote"></div>
  <div class="full"><button class="green">പേയ്മെന്റ് രേഖപ്പെടുത്തുക</button></div>
 </form></div>
 <div id="customerPaymentsTable" class="table-wrap"></div>
</section>

<section id="suppliers" class="page">
 <h2>Suppliers & Payables</h2>
 <div class="panel"><h3>Supplier ചേർക്കുക</h3><form id="supplierForm">
  <div><label>Supplier Name</label><input id="suName" required></div>
  <div><label>Phone</label><input id="suPhone"></div>
  <div><label>വിലാസം</label><input id="suAddress"></div>
  <div class="full"><button class="green">Supplier ചേർക്കുക</button></div>
 </form></div>
 <div id="suppliersTable" class="table-wrap"></div>
 <div class="panel"><h3>Supplier-ന് പണം നൽകിയ രേഖ</h3><form id="supplierPaymentForm">
  <div><label>Supplier</label><select id="spSupplier" required></select></div>
  <div><label>തുക (₹)</label><input id="spAmount" type="number" min=".01" step=".01" required></div>
  <div><label>തീയതി</label><input id="spDate" type="date" required></div>
  <div><label>Note</label><input id="spNote"></div>
  <div class="full"><button class="green">Payment രേഖപ്പെടുത്തുക</button></div>
 </form></div>
 <div id="supplierPaymentsTable" class="table-wrap"></div>
</section>

<section id="expenses" class="page">
 <h2>Expenses Register</h2>
 <div class="panel"><form id="expenseForm">
  <div><label>Date</label><input id="eDate" type="date" required></div>
  <div><label>Category</label><select id="eCategory">
   <option>Shop Rent</option><option>Electricity / Bills</option><option>Staff Salary</option>
   <option>Vehicle / Petrol</option><option>Packing / Printing</option><option>Delivery Cost</option><option>Other Expenses</option>
  </select></div>
  <div><label>Description</label><input id="eNote"></div>
  <div><label>Amount (₹)</label><input id="eAmount" type="number" min=".01" step=".01" required></div>
  <div class="full"><button class="green">ചെലവ് സേവ് ചെയ്യുക</button></div>
 </form></div>
 <div id="expensesTable" class="table-wrap"></div>
</section>

<section id="partners" class="page">
 <h2>Four Partners Accounting</h2>
 <div class="notice">ലാഭവിഹിതം കണക്കാക്കുന്നതിന് മുമ്പ് ചെലവുകളും വിൽപ്പനയും പരിശോധിക്കുക. ഉടമകൾ തമ്മിൽ തീരുമാനിച്ച ശതമാനങ്ങൾ മാത്രം നൽകുക.</div>
 <div class="panel"><h3>പാർട്ണർ വിവരങ്ങൾ</h3><form id="partnerForm">
  <div><label>Partner 1 Name</label><input id="ptName0" required></div><div><label>Share %</label><input id="ptShare0" type="number" min="0" max="100" step=".01" required></div>
  <div><label>Partner 2 Name</label><input id="ptName1" required></div><div><label>Share %</label><input id="ptShare1" type="number" min="0" max="100" step=".01" required></div>
  <div><label>Partner 3 Name</label><input id="ptName2" required></div><div><label>Share %</label><input id="ptShare2" type="number" min="0" max="100" step=".01" required></div>
  <div><label>Partner 4 Name</label><input id="ptName3" required></div><div><label>Share %</label><input id="ptShare3" type="number" min="0" max="100" step=".01" required></div>
  <div class="full"><button class="green">പാർട്ണർമാരെ സേവ് ചെയ്യുക</button></div>
 </form></div>
 <div class="panel"><h3>നിക്ഷേപം / പണം പിൻവലിക്കൽ</h3><form id="partnerTxnForm">
  <div><label>Partner</label><select id="ptWho" required></select></div>
  <div><label>Transaction Type</label><select id="ptType"><option value="investment">നിക്ഷേപം</option><option value="withdrawal">പണം പിൻവലിക്കൽ</option></select></div>
  <div><label>Amount (₹)</label><input id="ptAmount" type="number" min=".01" step=".01" required></div>
  <div><label>Date</label><input id="ptDate" type="date" required></div>
  <div><label>Note</label><input id="ptNote"></div>
  <div class="full"><button class="green">Transaction സേവ് ചെയ്യുക</button></div>
 </form></div>
 <div id="partnerSummary"></div>
 <h3>Partner Transaction Ledger</h3><div id="partnerLedger" class="table-wrap"></div>
</section>

<section id="reports" class="page">
 <h2>Monthly Reports</h2>
 <div class="panel"><label>മാസം തിരഞ്ഞെടുക്കുക</label><input id="reportMonth" type="month" style="max-width:260px">
 <div class="cards">
  <div class="card"><small>Product Sales (after discount)</small><div class="amount" id="rSales">₹0</div></div>
  <div class="card"><small>Delivery Collected</small><div class="amount" id="rDelivery">₹0</div></div>
  <div class="card"><small>Cost of Goods Sold</small><div class="amount" id="rCost">₹0</div></div>
  <div class="card"><small>Product Gross Profit</small><div class="amount" id="rGross">₹0</div></div>
  <div class="card"><small>Expenses</small><div class="amount" id="rExpenses">₹0</div></div>
  <div class="card"><small>Net Profit</small><div class="amount" id="rNet">₹0</div></div>
 </div>
 <p class="muted">കണക്കുകൾ: ഉൽപ്പന്ന ലാഭം = വിറ്റ വില − ഡിസ്‌കൗണ്ട് − വിറ്റ ഉൽപ്പന്നങ്ങളുടെ വാങ്ങൽ ചെലവ്. അറ്റലാഭം = ഉൽപ്പന്ന ലാഭം − രേഖപ്പെടുത്തിയ ചെലവുകൾ. ഡെലിവറി വരവും ചെലവും വേർതിരിച്ച് പരിശോധിക്കുക.</p>
 <div id="categorySummary"></div><button onclick="window.print()" class="no-print">റിപ്പോർട്ട് പ്രിന്റ് ചെയ്യുക</button>
 </div>
</section>

<section id="settings" class="page">
 <h2>Settings / Backup</h2>
 <div class="panel"><form id="settingsForm">
  <div><label>Store Name</label><input id="setStore" required></div>
  <div><label>Phone</label><input id="setPhone"></div>
  <div><label>Address</label><input id="setAddress"></div>
  <div><label>Invoice Prefix</label><input id="setPrefix" required></div>
  <div class="full"><label>Return / Exchange Policy</label><textarea id="setPolicy" rows="2"></textarea></div>
  <div class="full"><button class="green">Settings സേവ് ചെയ്യുക</button></div>
 </form></div>
 <div class="panel"><h3>Data Backup</h3><p class="muted">നിന്റെ ഡാറ്റ ബ്രൗസറിൽ മാത്രം സൂക്ഷിക്കുന്നു. ഇടയ്ക്കിടെ ബാക്കപ്പ് എടുക്കുക.</p>
  <div class="actions"><button onclick="backup()">JSON Backup Download</button><button class="gold" onclick="document.getElementById('restore').click()">Restore Backup</button><input id="restore" type="file" accept=".json" class="hidden"><button onclick="exportCSV()">Sales CSV Export</button><button class="red" onclick="resetAll()">Reset All Data</button></div>
 </div>
</section>

<section id="invoicePrint" class="page"><div id="invoiceContent"></div></section>
</main>

<div id="presentation" class="hidden">
 <div class="actions no-print"><button onclick="closePresentation()">← Back to Website</button><button onclick="window.print()">Print Presentation</button></div>
 <h1 id="presStore">QafilaTimes</h1><p id="presDate"></p>
 <div class="cards">
  <div class="card"><small>ആകെ വിൽപ്പന</small><div class="amount" id="prSales"></div></div>
  <div class="card"><small>ഉൽപ്പന്ന ലാഭം</small><div class="amount" id="prProfit"></div></div>
  <div class="card"><small>മറ്റ് ചെലവുകൾ</small><div class="amount" id="prExpense"></div></div>
  <div class="card"><small>അറ്റലാഭം</small><div class="amount" id="prNet"></div></div>
  <div class="card"><small>നിക്ഷേപം</small><div class="amount" id="prInvest"></div></div>
  <div class="card"><small>Customer Pending</small><div class="amount" id="prPending"></div></div>
 </div>
 <h2>Partner Profit Share</h2><div id="presPartners"></div>
 <h2>Stock Status</h2><div id="presStock"></div>
</div>

<script>
const KEY="QT_COMPLETE_MANAGER_V2";
const fresh=()=>({
 products:[],sales:[],expenses:[],customers:[],suppliers:[],
 customerPayments:[],supplierPayments:[],partnerTxns:[],stockHistory:[],
 partners:[{name:"Partner 1",share:25},{name:"Partner 2",share:25},{name:"Partner 3",share:25},{name:"Partner 4",share:25}],
 settings:{store:"QafilaTimes",phone:"",address:"",prefix:"QT",policy:"Please contact us for return / exchange policy."},
 nextInvoice:1
});
let db=load();
function load(){try{return {...fresh(),...JSON.parse(localStorage.getItem(KEY)||"{}")}}catch(e){return fresh()}}
function save(){localStorage.setItem(KEY,JSON.stringify(db));renderAll()}
function money(n){return "₹"+(Number(n)||0).toLocaleString("en-IN",{minimumFractionDigits:2,maximumFractionDigits:2})}
function esc(v){return String(v??"").replace(/[&<>"']/g,c=>({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"}[c]))}
function el(id){return document.getElementById(id)}
function val(id){return el(id).value}
function set(id,v){el(id).value=v}
function today(){return new Date().toISOString().slice(0,10)}
function uid(){return Date.now().toString(36)+Math.random().toString(36).slice(2,7)}
function sum(a,f){return a.reduce((n,x)=>n+Number(f(x)||0),0)}
function table(headers,rows){return rows.length?'<table><thead><tr>'+headers.map(h=>'<th>'+h+'</th>').join("")+'</tr></thead><tbody>'+rows.join("")+'</tbody></table>':'<p class="muted">രേഖകളൊന്നുമില്ല.</p>'}
function go(id){document.querySelectorAll(".page").forEach(x=>x.classList.remove("active"));document.querySelectorAll(".tab").forEach(x=>x.classList.toggle("active",x.dataset.page===id));el(id).classList.add("active");renderAll();window.scrollTo(0,0)}
document.querySelectorAll(".tab").forEach(b=>b.onclick=()=>go(b.dataset.page));
["sDate","eDate","cpDate","spDate","ptDate"].forEach(id=>set(id,today()));
set("reportMonth",today().slice(0,7));el("dateNow").textContent=new Date().toLocaleDateString("en-IN");

function salesTotals(list){
 return {bills:sum(list,s=>s.total),productSales:sum(list,s=>s.subtotal-s.discount),delivery:sum(list,s=>s.delivery),
 deliveryCost:sum(list,s=>s.deliveryCost),cost:sum(list,s=>s.cost*s.qty),
 profit:sum(list,s=>s.subtotal-s.discount-s.cost*s.qty),
 pending:sum(list,s=>Math.max(0,s.total-s.paid))};
}
function expenseTotal(list){return sum(list,e=>e.amount)}
function totalInvest(){return sum(db.partnerTxns.filter(t=>t.type==="investment"),t=>t.amount)}
function totalWithdraw(){return sum(db.partnerTxns.filter(t=>t.type==="withdrawal"),t=>t.amount)}
function customerBalance(c){return sum(db.sales.filter(s=>s.customerId===c.id),s=>s.total)-sum(db.customerPayments.filter(p=>p.customerId===c.id),p=>p.amount)}
function supplierBalance(s){return sum(db.stockHistory.filter(h=>h.supplierId===s.id),h=>h.cost*h.qty)-sum(db.supplierPayments.filter(p=>p.supplierId===s.id),p=>p.amount)}
function allExpenses(list){return expenseTotal(list)}
function netProfit(list,expenses){return salesTotals(list).profit-expenseTotal(expenses)}
function renderAll(){renderOptions();renderProducts();renderSales();renderCustomers();renderSuppliers();renderExpenses();renderPartners();renderDashboard();renderReport();loadSettings()}

function renderOptions(){
 const options=(arr,placeholder,labelFn)=>'<option value="">'+placeholder+'</option>'+arr.map(x=>`<option value="${esc(x.id)}">${esc(labelFn(x))}</option>`).join("");
 setHTML("sProduct",options(db.products,"ഉൽപ്പന്നം തിരഞ്ഞെടുക്കുക",p=>p.name+" · Stock "+p.stock));
 setHTML("stProduct",options(db.products,"ഉൽപ്പന്നം തിരഞ്ഞെടുക്കുക",p=>p.name));
 setHTML("pSupplier",options(db.suppliers,"Supplier (ഐച്ഛികം)",s=>s.name));
 setHTML("cpCustomer",options(db.customers,"Customer തിരഞ്ഞെടുക്കുക",c=>c.name+" · "+(c.phone||"")));
 setHTML("spSupplier",options(db.suppliers,"Supplier തിരഞ്ഞെടുക്കുക",s=>s.name));
 setHTML("ptWho",'<option value="">Partner തിരഞ്ഞെടുക്കുക</option>'+db.partners.map((p,i)=>`<option value="${i}">${esc(p.name)}</option>`).join(""));
}
function setHTML(id,html){el(id).innerHTML=html}

el("sProduct").onchange=()=>{
 const p=db.products.find(x=>x.id===val("sProduct"));if(!p)return;
 set("sCost",p.cost);set("sMrp",p.mrp);set("sPrice",p.price);updatePreview();
};
["sQty","sCost","sPrice","sDiscount","sDelivery","sDeliveryCost"].forEach(id=>el(id).addEventListener("input",updatePreview));
function updatePreview(){
 const q=+val("sQty")||0,c=+val("sCost")||0,p=+val("sPrice")||0,d=+val("sDiscount")||0,del=+val("sDelivery")||0;
 el("billPreview").textContent=money(Math.max(0,q*p-d+del));
 el("profitPreview").textContent="ഉൽപ്പന്ന ലാഭം: "+money(q*p-d-q*c)+" · ഡെലിവറി വരവ്: "+money(del);
}
el("saleForm").onsubmit=e=>{
 e.preventDefault();
 const p=db.products.find(x=>x.id===val("sProduct"));if(!p)return alert("ഉൽപ്പന്നം ചേർക്കുക.");
 const qty=+val("sQty"),cost=+val("sCost"),price=+val("sPrice"),discount=+val("sDiscount"),delivery=+val("sDelivery"),deliveryCost=+val("sDeliveryCost"),paid=+val("sPaid");
 const subtotal=qty*price,total=subtotal-discount+delivery;
 if(qty<=0||discount<0||discount>subtotal||delivery<0||deliveryCost<0||paid<0||paid>total)return alert("എണ്ണം, ഡിസ്‌കൗണ്ട്, പേയ്മെന്റ് എന്നിവ പരിശോധിക്കുക.");
 if(p.stock<qty&&!confirm("സ്റ്റോക്ക് കുറവാണ്. വിൽപ്പന തുടരണമോ?"))return;
 let c=db.customers.find(x=>x.phone&&x.phone===val("sPhone").trim());
 if(!c){c={id:uid(),name:val("sCustomer").trim(),phone:val("sPhone").trim(),address:val("sAddress").trim()};db.customers.push(c)}
 else{c.name=val("sCustomer").trim();c.address=val("sAddress").trim()}
 const s={id:uid(),invoice:db.settings.prefix+"-"+String(db.nextInvoice++).padStart(5,"0"),date:val("sDate"),customerId:c.id,customer:c.name,phone:c.phone,address:c.address,productId:p.id,product:p.name,qty,cost,mrp:+val("sMrp")||0,price,subtotal,discount,delivery,deliveryCost,total,paid,payment:val("sPayment")};
 db.sales.unshift(s);p.stock-=qty;
 if(deliveryCost>0)db.expenses.push({id:uid(),date:s.date,category:"Delivery Cost",note:"Delivery for "+s.invoice,amount:deliveryCost,linkedSale:s.id});
 save();e.target.reset();["sDate"].forEach(id=>set(id,today()));set("sQty",1);set("sDiscount",0);set("sDelivery",0);set("sDeliveryCost",0);set("sPaid",0);alert("വിൽപ്പന സേവ് ചെയ്തു.");
 if(confirm("Invoice പ്രിന്റ് ചെയ്യണോ?"))printInvoice(s.id);
};
function renderSales(){
 const q=(val("salesSearch")||"").toLowerCase();
 const list=db.sales.filter(s=>[s.invoice,s.customer,s.phone,s.product].join(" ").toLowerCase().includes(q));
 setHTML("salesTable",table(["Invoice","Date","Customer","Product","Qty","Profit","Delivery","Bill Total","Paid / Due","Action"],list.map(s=>`<tr><td>${esc(s.invoice)}</td><td>${esc(s.date)}</td><td>${esc(s.customer)}<br>${esc(s.phone)}</td><td>${esc(s.product)}</td><td>${s.qty}</td><td>${money(s.subtotal-s.discount-s.cost*s.qty)}</td><td>${money(s.delivery)}</td><td>${money(s.total)}</td><td>${money(s.paid)} / ${money(Math.max(0,s.total-s.paid))}</td><td><button onclick="printInvoice('${s.id}')">Bill</button> <button onclick="recordSalePayment('${s.id}')">Payment</button> <button class="red" onclick="deleteSale('${s.id}')">Delete</button></td></tr>`)));
}
el("salesSearch").oninput=renderSales;
function recordSalePayment(id){
 const s=db.sales.find(x=>x.id===id);if(!s)return;
 const due=s.total-s.paid;if(due<=0)return alert("ഈ ബില്ലിന് കുടിശ്ശികയില്ല.");
 const v=prompt("ബാക്കി തുക: "+money(due)+"\nഇപ്പോൾ ലഭിച്ച തുക നൽകുക:");
 if(v===null)return;const n=Number(v);if(!Number.isFinite(n)||n<=0||n>due)return alert("ശരിയായ തുക നൽകുക.");
 s.paid+=n;save();alert("Payment രേഖപ്പെടുത്തി.");
}
function deleteSale(id){
 const s=db.sales.find(x=>x.id===id);if(!s)return;
 if(!confirm("ഈ ബിൽ നീക്കം ചെയ്യണോ? സ്റ്റോക്ക് തിരികെ കൂട്ടും."))return;
 const p=db.products.find(x=>x.id===s.productId);if(p)p.stock+=s.qty;
 db.expenses=db.expenses.filter(e=>e.linkedSale!==id);db.sales=db.sales.filter(x=>x.id!==id);save();
}
el("productForm").onsubmit=e=>{
 e.preventDefault();const code=val("pCode").trim()||("QT"+Date.now().toString().slice(-6));
 if(db.products.some(p=>p.code===code))return alert("ഈ Product Code നിലവിലുണ്ട്.");
 db.products.push({id:uid(),name:val("pName").trim(),code,supplierId:val("pSupplier"),cost:+val("pCost"),mrp:+val("pMrp"),price:+val("pPrice"),stock:+val("pStock"),min:+val("pMin")||0});
 save();e.target.reset();alert("ഉൽപ്പന്നം ചേർത്തു.");
};
function renderProducts(){
 setHTML("productsTable",table(["Code","Product","Supplier","Cost","MRP","Selling","Stock","Action"],db.products.map(p=>`<tr><td>${esc(p.code)}</td><td>${esc(p.name)}</td><td>${esc(db.suppliers.find(s=>s.id===p.supplierId)?.name||"-")}</td><td>${money(p.cost)}</td><td>${money(p.mrp)}</td><td>${money(p.price)}</td><td>${p.stock} ${p.stock<=p.min?'<b style="color:#c0392b">LOW STOCK</b>':""}</td><td><button onclick="adjustStock('${p.id}')">Edit Stock</button> <button class="red" onclick="deleteProduct('${p.id}')">Delete</button></td></tr>`)));
 setHTML("stockHistory",table(["Date","Product","Qty","Unit Cost","Supplier / Note"],db.stockHistory.map(h=>`<tr><td>${esc(h.date)}</td><td>${esc(h.product)}</td><td>${h.qty}</td><td>${money(h.cost)}</td><td>${esc(h.supplierName||h.note||"-")}</td></tr>`)));
}
function adjustStock(id){const p=db.products.find(x=>x.id===id);const v=prompt("പുതിയ സ്റ്റോക്ക് എണ്ണം",p.stock);if(v===null)return;if(!Number.isFinite(+v)||+v<0)return alert("ശരിയായ എണ്ണം നൽകുക.");p.stock=+v;save()}
function deleteProduct(id){if(db.sales.some(s=>s.productId===id))return alert("ഈ ഉൽപ്പന്നത്തിന് വിൽപ്പന ചരിത്രമുണ്ട്. Delete ചെയ്യാൻ കഴിയില്ല.");if(confirm("ഉൽപ്പന്നം നീക്കം ചെയ്യണോ?")){db.products=db.products.filter(p=>p.id!==id);save()}}
el("stockForm").onsubmit=e=>{
 e.preventDefault();const p=db.products.find(x=>x.id===val("stProduct"));if(!p)return;
 const qty=+val("stQty"),cost=+val("stCost");p.stock+=qty;p.cost=cost;
 db.stockHistory.unshift({id:uid(),date:today(),product:p.name,productId:p.id,qty,cost,supplierId:p.supplierId,supplierName:db.suppliers.find(s=>s.id===p.supplierId)?.name||"",note:val("stNote")});
 save();e.target.reset();alert("സ്റ്റോക്ക് ചേർത്തു.");
};
el("customerForm").onsubmit=e=>{e.preventDefault();db.customers.push({id:uid(),name:val("cName").trim(),phone:val("cPhone").trim(),address:val("cAddress").trim()});save();e.target.reset()};
function renderCustomers(){
 setHTML("customersTable",table(["Customer","Phone","Address","Total Bills","Paid","Balance"],db.customers.map(c=>{
 const ss=db.sales.filter(s=>s.customerId===c.id);
 const paidSales=sum(ss,s=>s.paid),extra=sum(db.customerPayments.filter(p=>p.customerId===c.id),p=>p.amount);
 return `<tr><td>${esc(c.name)}</td><td>${esc(c.phone)}</td><td>${esc(c.address)}</td><td>${money(sum(ss,s=>s.total))}</td><td>${money(paidSales+extra)}</td><td>${money(Math.max(0,sum(ss,s=>s.total)-paidSales-extra))}</td></tr>`;
 })));
 setHTML("customerPaymentsTable",table(["Date","Customer","Amount","Note"],db.customerPayments.map(p=>`<tr><td>${esc(p.date)}</td><td>${esc(db.customers.find(c=>c.id===p.customerId)?.name||"")}</td><td>${money(p.amount)}</td><td>${esc(p.note)}</td></tr>`)));
}
el("customerPaymentForm").onsubmit=e=>{
 e.preventDefault();const c=db.customers.find(x=>x.id===val("cpCustomer"));if(!c)return;
 const amount=+val("cpAmount"),due=customerBalance(c);if(amount<=0||amount>due)return alert("കുടിശ്ശിക പരിശോധിക്കുക. നിലവിലെ കുടിശ്ശിക: "+money(due));
 db.customerPayments.unshift({id:uid(),customerId:c.id,amount,date:val("cpDate"),note:val("cpNote")});save();e.target.reset();set("cpDate",today());alert("Payment രേഖപ്പെടുത്തി.");
};
el("supplierForm").onsubmit=e=>{e.preventDefault();db.suppliers.push({id:uid(),name:val("suName").trim(),phone:val("suPhone").trim(),address:val("suAddress").trim()});save();e.target.reset()};
function renderSuppliers(){
 setHTML("suppliersTable",table(["Supplier","Phone","Address","Stock Purchases","Paid","Balance"],db.suppliers.map(s=>{
 const total=sum(db.stockHistory.filter(h=>h.supplierId===s.id),h=>h.qty*h.cost),paid=sum(db.supplierPayments.filter(p=>p.supplierId===s.id),p=>p.amount);
 return `<tr><td>${esc(s.name)}</td><td>${esc(s.phone)}</td><td>${esc(s.address)}</td><td>${money(total)}</td><td>${money(paid)}</td><td>${money(Math.max(0,total-paid))}</td></tr>`;
 })));
 setHTML("supplierPaymentsTable",table(["Date","Supplier","Amount","Note"],db.supplierPayments.map(p=>`<tr><td>${esc(p.date)}</td><td>${esc(db.suppliers.find(s=>s.id===p.supplierId)?.name||"")}</td><td>${money(p.amount)}</td><td>${esc(p.note)}</td></tr>`)));
}
el("supplierPaymentForm").onsubmit=e=>{
 e.preventDefault();const s=db.suppliers.find(x=>x.id===val("spSupplier"));if(!s)return;
 const amount=+val("spAmount"),due=supplierBalance(s);if(amount<=0||amount>due)return alert("Supplier balance പരിശോധിക്കുക. രേഖപ്പെടുത്തിയ ബാലൻസ്: "+money(due));
 db.supplierPayments.unshift({id:uid(),supplierId:s.id,amount,date:val("spDate"),note:val("spNote")});save();e.target.reset();set("spDate",today());alert("Supplier payment രേഖപ്പെടുത്തി.");
};
el("expenseForm").onsubmit=e=>{e.preventDefault();db.expenses.unshift({id:uid(),date:val("eDate"),category:val("eCategory"),note:val("eNote"),amount:+val("eAmount")});save();e.target.reset();set("eDate",today());alert("ചെലവ് സേവ് ചെയ്തു.")};
function renderExpenses(){
 setHTML("expensesTable",table(["Date","Category","Description","Amount","Action"],db.expenses.map(x=>`<tr><td>${esc(x.date)}</td><td>${esc(x.category)}</td><td>${esc(x.note)}</td><td>${money(x.amount)}</td><td><button class="red" onclick="deleteExpense('${x.id}')">Delete</button></td></tr>`)));
}
function deleteExpense(id){if(confirm("ചെലവ് നീക്കം ചെയ്യണോ?")){db.expenses=db.expenses.filter(x=>x.id!==id);save()}}
el("partnerForm").onsubmit=e=>{
 e.preventDefault();const arr=[0,1,2,3].map(i=>({name:val("ptName"+i).trim(),share:+val("ptShare"+i)})),total=sum(arr,p=>p.share);
 if(Math.abs(total-100)>.01)return alert("നാല് ശതമാനങ്ങളും ചേർത്താൽ 100% ആകണം. ഇപ്പോൾ "+total+"% ആണ്.");
 db.partners=arr;save();alert("Partner വിവരങ്ങൾ സേവ് ചെയ്തു.");
};
function renderPartners(){
 db.partners.forEach((p,i)=>{set("ptName"+i,p.name);set("ptShare"+i,p.share)});
 const profit=netProfit(db.sales,db.expenses);
 setHTML("partnerSummary",'<div class="cards">'+db.partners.map((p,i)=>{
 const tx=db.partnerTxns.filter(t=>t.partner===i),invest=sum(tx.filter(t=>t.type==="investment"),t=>t.amount),withdraw=sum(tx.filter(t=>t.type==="withdrawal"),t=>t.amount);
 return `<div class="card"><h3>${esc(p.name)}</h3><p>Share: ${p.share}%</p><p>നിക്ഷേപം: <b>${money(invest)}</b></p><p>പിൻവലിച്ചത്: <b>${money(withdraw)}</b></p><p>Profit share: <b>${money(profit*p.share/100)}</b></p></div>`;
 }).join("")+'</div><div class="notice">കണക്കാക്കിയ ലാഭവിഹിതം സ്വയം പണം വിതരണം ചെയ്തതായി അർത്ഥമാക്കില്ല. വിതരണം ചെയ്ത തുക പ്രത്യേകം രേഖപ്പെടുത്തണം.</div>');
 setHTML("partnerLedger",table(["Date","Partner","Type","Amount","Note"],db.partnerTxns.map(t=>`<tr><td>${esc(t.date)}</td><td>${esc(db.partners[t.partner]?.name||"")}</td><td>${t.type==="investment"?"നിക്ഷേപം":"പണം പിൻവലിക്കൽ"}</td><td>${money(t.amount)}</td><td>${esc(t.note)}</td></tr>`)));
}
el("partnerTxnForm").onsubmit=e=>{
 e.preventDefault();if(val("ptWho")==="")return;
 db.partnerTxns.unshift({id:uid(),partner:+val("ptWho"),type:val("ptType"),amount:+val("ptAmount"),date:val("ptDate"),note:val("ptNote")});save();e.target.reset();set("ptDate",today());alert("Partner transaction സേവ് ചെയ്തു.");
};
function renderDashboard(){
 const t=salesTotals(db.sales),ex=expenseTotal(db.expenses),net=t.profit-ex;
 set("dSales",money(t.bills));set("dProfit",money(t.profit));set("dExpense",money(ex));set("dNet",money(net));set("dInvest",money(totalInvest()));set("dPending",money(sum(db.customers,c=>Math.max(0,customerBalance(c)))));set("dPayable",money(sum(db.suppliers,s=>Math.max(0,supplierBalance(s)))));set("dStock",sum(db.products,p=>p.stock));
 const m=today().slice(0,7),ms=db.sales.filter(s=>s.date.startsWith(m)),me=db.expenses.filter(x=>x.date.startsWith(m)),mt=salesTotals(ms);
 setHTML("monthStats",`<p>ഈ മാസത്തെ ബിൽ തുക: <b>${money(mt.bills)}</b> · ഉൽപ്പന്ന ലാഭം: <b>${money(mt.profit)}</b> · ചെലവ്: <b>${money(expenseTotal(me))}</b> · അറ്റലാഭം: <b>${money(netProfit(ms,me))}</b></p>`);
 setHTML("recentSales",table(["Invoice","Date","Customer","Total"],db.sales.slice(0,7).map(s=>`<tr><td>${esc(s.invoice)}</td><td>${esc(s.date)}</td><td>${esc(s.customer)}</td><td>${money(s.total)}</td></tr>`)));
}
el("reportMonth").onchange=renderReport;
function renderReport(){
 const m=val("reportMonth")||today().slice(0,7),ss=db.sales.filter(s=>s.date.startsWith(m)),ee=db.expenses.filter(e=>e.date.startsWith(m)),t=salesTotals(ss);
 set("rSales",money(t.productSales));set("rDelivery",money(t.delivery));set("rCost",money(t.cost));set("rGross",money(t.profit));set("rExpenses",money(expenseTotal(ee)));set("rNet",money(netProfit(ss,ee)));
 const cats={};ee.forEach(e=>cats[e.category]=(cats[e.category]||0)+Number(e.amount));
 setHTML("categorySummary",'<h3>ചെലവ് വിഭാഗങ്ങൾ</h3>'+table(["Category","Amount"],Object.entries(cats).map(([k,v])=>`<tr><td>${esc(k)}</td><td>${money(v)}</td></tr>`)));
}
el("settingsForm").onsubmit=e=>{e.preventDefault();db.settings={store:val("setStore").trim(),phone:val("setPhone").trim(),address:val("setAddress").trim(),prefix:val("setPrefix").trim()||"QT",policy:val("setPolicy").trim()};save();alert("Settings സേവ് ചെയ്തു.")};
function loadSettings(){set("setStore",db.settings.store||"QafilaTimes");set("setPhone",db.settings.phone||"");set("setAddress",db.settings.address||"");set("setPrefix",db.settings.prefix||"QT");set("setPolicy",db.settings.policy||"")}
function printInvoice(id){
 const s=db.sales.find(x=>x.id===id);if(!s)return;
 setHTML("invoiceContent",`<div style="max-width:760px;margin:20px auto;font-family:Arial;color:#222"><h1>${esc(db.settings.store)}</h1><p>${esc(db.settings.address)}<br>Phone: ${esc(db.settings.phone)}</p><hr><h2>INVOICE</h2><p>Invoice: ${esc(s.invoice)} · Date: ${esc(s.date)}</p><p>Customer: ${esc(s.customer)}<br>Phone: ${esc(s.phone)}<br>Address: ${esc(s.address)}</p>${table(["Product","Qty","Unit Price","Amount"],[`<tr><td>${esc(s.product)}</td><td>${s.qty}</td><td>${money(s.price)}</td><td>${money(s.subtotal)}</td></tr>`])}<p>Discount: ${money(s.discount)}<br>Delivery charge: ${money(s.delivery)}</p><h2>Total: ${money(s.total)}</h2><p>Paid: ${money(s.paid)} · Balance: ${money(Math.max(0,s.total-s.paid))}</p><p>Payment: ${esc(s.payment)}</p><p>${esc(db.settings.policy)}</p><p style="margin-top:50px;text-align:right">Signature: __________________</p></div>`);
 document.querySelectorAll(".page").forEach(x=>x.classList.remove("active"));el("invoicePrint").classList.add("active");window.print();el("invoicePrint").classList.remove("active");go("sales");
}
function exportCSV(){
 const rows=[["Invoice","Date","Customer","Phone","Product","Qty","Cost","MRP","Selling","Discount","Delivery","Delivery Cost","Total","Paid","Due","Profit","Payment"]];
 db.sales.forEach(s=>rows.push([s.invoice,s.date,s.customer,s.phone,s.product,s.qty,s.cost,s.mrp,s.price,s.discount,s.delivery,s.deliveryCost,s.total,s.paid,Math.max(0,s.total-s.paid),s.subtotal-s.discount-s.cost*s.qty,s.payment]));
 const csv="\uFEFF"+rows.map(r=>r.map(v=>'"'+String(v??"").replace(/"/g,'""')+'"').join(",")).join("\r\n");
 downloadBlob(csv,"QafilaTimes-sales.csv","text/csv;charset=utf-8");
}
function downloadBlob(content,name,type){const a=document.createElement("a"),u=URL.createObjectURL(new Blob([content],{type}));a.href=u;a.download=name;a.click();setTimeout(()=>URL.revokeObjectURL(u),1000)}
function backup(){downloadBlob(JSON.stringify(db,null,2),"QafilaTimes-backup-"+today()+".json","application/json")}
el("restore").onchange=async e=>{
 const f=e.target.files[0];if(!f)return;
 try{const x=JSON.parse(await f.text());if(!Array.isArray(x.products)||!Array.isArray(x.sales)||!Array.isArray(x.partners))throw Error();if(!confirm("നിലവിലെ ഡാറ്റ മാറ്റി ഈ ബാക്കപ്പ് ലോഡ് ചെയ്യണോ?"))return;db={...fresh(),...x};save();alert("Backup restored.");}
 catch(err){alert("ശരിയായ ബാക്കപ്പ് JSON ഫയൽ തിരഞ്ഞെടുക്കുക.");}e.target.value="";
};
function resetAll(){if(!confirm("എല്ലാ ഡാറ്റയും മായ്ക്കണോ? ആദ്യം Backup എടുത്തിട്ടുണ്ടെന്ന് ഉറപ്പാക്കുക."))return;if(!confirm("അവസാന ഉറപ്പ്: തുടരട്ടേ?"))return;db=fresh();save();alert("ഡാറ്റ റീസെറ്റ് ചെയ്തു.")}
function showPresentation(){
 const t=salesTotals(db.sales),ex=expenseTotal(db.expenses),net=t.profit-ex;
 set("prSales",money(t.bills));set("prProfit",money(t.profit));set("prExpense",money(ex));set("prNet",money(net));set("prInvest",money(totalInvest()));set("prPending",money(sum(db.customers,c=>Math.max(0,customerBalance(c)))));
 set("presStore",db.settings.store);set("presDate","Business Review · "+new Date().toLocaleDateString("en-IN"));
 setHTML("presPartners",table(["Partner","Share","Investment","Profit Share"],db.partners.map((p,i)=>`<tr><td>${esc(p.name)}</td><td>${p.share}%</td><td>${money(sum(db.partnerTxns.filter(t=>t.partner===i&&t.type==="investment"),t=>t.amount))}</td><td>${money(net*p.share/100)}</td></tr>`)));
 setHTML("presStock",table(["Product","Code","Stock","Selling Price"],db.products.map(p=>`<tr><td>${esc(p.name)}</td><td>${esc(p.code)}</td><td>${p.stock}${p.stock<=p.min?" ⚠ Low":""}</td><td>${money(p.price)}</td></tr>`)));
 el("presentation").classList.remove("hidden");document.body.style.overflow="hidden";
}
function closePresentation(){el("presentation").classList.add("hidden");document.body.style.overflow=""}
renderAll();
</script>
</body>
</html>
