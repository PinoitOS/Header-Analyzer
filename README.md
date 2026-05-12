<h1 align="center">📧 Header Analyzer</h1>

<div align="center">

<h3>Visual Email Header & SMTP Route Analyzer</h3>

<p>
  Analiza cabeceras SMTP, autenticación de correo y rutas de entrega desde una interfaz visual moderna.
</p>

<br>

<img src="https://img.shields.io/badge/HTML5-Frontend-orange?style=for-the-badge&logo=html5">
<img src="https://img.shields.io/badge/CSS3-UI-blue?style=for-the-badge&logo=css3">
<img src="https://img.shields.io/badge/JavaScript-Vanilla-yellow?style=for-the-badge&logo=javascript">
<img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge">

<br><br>

<img src="https://img.shields.io/badge/SPF-Analysis-success?style=flat-square">
<img src="https://img.shields.io/badge/DKIM-Validation-success?style=flat-square">
<img src="https://img.shields.io/badge/DMARC-Detection-success?style=flat-square">
<img src="https://img.shields.io/badge/SMTP-Route%20Analysis-success?style=flat-square">

</div>

<hr>

<h2>✨ Overview</h2>

<p>
  <strong>Header Analyzer</strong> es una herramienta visual para analizar cabeceras de correo electrónico directamente desde el navegador.
</p>

<p>Permite inspeccionar:</p>

<ul>
  <li>Autenticación SMTP,</li>
  <li>Rutas <code>Received</code>,</li>
  <li>Señales antispam,</li>
  <li>Inconsistencias de remitente,</li>
  <li>Indicadores de spoofing o phishing,</li>
  <li>Y anomalías comunes en correos sospechosos.</li>
</ul>

<p>
  Todo desde una interfaz moderna y completamente client-side.
</p>

<hr>

<h2>🖥️ Features</h2>

<h3>🔐 Authentication Analysis</h3>

<ul>
  <li>SPF validation</li>
  <li>DKIM parsing</li>
  <li>DMARC analysis</li>
  <li>Authentication-Results parsing</li>
  <li>Microsoft CompAuth support</li>
  <li>Envelope analysis</li>
</ul>

<h3>🌐 SMTP Route Visualization</h3>

<ul>
  <li>Full <code>Received</code> chain parsing</li>
  <li>SMTP hop visualization</li>
  <li>Delivery delays</li>
  <li>Internal/private IP detection</li>
  <li>Route inconsistencies</li>
  <li>Suspicious relay detection</li>
</ul>

<h3>🚨 Security Detection</h3>

<ul>
  <li>SPF <code>fail</code></li>
  <li>DKIM ausente</li>
  <li>DMARC inválido</li>
  <li>Envelope mismatch</li>
  <li>Reply-To sospechoso</li>
  <li>SMTP anomalies</li>
  <li>Suspicious HELO/EHLO</li>
  <li>Antispam indicators</li>
  <li>Potential spoofing attempts</li>
</ul>

<h3>🎨 Interface</h3>

<ul>
  <li>🌙 Dark / Light mode</li>
  <li>🌍 ES / EN language support</li>
  <li>📄 PDF export</li>
  <li>📋 Copy report</li>
  <li>⚡ Instant analysis</li>
  <li>📱 Responsive design</li>
  <li>⌨️ Ctrl + Enter shortcut</li>
</ul>

<hr>

<h2>📸 Screenshots</h2>

<div align="center">

<h3>Main Interface</h3>
<img width="100%" src="images/main-ui.png">

<br><br>

<h3>SMTP Route Analysis</h3>
<img width="100%" src="images/smtp-route.png">

<br><br>

<h3>Security Findings</h3>
<img width="100%" src="images/security-findings.png">

</div>

<hr>

<h2>🚀 Quick Start</h2>

<h3>Clone repository</h3>

<pre><code>git clone https://github.com/PinoitOS/Header-Analyzer.git
cd Header-Analyzer
</code></pre>

<h3>Run locally</h3>

<p>No backend required.</p>

<p>Simply open:</p>

<pre><code>index.html
</code></pre>

<p>or run:</p>

<pre><code>python -m http.server
</code></pre>

<p>Then open:</p>

<pre><code>http://localhost:8000
</code></pre>

<hr>

<h2>🧪 Usage</h2>

<ol>
  <li>Copy raw email headers.</li>
  <li>Paste them into the analyzer.</li>
  <li>Click <code>Analyze</code>.</li>
  <li>Review:
    <ul>
      <li>risk score,</li>
      <li>SMTP route,</li>
      <li>SPF/DKIM/DMARC,</li>
      <li>security findings,</li>
      <li>antispam indicators.</li>
    </ul>
  </li>
</ol>

<p>
  También puedes cargar un ejemplo integrado para pruebas rápidas.
</p>

<hr>

<h2>🧠 What It Analyzes</h2>

<table>
  <thead>
    <tr>
      <th>Header</th>
      <th>Purpose</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>Received</code></td>
      <td>SMTP route</td>
    </tr>
    <tr>
      <td><code>Authentication-Results</code></td>
      <td>SPF / DKIM / DMARC</td>
    </tr>
    <tr>
      <td><code>Received-SPF</code></td>
      <td>SPF validation</td>
    </tr>
    <tr>
      <td><code>DKIM-Signature</code></td>
      <td>DKIM verification</td>
    </tr>
    <tr>
      <td><code>Return-Path</code></td>
      <td>Envelope sender</td>
    </tr>
    <tr>
      <td><code>Reply-To</code></td>
      <td>Response address</td>
    </tr>
    <tr>
      <td><code>X-Originating-IP</code></td>
      <td>Original sender IP</td>
    </tr>
    <tr>
      <td><code>X-Forefront-AntiSpam-Report</code></td>
      <td>Microsoft antispam telemetry</td>
    </tr>
    <tr>
      <td><code>X-Microsoft-Antispam</code></td>
      <td>Filtering indicators</td>
    </tr>
    <tr>
      <td><code>Message-ID</code></td>
      <td>Message tracking</td>
    </tr>
  </tbody>
</table>

<hr>

<h2>🛠️ Built With</h2>

<ul>
  <li>HTML5</li>
  <li>CSS3</li>
  <li>Vanilla JavaScript</li>
</ul>

<p>No:</p>

<ul>
  <li>frameworks,</li>
  <li>backend,</li>
  <li>external dependencies.</li>
</ul>

<hr>

<h2>🎯 Use Cases</h2>

<ul>
  <li>Phishing investigations</li>
  <li>SOC analysis</li>
  <li>Threat hunting</li>
  <li>Email forensics</li>
  <li>SMTP learning</li>
  <li>Security labs</li>
  <li>Blue Team workflows</li>
</ul>

<hr>

<h2>📌 Roadmap</h2>

<ul>
  <li>☐ <code>.eml</code> support</li>
  <li>☐ JSON export</li>
  <li>☐ MIME parsing</li>
  <li>☐ IOC extraction</li>
  <li>☐ Graph visualization</li>
  <li>☐ DNS lookups</li>
  <li>☐ Advanced spoofing detection</li>
</ul>

<hr>

<h2>⚠️ Disclaimer</h2>

<p>This project is intended for:</p>

<ul>
  <li>defensive security,</li>
  <li>education,</li>
  <li>email analysis,</li>
  <li>and research purposes only.</li>
</ul>

<hr>

<h2>📄 License</h2>

<p>MIT License</p>

<hr>

<div align="center">

<h3>⭐ If you like the project, consider starring the repository</h3>

</div>
