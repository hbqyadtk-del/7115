<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="utf-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>نظام إدارة شركة شعبيات الحارة</title>
<style>
  :root{
    --bg:#000000;
    --card:#111111;
    --text:#ffffff;
    --accent:#40e0d0;
    --muted:#bbbbbb;
    --danger:#ff5555;
    --good:#40e0d0;
    --glass: rgba(64, 224, 208, 0.08);
    --table-border:#40e0d0;
  }
  *{box-sizing:border-box;font-family:Arial,"Noto Naskh Arabic",sans-serif}
  body{margin:0;background:var(--bg);color:var(--text);direction:rtl}
  header{
    padding:18px;
    text-align:center;
    border-bottom:1px solid var(--table-border);
    background:linear-gradient(0deg, #0a0a0a, #111111);
  }
  h1{margin:0;font-size:20px;font-weight:900;color:var(--text)}
  .wrap{padding:18px;max-width:1200px;margin:0 auto}
  .muted{color:var(--muted);font-size:13px}
  .dash-grid{
    display:grid;
    grid-template-columns:repeat(3,1fr);
    gap:14px;
    margin-top:18px;
  }
  .dash-btn{
    background:var(--card);
    border:2px solid var(--table-border);
    padding:18px;
    border-radius:10px;
    cursor:pointer;
    text-align:center;
    box-shadow:0 8px 30px var(--glass);
    transition:transform .12s;
    color:var(--text);
  }
  .dash-btn:hover{
    transform:translateY(-6px);
    background:#1a1a1a;
  }
  .dash-emoji{font-size:26px;display:block;margin-bottom:6px}
  @media(max-width:900px){ .dash-grid{grid-template-columns:repeat(2,1fr)} }
  @media(max-width:560px){ .dash-grid{grid-template-columns:1fr} }
  .page{
    display:none;
    background:var(--card);
    padding:14px;
    border-radius:10px;
    margin:16px 0;
    box-shadow:0 10px 30px var(--glass);
    color:var(--text);
  }
  .page.active{display:block}
  .flex{display:flex;gap:8px;align-items:center}
  .btn{
    padding:8px 10px;
    border-radius:8px;
    border:1px solid var(--table-border);
    background:var(--card);
    color:var(--text);
    cursor:pointer;
    font-weight:700;
  }
  .btn.primary{
    background:var(--accent);
    color:#000000;
    border-color:var(--accent);
    font-weight:800;
  }
  .search{
    padding:8px;
    border:1px solid var(--table-border);
    width:100%;
    border-radius:6px;
    background:var(--card);
    color:var(--text);
  }
  table{
    width:100%;
    border-collapse:collapse;
    margin-top:8px;
  }
  th,td{
    padding:8px;
    border:1px solid var(--table-border);
    text-align:center;
    font-size:13px;
    color:var(--text);
  }
  th{
    background:#1a1a1a;
    color:var(--accent);
    font-weight:800;
  }
  .client-card{
    padding:8px;
    border-radius:8px;
    border:1px solid var(--table-border);
    background:#151515;
    margin-bottom:8px;
    color:var(--text);
  }
  label{
    display:block;
    margin-bottom:4px;
    font-size:13px;
    color:var(--text);
    font-weight:700;
  }
  input[type="text"], input[type="number"], select, textarea {
    width:100%;
    padding:8px;
    border-radius:6px;
    border:1px solid var(--table-border);
    background:var(--card);
    color:var(--text);
  }
  textarea{resize:vertical}
  .muted-note{color:var(--muted);font-size:12px;margin-top:6px}
  .small{font-size:12px;color:var(--muted)}
  .section-row{display:flex;gap:12px;align-items:flex-start;flex-wrap:wrap}
  .col{flex:1;min-width:240px}
  .right-col{width:420px}
  .prod-qty{
    width:80px;
    padding:6px;
    border-radius:6px;
    border:1px solid var(--table-border);
    text-align:center;
    background:var(--card);
    color:var(--text);
  }
  .overlay{
    position:fixed;
    left:0;top:0;right:0;bottom:0;
    background:rgba(0,0,0,0.6);
    z-index:80;
  }
  tr.clickable:hover{
    background:#1a1a1a;
    cursor:pointer;
  }
  .badge{
    display:inline-block;
    padding:4px 8px;
    border-radius:6px;
    background:var(--accent);
    color:#000000;
    font-weight:700;
  }
  .balance-positive{color:var(--good);font-weight:800}
  .balance-negative{color:var(--danger);font-weight:800}
  @media print {
    body *{visibility:hidden}
    #printArea, #printArea *{visibility:visible}
    #printArea{position:fixed;left:0;top:0;width:100%}
  }
  .logo-small{height:48px}
  .muted-tiny{font-size:11px;color:var(--muted)}
</style>
</head>
<body>
<header>
  <h1>نظام إدارة   شعبيات الحارة</h1>
  <div class="muted">نسخة محلية — كل البيانات مخزنة في متصفحك (LocalStorage)</div>
</header>
<div class="wrap">
  <!-- Dashboard -->
  <div id="dashboard" class="dash-grid">
    <div class="dash-btn" onclick="openPage('clientsPage')">
      <span class="dash-emoji">👥</span>
      <div style="font-weight:700">العملاء & الموردين</div>
      <div class="muted">إدارة سجلات</div>
    </div>
    <div class="dash-btn" onclick="openPage('inventoryPage')">
      <span class="dash-emoji">📦</span>
      <div style="font-weight:700">الأصناف & المخزون</div>
      <div class="muted">إضافة/تعديل/حذف الأصناف</div>
    </div>
    <div class="dash-btn" onclick="openPage('salesPage')">
      <span class="dash-emoji">💰</span>
      <div style="font-weight:700">المبيعات / فواتير</div>
      <div class="muted">فاتورة سريعة</div>
    </div>
    <div class="dash-btn" onclick="openPage('invoicesPage')">
      <span class="dash-emoji">🧾</span>
      <div style="font-weight:700">سجل الفواتير</div>
      <div class="muted">فواتير العملاء والموردين</div>
    </div>
    <div class="dash-btn" onclick="openPage('clientDocsPage')">
      <span class="dash-emoji">📄</span>
      <div style="font-weight:700">مستندات & سندات</div>
      <div class="muted">سند قبض / سند صرف</div>
    </div>
    <div class="dash-btn" onclick="openPage('reportsPage')">
      <span class="dash-emoji">📊</span>
      <div style="font-weight:700">التقارير</div>
      <div class="muted">تقرير يومي وشهري</div>
    </div>
  </div>

  <!-- Inventory Page -->
  <div id="inventoryPage" class="page">
    <div style="display:flex;justify-content:space-between;align-items:center">
      <h2>الأصناف والمخزون</h2>
      <div class="flex">
        <button class="btn" onclick="openPage('dashboard')">الرجوع</button>
      </div>
    </div>
    <div class="section-row" style="margin-top:10px">
      <div class="col">
        <label>ابحث عن مصنف أو منتج</label>
        <input id="invSearch" class="search" placeholder="مثال: مشروبات, مياه ..." oninput="renderInventory()">
        <div id="inventoryContainer" style="margin-top:10px"></div>
      </div>
      <div class="col right-col">
        <h4>إضافة / تعديل صنف</h4>
        <label>نوع المنتج (المصنف)</label>
        <input id="inv_cat" type="text" placeholder="مثال: مشروبات، وجبات، حلويات">
        <label>اسم المنتج</label>
        <input id="inv_prod" type="text" placeholder="مثال: مياه معدنية 500 مل">
        <div style="margin-top:12px;padding:10px;background:#151515;border-radius:8px;border:1px solid var(--table-border);">
          <div style="font-weight:700;color:var(--accent);margin-bottom:8px;">📦 تفاصيل الكرتون</div>
          <label>كمية الوحدات داخل الكرتون الواحد</label>
          <input id="inv_unitsPerCarton" type="number" min="1" value="12" placeholder="مثال: 12">
          <label>سعر الوحدة (الحبّة)</label>
          <input id="inv_unitPrice" type="number" min="0" step="0.01" value="1.00" placeholder="مثال: 1.25">
          <label>سعر الكرتون الكامل</label>
          <input id="inv_cartonPrice" type="number" min="0" step="0.01" value="10.00" placeholder="مثال: 12.00">
        </div>
        <label style="margin-top:12px;">عدد الكراتين المتوفرة</label>
        <input id="inv_cartonCount" type="number" min="0" value="0" placeholder="مثال: 5">
        <label style="margin-top:12px;">باركود (اختياري)</label>
        <input id="inv_barcode" type="text" placeholder="مثال: 1234567890123">
        <div style="margin-top:16px;display:flex;gap:10px;flex-wrap:wrap">
          <button class="btn primary" onclick="saveInventory()">💾 حفظ الصنف</button>
          <button class="btn" onclick="clearInventoryForm()">🗑️ مسح النموذج</button>
          <button class="btn" onclick="exportCategories()">📤 تصدير JSON</button>
        </div>
        <div class="muted-note" style="margin-top:10px;">
          ✅ يمكنك تعديل أو حذف أي صنف من الجدول أدناه بنقرة واحدة.
        </div>
      </div>
    </div>
  </div>

  <!-- Clients Page -->
  <div id="clientsPage" class="page">
    <div style="display:flex;justify-content:space-between;align-items:center">
      <h2>العملاء / الموردين</h2>
      <div class="flex">
        <button class="btn" onclick="openPage('dashboard')">الرجوع</button>
      </div>
    </div>
    <div class="section-row" style="margin-top:10px">
      <div class="col">
        <label>بحث</label>
        <input id="clientSearch" class="search" placeholder="ابحث باسم أو هاتف أو نوع..." oninput="renderClients()">
        <div id="clientsList" style="margin-top:10px"></div>
      </div>
      <div class="col right-col">
        <h4>إضافة / تعديل سجل</h4>
        <label>الاسم</label><input id="c_name" type="text">
        <label>رقم الهوية</label><input id="c_idnum" type="text">
        <label>الهاتف</label><input id="c_phone" type="text">
        <label>البريد الإلكتروني</label><input id="c_email" type="text">
        <label>العنوان</label><input id="c_address" type="text">
        <label>نوع السجل</label>
        <select id="c_type"><option value="عميل">عميل</option><option value="تاجر">تاجر</option><option value="مورد">مورد</option></select>
        <label>ملاحظات</label><textarea id="c_notes" rows="2"></textarea>
        <div style="margin-top:8px;display:flex;gap:8px">
          <button class="btn primary" onclick="saveClient()">حفظ</button>
          <button class="btn" onclick="clearClientForm()">مسح</button>
          <button class="btn" onclick="exportClients()">تصدير JSON</button>
        </div>
      </div>
    </div>
  </div>

  <!-- Sales Page -->
  <div id="salesPage" class="page">
    <div style="display:flex;justify-content:space-between;align-items:center">
      <h2>المبيعات — إنشاء فاتورة</h2>
      <div class="flex">
        <button class="btn" onclick="openPage('dashboard')">الرجوع</button>
      </div>
    </div>
    <div class="section-row" style="margin-top:10px">
      <div class="col">
        <div style="display:flex;justify-content:space-between;align-items:center">
          <div style="font-weight:800">قائمة الأصناف و أنواعها</div>
          <div style="display:flex;gap:8px;align-items:center">
            <input id="prodSearch" class="search" placeholder="ابحث..." style="width:240px" oninput="renderProductsTable()">
            <button class="btn" onclick="renderProductsTable()">تحديث</button>
          </div>
        </div>
        <div style="margin-top:8px">
          <label>مسح باركود (أو اكتب يدويًا)</label>
          <input id="barcodeInput" class="search" placeholder="امسح الباركود أو اكتب الرقم" onkeydown="if(event.key==='Enter') addProductByBarcode()">
        </div>
        <div style="margin-top:8px;overflow:auto">
          <div id="productsTable"></div>
        </div>
      </div>
      <div class="col right-col">
        <h4>تفاصيل الفاتورة</h4>
        <label style="margin-top:8px">نوع العميل</label>
        <div style="margin-top:6px;display:flex;gap:8px">
          <button class="btn" onclick="openClientSelectorForType('client')">عميل</button>
          <button class="btn" onclick="openClientSelectorForType('supplier')">مورد</button>
        </div>
        <div id="chosenClientBox" class="client-card" style="margin-top:8px">لم يتم اختيار عميل بعد</div>
        <label style="margin-top:8px">نوع الدفع</label>
        <select id="paymentType" class="search">
          <option value="نقدا">نقدا / كاش</option>
          <option value="شبكة">شبكة / بطاقة</option>
          <option value="بنك">بنك</option>
          <option value="آجل">آجل</option>
        </select>
        <label style="margin-top:8px">المبلغ المسلم الآن</label>
        <input id="invoicePaidAmount" type="number" min="0" value="0" class="search">
        <label style="margin-top:8px">ملاحظات الفاتورة</label>
        <textarea id="invoiceNotes" rows="2"></textarea>
        <h4 style="margin-top:12px">السلة</h4>
        <table>
          <thead><tr><th>المنتج</th><th>الكمية</th><th>النوع</th><th>السعر</th><th>المجموع</th><th>إزالة</th></tr></thead>
          <tbody id="cartBody"></tbody>
        </table>
        <div style="margin-top:8px;font-weight:800">الإجمالي: <span id="grandTotal">0.00</span></div>
        <div style="margin-top:10px;display:flex;gap:8px">
          <button class="btn primary" onclick="finalizeInvoice()">إنهاء الفاتورة (حفظ + تسجيل الدفعة)</button>
          <button class="btn" onclick="clearCartConfirm()">تفريغ السلة</button>
        </div>
        <div style="margin-top:8px">
          <button class="btn" onclick="exportCurrentInvoiceDraft()">تصدير المسودة (JSON)</button>
        </div>
      </div>
    </div>
  </div>

  <!-- Invoices Page -->
  <div id="invoicesPage" class="page">
    <div style="display:flex;justify-content:space-between;align-items:center">
      <h2>سجل الفواتير</h2>
      <div class="flex">
        <button class="btn" onclick="openPage('dashboard')">الرجوع</button>
      </div>
    </div>
    <div style="margin-top:8px;display:flex;gap:8px;align-items:center">
      <input id="invFilter" class="search" placeholder="ابحث باسم العميل أو رقم الفاتورة..." oninput="renderInvoicesView()">
      <button class="btn" onclick="renderInvoicesView()">عرض</button>
      <button class="btn" onclick="exportAllInvoices()">تصدير كل الفواتير (JSON)</button>
    </div>
    <div id="invoicesContainer" style="margin-top:10px"></div>
  </div>

  <!-- Client Documents Page -->
  <div id="clientDocsPage" class="page">
    <div style="display:flex;justify-content:space-between;align-items:center">
      <h2>مستندات العملاء — سند قبض / سند صرف</h2>
      <div class="flex">
        <button class="btn" onclick="openPage('dashboard')">الرجوع</button>
      </div>
    </div>
    <div style="margin-top:10px;display:flex;gap:12px;flex-wrap:wrap">
      <div class="col">
        <h4>إضافة مستند / سند</h4>
        <label>نوع المستند</label>
        <select id="docType" class="search" onchange="onDocTypeChange()">
          <option value="سند قبض">سند قبض (لصالح العميل)</option>
          <option value="سند صرف">سند صرف (مدفوع للمورد)</option>
        </select>
        <label>اختر العميل/المورد</label>
        <select id="docClientSelect" class="search" onchange="onDocClientChange()"><option value="">— اختر —</option></select>
        <div style="display:flex;gap:8px;margin-top:6px">
          <div style="flex:1">
            <label>اسم (سيملأ تلقائياً أو اكتب)</label>
            <input id="docName" type="text">
          </div>
          <div style="width:160px">
            <label>ربط بفاتورة (اختياري)</label>
            <select id="docInvoiceSelect" class="search"><option value="">— لا يوجد —</option></select>
          </div>
        </div>
        <label style="margin-top:12px">قائمة المنتجات</label>
        <div style="display:flex;gap:8px;margin-top:6px;align-items:center">
          <input id="docProdSearch" class="search" placeholder="ابحث عن منتج..." style="flex:1" oninput="renderDocProductsTable()">
          <button class="btn" onclick="renderDocProductsTable()" style="padding:6px 10px;font-size:13px">تحديث</button>
        </div>
        <div style="margin-top:8px;overflow:auto;max-height:200px">
          <div id="docProductsTable"></div>
        </div>
        <label style="margin-top:12px">طريقة الدفع</label>
        <select id="docPaymentMethod" class="search">
          <option value="نقدا">نقدا</option>
          <option value="شبكة">شبكة</option>
          <option value="بنك">بنك</option>
        </select>
        <label>السبب / ملاحظات</label>
        <input id="docReason" type="text">
        <h4 style="margin-top:12px">سلة السند</h4>
        <table>
          <thead><tr><th>المنتج</th><th>كمية</th><th>سعر</th><th>المجموع</th><th>تعديل</th><th>إزالة</th></tr></thead>
          <tbody id="docCartBody"></tbody>
        </table>
        <div style="margin-top:8px;font-weight:800">الإجمالي: <span id="docGrandTotal">0.00</span></div>
        <div style="margin-top:10px;display:flex;gap:8px">
          <button class="btn primary" onclick="addDocument()">حفظ المستند</button>
          <button class="btn" onclick="clearDocForm()">مسح</button>
          <button class="btn" onclick="printClientDocuments()">طباعة</button>
          <button class="btn" onclick="exportClientDocsCSV()">تصدير CSV</button>
        </div>
      </div>
      <div class="col" style="flex:1">
        <h4>قائمة المستندات</h4>
        <input id="docSearch" class="search" placeholder="ابحث..." oninput="renderDocumentsTable()">
        <div style="margin-top:8px;overflow:auto">
          <table>
            <thead><tr style="background:#1a1a1a"><th>النوع</th><th>الاسم</th><th>المنتجات</th><th>المبلغ</th><th>التاريخ</th><th>إجراء</th></tr></thead>
            <tbody id="docsTbody"></tbody>
          </table>
        </div>
      </div>
    </div>
  </div>

  <!-- Client Account Page -->
  <div id="clientAccountPage" class="page">
    <div style="display:flex;justify-content:space-between;align-items:center">
      <h2>حساب العميل / المورد</h2>
      <div class="flex">
        <button class="btn" onclick="openPage('clientsPage')">الرجوع إلى السجلات</button>
      </div>
    </div>
    <div id="accountHeader" style="margin-top:8px"></div>
    <div id="accountContent" style="margin-top:10px"></div>
  </div>

  <!-- Supplier Account Page -->
  <div id="supplierAccountPage" class="page">
    <div style="display:flex;justify-content:space-between;align-items:center">
      <h2>حساب المورد</h2>
      <div class="flex">
        <button class="btn" onclick="openPage('clientsPage')">الرجوع إلى السجلات</button>
      </div>
    </div>
    <div id="supplierAccountHeader" style="margin-top:8px"></div>
    <div id="supplierAccountContent" style="margin-top:10px"></div>
  </div>

  <!-- Reports Page -->
  <div id="reportsPage" class="page">
    <div style="display:flex;justify-content:space-between;align-items:center">
      <h2>التقارير</h2>
      <div class="flex"><button class="btn" onclick="openPage('dashboard')">الرجوع</button></div>
    </div>
    <div style="margin-top:10px;display:flex;gap:10px;flex-wrap:wrap">
      <div class="col" style="min-width:300px">
        <h4>تقرير اليوم</h4>
        <div class="small">التاريخ:</div>
        <input type="date" id="reportDay" value="">
        <div style="margin-top:8px">
          <button class="btn primary" onclick="generateDailyReport()">عرض تقرير اليوم</button>
          <button class="btn" onclick="exportDailyCSV()">تصدير CSV</button>
        </div>
        <div id="dailyReport" style="margin-top:8px"></div>
      </div>
      <div class="col" style="min-width:300px">
        <h4>تقرير الشهر</h4>
        <div class="small">اختر شهر</div>
        <input type="month" id="reportMonth" value="">
        <div style="margin-top:8px">
          <button class="btn primary" onclick="generateMonthlyReport()">عرض تقرير الشهر</button>
          <button class="btn" onclick="exportMonthlyCSV()">تصدير CSV</button>
        </div>
        <div id="monthlyReport" style="margin-top:8px"></div>
      </div>
    </div>
  </div>

  <!-- Client selector modal -->
  <div id="clientSelector" style="display:none;position:fixed;left:50%;top:50%;transform:translate(-50%,-50%);z-index:90">
    <div style="background:#111111;padding:12px;border-radius:8px;box-shadow:0 16px 48px var(--glass);min-width:320px;color:#ffffff;border:1px solid var(--table-border)">
      <div style="display:flex;justify-content:space-between;align-items:center">
        <h3 style="margin:0;color:var(--accent)">اختر العميل</h3>
        <button class="btn" onclick="closeClientSelector()">إغلاق</button>
      </div>
      <div style="margin-top:8px">
        <input id="selectorSearch" class="search" placeholder="ابحث..." oninput="renderClientSelectorList()">
        <div id="clientSelectorList" style="max-height:320px;overflow:auto;margin-top:8px"></div>
      </div>
    </div>
  </div>
</div>
<div id="printArea" style="display:none"></div>
<script>
/* ===========================
   Data initialization
   =========================== */
let clients = JSON.parse(localStorage.getItem('clients') || '[]');
let categories = JSON.parse(localStorage.getItem('categories_v3') || '[]');
let invoices = JSON.parse(localStorage.getItem('sales_history') || '[]');
let documents = JSON.parse(localStorage.getItem('clientDocs') || '[]');
let receipts = JSON.parse(localStorage.getItem('receipts') || '[]');
let expenses = JSON.parse(localStorage.getItem('expenses') || '[]');
let salesAgents = JSON.parse(localStorage.getItem('salesAgents') || '[]');

if (!salesAgents.length) {
  salesAgents = [{id:'agent-1', name:'خالد'},{id:'agent-2', name:'سالم'}];
  localStorage.setItem('salesAgents', JSON.stringify(salesAgents));
}

/* ===========================
   Helpers
   =========================== */
function saveAll(){
  localStorage.setItem('clients', JSON.stringify(clients));
  localStorage.setItem('categories_v3', JSON.stringify(categories));
  localStorage.setItem('sales_history', JSON.stringify(invoices));
  localStorage.setItem('clientDocs', JSON.stringify(documents));
  localStorage.setItem('receipts', JSON.stringify(receipts));
  localStorage.setItem('expenses', JSON.stringify(expenses));
  localStorage.setItem('salesAgents', JSON.stringify(salesAgents));
}
function escapeHtml(s){ 
  if(s===undefined||s===null) return ''; 
  return String(s).replace(/[&<>"'`]/g,m=>({'&':'&amp;','<':'<','>':'>','"':'&quot;',"'":'&#39;','`':'&#96;'}[m])); 
}
function uid(prefix='id'){ 
  return prefix + '-' + Date.now() + '-' + Math.random().toString(36).slice(2,6); 
}
function toDateString(iso){ 
  try{ return new Date(iso).toLocaleString(); }catch(e){ return iso; } 
}
function sumPaymentsOfInvoice(inv){ 
  return (inv.payments||[]).reduce((s,p)=>s + (Number(p.amount)||0),0); 
}
function lastPaymentMethod(inv){ 
  const p = (inv.payments||[]).slice(-1)[0]; 
  return p? p.method : (inv.paymentType||''); 
}

/* ===========================================
   Logo data URL
   =========================================== */
const svgLogo = `<svg xmlns='http://www.w3.org/2000/svg' width='420' height='80' viewBox='0 0 420 80'>
  <defs>
    <linearGradient id='g' x1='0' x2='1'>
      <stop offset='0' stop-color='#f6d365'/>
      <stop offset='1' stop-color='#fda085'/>
    </linearGradient>
  </defs>
  <rect rx='10' width='420' height='80' fill='white'/>
  <g transform='translate(12,12)'>
    <circle cx='24' cy='26' r='22' fill='url(#g)' stroke='#b37a3b' stroke-width='1'/>
    <text x='60' y='36' font-family='Arial' font-size='20' fill='#b37a3b' font-weight='700'>Abo Alfuraq Company</text>
  </g>
</svg>`;
const logoDataUrl = 'data:image/svg+xml;utf8,' + encodeURIComponent(svgLogo);

/* ===========================
   Navigation
   =========================== */
function openPage(id){
  document.getElementById('dashboard').style.display = (id==='dashboard') ? 'grid' : 'none';
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  if(id !== 'dashboard') document.getElementById(id).classList.add('active');
  
  if(id === 'clientsPage') renderClients();
  else if(id === 'inventoryPage') { renderInventory(); clearInventoryForm(); }
  else if(id === 'salesPage') { renderProductsTable(); populateClientSelects(); renderCart(); }
  else if(id === 'invoicesPage') renderInvoicesView();
  else if(id === 'clientDocsPage') { populateClientSelects(); renderDocProductsTable(); renderDocumentsTable(); }
}
openPage('dashboard');

/* ===========================
   Utility Functions
   =========================== */
function downloadText(filename, text){
  const a = document.createElement('a');
  const blob = new Blob([text], {type:'text/plain;charset=utf-8'});
  a.href = URL.createObjectURL(blob); a.download = filename; document.body.appendChild(a); a.click();
  setTimeout(()=>{ URL.revokeObjectURL(a.href); a.remove(); },500);
}

/* ===========================
   Inventory CRUD
   =========================== */
let editingItem = null;
function saveInventory(){
  const catName = (document.getElementById('inv_cat').value||'').trim();
  const prodName = (document.getElementById('inv_prod').value||'').trim();
  const unitsPerCarton = Number(document.getElementById('inv_unitsPerCarton').value) || 1;
  const unitPrice = parseFloat(document.getElementById('inv_unitPrice').value) || 0;
  const cartonPrice = parseFloat(document.getElementById('inv_cartonPrice').value) || 0;
  const cartonCount = Number(document.getElementById('inv_cartonCount').value) || 0;
  const barcode = (document.getElementById('inv_barcode').value||'').trim();
  if(!catName || !prodName){
    alert('أدخل المصنف واسم المنتج');
    return;
  }
  let cat = categories.find(c => c.name === catName);
  if(!cat){
    cat = {name: catName, products: {}};
    categories.push(cat);
  }
  if(editingItem){
    const oldCat = categories.find(c => c.name === editingItem.catName);
    if(oldCat && oldCat.products[editingItem.prodName]){
      delete oldCat.products[editingItem.prodName];
    }
    cat.products[prodName] = {
      unitsPerCarton,
      unitPrice,
      cartonPrice,
      cartonCount,
      barcode,
      datetime: new Date().toISOString()
    };
    editingItem = null;
  } else {
    cat.products[prodName] = {
      unitsPerCarton,
      unitPrice,
      cartonPrice,
      cartonCount,
      barcode,
      datetime: new Date().toISOString()
    };
  }
  saveAll();
  clearInventoryForm();
  renderInventory();
  alert('تم الحفظ');
}
function editInventoryItem(catName, prodName){
  const cat = categories.find(c => c.name === catName);
  if(!cat || !cat.products[prodName]) return;
  const item = cat.products[prodName];
  document.getElementById('inv_cat').value = catName;
  document.getElementById('inv_prod').value = prodName;
  document.getElementById('inv_unitsPerCarton').value = item.unitsPerCarton;
  document.getElementById('inv_unitPrice').value = item.unitPrice;
  document.getElementById('inv_cartonPrice').value = item.cartonPrice;
  document.getElementById('inv_cartonCount').value = item.cartonCount;
  document.getElementById('inv_barcode').value = item.barcode || '';
  editingItem = {catName, prodName};
  window.scrollTo(0,0);
}
function deleteInventoryItem(catName, prodName){
  if(!confirm('هل تريد حذف هذا الصنف؟')) return;
  const cat = categories.find(c => c.name === catName);
  if(cat && cat.products[prodName]){
    delete cat.products[prodName];
    if(Object.keys(cat.products).length === 0){
      categories = categories.filter(c => c.name !== catName);
    }
    saveAll();
    renderInventory();
    alert('تم الحذف');
  }
}
function clearInventoryForm(){
  ['inv_cat','inv_prod','inv_unitsPerCarton','inv_unitPrice','inv_cartonPrice','inv_cartonCount','inv_barcode'].forEach(id=>{
    const el = document.getElementById(id);
    if(el) el.value = id.includes('Count') || id.includes('PerCarton') ? '0' : '';
  });
  editingItem = null;
}
function renderInventory(){
  const q = (document.getElementById('invSearch')||{value:''}).value.trim().toLowerCase();
  const cont = document.getElementById('inventoryContainer'); cont.innerHTML = '';
  if(!categories.length){
    cont.innerHTML = '<div class="small">لا توجد أصناف.</div>';
    return;
  }
  categories.forEach(cat=>{
    const prodNames = Object.keys(cat.products || {});
    const matching = prodNames.filter(name => {
      const label = `${cat.name} - ${name}`.toLowerCase();
      return !q || label.includes(q) || name.toLowerCase().includes(q) || cat.name.toLowerCase().includes(q);
    });
    if(matching.length === 0) return;
    const wrap = document.createElement('div');
    wrap.innerHTML = `<div style="font-weight:700;margin-top:8px">${escapeHtml(cat.name)}</div>`;
    const table = document.createElement('table');
    table.innerHTML = `<thead><tr><th>المنتج</th><th>الكرتون</th><th>الوحدة</th><th>الكراتين</th><th>الإجراءات</th></tr></thead><tbody></tbody>`;
    const tbody = table.querySelector('tbody');
    matching.forEach(prodName => {
      const item = cat.products[prodName];
      const totalUnits = item.cartonCount * item.unitsPerCarton;
      const row = document.createElement('tr');
      row.innerHTML = `
        <td>${escapeHtml(prodName)}<br><small>باركود: ${escapeHtml(item.barcode || '-')}</small></td>
        <td>${item.unitsPerCarton} وحدة<br>السعر: ${item.cartonPrice.toFixed(2)}</td>
        <td>السعر: ${item.unitPrice.toFixed(2)}</td>
        <td>${item.cartonCount} (${totalUnits} وحدة)</td>
        <td>
          <button class="btn" onclick="editInventoryItem('${escapeHtml(cat.name)}','${escapeHtml(prodName)}')">تعديل</button>
          <button class="btn" onclick="deleteInventoryItem('${escapeHtml(cat.name)}','${escapeHtml(prodName)}')">حذف</button>
        </td>
      `;
      tbody.appendChild(row);
    });
    wrap.appendChild(table);
    cont.appendChild(wrap);
  });
}

/* ===========================
   Products for Sales
   =========================== */
let cart = []; 
let selectedClient = null; 
let currentClientType = null;

function renderProductsTable(){
  const container = document.getElementById('productsTable');
  const q = (document.getElementById('prodSearch')||{value:''}).value.trim().toLowerCase();
  container.innerHTML = `
    <table>
      <thead>
        <tr>
          <th>المصنف</th>
          <th>المنتج</th>
          <th>الوحدة</th>
          <th>الكرتون</th>
          <th>المتوفر</th>
          <th>الإجراء</th>
        </tr>
      </thead>
      <tbody id="productsTbody"></tbody>
    </table>
  `;
  const tbody = document.getElementById('productsTbody');
  if(!categories.length){
    tbody.innerHTML = '<tr><td colspan="6" class="small">لا توجد أصناف.</td></tr>';
    return;
  }
  let hasResults = false;
  categories.forEach(cat => {
    const rows = [];
    Object.keys(cat.products || {}).forEach(prodName => {
      const item = cat.products[prodName];
      const totalUnits = item.cartonCount * item.unitsPerCarton;
      const label = `${cat.name} - ${prodName}`.toLowerCase();
      if(q && !label.includes(q) && !prodName.toLowerCase().includes(q) && !cat.name.toLowerCase().includes(q)) return;
      const tr = document.createElement('tr');
      tr.innerHTML = `
        <td>${escapeHtml(cat.name)}</td>
        <td style="text-align:left">${escapeHtml(prodName)}</td>
        <td>${item.unitPrice.toFixed(2)}</td>
        <td>${item.cartonPrice.toFixed(2)} (${item.unitsPerCarton}/كرتون)</td>
        <td>${item.cartonCount} كرتون (${totalUnits} وحدة)</td>
        <td>
          <button class="btn" style="font-size:12px;padding:4px 6px;" 
                  onclick="addToCart('${escapeHtml(cat.name)}','${escapeHtml(prodName)}','unit')">
            + وحدة
          </button>
          <button class="btn" style="font-size:12px;padding:4px 6px;margin-top:4px;" 
                  onclick="addToCart('${escapeHtml(cat.name)}','${escapeHtml(prodName)}','carton')">
            + كرتون
          </button>
        </td>
      `;
      rows.push(tr);
    });
    if(rows.length > 0){
      hasResults = true;
      const headerRow = document.createElement('tr');
      headerRow.innerHTML = `<td colspan="6" style="background:#1a1a1a;font-weight:800;text-align:right;">${escapeHtml(cat.name)}</td>`;
      tbody.appendChild(headerRow);
      rows.forEach(r => tbody.appendChild(r));
    }
  });
  if(!hasResults){
    tbody.innerHTML = '<tr><td colspan="6" class="small">لا توجد نتائج.</td></tr>';
  }
}
function addToCart(catName, prodName, type){
  const cat = categories.find(c => c.name === catName);
  if(!cat || !cat.products[prodName]) return;
  const item = cat.products[prodName];
  const totalUnits = item.cartonCount * item.unitsPerCarton;
  const key = `${catName}|${prodName}`;
  const existing = cart.find(c => c.key === key && c.sellType === type);
  if(type === 'unit'){
    if(existing){
      if(existing.qty + 1 > totalUnits){
        alert('الكمية المطلوبة أكبر من المتوفر');
        return;
      }
      existing.qty += 1;
    } else {
      if(totalUnits < 1){
        alert('المنتج نفد');
        return;
      }
      cart.push({
        key,
        catName,
        prodName,
        sellType: 'unit',
        qty: 1,
        unitPrice: item.unitPrice,
        unitsPerCarton: item.unitsPerCarton,
        cartonPrice: item.cartonPrice
      });
    }
  } else if(type === 'carton'){
    if(existing){
      if(existing.qty + 1 > item.cartonCount){
        alert('الكراتين المطلوبة أكثر من المتوفر');
        return;
      }
      existing.qty += 1;
    } else {
      if(item.cartonCount < 1){
        alert('لا توجد كراتين متوفرة');
        return;
      }
      cart.push({
        key,
        catName,
        prodName,
        sellType: 'carton',
        qty: 1,
        unitPrice: item.unitPrice,
        cartonPrice: item.cartonPrice,
        unitsPerCarton: item.unitsPerCarton
      });
    }
  }
  renderCart();
}
function renderCart(){
  const body = document.getElementById('cartBody'); body.innerHTML = '';
  let total = 0;
  cart.forEach((it, idx)=>{
    let price, subtotal, displayQty;
    if(it.sellType === 'unit'){
      price = it.unitPrice;
      subtotal = it.qty * price;
      displayQty = `${it.qty} وحدة`;
    } else {
      price = it.cartonPrice;
      subtotal = it.qty * price;
      displayQty = `${it.qty} كرتون (${it.qty * it.unitsPerCarton} وحدة)`;
    }
    total += subtotal;
    const tr = document.createElement('tr');
    tr.innerHTML = `
      <td style="text-align:left">${escapeHtml(it.prodName)}<br><small>${escapeHtml(it.catName)}</small></td>
      <td>${displayQty}</td>
      <td>${it.sellType === 'unit' ? 'وحدة' : 'كرتون'}</td>
      <td>${price.toFixed(2)}</td>
      <td>${subtotal.toFixed(2)}</td>
      <td><button class="btn" onclick="removeCartItem(${idx})">حذف</button></td>
    `;
    body.appendChild(tr);
  });
  document.getElementById('grandTotal').innerText = total.toFixed(2);
  renderChosenClient();
}
function removeCartItem(i){ cart.splice(i,1); renderCart(); }
function clearCartConfirm(){ 
  if(!cart.length){ alert('السلة فارغة'); return; } 
  if(!confirm('تفريغ السلة؟')) return; 
  cart=[]; renderCart(); 
}

/* ===========================
   Finalize Invoice
   =========================== */
function finalizeInvoice(){
  if(!cart.length){ alert('السلة فارغة'); return; }
  if(!selectedClient){ 
    if(!confirm('لم تختَر عميلًا. الاستمرار كعميل مؤقت؟')) return; 
    selectedClient = {name:'عميل مؤقت', type:'عميل'}; 
  }
  // Validate stock
  for(const it of cart){
    const cat = categories.find(c=>c.name===it.catName);
    if(!cat || !cat.products[it.prodName]){
      alert('المنتج غير موجود: '+it.prodName);
      return;
    }
    const item = cat.products[it.prodName];
    if(it.sellType === 'unit'){
      const totalUnits = item.cartonCount * item.unitsPerCarton;
      if(it.qty > totalUnits){
        alert(`الكمية المطلوبة للمنتج ${it.prodName} أكبر من المتوفر (${totalUnits} وحدة)`);
        return;
      }
    } else {
      if(it.qty > item.cartonCount){
        alert(`الكراتين المطلوبة للمنتج ${it.prodName} أكبر من المتوفر (${item.cartonCount})`);
        return;
      }
    }
  }
  // Deduct from inventory
  cart.forEach(it => {
    const cat = categories.find(c=>c.name===it.catName);
    const item = cat.products[it.prodName];
    if(it.sellType === 'unit'){
      const totalUnits = item.cartonCount * item.unitsPerCarton;
      const newTotal = totalUnits - it.qty;
      item.cartonCount = Math.floor(newTotal / item.unitsPerCarton);
    } else {
      item.cartonCount -= it.qty;
    }
  });
  const now = new Date();
  const paymentType = document.getElementById('paymentType').value || 'نقدا';
  const notes = (document.getElementById('invoiceNotes').value||'').trim();
  const total = Number(document.getElementById('grandTotal').innerText) || 0;
  const inv = { 
    id: uid('INV'), 
    datetime: now.toISOString(), 
    client: selectedClient, 
    products: JSON.parse(JSON.stringify(cart)), 
    total: total, 
    paymentType, 
    notes, 
    payments: [] 
  };
  const paidNow = Number(document.getElementById('invoicePaidAmount').value || 0);
  if(paidNow > 0){
    const pay = { id: uid('PAY'), datetime: new Date().toISOString(), amount: paidNow, method: paymentType, note: 'دفعة عند إنشاء الفاتورة' };
    inv.payments.push(pay);
    receipts.push({ 
      id: pay.id, 
      type: 'سند قبض', 
      clientIndex: null, 
      clientName: selectedClient.name, 
      items: inv.products.map(p=>p.prodName).join(', '), 
      amount: paidNow, 
      reason: 'دفعة مرتبطة بفاتورة', 
      datetime: pay.datetime, 
      invoiceId: inv.id, 
      method: pay.method 
    });
  }
  invoices.push(inv);
  saveAll();
  cart = []; selectedClient = null;
  document.getElementById('paymentType').value = 'نقدا';
  document.getElementById('invoiceNotes').value = '';
  document.getElementById('invoicePaidAmount').value = 0;
  renderCart(); renderProductsTable(); renderInvoicesView();
  alert('تم حفظ الفاتورة وتسجيل الدفعة (إن وجدت).');
}

/* ===========================
   Print Invoice
   =========================== */
function printInvoice(id){
  const inv = invoices.find(x=>x.id===id); if(!inv) return;
  const companyName='شركة شعبيات الحارة ';
  let paymentsHtml = '';
  const paid = sumPaymentsOfInvoice(inv);
  (inv.payments||[]).forEach(p=> paymentsHtml += `<tr><td>${toDateString(p.datetime)}</td><td>${p.id}</td><td>${p.amount}</td><td>${escapeHtml(p.method||'')}</td></tr>`);
  let html = `<html dir="rtl"><head><meta charset="utf-8"><title>فاتورة ${escapeHtml(inv.id)}</title>
    <style>body{font-family:Arial,"Noto Naskh Arabic",sans-serif;direction:rtl;color:#111}
    .frame{max-width:800px;margin:18px auto;border:1px solid #ddd;padding:18px;border-radius:8px}
    .hdr{display:flex;justify-content:space-between;align-items:center;margin-bottom:12px}
    .comp{font-size:22px;font-weight:900;color:#0aa}
    table{width:100%;border-collapse:collapse;margin-top:12px}
    th,td{padding:8px;border:1px solid #ddd;text-align:center}
    th{background:#f6f6f6}
    .total{margin-top:10px;text-align:left;font-size:18px;font-weight:800}
    .footer{margin-top:20px;font-size:12px;color:#666}
    .logo{height:56px}
    </style></head><body>
    <div class="frame">
      <div class="hdr">
        <div>
          <img src="${logoDataUrl}" class="logo" alt="logo" />
          <div style="font-weight:900;color:#0aa;font-size:18px;margin-top:6px">${escapeHtml(companyName)}</div>
          <div class="muted-tiny">عنوان الشركة — هاتف: 000000 — بريد إلكتروني: info@example.com</div>
        </div>
        <div style="text-align:left;font-size:13px">فاتورة: ${escapeHtml(inv.id)}<br>التاريخ: ${toDateString(inv.datetime)}</div>
      </div>
      <div><strong>العميل:</strong> ${escapeHtml(inv.client.name||'-')} — ${escapeHtml(inv.client.type||'')}</div>
      <div style="margin-top:8px"><table><thead><tr><th>المنتج</th><th>النوع</th><th>الكمية</th><th>السعر</th><th>المجموع</th></tr></thead><tbody>`;
  inv.products.forEach(p=>{ 
    let qtyDisplay, priceDisplay;
    if(p.sellType === 'unit'){
      qtyDisplay = `${p.qty} وحدة`;
      priceDisplay = `${p.unitPrice.toFixed(2)} / وحدة`;
    } else {
      qtyDisplay = `${p.qty} كرتون (${p.qty * p.unitsPerCarton} وحدة)`;
      priceDisplay = `${p.cartonPrice.toFixed(2)} / كرتون (${p.unitsPerCarton} وحدة)`;
    }
    html += `<tr><td style="text-align:left">${escapeHtml(p.prodName)}</td><td>${p.sellType === 'unit' ? 'وحدة' : 'كرتون'}</td><td>${qtyDisplay}</td><td>${priceDisplay}</td><td>${(p.sellType === 'unit' ? p.qty * p.unitPrice : p.qty * p.cartonPrice).toFixed(2)}</td></tr>`; 
  });
  html += `</tbody></table></div>
    <div class="total">الإجمالي: ${inv.total.toFixed(2)} — مدفوع: ${paid.toFixed(2)} — المتبقي: ${(inv.total-paid).toFixed(2)}</div>
    <div style="margin-top:8px"><strong>الدفعات:</strong></div>
    <table><thead><tr><th>التاريخ</th><th>رقم السند/الدفعة</th><th>المبلغ</th><th>الطريقة</th></tr></thead><tbody>${paymentsHtml || '<tr><td colspan="4">لا دفعات</td></tr>'}</tbody></table>
    <div style="margin-top:20px">ملاحظات: ${escapeHtml(inv.notes||'')}</div>
    <div style="margin-top:20px">توقيع: ________________</div>
    <div class="footer">شكراً لتعاملكم مع ${escapeHtml(companyName)}</div>
    </div></body></html>`;
  const w = window.open('','_blank'); w.document.write(html); w.document.close(); w.focus(); w.print();
}

/* ===========================
   Clients Management
   =========================== */
function renderClients(){
  const q = (document.getElementById('clientSearch')||{value:''}).value.trim().toLowerCase();
  const area = document.getElementById('clientsList'); area.innerHTML = '';
  if(!clients.length){ area.innerHTML = '<div class="small">لا يوجد سجلات بعد.</div>'; return; }
  clients.forEach((c,i)=>{
    if(q && !((c.name||'').toLowerCase().includes(q) || (c.phone||'').includes(q) || (c.type||'').toLowerCase().includes(q))) return;
    const d = document.createElement('div'); d.className='client-card';
    d.innerHTML = `<div style="font-weight:800">${escapeHtml(c.name)} <span class="small">(${escapeHtml(c.type||'عميل')})</span></div>
      <div>الهاتف: ${escapeHtml(c.phone||'-')} — الهوية: ${escapeHtml(c.idnum||'-')}</div>
      <div>البريد: ${escapeHtml(c.email||'-')}</div>
      <div>العنوان: ${escapeHtml(c.address||'-')}</div>
      <div class="small">ملاحظات: ${escapeHtml(c.notes||'-')}</div>
      <div style="margin-top:8px;display:flex;gap:8px">
        <button class="btn" onclick="pickClient(${i})">اختر</button>
        <button class="btn" onclick="editClient(${i})">تعديل</button>
        <button class="btn" onclick="deleteClient(${i})">حذف</button>
        <button class="btn" onclick="openClientAccount(${i})">عرض الحساب</button>
        <button class="btn" onclick="openSupplierAccount(${i})">عرض مورد (لو كان)</button>
      </div>`;
    area.appendChild(d);
  });
  populateClientSelects();
}
let editingClientIndex = -1;
function saveClient(){
  const obj = {
    name: (document.getElementById('c_name').value||'').trim(),
    idnum: (document.getElementById('c_idnum').value||'').trim(),
    phone: (document.getElementById('c_phone').value||'').trim(),
    email: (document.getElementById('c_email').value||'').trim(),
    address: (document.getElementById('c_address').value||'').trim(),
    type: (document.getElementById('c_type').value||'عميل'),
    notes: (document.getElementById('c_notes').value||'').trim()
  };
  if(!obj.name){ alert('أدخل اسم العميل'); return; }
  if(editingClientIndex >= 0){ 
    clients[editingClientIndex] = obj; 
    editingClientIndex = -1; 
  } else clients.push(obj);
  saveAll(); 
  clearClientForm(); 
  renderClients(); 
  alert('تم الحفظ');
}
function editClient(i){
  const c = clients[i]; if(!c) return;
  editingClientIndex = i;
  document.getElementById('c_name').value = c.name||'';
  document.getElementById('c_idnum').value = c.idnum||'';
  document.getElementById('c_phone').value = c.phone||'';
  document.getElementById('c_email').value = c.email||'';
  document.getElementById('c_address').value = c.address||'';
  document.getElementById('c_type').value = c.type||'عميل';
  document.getElementById('c_notes').value = c.notes||'';
  window.scrollTo(0,0);
}
function deleteClient(i){ 
  if(!confirm('هل تريد حذف السجل؟')) return; 
  clients.splice(i,1); 
  saveAll(); 
  renderClients(); 
}
function clearClientForm(){ 
  ['c_name','c_idnum','c_phone','c_email','c_address','c_notes'].forEach(id=>document.getElementById(id).value=''); 
  document.getElementById('c_type').value='عميل'; 
  editingClientIndex=-1; 
}
function pickClient(i){ 
  const c = clients[i]; 
  if(!c) return; 
  selectedClient = c; 
  renderChosenClient(); 
  openPage('salesPage'); 
}
function exportClients(){ 
  downloadText('clients_export.json', JSON.stringify(clients,null,2)); 
}

/* ===========================
   Invoices View
   =========================== */
function renderInvoicesView(){
  const q = (document.getElementById('invFilter')||{value:''}).value.trim().toLowerCase();
  const area = document.getElementById('invoicesContainer'); area.innerHTML = '';
  if(!invoices.length){ area.innerHTML = '<div class="small">لا توجد فواتير</div>'; return; }
  const supp = invoices.filter(inv => (inv.client && (inv.client.type || '').toLowerCase() === 'مورد'));
  const cust = invoices.filter(inv => !(inv.client && (inv.client.type || '').toLowerCase() === 'مورد'));
  function buildTable(title, list){
    const wrapper = document.createElement('div'); wrapper.style.marginTop='10px';
    const h = document.createElement('div'); h.style.display='flex'; h.style.justifyContent='space-between'; h.style.alignItems='center';
    h.innerHTML = `<div style="font-weight:800">${title} (${list.length})</div><div style="display:flex;gap:8px"><button class="btn" onclick="printInvoicesSection('${title.replace(/\s+/g,'_')}')">طباعة</button><button class="btn" onclick="downloadText('${title.replace(/\s+/g,'_')}_export.json', JSON.stringify(${JSON.stringify(list)},null,2))">تصدير JSON</button></div>`;
    wrapper.appendChild(h);
    const table = document.createElement('table');
    table.innerHTML = `<thead><tr><th>العميل</th><th>النوع</th><th>رقم الفاتورة</th><th>التاريخ</th><th>الإجمالي</th><th>المسلم</th><th>الباقي</th><th>طريقة الدفع</th><th>الحالة</th><th>إجراء</th></tr></thead><tbody></tbody>`;
    const tb = table.querySelector('tbody');
    list.slice().reverse().forEach(inv=>{
      if(q){
        const matchClient = inv.client && ((inv.client.name||'').toLowerCase().includes(q) || (inv.client.phone||'').includes(q));
        const matchProd = inv.products.some(p=> (p.prodName||'').toLowerCase().includes(q));
        if(!matchClient && !matchProd) return;
      }
      const paid = sumPaymentsOfInvoice(inv);
      const rem = (inv.total||0) - paid;
      const tr = document.createElement('tr');
      tr.innerHTML = `<td>${escapeHtml(inv.client.name||'-')}</td>
        <td>${escapeHtml(inv.client.type||'عميل')}</td>
        <td>${escapeHtml(inv.id)}</td>
        <td>${toDateString(inv.datetime)}</td>
        <td>${inv.total.toFixed(2)}</td>
        <td>${paid.toFixed(2)}</td>
        <td>${rem.toFixed(2)}</td>
        <td>${escapeHtml(lastPaymentMethod(inv)||'')}</td>
        <td>${inv.isModified ? '<span style="color:#ff5555;font-weight:800">تم التعديل</span>' : '—'}</td>
        <td style="display:flex;gap:6px;justify-content:center">
          <button class="btn" onclick="viewInvoice('${inv.id}')">عرض</button>
          <button class="btn" onclick="printInvoice('${inv.id}')">طباعة</button>
          <button class="btn" onclick="editInvoice('${inv.id}')">تعديل</button>
          <button class="btn" onclick="deleteInvoice('${inv.id}')">حذف</button>
        </td>`;
      tb.appendChild(tr);
    });
    wrapper.appendChild(table);
    return wrapper;
  }
  area.appendChild(buildTable('فواتير العملاء', cust));
  area.appendChild(document.createElement('hr'));
  area.appendChild(buildTable('فواتير الموردين', supp));
}
function viewInvoice(id){
  const inv = invoices.find(x=>x.id===id); if(!inv){ alert('لم أجد الفاتورة'); return; }
  let txt = `تاريخ: ${toDateString(inv.datetime)}
رقم: ${inv.id}
العميل: ${inv.client.name} (${inv.client.type || ''})
المنتجات:
`;
  inv.products.forEach((p,i)=> txt += `${i+1}. ${p.prodName} — ${p.sellType === 'unit' ? 'وحدة' : 'كرتون'} — كمية: ${p.qty} — سعر: ${p.sellType === 'unit' ? p.unitPrice : p.cartonPrice} — مجموع: ${(p.sellType === 'unit' ? p.qty * p.unitPrice : p.qty * p.cartonPrice).toFixed(2)}
`);
  const paid = sumPaymentsOfInvoice(inv);
  txt += `
الإجمالي: ${inv.total.toFixed(2)}
مدفوع: ${paid.toFixed(2)}
المتبقي: ${(inv.total - paid).toFixed(2)}
الدفعات:
`;
  (inv.payments||[]).forEach(p=> txt += ` - ${toDateString(p.datetime)} — ${p.amount} — ${p.method||''}
`);
  txt += `
نوع الدفع الافتراضي: ${inv.paymentType}
ملاحظات: ${inv.notes||''}`;
  alert(txt);
}
function deleteInvoice(id){ 
  if(!confirm('حذف الفاتورة؟')) return; 
  invoices = invoices.filter(x=>x.id !== id); 
  saveAll(); 
  renderInvoicesView(); 
}
function editInvoice(id){
  alert('تعديل الفاتورة غير مدعوم حالياً. يمكنك حذفها وإعادة إنشائها.');
}
function printInvoicesSection(sectionName){
  alert('طباعة مجموعة الفواتير غير مدعومة حالياً. يمكنك طباعة كل فاتورة على حدة.');
}

/* ===========================
   Client Selector Modal
   =========================== */
function renderChosenClient(){ 
  const box = document.getElementById('chosenClientBox'); 
  if(!selectedClient){ 
    box.innerHTML = 'لم يتم اختيار عميل بعد'; 
    return; 
  } 
  box.innerHTML = `<div style="font-weight:800">${escapeHtml(selectedClient.name)} <span class="small">(${escapeHtml(selectedClient.type||'عميل')})</span></div><div>الهاتف: ${escapeHtml(selectedClient.phone||'-')}</div><div class="small">${escapeHtml(selectedClient.address||'')}</div>`; 
}
function openClientSelectorForType(type){
  currentClientType = type;
  document.getElementById('clientSelector').style.display='block';
  document.body.appendChild(Object.assign(document.createElement('div'),{id:'modalOverlay',className:'overlay',onclick:closeClientSelector}));
  renderClientSelectorList();
}
function closeClientSelector(){ 
  document.getElementById('clientSelector').style.display='none'; 
  const o=document.getElementById('modalOverlay'); 
  if(o) o.remove(); 
}
function renderClientSelectorList(){
  const q = (document.getElementById('selectorSearch')||{value:''}).value.trim().toLowerCase();
  const area = document.getElementById('clientSelectorList'); area.innerHTML = '';
  if(!clients.length){ area.innerHTML = '<div class="small">لا يوجد سجلات.</div>'; return; }
  const allowedTypes = currentClientType === 'supplier' ? ['مورد'] : ['عميل', 'تاجر'];
  clients.forEach((c,i)=>{
    if(!allowedTypes.includes(c.type || '')) return;
    if(q && !((c.name||'').toLowerCase().includes(q) || (c.phone||'').includes(q) || (c.type||'').toLowerCase().includes(q))) return;
    const d = document.createElement('div'); d.className='client-card';
    d.innerHTML = `<div style="font-weight:700">${escapeHtml(c.name)} — <span class="small">${escapeHtml(c.type)}</span></div>
      <div>الهاتف: ${escapeHtml(c.phone||'-')}</div>
      <div style="margin-top:6px"><button class="btn" onclick="chooseClient(${i})">اختيار</button></div>`;
    area.appendChild(d);
  });
}
function chooseClient(i){ 
  selectedClient = clients[i]; 
  renderChosenClient(); 
  closeClientSelector(); 
}

/* ===========================
   Client Accounts
   =========================== */
function openClientAccount(index){
  const client = clients[index];
  if(!client){ alert('لا يوجد'); return; }
  document.getElementById('accountHeader').innerHTML = `<div style="font-weight:800">${escapeHtml(client.name)} — <span class="small">${escapeHtml(client.type||'')}</span></div>
    <div>الهاتف: ${escapeHtml(client.phone||'-')} — البريد: ${escapeHtml(client.email||'-')}</div>`;
  const clientInvoices = invoices.filter(inv => inv.client && inv.client.name === client.name);
  const paymentsOnInvoices = clientInvoices.reduce((s,inv)=> s + sumPaymentsOfInvoice(inv), 0);
  const receiptsNotLinked = receipts.filter(r=> r.clientName === client.name && !r.invoiceId).reduce((s,r)=> s + (Number(r.amount)||0), 0);
  const totalInvoices = clientInvoices.reduce((s,i)=> s + (i.total||0), 0);
  const totalPaid = paymentsOnInvoices + receiptsNotLinked;
  const remaining = totalInvoices - totalPaid;
  let html = `<div class="client-card">إجمالي الفواتير: ${totalInvoices.toFixed(2)} — إجمالي المدفوع: ${totalPaid.toFixed(2)} — المتبقي: <span class="${remaining<=0? 'balance-positive':'balance-negative'}">${remaining.toFixed(2)}</span></div>`;
  html += `<h4>فواتير العميل</h4><table><thead><tr><th>رقم</th><th>التاريخ</th><th>الإجمالي</th><th>المدفوع</th><th>المتبقي</th><th>إجراء</th></tr></thead><tbody>`;
  clientInvoices.forEach(inv=>{
    const paid = sumPaymentsOfInvoice(inv);
    const rem = (inv.total||0) - paid;
    html += `<tr><td>${escapeHtml(inv.id)}</td><td>${toDateString(inv.datetime)}</td><td>${(inv.total||0).toFixed(2)}</td><td>${paid.toFixed(2)}</td><td>${rem.toFixed(2)}</td><td><button class="btn" onclick="printInvoice('${inv.id}')">طباعة</button></td></tr>`;
  });
  html += `</tbody></table>`;
  const clientReceipts = receipts.filter(r=> r.clientName === client.name);
  html += `<h4 style="margin-top:10px">سندات القبض (دفعات)</h4><table><thead><tr><th>رقم السند</th><th>التاريخ</th><th>المبلغ</th><th>مرتبط بفاتورة</th><th>طريقة</th><th>إجراء</th></tr></thead><tbody>`;
  clientReceipts.forEach(r=> html += `<tr><td>${escapeHtml(r.id)}</td><td>${toDateString(r.datetime)}</td><td>${r.amount}</td><td>${escapeHtml(r.invoiceId || '-')}</td><td>${escapeHtml(r.method||'-')}</td><td><button class="btn" onclick="printSingleDocument('${r.id}')">طباعة</button></td></tr>`);
  html += `</tbody></table>`;
  document.getElementById('accountContent').innerHTML = html;
  openPage('clientAccountPage');
}
function openSupplierAccount(index){
  const supplier = clients[index];
  if(!supplier){ alert('لا يوجد'); return; }
  document.getElementById('supplierAccountHeader').innerHTML = `<div style="font-weight:800">${escapeHtml(supplier.name)} — <span class="small">${escapeHtml(supplier.type||'')}</span></div>
    <div>الهاتف: ${escapeHtml(supplier.phone||'-')} — البريد: ${escapeHtml(supplier.email||'-')}</div>`;
  const suppInvoices = invoices.filter(inv => inv.client && inv.client.name === supplier.name && (inv.client.type||'').toLowerCase() === 'مورد');
  const suppExpenses = expenses.filter(e => e.clientName === supplier.name);
  const totalInvoices = suppInvoices.reduce((s,i)=> s + (i.total||0), 0);
  const totalPaid = suppExpenses.reduce((s,e)=> s + (e.amount||0), 0) + suppInvoices.reduce((s,inv)=> s + sumPaymentsOfInvoice(inv),0);
  const remaining = totalInvoices - totalPaid;
  let html = `<div class="client-card">إجمالي المستحقات: ${totalInvoices.toFixed(2)} — المدفوع: ${totalPaid.toFixed(2)} — المتبقي: <span class="${remaining<=0? 'balance-positive':'balance-negative'}">${remaining.toFixed(2)}</span></div>`;
  html += `<h4>فواتير المورد</h4><table><thead><tr><th>رقم</th><th>التاريخ</th><th>الإجمالي</th><th>المدفوع</th><th>المتبقي</th><th>إجراء</th></tr></thead><tbody>`;
  suppInvoices.forEach(inv => {
    const paid = sumPaymentsOfInvoice(inv);
    html += `<tr><td>${escapeHtml(inv.id)}</td><td>${toDateString(inv.datetime)}</td><td>${(inv.total||0).toFixed(2)}</td><td>${paid.toFixed(2)}</td><td>${((inv.total||0)-paid).toFixed(2)}</td><td><button class="btn" onclick="printInvoice('${inv.id}')">طباعة</button></td></tr>`;
  });
  html += `</tbody></table>`;
  html += `<h4 style="margin-top:10px">سندات الصرف</h4><table><thead><tr><th>رقم السند</th><th>التاريخ</th><th>المبلغ</th><th>طريقة</th><th>إجراء</th></tr></thead><tbody>`;
  suppExpenses.forEach(e => html += `<tr><td>${escapeHtml(e.id)}</td><td>${toDateString(e.datetime)}</td><td>${e.amount}</td><td>${escapeHtml(e.method||'-')}</td><td><button class="btn" onclick="printSingleDocument('${e.id}')">طباعة</button></td></tr>`);
  html += `</tbody></table>`;
  document.getElementById('supplierAccountContent').innerHTML = html;
  openPage('supplierAccountPage');
}

/* ===========================
   Client Docs (Vouchers)
   =========================== */
let docCart = [];
function renderDocProductsTable(){
  const container = document.getElementById('docProductsTable');
  const q = (document.getElementById('docProdSearch')||{value:''}).value.trim().toLowerCase();
  container.innerHTML = `
    <table style="font-size:12px">
      <thead>
        <tr>
          <th>المصنف</th>
          <th>المنتج</th>
          <th>الوحدة</th>
          <th>الكرتون</th>
          <th>المتوفر</th>
          <th>+</th>
        </tr>
      </thead>
      <tbody id="docProductsTbody"></tbody>
    </table>
  `;
  const tbody = document.getElementById('docProductsTbody');
  if(!categories.length){
    tbody.innerHTML = '<tr><td colspan="6" class="small">لا توجد أصناف.</td></tr>';
    return;
  }
  let hasResults = false;
  categories.forEach(cat => {
    const catName = cat.name;
    const rows = [];
    Object.keys(cat.products || {}).forEach(prodName => {
      const item = cat.products[prodName];
      const totalUnits = item.cartonCount * item.unitsPerCarton;
      const label = `${catName} - ${prodName}`.toLowerCase();
      if (q && !label.includes(q) && !prodName.toLowerCase().includes(q) && !catName.toLowerCase().includes(q)) return;
      const tr = document.createElement('tr');
      tr.innerHTML = `
        <td>${escapeHtml(catName)}</td>
        <td style="text-align:left">${escapeHtml(prodName)}</td>
        <td>${item.unitPrice.toFixed(2)}</td>
        <td>${item.cartonPrice.toFixed(2)} (${item.unitsPerCarton}/كرتون)</td>
        <td>${item.cartonCount} كرتون (${totalUnits} وحدة)</td>
        <td><button class="btn" style="padding:4px 8px;font-size:13px;" onclick="docAddProduct('${escapeHtml(catName)}','${escapeHtml(prodName)}','unit')">+ وحدة</button><br>
            <button class="btn" style="padding:4px 8px;font-size:13px;margin-top:4px;" onclick="docAddProduct('${escapeHtml(catName)}','${escapeHtml(prodName)}','carton')">+ كرتون</button></td>
      `;
      rows.push(tr);
    });
    if (rows.length > 0) {
      hasResults = true;
      const headerRow = document.createElement('tr');
      headerRow.innerHTML = `<td colspan="6" style="background:#1a1a1a;font-weight:700;text-align:right;">${escapeHtml(catName)}</td>`;
      tbody.appendChild(headerRow);
      rows.forEach(row => tbody.appendChild(row));
    }
  });
  if (!hasResults) {
    tbody.innerHTML = '<tr><td colspan="6" class="small">لا توجد نتائج.</td></tr>';
  }
}
function docAddProduct(catName, prodName, type){
  const cat = categories.find(c=>c.name===catName);
  if(!cat || !cat.products[prodName]) return;
  const item = cat.products[prodName];
  const totalUnits = item.cartonCount * item.unitsPerCarton;
  const key = `${catName}|${prodName}|${type}`;
  const existing = docCart.find(c => c.key === key);
  if(type === 'unit'){
    if(existing){
      if(existing.qty + 1 > totalUnits){
        alert('الكمية المطلوبة أكبر من المتوفر');
        return;
      }
      existing.qty += 1;
    } else {
      if(totalUnits < 1){
        alert('المنتج نفد');
        return;
      }
      docCart.push({
        key,
        catName,
        prodName,
        sellType: 'unit',
        qty: 1,
        unitPrice: item.unitPrice,
        cartonPrice: item.cartonPrice,
        unitsPerCarton: item.unitsPerCarton
      });
    }
  } else {
    if(existing){
      if(existing.qty + 1 > item.cartonCount){
        alert('الكراتين المطلوبة أكثر من المتوفر');
        return;
      }
      existing.qty += 1;
    } else {
      if(item.cartonCount < 1){
        alert('لا توجد كراتين متوفرة');
        return;
      }
      docCart.push({
        key,
        catName,
        prodName,
        sellType: 'carton',
        qty: 1,
        unitPrice: item.unitPrice,
        cartonPrice: item.cartonPrice,
        unitsPerCarton: item.unitsPerCarton
      });
    }
  }
  renderDocCart();
}
function renderDocCart(){
  const body = document.getElementById('docCartBody'); body.innerHTML = '';
  let total = 0;
  docCart.forEach((it, idx)=>{
    let price, subtotal, displayQty;
    if(it.sellType === 'unit'){
      price = it.unitPrice;
      subtotal = it.qty * price;
      displayQty = `${it.qty} وحدة`;
    } else {
      price = it.cartonPrice;
      subtotal = it.qty * price;
      displayQty = `${it.qty} كرتون (${it.qty * it.unitsPerCarton} وحدة)`;
    }
    total += subtotal;
    const tr = document.createElement('tr');
    tr.innerHTML = `<td style="text-align:left">${escapeHtml(it.prodName)} <div class="small">${escapeHtml(it.catName)}</div></td>
      <td>${displayQty}</td>
      <td>${price.toFixed(2)}</td><td>${subtotal.toFixed(2)}</td>
      <td><button class="btn" onclick="docEditItem(${idx})">تعديل</button></td>
      <td><button class="btn" onclick="docRemoveItem(${idx})">حذف</button></td>`;
    body.appendChild(tr);
  });
  document.getElementById('docGrandTotal').innerText = total.toFixed(2);
}
function docRemoveItem(i){ docCart.splice(i,1); renderDocCart(); }
function docEditItem(i){
  const item = docCart[i];
  if(!item) return;
  const newQty = prompt('أدخل الكمية الجديدة:', item.qty);
  const newPrice = prompt('أدخل السعر الجديد:', item.sellType === 'unit' ? item.unitPrice : item.cartonPrice);
  if(newQty === null || newPrice === null) return;
  const qty = Number(newQty);
  const price = Number(newPrice);
  if(isNaN(qty) || isNaN(price) || qty <= 0 || price < 0){
    alert('الرجاء إدخال قيم صحيحة');
    return;
  }
  if(item.sellType === 'unit'){
    const cat = categories.find(c=>c.name===item.catName);
    const available = (cat && cat.products[item.prodName]) ? cat.products[item.prodName].cartonCount * cat.products[item.prodName].unitsPerCarton : 0;
    if(qty > available){
      alert(`الكمية المطلوبة تفوق المتوفر (${available})`);
      return;
    }
  } else {
    const cat = categories.find(c=>c.name===item.catName);
    const available = (cat && cat.products[item.prodName]) ? cat.products[item.prodName].cartonCount : 0;
    if(qty > available){
      alert(`الكمية المطلوبة تفوق المتوفر (${available})`);
      return;
    }
  }
  docCart[i].qty = qty;
  if(item.sellType === 'unit'){
    docCart[i].unitPrice = price;
  } else {
    docCart[i].cartonPrice = price;
  }
  renderDocCart();
}
function addDocument(){
  const type = document.getElementById('docType').value || 'سند قبض';
  const clientIdx = Number(document.getElementById('docClientSelect').value);
  const name = (document.getElementById('docName').value || (clients[clientIdx] ? clients[clientIdx].name : '')).trim();
  const amount = Number(document.getElementById('docGrandTotal').innerText) || 0;
  const reason = (document.getElementById('docReason').value||'').trim();
  const invoiceId = (document.getElementById('docInvoiceSelect') ? document.getElementById('docInvoiceSelect').value : '');
  const method = (document.getElementById('docPaymentMethod')||{value:'نقدا'}).value || 'نقدا';
  if(!name){ alert('أدخل اسم العميل/المورد'); return; }
  if(docCart.length === 0){ alert('أضف منتجات إلى السند'); return; }
  for(const it of docCart){
    const cat = categories.find(c=>c.name===it.catName);
    if(!cat || !cat.products[it.prodName]){
      alert('منتج غير موجود في المخزون: '+it.prodName); return;
    }
    const item = cat.products[it.prodName];
    if(it.sellType === 'unit'){
      const totalUnits = item.cartonCount * item.unitsPerCarton;
      if(it.qty > totalUnits){
        alert(`الكمية المطلوبة لـ ${it.prodName} أكبر من المتوفر (${totalUnits})`);
        return;
      }
    } else {
      if(it.qty > item.cartonCount){
        alert(`الكراتين المطلوبة لـ ${it.prodName} أكبر من المتوفر (${item.cartonCount})`);
        return;
      }
    }
  }
  docCart.forEach(it => {
    const cat = categories.find(c=>c.name===it.catName);
    const item = cat.products[it.prodName];
    if(it.sellType === 'unit'){
      const totalUnits = item.cartonCount * item.unitsPerCarton;
      const newTotal = totalUnits - it.qty;
      item.cartonCount = Math.floor(newTotal / item.unitsPerCarton);
    } else {
      item.cartonCount -= it.qty;
    }
  });
  const rec = { 
    id: uid('DOC'), 
    type, 
    clientIndex: isFinite(clientIdx) ? clientIdx : null, 
    clientName: name, 
    products: JSON.parse(JSON.stringify(docCart)),
    amount, 
    reason, 
    datetime: new Date().toISOString(), 
    invoiceId: invoiceId || null, 
    method 
  };
  documents.push(rec);
  if(type === 'سند قبض'){
    receipts.push(rec);
  } else if(type === 'سند صرف'){
    expenses.push(rec);
  }
  if(invoiceId){
    const inv = invoices.find(i=> i.id === invoiceId);
    if(inv){
      if(!inv.payments) inv.payments = [];
      inv.payments.push({ id: rec.id, datetime: rec.datetime, amount: rec.amount, method: rec.method });
    }
  }
  saveAll();
  clearDocForm();
  renderDocumentsTable();
  renderInvoicesView();
  alert('تم حفظ السند وخصم الكميات من المخزون.');
}
function clearDocForm(){
  document.getElementById('docType').value = 'سند قبض';
  document.getElementById('docClientSelect').value = '';
  document.getElementById('docName').value = '';
  document.getElementById('docProdSearch').value = '';
  document.getElementById('docReason').value = '';
  document.getElementById('docPaymentMethod').value = 'نقدا';
  docCart = [];
  renderDocCart();
  renderDocProductsTable();
  onDocTypeChange();
}
function onDocTypeChange(){
  const t = document.getElementById('docType').value;
  populateClientSelects();
  const clientSel = document.getElementById('docClientSelect');
  Array.from(clientSel.options).forEach(opt => {
    if(!opt.value) return;
    const idx = Number(opt.value);
    const c = clients[idx];
    if(!c) return;
    if(t === 'سند قبض' && c.type !== 'عميل' && c.type !== 'تاجر'){
      opt.style.display = 'none';
    } else if(t === 'سند صرف' && c.type !== 'مورد'){
      opt.style.display = 'none';
    } else {
      opt.style.display = 'block';
    }
  });
  renderDocProductsTable();
}
function onDocClientChange(){
  const idx = Number(document.getElementById('docClientSelect').value);
  if(!Number.isFinite(idx) || !clients[idx]){ document.getElementById('docName').value=''; return; }
  const c = clients[idx];
  document.getElementById('docName').value = c.name;
}
function renderDocumentsTable(){
  const q = (document.getElementById('docSearch')||{value:''}).value.trim().toLowerCase();
  const tbody = document.getElementById('docsTbody'); tbody.innerHTML = '';
  if(!documents.length){ tbody.innerHTML = '<tr><td colspan="6" class="small">لا توجد مستندات</td></tr>'; return; }
  documents.slice().reverse().forEach(d=>{
    if(q && !((d.clientName||'').toLowerCase().includes(q) || (d.reason||'').toLowerCase().includes(q) || (d.type||'').toLowerCase().includes(q))) return;
    const productsText = (d.products || []).map(p => p.sellType === 'unit' ? `${p.prodName} (${p.qty} وحدة)` : `${p.prodName} (${p.qty} كرتون)`).join(', ') || '-';
    const tr = document.createElement('tr');
    tr.innerHTML = `<td>${escapeHtml(d.type)}</td><td>${escapeHtml(d.clientName)}</td><td>${escapeHtml(productsText)}</td><td>${d.amount}</td><td>${toDateString(d.datetime)}</td>
      <td>
        <button class="btn" onclick="printSingleDocument('${d.id}')">طباعة</button>
        <button class="btn" onclick="deleteDocument('${d.id}')">حذف</button>
      </td>`;
    tbody.appendChild(tr);
  });
}
function printSingleDocument(id){
  const d = documents.find(x=>x.id===id); if(!d) return;
  const company = ' شعبيات الحارة';
  const productsText = (d.products || []).map(p => p.sellType === 'unit' ? `${p.prodName} (${p.qty} وحدة)` : `${p.prodName} (${p.qty} كرتون)`).join(', ') || '-';
  const html = `<div style="direction:rtl;font-family:Arial;padding:10px;max-width:700px;margin:10px auto;border:1px solid #ddd;border-radius:8px">
    <div style="display:flex;justify-content:space-between"><div style="font-weight:900;color:#b37a3b"><img src="${logoDataUrl}" style="height:36px;vertical-align:middle" /> ${company}</div><div>تاريخ: ${toDateString(d.datetime)}</div></div>
    <div style="margin-top:8px"><strong>النوع:</strong> ${escapeHtml(d.type)}</div>
    <div><strong>الاسم:</strong> ${escapeHtml(d.clientName)}</div>
    <div><strong>المنتجات:</strong> ${escapeHtml(productsText)}</div>
    <div><strong>المبلغ:</strong> ${d.amount}</div>
    <div style="margin-top:8px"><strong>السبب:</strong> ${escapeHtml(d.reason||'-')}</div>
    <div style="margin-top:8px"><strong>مرتبطة بفاتورة:</strong> ${escapeHtml(d.invoiceId || '-')}</div>
    <div style="margin-top:8px"><strong>الطريقة:</strong> ${escapeHtml(d.method||'-')}</div>
  </div>`;
  const w = window.open('','_blank'); w.document.write(`<html dir="rtl"><head><meta charset="utf-8"></head><body>${html}</body></html>`); w.document.close(); w.focus(); w.print();
}
function deleteDocument(id){ 
  if(!confirm('حذف المستند؟')) return; 
  documents = documents.filter(x=>x.id !== id); 
  receipts = receipts.filter(x=>x.id !== id); 
  expenses = expenses.filter(x=>x.id !== id); 
  invoices.forEach(inv=>{ 
    if(inv.payments) inv.payments = inv.payments.filter(p=> p.id !== id); 
  }); 
  saveAll(); 
  renderDocumentsTable(); 
  renderInvoicesView(); 
}
function exportClientDocsCSV(){
  if(!documents.length){ alert('لا توجد مستندات'); return; }
  const rows = [['النوع','الاسم','المنتجات','المبلغ','التاريخ','فاتورة مرتبطة','طريقة']];
  documents.forEach(d=> {
    const productsText = (d.products || []).map(p => p.sellType === 'unit' ? `${p.prodName}(${p.qty}u)` : `${p.prodName}(${p.qty}c)`).join('; ');
    rows.push([d.type,d.clientName,productsText,d.amount,toDateString(d.datetime),d.invoiceId||'',d.method||'']);
  });
  const csv = rows.map(r => r.map(c => `"${String(c||'').replace(/"/g,'""')}"`).join(',')).join('\n');
  downloadText('client_documents.csv', csv);
}

/* ===========================
   Reports
   =========================== */
function generateDailyReport(){
  const day = document.getElementById('reportDay').value; if(!day){ alert('اختر تاريخاً'); return; }
  const start = new Date(day); start.setHours(0,0,0,0); const end = new Date(day); end.setHours(23,59,59,999);
  const list = invoices.filter(inv => { const d=new Date(inv.datetime); return d>=start && d<=end; });
  let total = 0; let paidTotal = 0; list.forEach(i=> { total += (i.total||0); paidTotal += sumPaymentsOfInvoice(i); });
  let html = `<div class="client-card">عدد الفواتير: ${list.length} — المجموع الكلي: ${total.toFixed(2)} — المدفوع: ${paidTotal.toFixed(2)}</div>`;
  html += `<table><thead><tr><th>رقم الفاتورة</th><th>العميل</th><th>التاريخ</th><th>الإجمالي</th><th>المدفوع</th></tr></thead><tbody>`;
  list.forEach(i=> html += `<tr><td>${escapeHtml(i.id)}</td><td>${escapeHtml(i.client.name||'-')}</td><td>${toDateString(i.datetime)}</td><td>${i.total.toFixed(2)}</td><td>${sumPaymentsOfInvoice(i).toFixed(2)}</td></tr>`);
  html += `</tbody></table>`;
  document.getElementById('dailyReport').innerHTML = html; window._lastDailyReport = {date:day, rows:list};
}
function exportDailyCSV(){ 
  const data = window._lastDailyReport; 
  if(!data){ alert('اعرض التقرير أولاً'); return; } 
  const rows = [['رقم الفاتورة','العميل','التاريخ','الإجمالي','المدفوع']]; 
  data.rows.forEach(i=> rows.push([i.id,i.client.name,toDateString(i.datetime),i.total,sumPaymentsOfInvoice(i)])); 
  const csv = rows.map(r => r.map(c=>`"${String(c||'').replace(/"/g,'""')}"`).join(',')).join('\n'); 
  downloadText(`daily_report_${data.date}.csv`, csv); 
}
function generateMonthlyReport(){ 
  const m = document.getElementById('reportMonth').value; 
  if(!m){ alert('اختر شهراً'); return; } 
  const [y,mm] = m.split('-').map(Number); 
  const start = new Date(y,mm-1,1,0,0,0,0); 
  const end = new Date(y,mm,0,23,59,59,999); 
  const list = invoices.filter(inv => { const d=new Date(inv.datetime); return d>=start && d<=end; }); 
  let total = 0; let paidTotal = 0; list.forEach(i=> { total += (i.total||0); paidTotal += sumPaymentsOfInvoice(i); }); 
  let html = `<div class="client-card">عدد الفواتير: ${list.length} — المجموع الكلي: ${total.toFixed(2)} — المدفوع: ${paidTotal.toFixed(2)}</div>`; 
  html += `<table><thead><tr><th>رقم الفاتورة</th><th>العميل</th><th>التاريخ</th><th>الإجمالي</th><th>المدفوع</th></tr></thead><tbody>`; 
  list.forEach(i=> html += `<tr><td>${escapeHtml(i.id)}</td><td>${escapeHtml(i.client.name||'-')}</td><td>${toDateString(i.datetime)}</td><td>${i.total.toFixed(2)}</td><td>${sumPaymentsOfInvoice(i).toFixed(2)}</td></tr>`); 
  html += `</tbody></table>`; 
  document.getElementById('monthlyReport').innerHTML = html; 
  window._lastMonthlyReport = {month:m, rows:list}; 
}
function exportMonthlyCSV(){ 
  const data = window._lastMonthlyReport; 
  if(!data){ alert('اعرض التقرير أولاً'); return; } 
  const rows = [['رقم الفاتورة','العميل','التاريخ','الإجمالي','المدفوع']]; 
  data.rows.forEach(i=> rows.push([i.id,i.client.name,toDateString(i.datetime),i.total,sumPaymentsOfInvoice(i)])); 
  const csv = rows.map(r => r.map(c=>`"${String(c||'').replace(/"/g,'""')}"`).join(',')).join('\n'); 
  downloadText(`monthly_report_${data.month}.csv`, csv); 
}

/* ===========================
   Init
   =========================== */
window.addEventListener('load', ()=>{
  const today = new Date().toISOString().slice(0,10);
  document.getElementById('reportDay').value = today;
  document.getElementById('reportMonth').value = new Date().toISOString().slice(0,7);
  renderAllInitial();
});
function renderAllInitial(){
  renderClients();
  renderInventory();
  renderProductsTable();
  populateClientSelects();
  renderCart();
  renderInvoicesView();
  renderDocumentsTable();
}
function populateClientSelects(){
  const docSel = document.getElementById('docClientSelect');
  if(docSel){ 
    docSel.innerHTML = '<option value="">— اختر —</option>'; 
    clients.forEach((c,i)=> docSel.insertAdjacentHTML('beforeend', `<option value="${i}">${escapeHtml(c.name)} — ${escapeHtml(c.type||'')}</option>`)); 
  }
}
function addProductByBarcode(){
  const code = document.getElementById('barcodeInput').value.trim();
  if(!code) return;
  let found = false;
  categories.forEach(cat => {
    Object.keys(cat.products || {}).forEach(prodName => {
      const item = cat.products[prodName];
      if(item.barcode === code){
        addToCart(cat.name, prodName, 'unit');
        found = true;
      }
    });
  });
  if(!found) alert('الباركود غير موجود');
  document.getElementById('barcodeInput').value = '';
}
function exportCurrentInvoiceDraft(){
  if(cart.length === 0){ alert('السلة فارغة'); return; }
  const draft = { cart, selectedClient, paymentType: document.getElementById('paymentType').value, paidAmount: document.getElementById('invoicePaidAmount').value, notes: document.getElementById('invoiceNotes').value };
  downloadText('invoice_draft.json', JSON.stringify(draft, null, 2));
}
function exportCategories(){
  downloadText('inventory_export.json', JSON.stringify(categories, null, 2));
}
function exportAllInvoices(){
  downloadText('all_invoices.json', JSON.stringify(invoices, null, 2));
}
function printClientDocuments(){
  alert('طباعة جميع المستندات غير مدعومة حالياً. يمكنك طباعة كل مستند على حدة.');
}
</script>
</body>
</html>
