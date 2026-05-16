<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <title>Header Analyzer</title>
  <meta name="description" content="Analizador offline de cabeceras de correo (.eml/.msg) para investigacion rapida.">
  <style>
    :root{
      --bg:#070b18; --surface:#0d1424; --surface2:#111827;
      --text:#e6edf7; --muted:#8d9ab8;
      --primary:#19c7d4; --accent:#8b5cf6;
      --border:rgba(124,140,181,.22); --shadow:rgba(0,0,0,.45);
      --mono: ui-monospace, SFMono-Regular, Menlo, Consolas, "Cascadia Mono", monospace;
      --sans: system-ui, -apple-system, "Segoe UI", Roboto, Arial, sans-serif;
    }
    *{box-sizing:border-box}
    body{
      margin:0;
      font-family:var(--sans);
      color:var(--text);
      background:
        radial-gradient(circle at 20% 0%, rgba(139,92,246,0.18), transparent 28%),
        radial-gradient(circle at 85% 12%, rgba(25,199,212,0.14), transparent 30%),
        var(--bg);
      line-height:1.55;
    }
    a{color:inherit}
    code{font-family:var(--mono); font-size:.95em}

    .wrap{max-width:1120px; margin:0 auto; padding:24px 18px 60px}

    .topbar{
      position:sticky; top:0; z-index:50;
      background:rgba(7,11,24,.78);
      backdrop-filter:blur(14px);
      border-bottom:1px solid var(--border);
    }
    .topbar-inner{
      max-width:1120px; margin:0 auto;
      padding:14px 18px;
      display:flex; align-items:center; gap:12px;
    }
    .brand{display:flex; align-items:center; gap:10px; flex:1; min-width:0}
    .logo{
      width:34px; height:34px; border-radius:10px;
      background:linear-gradient(135deg, rgba(25,199,212,.20), rgba(139,92,246,.20));
      border:1px solid var(--border);
      display:grid; place-items:center;
      box-shadow:0 10px 26px rgba(0,0,0,.25);
      flex:0 0 auto;
    }
    .brand h1{margin:0; font-size:14px; letter-spacing:.12em; text-transform:uppercase; white-space:nowrap; overflow:hidden; text-overflow:ellipsis}

    .lang{
      display:flex; gap:6px; padding:6px;
      border:1px solid var(--border); border-radius:12px;
      background:rgba(255,255,255,.04);
    }
    .lang button{
      border:0; cursor:pointer;
      padding:8px 10px; border-radius:9px;
      background:transparent; color:var(--muted);
      font-weight:850; font-size:12px; letter-spacing:.08em;
    }
    .lang button.active{
      color:#fff;
      background:linear-gradient(135deg,var(--primary),var(--accent));
      box-shadow:0 10px 26px rgba(25,199,212,.16);
    }

    .hero{
      display:grid; grid-template-columns:1.05fr .95fr;
      gap:18px; align-items:stretch;
      padding:22px; margin-top:18px;
      border:1px solid var(--border); border-radius:18px;
      background:linear-gradient(180deg, rgba(17,24,39,.92), rgba(13,20,36,.92));
      box-shadow:0 20px 60px var(--shadow);
    }
    .hero h2{margin:0 0 8px; font-size:30px; letter-spacing:.02em}
    .hero p{margin:0; color:var(--muted); font-size:15px}
    .chips{display:flex; flex-wrap:wrap; gap:10px; margin-top:14px}
    .chip{
      border:1px solid var(--border); border-radius:999px;
      padding:6px 10px; font-weight:800; font-size:12px;
      background:rgba(255,255,255,.04);
    }
    .chip.off{border-color:rgba(25,199,212,.35)}
    .chip.file{border-color:rgba(139,92,246,.35)}
    .chip.safe{border-color:rgba(23,185,120,.35)}

    .hero-card{
      border:1px solid var(--border); border-radius:16px;
      background:rgba(7,11,24,.35);
      padding:16px;
      display:flex; flex-direction:column; gap:10px;
    }
    .hero-card-title{margin:0; font-size:12px; letter-spacing:.14em; text-transform:uppercase; color:var(--primary); font-weight:900}
    .kv{display:grid; grid-template-columns:150px 1fr; gap:10px; align-items:start}
    .k{color:var(--muted); font-weight:800; font-size:12px; letter-spacing:.08em; text-transform:uppercase}
    .v{font-family:var(--mono); font-size:12.5px; color:var(--text); word-break:break-word}

    .grid{display:grid; grid-template-columns:repeat(12,1fr); gap:16px; margin-top:18px}
    .card{
      grid-column:span 6;
      border:1px solid var(--border); border-radius:16px;
      background:linear-gradient(180deg, rgba(17,24,39,.90), rgba(13,20,36,.90));
      box-shadow:0 16px 48px rgba(0,0,0,.22);
      padding:18px;
    }
    .card h3{margin:0 0 10px; font-size:14px; letter-spacing:.12em; text-transform:uppercase}
    .card p{margin:0; color:var(--muted); font-size:14px}
    .list{margin:12px 0 0; padding-left:18px; color:var(--text); font-size:14px}
    .list li{margin:6px 0}

    .gallery{
      margin-top:18px;
      border:1px solid var(--border); border-radius:18px;
      background:rgba(7,11,24,.25);
      overflow:hidden;
    }
    .gallery-head{
      padding:14px 16px;
      display:flex; gap:12px; align-items:center; justify-content:space-between;
      border-bottom:1px solid var(--border);
      background:rgba(255,255,255,.03);
    }
    .gallery-head h3{margin:0; font-size:14px; letter-spacing:.12em; text-transform:uppercase}
    .gallery-body{display:grid; grid-template-columns:1fr; gap:0}
    .shot{padding:14px; border-top:1px solid var(--border)}
    .shot:first-child{border-top:0}
    .shot img{
      width:100%; height:auto; display:block;
      border-radius:14px;
      border:1px solid rgba(124,140,181,.25);
      box-shadow:0 18px 60px rgba(0,0,0,.35);
      background:#000;
    }
    .caption{margin:10px 4px 0; color:var(--muted); font-size:13px}

    .footer{
      margin-top:22px;
      border-top:1px solid var(--border);
      padding-top:18px;
      display:flex; flex-wrap:wrap; gap:10px; justify-content:space-between;
      color:var(--muted);
      font-size:13px;
    }

    @media (max-width: 900px){
      .hero{grid-template-columns:1fr}
      .card{grid-column:span 12}
      .kv{grid-template-columns:1fr}
    }
  </style>
</head>
<body>
  <div class="topbar">
    <div class="topbar-inner">
      <div class="brand">
        <div class="logo" aria-hidden="true">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" style="color:var(--primary)" stroke-width="2">
            <circle cx="11" cy="11" r="7"></circle>
            <path d="M21 21l-4.3-4.3"></path>
          </svg>
        </div>
        <h1>Header Analyzer</h1>
      </div>

      <div class="lang" aria-label="Language selector">
        <button type="button" id="langEs" class="active">ES</button>
        <button type="button" id="langEn">EN</button>
      </div>
    </div>
  </div>

  <main class="wrap">
    <section class="hero">
      <div>
        <h2 data-i18n="heroTitle">Analizador offline de cabeceras (.eml / .msg)</h2>
        <p data-i18n="heroSubtitle">Investiga rutas de entrega, autenticacion y senales antispam sin enviar nada a servidores: todo ocurre en tu navegador.</p>
        <div class="chips" aria-label="Highlights">
          <span class="chip off" data-i18n="chipOffline">100% offline</span>
          <span class="chip file" data-i18n="chipFormats">EML + MSG</span>
          <span class="chip safe" data-i18n="chipPrivate">Sin red / sin tracking</span>
        </div>
      </div>

      <aside class="hero-card">
        <p class="hero-card-title" data-i18n="quickFacts">Ficha rapida</p>
        <div class="kv">
          <div class="k" data-i18n="factTech">Tecnologias</div>
          <div class="v" data-i18n="factTechValue">HTML + CSS + JavaScript (sin backend). MsgReader (Apache-2.0) para .msg.</div>

          <div class="k" data-i18n="factRuns">Ejecucion</div>
          <div class="v" data-i18n="factRunsValue">Navegador moderno (Brave/Chrome/Firefox). Sin instalacion.</div>

          <div class="k" data-i18n="factSecurity">Seguridad</div>
          <div class="v" data-i18n="factSecurityValue">CSP pragmatica + render con DOM/textContent para minimizar XSS.</div>

          <div class="k" data-i18n="factLimit">Limite</div>
          <div class="v" data-i18n="factLimitValue">Archivos grandes pueden consumir CPU/memoria (especialmente .msg).</div>
        </div>
      </aside>
    </section>

    <section class="grid">
      <article class="card">
        <h3 data-i18n="whatTitle">Que hace</h3>
        <p data-i18n="whatIntro">Extrae y organiza senales tecnicas habituales para acelerar el triage.</p>
        <ul class="list">
          <li data-i18n="what1">Ruta de entrega (Received): saltos, delays y anomalias.</li>
          <li data-i18n="what2">Autenticacion: SPF / DKIM / DMARC / CompAuth (cuando existe).</li>
          <li data-i18n="what3">Senales Microsoft: X-Forefront-Antispam-Report y X-Microsoft-Antispam.</li>
          <li data-i18n="what4">Exportacion (PDF/JSON/TXT) y copia de IOCs.</li>
        </ul>
      </article>

      <article class="card">
        <h3 data-i18n="howTitle">Como se usa</h3>
        <p data-i18n="howIntro">Pensado para uso rapido en analisis e investigacion.</p>
        <ul class="list">
          <li data-i18n="how1">Pega cabeceras crudas o carga un archivo .eml/.msg.</li>
          <li data-i18n="how2">Ejecuta el analisis y revisa el resumen, la ruta y las senales.</li>
          <li data-i18n="how3">Exporta o copia IOCs si necesitas compartir hallazgos.</li>
        </ul>
      </article>

      <article class="card">
        <h3 data-i18n="privacyTitle">Privacidad</h3>
        <p data-i18n="privacyIntro">El diseno prioriza aislamiento y control local.</p>
        <ul class="list">
          <li data-i18n="privacy1">No se hacen peticiones de red (CSP: connect-src 'none').</li>
          <li data-i18n="privacy2">Los datos permanecen en tu navegador.</li>
          <li data-i18n="privacy3">El export "raw" puede contener datos sensibles: usalo con cuidado.</li>
        </ul>
      </article>

      <article class="card">
        <h3 data-i18n="limitsTitle">Limitaciones</h3>
        <p data-i18n="limitsIntro">Importante para interpretar resultados correctamente.</p>
        <ul class="list">
          <li data-i18n="limits1">En .msg no siempre se puede reconstruir la cadena Received completa.</li>
          <li data-i18n="limits2">Archivos complejos pueden tardar o consumir recursos.</li>
          <li data-i18n="limits3">Algunas senales pueden estar ausentes segun el proveedor.</li>
        </ul>
      </article>
    </section>

    <section class="gallery" aria-label="Screenshots">
      <div class="gallery-head">
        <h3 data-i18n="shotsTitle">Capturas</h3>
        <div class="caption" data-i18n="shotsHint">Orden: 3 -> 1 -> 2</div>
      </div>
      <div class="gallery-body">
        <div class="shot">
          <img alt="Screenshot 3" src="https://raw.githubusercontent.com/PinoitOS/Header-Analyzer/main/3.png">
          <div class="caption" data-i18n="shot3">Vista general del analisis.</div>
        </div>
        <div class="shot">
          <img alt="Screenshot 1" src="https://raw.githubusercontent.com/PinoitOS/Header-Analyzer/main/1.png">
          <div class="caption" data-i18n="shot1">Panel de entrada y flujo de uso.</div>
        </div>
        <div class="shot">
          <img alt="Screenshot 2" src="https://raw.githubusercontent.com/PinoitOS/Header-Analyzer/main/2.png">
          <div class="caption" data-i18n="shot2">Detalles tecnicos y secciones del reporte.</div>
        </div>
      </div>
    </section>

    <footer class="footer">
      <div data-i18n="footerLicense">Incluye dependencias third-party (MsgReader, Apache-2.0). Ver carpeta <code>third_party/msgreader/</code>.</div>
      <div><span data-i18n="footerVersion">Version:</span> <code>landing23</code></div>
    </footer>
  </main>

  <script>
    (function(){
      'use strict';
      var current = 'es';
      var dict = {
        es: {
          heroTitle: 'Analizador offline de cabeceras (.eml / .msg)',
          heroSubtitle: 'Investiga rutas de entrega, autenticacion y senales antispam sin enviar nada a servidores: todo ocurre en tu navegador.',
          chipOffline: '100% offline',
          chipFormats: 'EML + MSG',
          chipPrivate: 'Sin red / sin tracking',
          quickFacts: 'Ficha rapida',
          factTech: 'Tecnologias',
          factTechValue: 'HTML + CSS + JavaScript (sin backend). MsgReader (Apache-2.0) para .msg.',
          factRuns: 'Ejecucion',
          factRunsValue: 'Navegador moderno (Brave/Chrome/Firefox). Sin instalacion.',
          factSecurity: 'Seguridad',
          factSecurityValue: 'CSP pragmatica + render con DOM/textContent para minimizar XSS.',
          factLimit: 'Limite',
          factLimitValue: 'Archivos grandes pueden consumir CPU/memoria (especialmente .msg).',
          whatTitle: 'Que hace',
          whatIntro: 'Extrae y organiza senales tecnicas habituales para acelerar el triage.',
          what1: 'Ruta de entrega (Received): saltos, delays y anomalias.',
          what2: 'Autenticacion: SPF / DKIM / DMARC / CompAuth (cuando existe).',
          what3: 'Senales Microsoft: X-Forefront-Antispam-Report y X-Microsoft-Antispam.',
          what4: 'Exportacion (PDF/JSON/TXT) y copia de IOCs.',
          howTitle: 'Como se usa',
          howIntro: 'Pensado para uso rapido en analisis e investigacion.',
          how1: 'Pega cabeceras crudas o carga un archivo .eml/.msg.',
          how2: 'Ejecuta el analisis y revisa el resumen, la ruta y las senales.',
          how3: 'Exporta o copia IOCs si necesitas compartir hallazgos.',
          privacyTitle: 'Privacidad',
          privacyIntro: 'El diseno prioriza aislamiento y control local.',
          privacy1: 'No se hacen peticiones de red (CSP: connect-src \'none\').',
          privacy2: 'Los datos permanecen en tu navegador.',
          privacy3: 'El export "raw" puede contener datos sensibles: usalo con cuidado.',
          limitsTitle: 'Limitaciones',
          limitsIntro: 'Importante para interpretar resultados correctamente.',
          limits1: 'En .msg no siempre se puede reconstruir la cadena Received completa.',
          limits2: 'Archivos complejos pueden tardar o consumir recursos.',
          limits3: 'Algunas senales pueden estar ausentes segun el proveedor.',
          shotsTitle: 'Capturas',
          shotsHint: 'Orden: 3 -> 1 -> 2',
          shot3: 'Vista general del analisis.',
          shot1: 'Panel de entrada y flujo de uso.',
          shot2: 'Detalles tecnicos y secciones del reporte.',
          footerLicense: 'Incluye dependencias third-party (MsgReader, Apache-2.0). Ver carpeta third_party/msgreader/.',
          footerVersion: 'Version:'
        },
        en: {
          heroTitle: 'Offline email header analyzer (.eml / .msg)',
          heroSubtitle: 'Investigate delivery routes, authentication, and antispam signals without sending anything to servers: everything runs in your browser.',
          chipOffline: '100% offline',
          chipFormats: 'EML + MSG',
          chipPrivate: 'No network / no tracking',
          quickFacts: 'Quick facts',
          factTech: 'Tech',
          factTechValue: 'HTML + CSS + JavaScript (no backend). MsgReader (Apache-2.0) for .msg.',
          factRuns: 'Runs on',
          factRunsValue: 'Modern browser (Brave/Chrome/Firefox). No install.',
          factSecurity: 'Security',
          factSecurityValue: 'Pragmatic CSP + DOM/textContent rendering to minimize XSS.',
          factLimit: 'Limit',
          factLimitValue: 'Large/complex files may consume CPU/memory (especially .msg).',
          whatTitle: 'What it does',
          whatIntro: 'Extracts and organizes common technical signals to speed up triage.',
          what1: 'Delivery route (Received): hops, delays, anomalies.',
          what2: 'Authentication: SPF / DKIM / DMARC / CompAuth (when present).',
          what3: 'Microsoft signals: X-Forefront-Antispam-Report and X-Microsoft-Antispam.',
          what4: 'Export (PDF/JSON/TXT) and IOC copy.',
          howTitle: 'How to use',
          howIntro: 'Designed for fast analysis and investigation workflows.',
          how1: 'Paste raw headers or load an .eml/.msg file.',
          how2: 'Run the analysis and review the summary, route, and signals.',
          how3: 'Export or copy IOCs if you need to share findings.',
          privacyTitle: 'Privacy',
          privacyIntro: 'The design prioritizes isolation and local control.',
          privacy1: 'No network requests (CSP: connect-src \'none\').',
          privacy2: 'Data stays in your browser.',
          privacy3: '"Raw" exports may contain sensitive data: handle with care.',
          limitsTitle: 'Limitations',
          limitsIntro: 'Important to interpret results correctly.',
          limits1: 'For .msg, the full Received chain cannot always be reconstructed.',
          limits2: 'Complex files may be slow or resource-heavy.',
          limits3: 'Some signals may be missing depending on the provider.',
          shotsTitle: 'Screenshots',
          shotsHint: 'Order: 3 -> 1 -> 2',
          shot3: 'High-level report view.',
          shot1: 'Input panel and workflow.',
          shot2: 'Technical details and report sections.',
          footerLicense: 'Includes third-party dependencies (MsgReader, Apache-2.0). See third_party/msgreader/.',
          footerVersion: 'Version:'
        }
      };

      function apply(lang){
        current = (lang === 'en') ? 'en' : 'es';
        document.documentElement.lang = current;
        var nodes = document.querySelectorAll('[data-i18n]');
        for (var i=0;i<nodes.length;i++){
          var k = nodes[i].getAttribute('data-i18n');
          if (!k) continue;
          nodes[i].textContent = (dict[current][k] || dict.en[k] || k);
        }
        document.getElementById('langEs').classList.toggle('active', current === 'es');
        document.getElementById('langEn').classList.toggle('active', current === 'en');
      }

      document.getElementById('langEs').addEventListener('click', function(){ apply('es'); });
      document.getElementById('langEn').addEventListener('click', function(){ apply('en'); });
      apply('es');
    })();
  </script>
</body>
</html>
