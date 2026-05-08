<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Dashboard HSSE Bulanan — Pertamina Gas</title>
  <link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='.9em' font-size='90'>🛡️</text></svg>">
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --green-50:  #E1F5EE;
      --green-100: #9FE1CB;
      --green-400: #1D9E75;
      --green-600: #0F6E56;
      --green-800: #085041;
      --green-900: #04342C;
      --amber-50:  #FAEEDA;
      --amber-400: #EF9F27;
      --amber-600: #BA7517;
      --amber-800: #633806;
      --red-50:    #FCEBEB;
      --red-400:   #E24B4A;
      --red-600:   #A32D2D;
      --red-800:   #501313;
      --blue-50:   #E6F1FB;
      --blue-400:  #378ADD;
      --blue-600:  #185FA5;
      --blue-800:  #042C53;
      --bg:        #F4F2EC;
      --surface:   #FFFFFF;
      --surface2:  #F1EFE8;
      --border:    rgba(0,0,0,.09);
      --text:       #1A1A18;
      --text-muted: #5F5E5A;
      --text-hint:  #888780;
      --radius-sm: 6px;
      --radius-md: 10px;
      --radius-lg: 14px;
      --shadow-sm: 0 1px 3px rgba(0,0,0,.07);
    }

    @media (prefers-color-scheme: dark) {
      :root {
        --bg:       #1A1A18;
        --surface:  #232320;
        --surface2: #2C2C2A;
        --border:   rgba(255,255,255,.09);
        --text:       #F0EDE8;
        --text-muted: #B4B2A9;
        --text-hint:  #888780;
      }
    }

    html { font-size: 15px; }

    body {
      font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
      background: var(--bg);
      color: var(--text);
      min-height: 100vh;
      padding: 1rem;
      line-height: 1.5;
    }

    .container { max-width: 960px; margin: 0 auto; }

    /* NAV */
    .top-nav {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 0.9rem 1.25rem;
      background: var(--green-800);
      border-radius: var(--radius-lg);
      margin-bottom: 1.25rem;
      gap: 1rem;
    }
    .nav-brand { display: flex; align-items: center; gap: 14px; }
    .nav-logo {
      background: rgba(255,255,255,.18);
      color: #fff;
      font-size: 12px;
      font-weight: 600;
      letter-spacing: 2px;
      padding: 7px 14px;
      border-radius: var(--radius-sm);
      flex-shrink: 0;
    }
    .nav-title { color: #fff; font-size: 15px; font-weight: 500; }
    .nav-sub   { color: var(--green-100); font-size: 11px; margin-top: 1px; }
    .nav-actions { display: flex; gap: 8px; flex-shrink: 0; }

    /* TABS */
    .tabs { display: flex; gap: 8px; margin-bottom: 1.25rem; flex-wrap: wrap; }
    .tab-btn {
      padding: 8px 22px;
      border-radius: 20px;
      border: 1px solid var(--border);
      background: var(--surface);
      color: var(--text-muted);
      font-size: 13px;
      cursor: pointer;
      transition: background .18s, color .18s, border-color .18s;
    }
    .tab-btn.active { background: var(--green-600); color: #fff; border-color: var(--green-600); }
    .tab-btn:hover:not(.active) { background: var(--surface2); }

    .section { display: none; }
    .section.visible { display: block; }

    /* BUTTONS */
    .btn-primary {
      padding: 10px 30px;
      background: var(--green-600);
      color: #fff;
      border: none;
      border-radius: var(--radius-md);
      font-size: 14px;
      font-weight: 500;
      cursor: pointer;
      transition: background .18s;
    }
    .btn-primary:hover { background: var(--green-800); }
    .btn-ghost {
      padding: 8px 18px;
      background: transparent;
      color: var(--text-muted);
      border: 1px solid var(--border);
      border-radius: var(--radius-md);
      font-size: 13px;
      cursor: pointer;
      transition: background .18s;
    }
    .btn-ghost:hover { background: var(--surface2); }

    /* FORM */
    .form-card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius-lg);
      padding: 1.5rem;
      box-shadow: var(--shadow-sm);
    }
    .form-block { margin-bottom: 1.5rem; }
    .form-block-title {
      font-size: 12px;
      font-weight: 600;
      color: var(--green-600);
      text-transform: uppercase;
      letter-spacing: .8px;
      margin-bottom: 10px;
      padding-bottom: 6px;
      border-bottom: 2px solid var(--green-400);
      display: flex;
      align-items: center;
      gap: 6px;
    }
    .form-grid { display: grid; gap: 12px; }
    .form-grid.col2 { grid-template-columns: 1fr 1fr; }
    @media (max-width: 560px) { .form-grid.col2 { grid-template-columns: 1fr; } }
    .form-group { display: flex; flex-direction: column; gap: 5px; }
    .form-group label { font-size: 11px; color: var(--text-muted); font-weight: 500; }
    .form-group input,
    .form-group select {
      padding: 9px 11px;
      border-radius: var(--radius-sm);
      border: 1px solid var(--border);
      background: var(--surface2);
      color: var(--text);
      font-size: 13px;
      transition: border-color .18s, box-shadow .18s;
    }
    .form-group input:focus,
    .form-group select:focus {
      outline: none;
      border-color: var(--green-400);
      box-shadow: 0 0 0 3px rgba(29,158,117,.12);
    }
    .form-group input.readonly { color: var(--text-muted); cursor: default; }
    .form-actions {
      display: flex;
      gap: 10px;
      align-items: center;
      margin-top: 1.5rem;
      padding-top: 1.25rem;
      border-top: 1px solid var(--border);
    }
    .empty-state { text-align: center; padding: 5rem 1rem; color: var(--text-muted); }
    .empty-icon { font-size: 3rem; margin-bottom: 1rem; }

    /* INFOGRAFIS */
    .infografis { animation: fadeIn .4s ease; }
    @keyframes fadeIn { from { opacity: 0; transform: translateY(8px); } to { opacity: 1; transform: translateY(0); } }

    .info-header {
      background: linear-gradient(135deg, var(--green-900) 0%, var(--green-400) 100%);
      border-radius: var(--radius-lg);
      padding: 1.25rem 1.5rem;
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 12px;
      gap: 1rem;
    }
    .info-header-left .eyebrow { font-size: 10px; color: var(--green-100); letter-spacing: 1.5px; text-transform: uppercase; margin-bottom: 4px; }
    .info-header-left .company { color: #fff; font-size: 22px; font-weight: 500; }
    .info-header-left .period  { color: var(--green-100); font-size: 12px; margin-top: 2px; }
    .info-header-right { text-align: right; flex-shrink: 0; }
    .info-badge {
      background: rgba(255,255,255,.18);
      color: #fff;
      font-size: 12px;
      font-weight: 600;
      letter-spacing: 2px;
      padding: 7px 14px;
      border-radius: var(--radius-sm);
      display: inline-block;
      margin-bottom: 8px;
    }

    .metrics-row { display: grid; grid-template-columns: repeat(4, minmax(0,1fr)); gap: 10px; margin-bottom: 12px; }
    @media (max-width: 600px) { .metrics-row { grid-template-columns: repeat(2,1fr); } }

    .row2 { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-bottom: 12px; }
    @media (max-width: 620px) { .row2 { grid-template-columns: 1fr; } }

    .section-card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius-lg);
      padding: 14px;
      box-shadow: var(--shadow-sm);
    }
    .section-card h3 {
      font-size: 11px;
      font-weight: 600;
      color: var(--text-muted);
      text-transform: uppercase;
      letter-spacing: .6px;
      margin-bottom: 12px;
      display: flex;
      align-items: center;
      gap: 6px;
    }

    .metric-card { background: var(--surface2); border-radius: var(--radius-md); padding: 12px; }
    .mc-label { font-size: 10px; color: var(--text-muted); text-transform: uppercase; letter-spacing: .4px; margin-bottom: 4px; }
    .mc-val   { font-size: 22px; font-weight: 500; line-height: 1; }
    .mc-sub   { font-size: 10px; color: var(--text-hint); margin-top: 3px; }

    .ag { background: var(--green-50); }
    .ag .mc-val { color: var(--green-800); }
    .ag .mc-label { color: var(--green-600); }
    .aa { background: var(--amber-50); }
    .aa .mc-val { color: var(--amber-800); }
    .aa .mc-label { color: var(--amber-600); }
    .ar { background: var(--red-50); }
    .ar .mc-val { color: var(--red-800); }
    .ar .mc-label { color: var(--red-600); }
    .ab { background: var(--blue-50); }
    .ab .mc-val { color: var(--blue-800); }
    .ab .mc-label { color: var(--blue-600); }

    .dot { width: 8px; height: 8px; border-radius: 50%; display: inline-block; flex-shrink: 0; }
    .dg { background: var(--green-400); }
    .da { background: var(--amber-400); }
    .dr { background: var(--red-400); }
    .db { background: var(--blue-400); }

    .insiden-row { display: flex; justify-content: space-between; align-items: center; padding: 6px 0; border-bottom: 1px solid var(--border); }
    .insiden-row:last-child { border-bottom: none; }
    .insiden-row .lbl { font-size: 12px; color: var(--text-muted); }
    .insiden-row .val { font-size: 14px; font-weight: 500; }

    .pill { display: inline-block; padding: 2px 9px; border-radius: 10px; font-size: 10px; font-weight: 600; }
    .pg { background: var(--green-50); color: var(--green-800); }
    .pa { background: var(--amber-50); color: var(--amber-800); }
    .pr { background: var(--red-50); color: var(--red-800); }

    .bar-header { display: flex; justify-content: space-between; font-size: 11px; color: var(--text-muted); margin-bottom: 3px; }
    .bar-bg { background: var(--surface2); border-radius: 3px; height: 6px; overflow: hidden; }
    .bar-fill { height: 100%; border-radius: 3px; transition: width .8s ease; }

    .mini-grid2 { display: grid; grid-template-columns: 1fr 1fr; gap: 8px; margin-bottom: 12px; }

    .ltifr-row { margin-top: 10px; padding-top: 10px; border-top: 1px solid var(--border); display: flex; justify-content: space-between; align-items: center; }
    .ltifr-label { font-size: 11px; color: var(--text-muted); }
    .ltifr-val   { font-size: 22px; font-weight: 500; }

    .info-footer { display: flex; justify-content: space-between; align-items: center; padding: 10px 14px; background: var(--surface2); border-radius: var(--radius-md); margin-top: 12px; }
    .info-footer span { font-size: 10px; color: var(--text-hint); }

    @media print {
      body { background: #fff; padding: 0; }
      .top-nav, .tabs { display: none !important; }
      .section { display: block !important; }
      #section-form { display: none !important; }
      .section-card, .form-card { box-shadow: none; border: 1px solid #ddd; }
    }
  </style>
</head>
<body>
  <div class="container">

    <header class="top-nav">
      <div class="nav-brand">
        <div class="nav-logo">HSSE</div>
        <div>
          <div class="nav-title">Dashboard HSSE Bulanan</div>
          <div class="nav-sub">Pertamina Gas — Sistem Pelaporan Terintegrasi</div>
        </div>
      </div>
      <div class="nav-actions">
        <button class="btn-ghost" style="color:#fff;border-color:rgba(255,255,255,.3);background:rgba(255,255,255,.1);" onclick="window.print()">🖨️ Cetak</button>
      </div>
    </header>

    <div class="tabs">
      <button class="tab-btn active" id="tab-form-btn" onclick="showTab('form', this)">📝 Form Input</button>
      <button class="tab-btn" id="tab-infografis-btn" onclick="showTab('infografis', this)">📊 Infografis</button>
    </div>

    <!-- FORM INPUT -->
    <section class="section visible" id="section-form">
      <div class="form-card">

        <div class="form-block">
          <div class="form-block-title"><span>📅</span> Periode Laporan</div>
          <div class="form-grid col2">
            <div class="form-group">
              <label>Bulan</label>
              <select id="f-bulan">
                <option>Januari</option><option>Februari</option><option>Maret</option>
                <option selected>April</option><option>Mei</option><option>Juni</option>
                <option>Juli</option><option>Agustus</option><option>September</option>
                <option>Oktober</option><option>November</option><option>Desember</option>
              </select>
            </div>
            <div class="form-group">
              <label>Tahun</label>
              <input type="number" id="f-tahun" value="2025" min="2020" max="2040" />
            </div>
          </div>
        </div>

        <div class="form-block">
          <div class="form-block-title"><span>⏱️</span> Jam Kerja Selamat</div>
          <div class="form-grid col2">
            <div class="form-group"><label>Total Jam Kerja (jam)</label><input type="number" id="f-jam-kerja" placeholder="cth: 125000" min="0" oninput="calcLTIFR()" /></div>
            <div class="form-group"><label>Jam Kerja Selamat (jam)</label><input type="number" id="f-jam-selamat" placeholder="cth: 124500" min="0" /></div>
            <div class="form-group"><label>Jumlah Tenaga Kerja</label><input type="number" id="f-tenaga-kerja" placeholder="cth: 350" min="0" /></div>
            <div class="form-group"><label>Man-hours Kumulatif YTD</label><input type="number" id="f-ytd" placeholder="cth: 480000" min="0" /></div>
          </div>
        </div>

        <div class="form-block">
          <div class="form-block-title"><span>🚨</span> Laporan Insiden</div>
          <div class="form-grid col2">
            <div class="form-group"><label>Fatality (FAT)</label><input type="number" id="f-fat" value="0" min="0" /></div>
            <div class="form-group"><label>Lost Time Injury (LTI)</label><input type="number" id="f-lti" value="0" min="0" oninput="calcLTIFR()" /></div>
            <div class="form-group"><label>Restricted Work Case (RWC)</label><input type="number" id="f-rwc" value="0" min="0" /></div>
            <div class="form-group"><label>Medical Treatment Case (MTC)</label><input type="number" id="f-mtc" value="0" min="0" /></div>
            <div class="form-group"><label>First Aid Case (FAC)</label><input type="number" id="f-fac" value="0" min="0" /></div>
            <div class="form-group"><label>Near Miss (NM)</label><input type="number" id="f-nm" value="0" min="0" /></div>
            <div class="form-group"><label>Property Damage (PD)</label><input type="number" id="f-pd" value="0" min="0" /></div>
            <div class="form-group"><label>LTIFR (otomatis)</label><input type="text" id="f-ltifr-show" readonly placeholder="—" class="readonly" /></div>
          </div>
        </div>

        <div class="form-block">
          <div class="form-block-title"><span>👁️</span> Laporan PEKA</div>
          <div class="form-grid col2">
            <div class="form-group"><label>Target Observasi PEKA</label><input type="number" id="f-peka-target" placeholder="cth: 200" min="0" /></div>
            <div class="form-group"><label>Realisasi Observasi PEKA</label><input type="number" id="f-peka-real" placeholder="cth: 185" min="0" /></div>
            <div class="form-group"><label>Safe Behavior (%)</label><input type="number" id="f-peka-safe" placeholder="cth: 92" min="0" max="100" /></div>
            <div class="form-group"><label>At-Risk Behavior (%)</label><input type="number" id="f-peka-risk" placeholder="cth: 8" min="0" max="100" /></div>
          </div>
        </div>

        <div class="form-block">
          <div class="form-block-title"><span>🌿</span> Laporan Lingkungan</div>
          <div class="form-grid col2">
            <div class="form-group"><label>Limbah B3 Dihasilkan (kg)</label><input type="number" id="f-b3" placeholder="cth: 450" min="0" /></div>
            <div class="form-group"><label>Limbah B3 Terkelola (kg)</label><input type="number" id="f-b3-kelola" placeholder="cth: 450" min="0" /></div>
            <div class="form-group"><label>Konsumsi Air (m³)</label><input type="number" id="f-air" placeholder="cth: 1200" min="0" /></div>
            <div class="form-group"><label>Emisi GRK (ton CO₂e)</label><input type="number" id="f-grk" placeholder="cth: 85" min="0" /></div>
            <div class="form-group"><label>Tumpahan Minyak (kl)</label><input type="number" id="f-tumpahan" value="0" min="0" /></div>
            <div class="form-group"><label>Jumlah Temuan Lingkungan</label><input type="number" id="f-temuan-ling" value="0" min="0" /></div>
          </div>
        </div>

        <div class="form-block">
          <div class="form-block-title"><span>🦺</span> Laporan Safety Program</div>
          <div class="form-grid col2">
            <div class="form-group"><label>Safety Talk (sesi)</label><input type="number" id="f-safety-talk" placeholder="cth: 12" min="0" /></div>
            <div class="form-group"><label>Safety Inspection (kali)</label><input type="number" id="f-safety-insp" placeholder="cth: 8" min="0" /></div>
            <div class="form-group"><label>Safety Training (peserta)</label><input type="number" id="f-safety-train" placeholder="cth: 75" min="0" /></div>
            <div class="form-group"><label>Emergency Drill (kali)</label><input type="number" id="f-drill" placeholder="cth: 2" min="0" /></div>
            <div class="form-group"><label>Temuan Safety Terbuka</label><input type="number" id="f-temuan-open" value="0" min="0" /></div>
            <div class="form-group"><label>Temuan Safety Tertutup</label><input type="number" id="f-temuan-closed" value="0" min="0" /></div>
          </div>
        </div>

        <div class="form-actions">
          <button class="btn-primary" onclick="generateInfografis()">Generate Infografis →</button>
          <button class="btn-ghost" onclick="resetForm()">Reset Form</button>
        </div>
      </div>
    </section>

    <!-- INFOGRAFIS -->
    <section class="section" id="section-infografis">
      <div id="infografis-content">
        <div class="empty-state">
          <div class="empty-icon">📋</div>
          <p>Isi form input terlebih dahulu, lalu klik <strong>Generate Infografis</strong></p>
        </div>
      </div>
    </section>

  </div>

  <script>
    const get = id => document.getElementById(id);
    const n   = id => parseFloat(get(id).value) || 0;
    const s   = id => get(id).value || '—';
    const num = v  => parseInt(v).toLocaleString('id-ID');
    const pct = (a, b) => b > 0 ? Math.min(100, (a / b) * 100).toFixed(0) : 0;

    function bar(val, total, color) {
      const p = total > 0 ? Math.min(100, (val / total) * 100).toFixed(0) : 0;
      return `<div class="bar-bg"><div class="bar-fill" style="width:${p}%;background:${color};"></div></div>`;
    }

    function labeledBar(label, val, total, color) {
      const p = pct(val, total);
      return `<div style="margin-bottom:8px;"><div class="bar-header"><span>${label}</span><span>${p}%</span></div>${bar(val, total, color)}</div>`;
    }

    function showTab(tab, btn) {
      document.querySelectorAll('.section').forEach(s => s.classList.remove('visible'));
      document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
      get('section-' + tab).classList.add('visible');
      if (btn) btn.classList.add('active');
      else get('tab-' + tab + '-btn').classList.add('active');
    }

    function calcLTIFR() {
      const jam = n('f-jam-kerja'), lti = n('f-lti');
      get('f-ltifr-show').value = jam > 0 ? ((lti / jam) * 1000000).toFixed(2) : '0.00';
    }

    function resetForm() {
      if (!confirm('Reset semua data form?')) return;
      ['f-jam-kerja','f-jam-selamat','f-tenaga-kerja','f-ytd',
       'f-fat','f-lti','f-rwc','f-mtc','f-fac','f-nm','f-pd',
       'f-peka-target','f-peka-real','f-peka-safe','f-peka-risk',
       'f-b3','f-b3-kelola','f-air','f-grk','f-tumpahan','f-temuan-ling',
       'f-safety-talk','f-safety-insp','f-safety-train','f-drill',
       'f-temuan-open','f-temuan-closed'].forEach(id => {
        const el = get(id);
        if (el) el.value = el.type === 'number' ? 0 : '';
      });
      get('f-ltifr-show').value = '';
    }

    function generateInfografis() {
      const bulan = s('f-bulan'), tahun = s('f-tahun');
      const jamKerja = n('f-jam-kerja'), jamSelamat = n('f-jam-selamat');
      const tenagaKerja = n('f-tenaga-kerja'), ytd = n('f-ytd');
      const fat = n('f-fat'), lti = n('f-lti'), rwc = n('f-rwc');
      const mtc = n('f-mtc'), fac = n('f-fac'), nm = n('f-nm'), pd = n('f-pd');
      const ltifr = jamKerja > 0 ? ((lti / jamKerja) * 1000000).toFixed(2) : '0.00';
      const pekaTarget = n('f-peka-target'), pekaReal = n('f-peka-real');
      const pekaSafe = n('f-peka-safe'), pekaRisk = n('f-peka-risk');
      const pekaPct = pct(pekaReal, pekaTarget);
      const b3 = n('f-b3'), b3k = n('f-b3-kelola');
      const air = n('f-air'), grk = n('f-grk');
      const tump = n('f-tumpahan'), temuanLing = n('f-temuan-ling');
      const stalk = n('f-safety-talk'), sinsp = n('f-safety-insp');
      const strain = n('f-safety-train'), drill = n('f-drill');
      const tOpen = n('f-temuan-open'), tClosed = n('f-temuan-closed');
      const closeRate = pct(tClosed, tOpen + tClosed);
      const insidenTotal = fat + lti + rwc + mtc;
      const statusBadge = insidenTotal === 0
        ? '<span class="pill pg">✅ Zero Incident</span>'
        : (fat + lti > 0 ? '<span class="pill pr">🔴 Ada LTI / Fatality</span>' : '<span class="pill pa">⚠️ Perlu Perhatian</span>');
      const green = 'var(--green-400)', amber = 'var(--amber-400)';
      const redIf   = v => v > 0 ? 'color:var(--red-600);' : '';
      const amberIf = v => v > 0 ? 'color:var(--amber-600);' : '';
      const ltifrColor = parseFloat(ltifr) > 0 ? 'var(--red-600)' : 'var(--green-600)';
      const pekaColor  = pekaPct >= 80 ? 'var(--green-800)' : 'var(--amber-800)';
      const b3EffPct = b3 > 0 ? ((b3k / b3) * 100).toFixed(0) : 0;
      const nowStr = new Date().toLocaleDateString('id-ID', {day:'2-digit', month:'long', year:'numeric'});

      get('infografis-content').innerHTML = `
      <div class="infografis">
        <div class="info-header">
          <div class="info-header-left">
            <div class="eyebrow">Laporan Bulanan HSSE</div>
            <div class="company">Pertamina Gas</div>
            <div class="period">${bulan} ${tahun}</div>
          </div>
          <div class="info-header-right">
            <div class="info-badge">HSSE</div><br>
            <button style="font-size:11px;padding:5px 12px;border-radius:12px;background:rgba(255,255,255,.12);border:1px solid rgba(255,255,255,.3);color:#fff;cursor:pointer;" onclick="showTab('form', get('tab-form-btn'))">✏️ Edit Data</button>
          </div>
        </div>

        <div class="section-card" style="margin-bottom:12px;">
          <h3><span class="dot dg"></span> Jam Kerja Selamat</h3>
          <div class="metrics-row">
            <div class="metric-card ag"><div class="mc-label">Jam Kerja Selamat</div><div class="mc-val">${num(jamSelamat)}</div><div class="mc-sub">jam bulan ini</div></div>
            <div class="metric-card"><div class="mc-label">Total Jam Kerja</div><div class="mc-val">${num(jamKerja)}</div><div class="mc-sub">jam</div></div>
            <div class="metric-card"><div class="mc-label">Tenaga Kerja</div><div class="mc-val">${num(tenagaKerja)}</div><div class="mc-sub">orang</div></div>
            <div class="metric-card ab"><div class="mc-label">Man-hours YTD</div><div class="mc-val">${num(ytd)}</div><div class="mc-sub">kumulatif</div></div>
          </div>
        </div>

        <div class="row2">
          <div class="section-card">
            <h3><span class="dot dr"></span> Laporan Insiden &nbsp;${statusBadge}</h3>
            <div class="insiden-row"><span class="lbl">Fatality (FAT)</span><span class="val" style="${redIf(fat)}">${fat}</span></div>
            <div class="insiden-row"><span class="lbl">Lost Time Injury (LTI)</span><span class="val" style="${redIf(lti)}">${lti}</span></div>
            <div class="insiden-row"><span class="lbl">Restricted Work Case (RWC)</span><span class="val">${rwc}</span></div>
            <div class="insiden-row"><span class="lbl">Medical Treatment Case (MTC)</span><span class="val">${mtc}</span></div>
            <div class="insiden-row"><span class="lbl">First Aid Case (FAC)</span><span class="val">${fac}</span></div>
            <div class="insiden-row"><span class="lbl">Near Miss (NM)</span><span class="val" style="${amberIf(nm)}">${nm}</span></div>
            <div class="insiden-row" style="border-bottom:none;"><span class="lbl">Property Damage (PD)</span><span class="val">${pd}</span></div>
            <div class="ltifr-row">
              <span class="ltifr-label">LTIFR (per 1.000.000 jam)</span>
              <span class="ltifr-val" style="color:${ltifrColor};">${ltifr}</span>
            </div>
          </div>
          <div class="section-card">
            <h3><span class="dot da"></span> Laporan PEKA</h3>
            <div style="text-align:center;margin:8px 0 16px;">
              <div style="font-size:11px;color:var(--text-muted);margin-bottom:4px;">Pencapaian Observasi</div>
              <div style="font-size:44px;font-weight:500;line-height:1;color:${pekaColor};">${pekaPct}%</div>
              <div style="font-size:11px;color:var(--text-hint);margin-top:4px;">${num(pekaReal)} / ${num(pekaTarget)} observasi</div>
            </div>
            ${labeledBar('Progress Observasi', pekaReal, pekaTarget, green)}
            ${labeledBar('Safe Behavior', pekaSafe, 100, green)}
            ${labeledBar('At-Risk Behavior', pekaRisk, 100, amber)}
          </div>
        </div>

        <div class="row2">
          <div class="section-card">
            <h3><span class="dot dg"></span> Laporan Lingkungan</h3>
            <div class="insiden-row"><span class="lbl">Limbah B3 Dihasilkan</span><span class="val">${num(b3)} kg</span></div>
            <div class="insiden-row"><span class="lbl">Limbah B3 Terkelola</span><span class="val" style="color:var(--green-600);">${num(b3k)} kg</span></div>
            <div class="insiden-row"><span class="lbl">Konsumsi Air</span><span class="val">${num(air)} m³</span></div>
            <div class="insiden-row"><span class="lbl">Emisi GRK</span><span class="val">${grk} tCO₂e</span></div>
            <div class="insiden-row"><span class="lbl">Tumpahan Minyak</span><span class="val" style="${redIf(tump)}">${tump} kl</span></div>
            <div class="insiden-row" style="border-bottom:none;"><span class="lbl">Temuan Lingkungan</span><span class="val">${temuanLing}</span></div>
            <div style="margin-top:12px;">
              <div class="bar-header"><span>Efisiensi Pengelolaan B3</span><span>${b3EffPct}% terkelola</span></div>
              ${bar(b3k, b3, green)}
            </div>
          </div>
          <div class="section-card">
            <h3><span class="dot db"></span> Laporan Safety Program</h3>
            <div class="mini-grid2">
              <div class="metric-card ab"><div class="mc-label">Safety Talk</div><div class="mc-val">${stalk}</div><div class="mc-sub">sesi</div></div>
              <div class="metric-card"><div class="mc-label">Inspection</div><div class="mc-val">${sinsp}</div><div class="mc-sub">kali</div></div>
              <div class="metric-card ag"><div class="mc-label">Training</div><div class="mc-val">${strain}</div><div class="mc-sub">peserta</div></div>
              <div class="metric-card"><div class="mc-label">Drill</div><div class="mc-val">${drill}</div><div class="mc-sub">kali</div></div>
            </div>
            <div style="font-size:11px;color:var(--text-muted);margin-bottom:6px;">Temuan Safety — Close-out Rate: <strong>${closeRate}%</strong></div>
            <div class="bar-header">
              <span style="color:var(--red-600);">Terbuka: ${tOpen}</span>
              <span style="color:var(--green-600);">Tertutup: ${tClosed}</span>
            </div>
            ${bar(tClosed, tOpen + tClosed, green)}
          </div>
        </div>

        <div class="info-footer">
          <span>Pertamina Gas · Laporan HSSE ${bulan} ${tahun}</span>
          <span>Dibuat: ${nowStr}</span>
        </div>
      </div>`;

      showTab('infografis', get('tab-infografis-btn'));
      window.scrollTo({ top: 0, behavior: 'smooth' });
    }
  </script>
</body>
</html>
