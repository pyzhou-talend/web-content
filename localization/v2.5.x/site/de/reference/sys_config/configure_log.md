---
id: configure_log.md
related_key: configure
group: system_configuration.md
summary: 'Erfahren Sie, wie Sie das Protokoll für Milvus konfigurieren.'
---
<h1 id="log-related-Configurations" class="common-anchor-header">log-bezogene Konfigurationen<button data-href="#log-related-Configurations" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h1><p>Konfiguriert die Ausgabe des Systemprotokolls.</p>
<h2 id="loglevel" class="common-anchor-header"><code translate="no">log.level</code><button data-href="#loglevel" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h2><table id="log.level">
  <thead>
    <tr>
      <th class="width80">Beschreibung</th>
      <th class="width20">Standardwert</th> 
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <li>Milvus-Protokollstufe. Option: debug, info, warn, error, panic und fatal. </li>      
        <li>Es wird empfohlen, die Debug-Stufe in Test- und Entwicklungsumgebungen und die Info-Stufe in Produktionsumgebungen zu verwenden.</li>      </td>
      <td>info</td>
    </tr>
  </tbody>
</table>
<h2 id="logfilerootPath" class="common-anchor-header"><code translate="no">log.file.rootPath</code><button data-href="#logfilerootPath" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h2><table id="log.file.rootPath">
  <thead>
    <tr>
      <th class="width80">Beschreibung</th>
      <th class="width20">Standardwert</th> 
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <li>Wurzelpfad zu den Protokolldateien.</li>      
        <li>Der Standardwert ist leer, was bedeutet, dass die Protokolldateien auf die Standardausgabe (stdout) und den Standardfehler (stderr) ausgegeben werden sollen.</li>      
        <li>Wenn dieser Parameter auf einen gültigen lokalen Pfad gesetzt ist, schreibt und speichert Milvus die Protokolldateien in diesem Pfad.</li>      
        <li>Setzen Sie diesen Parameter auf den Pfad, für den Sie eine Schreibberechtigung haben.</li>      </td>
      <td></td>
    </tr>
  </tbody>
</table>
<h2 id="logfilemaxSize" class="common-anchor-header"><code translate="no">log.file.maxSize</code><button data-href="#logfilemaxSize" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h2><table id="log.file.maxSize">
  <thead>
    <tr>
      <th class="width80">Beschreibung</th>
      <th class="width20">Standardwert</th> 
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>        Die maximale Größe einer Protokolldatei, Einheit: MB.      </td>
      <td>300</td>
    </tr>
  </tbody>
</table>
<h2 id="logfilemaxAge" class="common-anchor-header"><code translate="no">log.file.maxAge</code><button data-href="#logfilemaxAge" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h2><table id="log.file.maxAge">
  <thead>
    <tr>
      <th class="width80">Beschreibung</th>
      <th class="width20">Standardwert</th> 
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>        Die maximale Aufbewahrungszeit, bevor eine Protokolldatei automatisch gelöscht wird, Einheit: Tag. Der Mindestwert ist 1.  </td>
      <td>10</td>
    </tr>
  </tbody>
</table>
<h2 id="logfilemaxBackups" class="common-anchor-header"><code translate="no">log.file.maxBackups</code><button data-href="#logfilemaxBackups" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h2><table id="log.file.maxBackups">
  <thead>
    <tr>
      <th class="width80">Beschreibung</th>
      <th class="width20">Standardwert</th> 
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>        Die maximale Anzahl der zu sichernden Protokolldateien, Einheit: Tag. Der Mindestwert ist 1.  </td>
      <td>20</td>
    </tr>
  </tbody>
</table>
<h2 id="logformat" class="common-anchor-header"><code translate="no">log.format</code><button data-href="#logformat" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h2><table id="log.format">
  <thead>
    <tr>
      <th class="width80">Beschreibung</th>
      <th class="width20">Standardwert</th> 
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>        Milvus-Protokollformat. Option: Text und JSON    </td>
      <td>Text</td>
    </tr>
  </tbody>
</table>
<h2 id="logstdout" class="common-anchor-header"><code translate="no">log.stdout</code><button data-href="#logstdout" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h2><table id="log.stdout">
  <thead>
    <tr>
      <th class="width80">Beschreibung</th>
      <th class="width20">Standardwert</th> 
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>        Stdout aktivieren oder nicht     </td>
      <td>wahr</td>
    </tr>
  </tbody>
</table>
