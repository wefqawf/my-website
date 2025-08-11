# my-website
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>حاسبة ضريبة الدخل الأردنية</title>
<style>
  :root{
    --bg:#0f172a;
    --card:#111827;
    --muted:#94a3b8;
    --text:#e5e7eb;
    --accent:#22c55e;
    --accent-2:#3b82f6;
    --danger:#ef4444;
    --border:#1f2937;
    --chip:#0b1220;
  }
  *{box-sizing:border-box}
  body{
    margin:0; background:linear-gradient(180deg,#0b1022, #0a0f1c 50%, #080c16 100%);
    font-family: "Tajawal", system-ui, -apple-system, Segoe UI, Roboto, "Noto Sans Arabic", Arial, sans-serif;
    color:var(--text);
  }
  .container{max-width:1100px; margin:40px auto; padding:20px}
  .header{display:flex; align-items:center; gap:14px; margin-bottom:18px}
  .logo{
    width:44px; height:44px; border-radius:12px; background:linear-gradient(135deg, var(--accent), var(--accent-2));
    display:grid; place-items:center; font-weight:800; color:#041019; box-shadow:0 10px 30px rgba(34,197,94,.35);
  }
  h1{font-size:1.6rem; margin:0}
  p.lead{margin:.25rem 0 0; color:var(--muted); font-size:.95rem}

  .grid{display:grid; gap:16px; grid-template-columns:1fr}
  @media (min-width:980px){.grid{grid-template-columns:1.3fr .9fr}}

  .card{
    background:linear-gradient(180deg, #0b1020, #0a0e19);
    border:1px solid var(--border); border-radius:16px; padding:18px;
    box-shadow:0 10px 30px rgba(0,0,0,.35);
  }
  .section-title{display:flex; align-items:center; justify-content:space-between; margin-bottom:10px}
  .section-title h2{font-size:1.1rem; margin:0}
  .hint{color:var(--muted); font-size:.9rem}

  .row{display:grid; gap:12px; grid-template-columns:1fr}
  @media (min-width:680px){
    .row.cols-2{grid-template-columns:1fr 1fr}
    .row.cols-3{grid-template-columns:1fr 1fr 1fr}
  }

  label{display:block; font-size:.95rem; margin:4px 2px 6px}
  .control{display:flex; gap:10px; align-items:center; flex-wrap:wrap; margin:6px 0 12px}
  .radio{
    display:flex; align-items:center; gap:10px; background:#0a1222;
    border:1px solid var(--border); padding:10px 14px; border-radius:12px; cursor:pointer; transition:.2s;
  }
  .radio input{accent-color:var(--accent)}
  .radio:hover{border-color:#263244}

  .input{
    background:#0a1222; border:1px solid var(--border); color:var(--text);
    border-radius:12px; padding:12px 14px; width:100%; outline:none; transition:.2s;
  }
  .input:focus{border-color:#2a7ef3; box-shadow:0 0 0 3px rgba(59,130,246,.2)}
  .input[readonly]{opacity:.85}

  .note{color:var(--muted); font-size:.85rem; margin-top:6px}
  .toggle{display:flex; align-items:center; gap:10px; cursor:pointer; user-select:none}
  .toggle input{display:none}
  .switch{
    width:46px; height:26px; background:#0f192c; border:1px solid var(--border); border-radius:999px; position:relative; transition:.2s;
  }
  .switch::after{
    content:""; position:absolute; top:2px; right:2px; width:20px; height:20px; border-radius:50%;
    background:#263244; transition:.2s;
  }
  .toggle input:checked + .switch{background:linear-gradient(90deg,#1db954,#3ba55d); border-color:transparent}
  .toggle input:checked + .switch::after{right:24px; background:white}

  .dropzone{
    border:1.5px dashed #28405f; background:linear-gradient(180deg,#071225,#081022);
    border-radius:14px; padding:18px; text-align:center; transition:.2s;
  }
  .dropzone.drag{border-color:var(--accent); background:linear-gradient(180deg,#071a2a,#081a28)}
  .dropzone .title{font-weight:600; margin-bottom:8px}
  .dropzone .sub{color:var(--muted); font-size:.9rem}
  .dropzone input{display:none}
  .dz-actions{margin-top:12px; display:flex; gap:10px; justify-content:center; flex-wrap:wrap}
  .btn{
    background:#0e172a; border:1px solid var(--border); color:var(--text);
    border-radius:12px; padding:10px 14px; cursor:pointer; transition:.2s; font-weight:600;
  }
  .btn:hover{border-color:#334155}
  .btn.primary{background:linear-gradient(90deg,#2563eb,#22c55e); border:none}
  .chips{display:flex; flex-wrap:wrap; gap:8px; margin-top:8px}
  .chip{background:var(--chip); border:1px solid #182133; color:#9fb5d1; padding:6px 10px; border-radius:999px; font-size:.85rem}

  .summary{display:grid; gap:10px; grid-template-columns:1fr}
  @media (min-width:700px){.summary{grid-template-columns:1fr 1fr}}
  .stat{background:#0b1324; border:1px solid var(--border); border-radius:14px; padding:14px}
  .stat .label{color:var(--muted); font-size:.85rem}
  .stat .value{font-size:1.15rem; font-weight:700; margin-top:6px}

  table{width:100%; border-collapse:collapse; margin-top:10px; border-radius:12px; overflow:hidden}
  th, td{padding:10px 8px; border-bottom:1px solid #172132; text-align:center}
  th{background:#0b1426; color:#bcd0ec; font-weight:600}
  tr:last-child td{border-bottom:none}

  .footer-note{color:var(--muted); font-size:.85rem; margin-top:14px}
</style>
</head>
<body>
  <div class="container">
    <div class="header">
      <div class="logo">JD</div>
      <div>
        <h1>حاسبة ضريبة الدخل الأردنية</h1>
        <p class="lead">أدخل الدخل السنوي والإعفاءات، واختر الحالة: أعزب أو متزوج (مع إمكانية دمج الدخل).</p>
      </div>
    </div>

    <div class="grid">
      <!-- المدخلات -->
      <div class="card">
        <div class="section-title">
          <h2>المدخلات</h2>
          <span class="hint">كل القيم بالدينار الأردني</span>
        </div>

        <!-- الحالة الاجتماعية -->
        <label>الحالة الاجتماعية</label>
        <div class="control">
          <label class="radio">
            <input type="radio" name="status" value="single" checked />
            <span>أعزب</span>
          </label>
          <label class="radio">
            <input type="radio" name="status" value="married" />
            <span>متزوج</span>
          </label>
        </div>

        <!-- مسار الأعزب -->
        <div id="single-section">
          <div class="row cols-2">
            <div>
              <label for="singleIncome">الدخل السنوي</label>
              <input id="singleIncome" class="input" type="number" min="0" step="0.01" placeholder="مثال: 24000" />
            </div>
            <div>
              <label for="singleBaseEx">الإعفاء الأساسي</label>
              <input id="singleBaseEx" class="input" type="number" min="0" step="0.01" value="" />
            </div>
          </div>
          <div class="row cols-2">
            <div>
              <label for="singleExtraEx">الإعفاء الإضافي (بفواتير، حتى 1000)</label>
              <input id="singleExtraEx" class="input" type="number" min="0" max="1000" step="0.01" value="" />
            </div>
            <div>
              <label>فواتير الإعفاء الإضافي (اختياري)</label>
              <div id="dz-single" class="dropzone" tabindex="0">
                <div class="title">إسحب وأفلت الفواتير هنا</div>
                <div class="sub">أو</div>
                <div class="dz-actions">
                  <button class="btn">تصفح الملفات</button>
                  <span class="hint">صور أو PDF</span>
                </div>
                <input type="file" multiple accept=".jpg,.jpeg,.png,.pdf" />
                <div class="chips" data-files></div>
              </div>
            </div>
          </div>
        </div>

        <!-- مسار المتزوج -->
        <div id="married-section" style="display:none">
          <div class="control" style="margin-top:6px">
            <label class="toggle">
              <input id="mergeIncomes" type="checkbox" />
              <span class="switch"></span>
              <span>دمج دخل الزوجين؟</span>
            </label>
          </div>

          <div class="row cols-2">
            <div>
              <label for="husbandIncome">دخل الزوج السنوي</label>
              <input id="husbandIncome" class="input" type="number" min="0" step="0.01" placeholder="مثال: 24000" />
            </div>
            <div>
              <label for="husbandBaseEx">إعفاء الزوج الأساسي</label>
              <input id="husbandBaseEx" class="input" type="number" min="0" step="0.01" value="" />
              <!-- تمت إزالة ملاحظة "الافتراضي 9000" سابقًا حسب المطلوب -->
            </div>
          </div>

          <div class="row cols-3">
            <div>
              <label for="husbandExtraEx">إعفاء الزوج الإضافي (حتى 1000)</label>
              <input id="husbandExtraEx" class="input" type="number" min="0" max="1000" step="0.01" value="" />
            </div>
            <div>
              <label for="childrenCount">عدد الأبناء (حتى 3)</label>
              <input id="childrenCount" class="input" type="number" min="0" max="3" step="1" value="" />
              <div class="note">إعفاء الأبناء = عدد الأبناء × 1000 (بحد أقصى 3000).</div>
            </div>
            <div>
              <label for="childrenEx">عفاءات الأبناء</label>
              <input id="childrenEx" class="input" type="number" min="0" max="3000" step="0.01" value="" />
            </div>
          </div>

          <hr style="border:none; border-top:1px solid var(--border); margin:14px 0">

          <div class="control">
            <label class="toggle">
              <input id="wifeWorks" type="checkbox" />
              <span class="switch"></span>
              <span>الزوجة تعمل؟</span>
            </label>
            <label class="toggle">
              <input id="wifeAcceptsEx" type="checkbox" checked />
              <span class="switch"></span>
              <span>الزوجة تقبل الإعفاء؟</span>
            </label>
          </div>

          <div id="wife-row" class="row cols-3">
            <div>
              <label for="wifeIncome">دخل الزوجة السنوي</label>
              <input id="wifeIncome" class="input" type="number" min="0" step="0.01" value="" />
            </div>
            <div>
              <label for="wifeBaseEx">إعفاء الزوجة الأساسي</label>
              <input id="wifeBaseEx" class="input" type="number" min="0" step="0.01" placeholder="" />
              <div class="note">عند الدمج: يُخصم دخل الزوجة من هذا الإعفاء ويُحوَّل المتبقي لصالح الزوج.</div>
            </div>
            <div>
              <label for="wifeExtraEx">إعفاء الزوجة الإضافي (حتى 1000)</label>
              <input id="wifeExtraEx" class="input" type="number" min="0" max="1000" step="0.01" value="" />
            </div>
          </div>

          <div>
            <label>فواتير الإعفاءات الإضافية (اختياري)</label>
            <div id="dz-married" class="dropzone" tabindex="0">
              <div class="title">إسحب وأفلت الفواتير هنا</div>
              <div class="sub">أو</div>
              <div class="dz-actions">
                <button class="btn">تصفح الملفات</button>
                <span class="hint">صور أو PDF</span>
              </div>
              <input type="file" multiple accept=".jpg,.jpeg,.png,.pdf" />
              <div class="chips" data-files></div>
            </div>
          </div>
        </div>

        <div class="control" style="margin-top:16px">
          <button id="calcBtn" class="btn primary">حساب الضريبة</button>
          <button id="resetBtn" class="btn">إعادة تعيين</button>
        </div>
      </div>

      <!-- النتائج -->
      <div class="card">
        <div class="section-title">
          <h2>النتائج</h2>
          <span class="hint">تفاصيل الضريبة وفق الشرائح</span>
        </div>

        <div class="summary">
          <div class="stat">
            <div class="label">إجمالي الدخل</div>
            <div id="sumIncome" class="value">—</div>
          </div>
          <div class="stat">
            <div class="label">إجمالي الإعفاءات</div>
            <div id="sumExemptions" class="value">—</div>
          </div>
          <div class="stat">
            <div class="label">الدخل الخاضع للضريبة</div>
            <div id="taxableIncome" class="value">—</div>
          </div>
          <div class="stat">
            <div class="label">الضريبة المستحقة</div>
            <div id="taxDue" class="value">—</div>
          </div>
        </div>

        <div id="breakdownWrap" style="margin-top:14px; display:none">
          <table>
            <thead>
              <tr>
                <th>الشريحة</th>
                <th>المبلغ الخاضع</th>
                <th>النسبة</th>
                <th>قيمة الضريبة</th>
              </tr>
            </thead>
            <tbody id="breakdown"></tbody>
          </table>
          <div class="footer-note">
            الشرائح: 5% لأول 5000، 10% للخمسة آلاف التالية، 15% للخمسة آلاف التالية، 20% للخمسة آلاف التالية،
            25% لما بعد ذلك ولغاية مليون، 30% لما يزيد عن مليون.
          </div>
        </div>
      </div>
    </div>
  </div>

<script>
  // أدوات مساعدة
  const fmt = n => isNaN(n) ? "—" : new Intl.NumberFormat("ar-JO",{minimumFractionDigits:2, maximumFractionDigits:2}).format(n) + " د.أ";
  const clamp = (v, min, max) => Math.min(Math.max(v, min), max);

  // عناصر DOM
  const statusRadios = document.querySelectorAll('input[name="status"]');
  const singleSection = document.getElementById('single-section');
  const marriedSection = document.getElementById('married-section');

  const singleIncome = document.getElementById('singleIncome');
  const singleBaseEx = document.getElementById('singleBaseEx');
  const singleExtraEx = document.getElementById('singleExtraEx');

  const mergeIncomes = document.getElementById('mergeIncomes');
  const husbandIncome = document.getElementById('husbandIncome');
  const husbandBaseEx = document.getElementById('husbandBaseEx');
  const husbandExtraEx = document.getElementById('husbandExtraEx');
  const childrenCount = document.getElementById('childrenCount');
  const childrenEx = document.getElementById('childrenEx');

  const wifeWorks = document.getElementById('wifeWorks');
  const wifeAcceptsEx = document.getElementById('wifeAcceptsEx');
  const wifeIncome = document.getElementById('wifeIncome');
  const wifeBaseEx = document.getElementById('wifeBaseEx');
  const wifeExtraEx = document.getElementById('wifeExtraEx');

  const sumIncome = document.getElementById('sumIncome');
  const sumExemptions = document.getElementById('sumExemptions');
  const taxableIncome = document.getElementById('taxableIncome');
  const taxDue = document.getElementById('taxDue');

  const breakdownWrap = document.getElementById('breakdownWrap');
  const breakdown = document.getElementById('breakdown');

  const calcBtn = document.getElementById('calcBtn');
  const resetBtn = document.getElementById('resetBtn');

  // التنقل بين المسارات
  statusRadios.forEach(r => r.addEventListener('change', () => {
    const val = document.querySelector('input[name="status"]:checked').value;
    singleSection.style.display = val === 'single' ? 'block' : 'none';
    marriedSection.style.display = val === 'married' ? 'block' : 'none';
  }));

  // تفعيل حقول الزوجة حسب الخيارات
  function toggleWifeFields(){
    const works = wifeWorks.checked;
    wifeIncome.disabled = !works;
    wifeIncome.parentElement.style.opacity = works ? 1 : .7;

    const accepts = wifeAcceptsEx.checked;
    wifeExtraEx.disabled = !accepts;
    wifeExtraEx.parentElement.style.opacity = accepts ? 1 : .7;
    // ملاحظة: إبقاء خانة إعفاء الزوجة الأساسي مفعّلة دائمًا للإدخال اليدوي
  }
  wifeWorks.addEventListener('change', toggleWifeFields);
  wifeAcceptsEx.addEventListener('change', toggleWifeFields);
  toggleWifeFields();

  // مناطق رفع حديثة
  function setupDropzone(el){
    const input = el.querySelector('input[type="file"]');
    const btn = el.querySelector('.btn');
    const chips = el.querySelector('[data-files]');
    function refreshChips(files){
      chips.innerHTML = '';
      [...files].forEach(f=>{
        const c = document.createElement('span');
        c.className = 'chip';
        c.textContent = f.name;
        chips.appendChild(c);
      });
    }
    btn.addEventListener('click', (e)=>{ e.preventDefault(); input.click(); });
    el.addEventListener('dragover', (e)=>{ e.preventDefault(); el.classList.add('drag'); });
    el.addEventListener('dragleave', ()=> el.classList.remove('drag'));
    el.addEventListener('drop', (e)=>{
      e.preventDefault(); el.classList.remove('drag');
      input.files = e.dataTransfer.files;
      refreshChips(input.files);
    });
    input.addEventListener('change', ()=> refreshChips(input.files));
    el.addEventListener('keydown', (e)=>{ if(e.key==='Enter' || e.key===' ') { e.preventDefault(); input.click(); }});
  }
  setupDropzone(document.getElementById('dz-single'));
  setupDropzone(document.getElementById('dz-married'));

  // الشرائح التصاعدية
  function calcProgressiveTax(taxable){
    const rows = [];
    let remaining = Math.max(0, taxable);
    let total = 0;

    function take(amount, rate, label){
      const part = Math.min(remaining, amount);
      if(part > 0){
        const t = part * rate;
        rows.push({label, part, rate, tax: t});
        total += t;
        remaining -= part;
      } else {
        rows.push({label, part: 0, rate, tax: 0});
      }
    }

    take(5000, 0.05, 'أول 5000');
    take(5000, 0.10, 'الخمسة آلاف التالية');
    take(5000, 0.15, 'الخمسة آلاف التالية');
    take(5000, 0.20, 'الخمسة آلاف التالية');
    take(980000, 0.25, 'حتى مليون دينار');
    if(remaining > 0){
      rows.push({label:'ما زاد عن مليون', part: remaining, rate: 0.30, tax: remaining * 0.30});
      total += remaining * 0.30;
      remaining = 0;
    }
    return {rows, total};
  }

  // الحساب الرئيسي
  function calculate(){
    const status = document.querySelector('input[name="status"]:checked').value;

    let gross = 0;
    let exemptions = 0;

    if(status === 'single'){
      const income = Number(singleIncome.value || 0);
      const baseEx = Number(singleBaseEx.value || 0);
      const extraEx = clamp(Number(singleExtraEx.value || 0), 0, 1000);

      gross = income;
      exemptions = baseEx + extraEx;

    } else {
      const merge = mergeIncomes.checked;
      const hIncome = Number(husbandIncome.value || 0);
      const hBase = Number(husbandBaseEx.value || 0);
      const hExtra = clamp(Number(husbandExtraEx.value || 0), 0, 1000);
      const childEx = clamp(Number(childrenEx.value || 0), 0, 3000);

      if(!merge){
        gross = hIncome;
        exemptions = hBase + hExtra + childEx;
      } else {
        const wWorks = wifeWorks.checked;
        const wAccepts = wifeAcceptsEx.checked;
        const wIncome = wWorks ? Number(wifeIncome.value || 0) : 0;
        const wBaseInput = Number(wifeBaseEx.value || 0);
        const wExtra = wAccepts ? clamp(Number(wifeExtraEx.value || 0), 0, 1000) : 0;

        gross = hIncome + wIncome;

        // عند الدمج: يتم احتساب الإعفاء الأساسي للزوجة من المدخل اليدوي ثم طرح دخلها منه ونقل المتبقي
        const wBaseEffective = wAccepts ? Math.max(0, wBaseInput - wIncome) : 0;

        exemptions = hBase + wBaseEffective + hExtra + wExtra + childEx;
      }
    }

    const taxable = Math.max(0, gross - exemptions);
    const {rows, total} = calcProgressiveTax(taxable);

    // عرض النتائج
    sumIncome.textContent = fmt(gross);
    sumExemptions.textContent = fmt(exemptions);
    taxableIncome.textContent = fmt(taxable);
    taxDue.textContent = fmt(total);

    breakdownWrap.style.display = 'block';
    breakdown.innerHTML = rows.map(r => `
      <tr>
        <td>${r.label}</td>
        <td>${fmt(r.part)}</td>
        <td>${(r.rate*100).toFixed(0)}%</td>
        <td>${fmt(r.tax)}</td>
      </tr>
    `).join('');
  }

  // أزرار
  calcBtn.addEventListener('click', calculate);
  resetBtn.addEventListener('click', ()=>{
    document.querySelector('input[name="status"][value="single"]').checked = true;
    singleSection.style.display = 'block';
    marriedSection.style.display = 'none';

    singleIncome.value = '';
    singleBaseEx.value = 9000;
    singleExtraEx.value = 0;

    mergeIncomes.checked = false;
    husbandIncome.value = '';
    husbandBaseEx.value = 9000;
    husbandExtraEx.value = 0;
    childrenCount.value = 0;
    childrenEx.value = 0; // إدخال يدوي

    wifeWorks.checked = false;
    wifeAcceptsEx.checked = true;
    wifeIncome.value = 0;
    wifeBaseEx.value = ''; // إدخال يدوي بدون قيمة افتراضية
    wifeExtraEx.value = 0;
    toggleWifeFields();

    sumIncome.textContent = '—';
    sumExemptions.textContent = '—';
    taxableIncome.textContent = '—';
    taxDue.textContent = '—';
    breakdownWrap.style.display = 'none';
    breakdown.innerHTML = '';
  });

  // مستمعات اختيارية للحساب الفوري
  [singleIncome, singleBaseEx, singleExtraEx,
   husbandIncome, husbandBaseEx, husbandExtraEx,
   childrenCount, childrenEx, wifeIncome, wifeBaseEx, wifeExtraEx,
   mergeIncomes, wifeWorks, wifeAcceptsEx].forEach(el=>{
    el.addEventListener('input', ()=>{ /* يمكنك تفعيل حساب فوري إن رغبت */ });
  });
</script>
</body>
</html>
