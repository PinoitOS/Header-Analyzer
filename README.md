

<h1 align="center">Header Analyzer</h1>

<p align="center">
  <img alt="Header Analyzer icon" src="./icon.svg" width="96" height="96" />
</p>

<p align="center">
  <img alt="Header Analyzer" src="https://img.shields.io/badge/Header%20Analyzer-Offline%20Email%20Header%20Analyzer-19c7d4?style=for-the-badge&labelColor=070b18" />
</p>

<p align="center">
  <img alt="Offline" src="https://img.shields.io/badge/Offline-100%25-19c7d4?style=flat&labelColor=0b1224" />
  <img alt="Formats" src="https://img.shields.io/badge/Formats-EML%20%7C%20MSG-8b5cf6?style=flat&labelColor=0b1224" />
  <img alt="Network" src="https://img.shields.io/badge/Network-none-111827?style=flat&labelColor=0b1224" />
  <img alt="Runs in browser" src="https://img.shields.io/badge/Runs%20in-Browser-0b1224?style=flat&labelColor=0b1224" />
</p>

<p align="center">
  <strong>ES:</strong> Analizador <em>offline</em> de cabeceras de correo (<code>.eml</code> / <code>.msg</code>) para investigacion rapida.
  <br>
  <strong>EN:</strong> Offline email header analyzer (<code>.eml</code> / <code>.msg</code>) for fast investigations.
</p>

<p align="center">
  <img alt="Browsers" src="https://img.shields.io/badge/Browsers-Brave%20%7C%20Chrome%20%7C%20Firefox-0b1224?style=flat&labelColor=0b1224" />
  <img alt="Privacy" src="https://img.shields.io/badge/Privacy-local%20processing-0b1224?style=flat&labelColor=0b1224" />
  <img alt="License" src="https://img.shields.io/badge/MsgReader-Apache--2.0-0b1224?style=flat&labelColor=0b1224" />
</p>

<hr>

<h2>Resumen / Summary</h2>

<table>
  <tr>
    <td width="50%" valign="top">
      <h3>ES</h3>
      <p>Extrae y organiza senales tecnicas para acelerar el triage:</p>
      <ul>
        <li><strong>Ruta de entrega (Received):</strong> saltos, delays y anomalias.</li>
        <li><strong>Autenticacion:</strong> SPF / DKIM / DMARC / CompAuth (si existe).</li>
        <li><strong>Senales Microsoft:</strong> <code>X-Forefront-Antispam-Report</code> y <code>X-Microsoft-Antispam</code>.</li>
        <li><strong>Salida:</strong> export PDF/JSON/TXT y copia de IOCs.</li>
      </ul>
    </td>
    <td width="50%" valign="top">
      <h3>EN</h3>
      <p>Extracts and organizes technical signals to speed up triage:</p>
      <ul>
        <li><strong>Delivery route (Received):</strong> hops, delays, anomalies.</li>
        <li><strong>Authentication:</strong> SPF / DKIM / DMARC / CompAuth (when present).</li>
        <li><strong>Microsoft signals:</strong> <code>X-Forefront-Antispam-Report</code> and <code>X-Microsoft-Antispam</code>.</li>
        <li><strong>Output:</strong> export PDF/JSON/TXT and IOC copy.</li>
      </ul>
    </td>
  </tr>
</table>

<blockquote>
  <p><strong>ES:</strong> Objetivo: que puedas decidir rapido si un correo parece legitimo, masivo o suplantado, y extraer IOCs sin depender de servicios externos.</p>
  <p><strong>EN:</strong> Goal: quickly decide whether a message looks legitimate, bulk, or spoofed, and extract IOCs without relying on external services.</p>
</blockquote>

<h2>Flujo de trabajo / Workflow</h2>

<table>
  <tr>
    <td width="50%" valign="top">
      <h3>ES</h3>
      <ol>
        <li>Carga un <code>.eml</code> / <code>.msg</code> o pega cabeceras crudas.</li>
        <li>Revisa el <strong>Risk Score</strong> y el <strong>Analyst Summary</strong>.</li>
        <li>Confirma la ruta <strong>Delivery Route (Received)</strong>: origen, saltos, delays, alertas.</li>
        <li>Valida autenticacion: <strong>SPF/DKIM/DMARC</strong> y <strong>CompAuth</strong>.</li>
        <li>Extrae artefactos: exporta o copia IOCs.</li>
      </ol>
    </td>
    <td width="50%" valign="top">
      <h3>EN</h3>
      <ol>
        <li>Load an <code>.eml</code> / <code>.msg</code> file or paste raw headers.</li>
        <li>Review <strong>Risk Score</strong> and <strong>Analyst Summary</strong>.</li>
        <li>Confirm <strong>Delivery Route (Received)</strong>: origin, hops, delays, alerts.</li>
        <li>Validate authentication: <strong>SPF/DKIM/DMARC</strong> and <strong>CompAuth</strong>.</li>
        <li>Extract artifacts: export or copy IOCs.</li>
      </ol>
    </td>
  </tr>
</table>

<h2>Cobertura de senales / Signal coverage</h2>

<table>
  <tr>
    <th align="left">Area</th>
    <th align="left">Senales / Signals</th>
    <th align="left">Para que sirve / Why it matters</th>
  </tr>
  <tr>
    <td><strong>Ruta</strong></td>
    <td><code>Received</code>, hop delays, IP type (public/private), anomalies</td>
    <td>Detecta redirecciones raras, delays altos, o infra sospechosa.</td>
  </tr>
  <tr>
    <td><strong>Auth</strong></td>
    <td><code>SPF</code>, <code>DKIM</code>, <code>DMARC</code>, <code>Authentication-Results</code>, <code>Received-SPF</code></td>
    <td>Base para detectar suplantacion y problemas de alineacion.</td>
  </tr>
  <tr>
    <td><strong>Microsoft</strong></td>
    <td><code>X-Forefront-Antispam-Report</code>, <code>X-Microsoft-Antispam</code> (BCL/PCL/EFV)</td>
    <td>Contexto extra para bulk/spam/phishing en ecosistema M365.</td>
  </tr>
  <tr>
    <td><strong>Artefactos</strong></td>
    <td>Emails, dominios, IPs, Message-Id, HELO/PTR (si aparece)</td>
    <td>Facilita hunting, bloqueos y correlacion con otros eventos.</td>
  </tr>
</table>

<h2>Exportacion / Export</h2>

<table>
  <tr>
    <td width="50%" valign="top">
      <h3>ES</h3>
      <ul>
        <li><strong>PDF:</strong> reporte legible para compartir.</li>
        <li><strong>JSON:</strong> datos estructurados para automatizacion.</li>
        <li><strong>TXT:</strong> texto plano para tickets o notas.</li>
        <li><strong>IOCs:</strong> copia rapida (IPs/dominios/emails/Message-Id).</li>
      </ul>
    </td>
    <td width="50%" valign="top">
      <h3>EN</h3>
      <ul>
        <li><strong>PDF:</strong> human-readable report for sharing.</li>
        <li><strong>JSON:</strong> structured data for automation.</li>
        <li><strong>TXT:</strong> plain text for tickets/notes.</li>
        <li><strong>IOCs:</strong> quick copy (IPs/domains/emails/Message-Id).</li>
      </ul>
    </td>
  </tr>
</table>

<h2>Tecnologias / Technologies</h2>

<table>
  <tr>
    <td width="50%" valign="top">
      <h3>ES</h3>
      <ul>
        <li><strong>Stack:</strong> HTML + CSS + JavaScript (sin backend).</li>
        <li><strong>.msg:</strong> MsgReader (Apache-2.0).</li>
        <li><strong>Seguridad:</strong> CSP pragmatica + render con DOM/<code>textContent</code> para minimizar XSS.</li>
      </ul>
    </td>
    <td width="50%" valign="top">
      <h3>EN</h3>
      <ul>
        <li><strong>Stack:</strong> HTML + CSS + JavaScript (no backend).</li>
        <li><strong>.msg:</strong> MsgReader (Apache-2.0).</li>
        <li><strong>Security:</strong> pragmatic CSP + DOM/<code>textContent</code> rendering to minimize XSS.</li>
      </ul>
    </td>
  </tr>
</table>

<h2>Seguridad (modelo) / Security model</h2>

<table>
  <tr>
    <td width="50%" valign="top">
      <h3>ES</h3>
      <ul>
        <li><strong>Offline por diseno:</strong> no requiere backend.</li>
        <li><strong>Mitigacion XSS:</strong> render principal con DOM/<code>textContent</code> (evita interpretar HTML).</li>
        <li><strong>CSP:</strong> politica pragmatica para single-file.</li>
      </ul>
    </td>
    <td width="50%" valign="top">
      <h3>EN</h3>
      <ul>
        <li><strong>Offline by design:</strong> no backend required.</li>
        <li><strong>XSS mitigation:</strong> main rendering uses DOM/<code>textContent</code> (prevents HTML interpretation).</li>
        <li><strong>CSP:</strong> pragmatic policy for a single-file app.</li>
      </ul>
    </td>
  </tr>
</table>

<h2>Privacidad y limitaciones / Privacy & limitations</h2>

<table>
  <tr>
    <td width="50%" valign="top">
      <h3>ES</h3>
      <ul>
        <li><strong>Offline:</strong> no hay peticiones de red.</li>
        <li><strong>.msg:</strong> no siempre se puede reconstruir la cadena Received completa.</li>
        <li><strong>Rendimiento:</strong> archivos grandes o complejos pueden consumir CPU/memoria.</li>
        <li><strong>Export raw:</strong> puede contener datos sensibles; comparte con cuidado.</li>
      </ul>
    </td>
    <td width="50%" valign="top">
      <h3>EN</h3>
      <ul>
        <li><strong>Offline:</strong> no network requests.</li>
        <li><strong>.msg:</strong> the full Received chain cannot always be reconstructed.</li>
        <li><strong>Performance:</strong> large/complex files may be CPU/memory intensive.</li>
        <li><strong>Raw export:</strong> may contain sensitive data; share carefully.</li>
      </ul>
    </td>
  </tr>
</table>

<blockquote>
  <p><strong>Nota / Note:</strong> En <code>.msg</code> puede faltar parte del trazado porque no siempre es posible reconstruir la cadena <code>Received</code> completa desde el contenedor MSG.</p>
</blockquote>

<h2>Casos de uso / Use cases</h2>

<table>
  <tr>
    <td width="50%" valign="top">
      <h3>ES</h3>
      <ul>
        <li><strong>Soporte/Helpdesk:</strong> verificar rapido si un correo es suplantacion o un envio legitimo.</li>
        <li><strong>SOC/IR:</strong> extraer IOCs (IPs, dominios, Message-Id) para hunting y bloqueo.</li>
        <li><strong>M365/O365:</strong> interpretar <code>SCL</code>/<code>CAT</code>/<code>PCL</code>/<code>BCL</code> junto con SPF/DKIM/DMARC.</li>
        <li><strong>Auditoria tecnica:</strong> revisar alineacion From/Return-Path/MAIL FROM y saltos Received.</li>
      </ul>
    </td>
    <td width="50%" valign="top">
      <h3>EN</h3>
      <ul>
        <li><strong>Support/Helpdesk:</strong> quickly verify whether an email is spoofed or legitimate.</li>
        <li><strong>SOC/IR:</strong> extract IOCs (IPs, domains, Message-Id) for hunting and blocking.</li>
        <li><strong>M365/O365:</strong> interpret <code>SCL</code>/<code>CAT</code>/<code>PCL</code>/<code>BCL</code> together with SPF/DKIM/DMARC.</li>
        <li><strong>Technical audit:</strong> review From/Return-Path/MAIL FROM alignment and Received hops.</li>
      </ul>
    </td>
  </tr>
</table>

<h2>FAQ</h2>

<table>
  <tr>
    <td width="50%" valign="top">
      <h3>ES</h3>
      <details open>
        <summary><strong>¿El analizador envia datos a Internet?</strong></summary>
        <p>No. El flujo esta pensado para ejecutarse offline en el navegador. El unico riesgo de exposicion es si tu exportas/coplas datos y los compartes.</p>
      </details>
      <details>
        <summary><strong>¿Por que mi .msg no muestra todos los Received?</strong></summary>
        <p>El contenedor MSG no siempre permite reconstruir toda la cadena Received. Por eso el reporte indica que la traza puede estar incompleta.</p>
      </details>
      <details>
        <summary><strong>¿Como interpreto un DMARC fail?</strong></summary>
        <p>Un <code>DMARC=fail</code> con desalineacion (From vs MAIL FROM/Return-Path) es una senal fuerte de suplantacion, especialmente si el dominio aplica politica.</p>
      </details>
      <details>
        <summary><strong>¿Que significa Risk Score?</strong></summary>
        <p>Es una heuristica orientativa (no una prueba criptografica). Sirve para priorizar revision; valida siempre con el contexto y evidencias.</p>
      </details>
      <details>
        <summary><strong>¿Que export deberia usar?</strong></summary>
        <p><strong>PDF</strong> para compartir visualmente, <strong>JSON</strong> para automatizar, <strong>TXT</strong> para tickets. El JSON "raw" puede contener datos sensibles.</p>
      </details>
    </td>
    <td width="50%" valign="top">
      <h3>EN</h3>
      <details open>
        <summary><strong>Does the analyzer send data to the Internet?</strong></summary>
        <p>No. The workflow is designed to run offline in the browser. The main exposure risk is exporting/copying data and sharing it.</p>
      </details>
      <details>
        <summary><strong>Why does my .msg miss some Received headers?</strong></summary>
        <p>The MSG container does not always allow reconstructing the full Received chain. The report explicitly notes the trace may be incomplete.</p>
      </details>
      <details>
        <summary><strong>How should I interpret DMARC fail?</strong></summary>
        <p>A <code>DMARC=fail</code> with misalignment (From vs MAIL FROM/Return-Path) is a strong spoofing signal, especially when the domain enforces policy.</p>
      </details>
      <details>
        <summary><strong>What is Risk Score?</strong></summary>
        <p>An indicative heuristic (not cryptographic proof). Use it to prioritize review, and validate with context and evidence.</p>
      </details>
      <details>
        <summary><strong>Which export should I use?</strong></summary>
        <p><strong>PDF</strong> for human sharing, <strong>JSON</strong> for automation, <strong>TXT</strong> for tickets. "Raw" JSON may contain sensitive data.</p>
      </details>
    </td>
  </tr>
</table>

<hr>

<h2>Capturas / Screenshots</h2>
<p><em>Orden / Order:</em> 3 &rarr; 1 &rarr; 2</p>

<p>
  <img alt="Screenshot 3" src="https://raw.githubusercontent.com/PinoitOS/Header-Analyzer/main/3.png" width="100%" />
</p>
<p>
  <img alt="Screenshot 1" src="https://raw.githubusercontent.com/PinoitOS/Header-Analyzer/main/1.png" width="100%" />
</p>
<p>
  <img alt="Screenshot 2" src="https://raw.githubusercontent.com/PinoitOS/Header-Analyzer/main/2.png" width="100%" />
</p>

<hr>

<p><strong>Licencia / License:</strong> Incluye MsgReader (Apache-2.0). Ver <code>third_party/msgreader/</code>.</p>
