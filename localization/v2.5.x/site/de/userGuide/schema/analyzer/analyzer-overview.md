---
id: analyzer-overview.md
title: Analyzer Übersicht
summary: >-
  In der Textverarbeitung ist ein Analysator eine entscheidende Komponente, die
  Rohtext in ein strukturiertes, durchsuchbares Format umwandelt. Jeder Analyzer
  besteht in der Regel aus zwei Kernelementen: Tokenizer und Filter. Gemeinsam
  wandeln sie den Eingabetext in Token um, verfeinern diese Token und bereiten
  sie für eine effiziente Indizierung und Abfrage vor.
---
<h1 id="Analyzer-Overview" class="common-anchor-header">Analyzer Übersicht<button data-href="#Analyzer-Overview" class="anchor-icon" translate="no">
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
    </button></h1><p>In der Textverarbeitung ist ein <strong>Analyzer</strong> eine entscheidende Komponente, die Rohtext in ein strukturiertes, durchsuchbares Format umwandelt. Jeder Analyzer besteht in der Regel aus zwei Kernelementen: <strong>Tokenizer</strong> und <strong>Filter</strong>. Gemeinsam wandeln sie den Eingabetext in Token um, verfeinern diese Token und bereiten sie für eine effiziente Indizierung und Suche vor.</p>
<p>In Milvus werden die Analyzer während der Erstellung der Sammlung konfiguriert, wenn Sie <code translate="no">VARCHAR</code> Felder zum Schema der Sammlung hinzufügen. Die von einem Analyzer erzeugten Token können zum Aufbau eines Indexes für den Schlüsselwortabgleich verwendet oder in Sparse Embeddings für die Volltextsuche konvertiert werden. Weitere Informationen finden Sie unter <a href="/docs/de/keyword-match.md">Textabgleich</a> oder <a href="/docs/de/full-text-search.md">Volltextsuche</a>.</p>
<div class="alert note">
<p>Die Verwendung von Analyzern kann die Leistung beeinträchtigen:</p>
<ul>
<li><p><strong>Volltextsuche:</strong> Bei der Volltextsuche verbrauchen die <strong>DataNode-</strong> und <strong>QueryNode-Channels</strong> die Daten langsamer, da sie auf den Abschluss der Tokenisierung warten müssen. Infolgedessen dauert es länger, bis neu eingegebene Daten für die Suche verfügbar sind.</p></li>
<li><p><strong>Schlüsselwort-Abgleich:</strong> Beim Stichwortabgleich ist die Indexerstellung ebenfalls langsamer, da die Tokenisierung abgeschlossen werden muss, bevor ein Index erstellt werden kann.</p></li>
</ul>
</div>
<h2 id="Anatomy-of-an-analyzer" class="common-anchor-header">Anatomie eines Analyzers<button data-href="#Anatomy-of-an-analyzer" class="anchor-icon" translate="no">
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
    </button></h2><p>Ein Analyzer in Milvus besteht aus genau einem <strong>Tokenizer</strong> und <strong>null oder mehr</strong> Filtern.</p>
<ul>
<li><p><strong>Tokenisierer</strong>: Der Tokenisierer zerlegt den Eingabetext in diskrete Einheiten, die Token genannt werden. Diese Token können Wörter oder Phrasen sein, je nach Tokenizer-Typ.</p></li>
<li><p><strong>Filter</strong>: Filter können auf Token angewandt werden, um sie weiter zu verfeinern, z. B. durch Kleinschreibung oder das Entfernen häufiger Wörter.</p></li>
</ul>
<div class="alert note">
<p>Tokenizer unterstützen nur das UTF-8-Format. Die Unterstützung für andere Formate wird in zukünftigen Versionen hinzugefügt werden.</p>
</div>
<p>Der folgende Workflow zeigt, wie ein Analysator Text verarbeitet.</p>
<p>
  
   <span class="img-wrapper"> <img translate="no" src="/docs/v2.5.x/assets/analyzer-process-workflow.png" alt="analyzer-process-workflow" class="doc-image" id="analyzer-process-workflow" />
   </span> <span class="img-wrapper"> <span>Analysator-Verarbeitungs-Workflow</span> </span></p>
<h2 id="Analyzer-types" class="common-anchor-header">Analyzer-Typen<button data-href="#Analyzer-types" class="anchor-icon" translate="no">
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
    </button></h2><p>Milvus bietet zwei Arten von Analyzern, um unterschiedliche Anforderungen an die Textverarbeitung zu erfüllen:</p>
<ul>
<li><p><strong>Eingebauter Analysator</strong>: Hierbei handelt es sich um vordefinierte Konfigurationen, die gängige Textverarbeitungsaufgaben mit minimaler Einrichtung abdecken. Integrierte Analyzer sind ideal für allgemeine Suchvorgänge, da sie keine komplexe Konfiguration erfordern.</p></li>
<li><p><strong>Benutzerdefinierter Analyzer</strong>: Für anspruchsvollere Anforderungen können Sie mit benutzerdefinierten Analysatoren Ihre eigene Konfiguration definieren, indem Sie sowohl den Tokenizer als auch null oder mehr Filter angeben. Dieser Grad der Anpassung ist besonders nützlich für spezielle Anwendungsfälle, bei denen eine genaue Kontrolle über die Textverarbeitung erforderlich ist.</p></li>
</ul>
<div class="alert note">
<p>Wenn Sie bei der Erstellung der Sammlung die Konfiguration des Analysators weglassen, verwendet Milvus standardmäßig den <code translate="no">standard</code> Analysator für die gesamte Textverarbeitung. Weitere Informationen finden Sie unter <a href="/docs/de/standard-analyzer.md">Standard</a>.</p>
</div>
<h3 id="Built-in-analyzer" class="common-anchor-header">Eingebauter Analysator</h3><p>Eingebaute Analysatoren in Milvus sind mit spezifischen Tokenizern und Filtern vorkonfiguriert, so dass Sie sie sofort verwenden können, ohne diese Komponenten selbst definieren zu müssen. Jeder eingebaute Analyzer dient als Vorlage, die einen voreingestellten Tokenizer und Filter mit optionalen Parametern zur Anpassung enthält.</p>
<p>Um zum Beispiel den eingebauten Analyzer <code translate="no">standard</code> zu verwenden, geben Sie einfach seinen Namen <code translate="no">standard</code> als <code translate="no">type</code> an und fügen optional zusätzliche Konfigurationen hinzu, die für diesen Analyzer-Typ spezifisch sind, wie <code translate="no">stop_words</code>:</p>
<div class="multipleCode">
   <a href="#python">Python</a> <a href="#java">Java</a> <a href="#javascript">NodeJS</a> <a href="#bash">cURL</a></div>
<pre><code translate="no" class="language-python">analyzer_params = {
    <span class="hljs-string">&quot;type&quot;</span>: <span class="hljs-string">&quot;standard&quot;</span>, <span class="hljs-comment"># Uses the standard built-in analyzer</span>
    <span class="hljs-string">&quot;stop_words&quot;</span>: [<span class="hljs-string">&quot;a&quot;</span>, <span class="hljs-string">&quot;an&quot;</span>, <span class="hljs-string">&quot;for&quot;</span>] <span class="hljs-comment"># Defines a list of common words (stop words) to exclude from tokenization</span>
}
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-title class_">Map</span>&lt;<span class="hljs-title class_">String</span>, <span class="hljs-title class_">Object</span>&gt; analyzerParams = <span class="hljs-keyword">new</span> <span class="hljs-title class_">HashMap</span>&lt;&gt;();
analyzerParams.<span class="hljs-title function_">put</span>(<span class="hljs-string">&quot;type&quot;</span>, <span class="hljs-string">&quot;standard&quot;</span>);
analyzerParams.<span class="hljs-title function_">put</span>(<span class="hljs-string">&quot;stop_words&quot;</span>, <span class="hljs-title class_">Arrays</span>.<span class="hljs-title function_">asList</span>(<span class="hljs-string">&quot;a&quot;</span>, <span class="hljs-string">&quot;an&quot;</span>, <span class="hljs-string">&quot;for&quot;</span>));
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-keyword">const</span> analyzer_params = {
    <span class="hljs-string">&quot;type&quot;</span>: <span class="hljs-string">&quot;standard&quot;</span>, <span class="hljs-comment">// Uses the standard built-in analyzer</span>
    <span class="hljs-string">&quot;stop_words&quot;</span>: [<span class="hljs-string">&quot;a&quot;</span>, <span class="hljs-string">&quot;an&quot;</span>, <span class="hljs-string">&quot;for&quot;</span>] <span class="hljs-comment">// Defines a list of common words (stop words) to exclude from tokenization</span>
};
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-bash"><span class="hljs-built_in">export</span> analyzerParams=<span class="hljs-string">&#x27;{
       &quot;type&quot;: &quot;standard&quot;,
       &quot;stop_words&quot;: [&quot;a&quot;, &quot;an&quot;, &quot;for&quot;]
    }&#x27;</span>
<button class="copy-code-btn"></button></code></pre>
<p>Die obige Konfiguration des eingebauten Analyzers <code translate="no">standard</code> entspricht dem Einrichten eines <a href="/docs/de/analyzer-overview.md#null">benutzerdefinierten Analyzers</a> mit den folgenden Parametern, wobei die Optionen <code translate="no">tokenizer</code> und <code translate="no">filter</code> explizit definiert sind, um eine ähnliche Funktionalität zu erreichen:</p>
<div class="multipleCode">
   <a href="#python">Python</a> <a href="#java">Java</a> <a href="#javascript">NodeJS</a> <a href="#bash">cURL</a></div>
<pre><code translate="no" class="language-python">analyzer_params = {
    <span class="hljs-string">&quot;tokenizer&quot;</span>: <span class="hljs-string">&quot;standard&quot;</span>,
    <span class="hljs-string">&quot;filter&quot;</span>: [
        <span class="hljs-string">&quot;lowercase&quot;</span>,
        {
            <span class="hljs-string">&quot;type&quot;</span>: <span class="hljs-string">&quot;stop&quot;</span>,
            <span class="hljs-string">&quot;stop_words&quot;</span>: [<span class="hljs-string">&quot;a&quot;</span>, <span class="hljs-string">&quot;an&quot;</span>, <span class="hljs-string">&quot;for&quot;</span>]
        }
    ]
}
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-title class_">Map</span>&lt;<span class="hljs-title class_">String</span>, <span class="hljs-title class_">Object</span>&gt; analyzerParams = <span class="hljs-keyword">new</span> <span class="hljs-title class_">HashMap</span>&lt;&gt;();
analyzerParams.<span class="hljs-title function_">put</span>(<span class="hljs-string">&quot;tokenizer&quot;</span>, <span class="hljs-string">&quot;standard&quot;</span>);
analyzerParams.<span class="hljs-title function_">put</span>(<span class="hljs-string">&quot;filter&quot;</span>,
        <span class="hljs-title class_">Arrays</span>.<span class="hljs-title function_">asList</span>(<span class="hljs-string">&quot;lowercase&quot;</span>,
                <span class="hljs-keyword">new</span> <span class="hljs-title class_">HashMap</span>&lt;<span class="hljs-title class_">String</span>, <span class="hljs-title class_">Object</span>&gt;() {{
                    <span class="hljs-title function_">put</span>(<span class="hljs-string">&quot;type&quot;</span>, <span class="hljs-string">&quot;stop&quot;</span>);
                    <span class="hljs-title function_">put</span>(<span class="hljs-string">&quot;stop_words&quot;</span>, <span class="hljs-title class_">Arrays</span>.<span class="hljs-title function_">asList</span>(<span class="hljs-string">&quot;a&quot;</span>, <span class="hljs-string">&quot;an&quot;</span>, <span class="hljs-string">&quot;for&quot;</span>));
                }}));
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-keyword">const</span> analyzer_params = {
    <span class="hljs-string">&quot;tokenizer&quot;</span>: <span class="hljs-string">&quot;standard&quot;</span>,
    <span class="hljs-string">&quot;filter&quot;</span>: [
        <span class="hljs-string">&quot;lowercase&quot;</span>,
        {
            <span class="hljs-string">&quot;type&quot;</span>: <span class="hljs-string">&quot;stop&quot;</span>,
            <span class="hljs-string">&quot;stop_words&quot;</span>: [<span class="hljs-string">&quot;a&quot;</span>, <span class="hljs-string">&quot;an&quot;</span>, <span class="hljs-string">&quot;for&quot;</span>]
        }
    ]
};
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-bash"><span class="hljs-built_in">export</span> analyzerParams=<span class="hljs-string">&#x27;{
       &quot;type&quot;: &quot;standard&quot;,
       &quot;filter&quot;:  [
       &quot;lowercase&quot;,
       {
            &quot;type&quot;: &quot;stop&quot;,
            &quot;stop_words&quot;: [&quot;a&quot;, &quot;an&quot;, &quot;for&quot;]
       }
   ]
}&#x27;</span>
<button class="copy-code-btn"></button></code></pre>
<p>Milvus bietet die folgenden eingebauten Analyzer, die jeweils für spezifische Textverarbeitungsbedürfnisse entwickelt wurden:</p>
<ul>
<li><p><code translate="no">standard</code>: Geeignet für die allgemeine Textverarbeitung, mit Standard-Tokenisierung und Kleinbuchstaben-Filterung.</p></li>
<li><p><code translate="no">english</code>: Optimiert für englischsprachige Texte, mit Unterstützung für englische Stoppwörter.</p></li>
<li><p><code translate="no">chinese</code>: Spezialisiert für die Verarbeitung von chinesischem Text, einschließlich einer an die chinesischen Sprachstrukturen angepassten Tokenisierung.</p></li>
</ul>
<p>Eine Liste der eingebauten Analysatoren und ihrer anpassbaren Einstellungen finden Sie unter <a href="/docs/de/built-in-analyzers">Referenz der eingebauten Analysatoren</a>.</p>
<h3 id="Custom-analyzer" class="common-anchor-header">Benutzerdefinierter Analyzer</h3><p>Für eine fortgeschrittene Textverarbeitung können Sie mit den benutzerdefinierten Analysatoren in Milvus eine maßgeschneiderte Textverarbeitungspipeline aufbauen, indem Sie sowohl einen <strong>Tokenizer</strong> als auch <strong>Filter</strong> angeben. Dieses Setup ist ideal für spezielle Anwendungsfälle, bei denen eine präzise Kontrolle erforderlich ist.</p>
<h4 id="Tokenizer" class="common-anchor-header">Tokenisierer</h4><p>Der <strong>Tokenizer</strong> ist eine <strong>obligatorische</strong> Komponente für einen benutzerdefinierten Analyzer, der die Analyzer-Pipeline startet, indem er den Eingabetext in diskrete Einheiten oder <strong>Token</strong> zerlegt. Die Tokenisierung folgt je nach Tokenizer-Typ bestimmten Regeln, wie z. B. der Aufteilung nach Leerzeichen oder Interpunktion. Dieser Prozess ermöglicht eine präzisere und unabhängige Behandlung jedes Worts oder Satzes.</p>
<p>Ein Tokenizer würde zum Beispiel den Text <code translate="no">&quot;Vector Database Built for Scale&quot;</code> in einzelne Token umwandeln:</p>
<pre><code translate="no" class="language-plaintext">[<span class="hljs-string">&quot;Vector&quot;</span>, <span class="hljs-string">&quot;Database&quot;</span>, <span class="hljs-string">&quot;Built&quot;</span>, <span class="hljs-string">&quot;for&quot;</span>, <span class="hljs-string">&quot;Scale&quot;</span>]
<button class="copy-code-btn"></button></code></pre>
<p><strong>Beispiel für die Angabe eines Tokenizers</strong>:</p>
<div class="multipleCode">
   <a href="#python">Python</a> <a href="#java">Java</a> <a href="#javascript">NodeJS</a> <a href="#bash">cURL</a></div>
<pre><code translate="no" class="language-python">analyzer_params = {
    <span class="hljs-string">&quot;tokenizer&quot;</span>: <span class="hljs-string">&quot;whitespace&quot;</span>,
}
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-title class_">Map</span>&lt;<span class="hljs-title class_">String</span>, <span class="hljs-title class_">Object</span>&gt; analyzerParams = <span class="hljs-keyword">new</span> <span class="hljs-title class_">HashMap</span>&lt;&gt;();
analyzerParams.<span class="hljs-title function_">put</span>(<span class="hljs-string">&quot;tokenizer&quot;</span>, <span class="hljs-string">&quot;whitespace&quot;</span>);
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-keyword">const</span> analyzer_params = {
    <span class="hljs-string">&quot;tokenizer&quot;</span>: <span class="hljs-string">&quot;whitespace&quot;</span>,
};
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-bash"><span class="hljs-built_in">export</span> analyzerParams=<span class="hljs-string">&#x27;{
       &quot;type&quot;: &quot;whitespace&quot;
    }&#x27;</span>
<button class="copy-code-btn"></button></code></pre>
<p>Eine Liste der zur Auswahl stehenden Tokenizer finden Sie unter <a href="/docs/de/tokenizers">Tokenizer-Referenz</a>.</p>
<h4 id="Filter" class="common-anchor-header">Filter</h4><p><strong>Filter</strong> sind <strong>optionale</strong> Komponenten, die mit den vom Tokenizer erzeugten Token arbeiten und sie nach Bedarf umwandeln oder verfeinern. Nach Anwendung eines <code translate="no">lowercase</code> -Filters auf die tokenisierten Begriffe <code translate="no">[&quot;Vector&quot;, &quot;Database&quot;, &quot;Built&quot;, &quot;for&quot;, &quot;Scale&quot;]</code> könnte das Ergebnis zum Beispiel so aussehen:</p>
<pre><code translate="no" class="language-sql">[<span class="hljs-string">&quot;vector&quot;</span>, <span class="hljs-string">&quot;database&quot;</span>, <span class="hljs-string">&quot;built&quot;</span>, <span class="hljs-string">&quot;for&quot;</span>, <span class="hljs-string">&quot;scale&quot;</span>]
<button class="copy-code-btn"></button></code></pre>
<p>Filter in einem benutzerdefinierten Analyzer können entweder <strong>eingebaut</strong> oder <strong>benutzerdefiniert</strong> sein, je nach Konfigurationsbedarf.</p>
<ul>
<li><p><strong>Eingebaute Filter</strong>: Sie sind von Milvus vorkonfiguriert und erfordern nur eine minimale Einrichtung. Sie können diese Filter sofort verwenden, indem Sie ihre Namen angeben. Die folgenden Filter sind für den direkten Gebrauch eingebaut:</p>
<ul>
<li><p><code translate="no">lowercase</code>: Konvertiert Text in Kleinbuchstaben, um die Groß-/Kleinschreibung nicht zu berücksichtigen. Einzelheiten finden Sie unter <a href="/docs/de/lowercase-filter.md">Kleinschreibung</a>.</p></li>
<li><p><code translate="no">asciifolding</code>: Konvertiert Nicht-ASCII-Zeichen in ASCII-Äquivalente und vereinfacht so die Handhabung mehrsprachiger Texte. Weitere Informationen finden Sie unter <a href="/docs/de/ascii-folding-filter.md">ASCII-Faltung</a>.</p></li>
<li><p><code translate="no">alphanumonly</code>: Behält nur alphanumerische Zeichen bei und entfernt andere. Details finden Sie unter <a href="/docs/de/alphanumonly-filter.md">Alphanumonly</a>.</p></li>
<li><p><code translate="no">cnalphanumonly</code>: Entfernt Token, die andere Zeichen als chinesische Zeichen, englische Buchstaben oder Ziffern enthalten. Für weitere Informationen siehe <a href="/docs/de/cnalphanumonly-filter.md">Cnalphanumonly</a>.</p></li>
<li><p><code translate="no">cncharonly</code>: Entfernt Token, die nicht-chinesische Zeichen enthalten. Einzelheiten finden Sie unter <a href="/docs/de/cncharonly-filter.md">Cncharonly</a>.</p></li>
</ul>
<p><strong>Beispiel für die Verwendung eines eingebauten Filters:</strong></p>
<p><div class="multipleCode">
<a href="#python">Python</a><a href="#java">Java</a><a href="#javascript">NodeJS</a><a href="#bash">cURL</a></div></p>
<pre><code translate="no" class="language-python">analyzer_params = {
    <span class="hljs-string">&quot;tokenizer&quot;</span>: <span class="hljs-string">&quot;standard&quot;</span>, <span class="hljs-comment"># Mandatory: Specifies tokenizer</span>
    <span class="hljs-string">&quot;filter&quot;</span>: [<span class="hljs-string">&quot;lowercase&quot;</span>], <span class="hljs-comment"># Optional: Built-in filter that converts text to lowercase</span>
}
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-title class_">Map</span>&lt;<span class="hljs-title class_">String</span>, <span class="hljs-title class_">Object</span>&gt; analyzerParams = <span class="hljs-keyword">new</span> <span class="hljs-title class_">HashMap</span>&lt;&gt;();
analyzerParams.<span class="hljs-title function_">put</span>(<span class="hljs-string">&quot;tokenizer&quot;</span>, <span class="hljs-string">&quot;standard&quot;</span>);
analyzerParams.<span class="hljs-title function_">put</span>(<span class="hljs-string">&quot;filter&quot;</span>, <span class="hljs-title class_">Collections</span>.<span class="hljs-title function_">singletonList</span>(<span class="hljs-string">&quot;lowercase&quot;</span>));
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-keyword">const</span> analyzer_params = {
    <span class="hljs-string">&quot;tokenizer&quot;</span>: <span class="hljs-string">&quot;standard&quot;</span>, <span class="hljs-comment">// Mandatory: Specifies tokenizer</span>
    <span class="hljs-string">&quot;filter&quot;</span>: [<span class="hljs-string">&quot;lowercase&quot;</span>], <span class="hljs-comment">// Optional: Built-in filter that converts text to lowercase</span>
}
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-bash"><span class="hljs-built_in">export</span> analyzerParams=<span class="hljs-string">&#x27;{
       &quot;type&quot;: &quot;standard&quot;,
       &quot;filter&quot;:  [&quot;lowercase&quot;]
    }&#x27;</span>
<button class="copy-code-btn"></button></code></pre></li>
<li><p><strong>Benutzerdefinierte Filter</strong>: Benutzerdefinierte Filter ermöglichen spezielle Konfigurationen. Sie können einen benutzerdefinierten Filter definieren, indem Sie einen gültigen Filtertyp auswählen (<code translate="no">filter.type</code>) und spezifische Einstellungen für jeden Filtertyp hinzufügen. Beispiele für Filtertypen, die Anpassungen unterstützen:</p>
<ul>
<li><p><code translate="no">stop</code>: Entfernt bestimmte gebräuchliche Wörter, indem eine Liste von Stopp-Wörtern festgelegt wird (z. B. <code translate="no">&quot;stop_words&quot;: [&quot;of&quot;, &quot;to&quot;]</code>). Einzelheiten finden Sie unter <a href="/docs/de/stop-filter.md">Stopp</a>.</p></li>
<li><p><code translate="no">length</code>: Schließt Token aufgrund von Längenkriterien aus, z. B. durch Festlegen einer maximalen Tokenlänge. Weitere Informationen finden Sie unter <a href="/docs/de/length-filter.md">Länge</a>.</p></li>
<li><p><code translate="no">stemmer</code>: Reduziert Wörter auf ihre Stammformen für eine flexiblere Anpassung. Weitere Informationen finden Sie unter <a href="/docs/de/stemmer-filter.md">Stemmer</a>.</p></li>
</ul>
<p><strong>Beispiel für die Konfiguration eines benutzerdefinierten Filters:</strong></p>
<p><div class="multipleCode">
<a href="#python">Python</a><a href="#java">Java</a><a href="#javascript">NodeJS</a><a href="#bash">cURL</a></div></p>
<pre><code translate="no" class="language-python">analyzer_params = {
    <span class="hljs-string">&quot;tokenizer&quot;</span>: <span class="hljs-string">&quot;standard&quot;</span>, <span class="hljs-comment"># Mandatory: Specifies tokenizer</span>
    <span class="hljs-string">&quot;filter&quot;</span>: [
        {
            <span class="hljs-string">&quot;type&quot;</span>: <span class="hljs-string">&quot;stop&quot;</span>, <span class="hljs-comment"># Specifies &#x27;stop&#x27; as the filter type</span>
            <span class="hljs-string">&quot;stop_words&quot;</span>: [<span class="hljs-string">&quot;of&quot;</span>, <span class="hljs-string">&quot;to&quot;</span>], <span class="hljs-comment"># Customizes stop words for this filter type</span>
        }
    ]
}
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-title class_">Map</span>&lt;<span class="hljs-title class_">String</span>, <span class="hljs-title class_">Object</span>&gt; analyzerParams = <span class="hljs-keyword">new</span> <span class="hljs-title class_">HashMap</span>&lt;&gt;();
analyzerParams.<span class="hljs-title function_">put</span>(<span class="hljs-string">&quot;tokenizer&quot;</span>, <span class="hljs-string">&quot;standard&quot;</span>);
analyzerParams.<span class="hljs-title function_">put</span>(<span class="hljs-string">&quot;filter&quot;</span>,
        <span class="hljs-title class_">Collections</span>.<span class="hljs-title function_">singletonList</span>(<span class="hljs-keyword">new</span> <span class="hljs-title class_">HashMap</span>&lt;<span class="hljs-title class_">String</span>, <span class="hljs-title class_">Object</span>&gt;() {{
            <span class="hljs-title function_">put</span>(<span class="hljs-string">&quot;type&quot;</span>, <span class="hljs-string">&quot;stop&quot;</span>);
            <span class="hljs-title function_">put</span>(<span class="hljs-string">&quot;stop_words&quot;</span>, <span class="hljs-title class_">Arrays</span>.<span class="hljs-title function_">asList</span>(<span class="hljs-string">&quot;a&quot;</span>, <span class="hljs-string">&quot;an&quot;</span>, <span class="hljs-string">&quot;for&quot;</span>));
        }}));
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript">const analyzer_params = {
    <span class="hljs-string">&quot;tokenizer&quot;</span>: <span class="hljs-string">&quot;standard&quot;</span>, // Mandatory: Specifies tokenizer
    <span class="hljs-string">&quot;filter&quot;</span>: [
        {
            <span class="hljs-string">&quot;type&quot;</span>: <span class="hljs-string">&quot;stop&quot;</span>, // Specifies <span class="hljs-string">&#x27;stop&#x27;</span> <span class="hljs-keyword">as</span> the <span class="hljs-built_in">filter</span> <span class="hljs-built_in">type</span>
            <span class="hljs-string">&quot;stop_words&quot;</span>: [<span class="hljs-string">&quot;of&quot;</span>, <span class="hljs-string">&quot;to&quot;</span>], // Customizes stop words <span class="hljs-keyword">for</span> this <span class="hljs-built_in">filter</span> <span class="hljs-built_in">type</span>
        }
    ]
};
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-bash"><span class="hljs-built_in">export</span> analyzerParams=<span class="hljs-string">&#x27;{
       &quot;type&quot;: &quot;standard&quot;,
       &quot;filter&quot;:  [
       {
            &quot;type&quot;: &quot;stop&quot;,
            &quot;stop_words&quot;: [&quot;a&quot;, &quot;an&quot;, &quot;for&quot;]
       }
    ]
}&#x27;</span>
<button class="copy-code-btn"></button></code></pre>
<p>Eine Liste der verfügbaren Filtertypen und ihrer spezifischen Parameter finden Sie in der <a href="/docs/de/filters">Filterreferenz</a>.</p></li>
</ul>
<h2 id="Example-use" class="common-anchor-header">Beispiel für die Verwendung<button data-href="#Example-use" class="anchor-icon" translate="no">
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
    </button></h2><p>In diesem Beispiel definieren wir ein Sammlungsschema mit einem Vektorfeld für Einbettungen und zwei <code translate="no">VARCHAR</code> Feldern für Textverarbeitungsfunktionen. Jedes <code translate="no">VARCHAR</code> Feld wird mit eigenen Analyseeinstellungen konfiguriert, um unterschiedliche Verarbeitungsanforderungen zu erfüllen.</p>
<div class="multipleCode">
   <a href="#python">Python</a> <a href="#java">Java</a> <a href="#javascript">NodeJS</a> <a href="#bash">cURL</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> MilvusClient, DataType

<span class="hljs-comment"># Set up a Milvus client</span>
client = MilvusClient(
    uri=<span class="hljs-string">&quot;http://localhost:19530&quot;</span>
)

<span class="hljs-comment"># Create schema</span>
schema = client.create_schema(auto_id=<span class="hljs-literal">True</span>, enable_dynamic_field=<span class="hljs-literal">False</span>)

<span class="hljs-comment"># Add fields to schema</span>

<span class="hljs-comment"># Use a built-in analyzer</span>
analyzer_params_built_in = {
    <span class="hljs-string">&quot;type&quot;</span>: <span class="hljs-string">&quot;english&quot;</span>
}

<span class="hljs-comment"># Add VARCHAR field `title_en`</span>
schema.add_field(
    field_name=<span class="hljs-string">&#x27;title_en&#x27;</span>, 
    datatype=DataType.VARCHAR, 
    max_length=<span class="hljs-number">1000</span>, 
    enable_analyzer=<span class="hljs-literal">True</span>,
    analyzer_params=analyzer_params_built_in,
    enable_match=<span class="hljs-literal">True</span>, 
)

<span class="hljs-comment"># Configure a custom analyzer</span>
analyzer_params_custom = {
    <span class="hljs-string">&quot;tokenizer&quot;</span>: <span class="hljs-string">&quot;standard&quot;</span>,
    <span class="hljs-string">&quot;filter&quot;</span>: [
        <span class="hljs-string">&quot;lowercase&quot;</span>, <span class="hljs-comment"># Built-in filter</span>
        {
            <span class="hljs-string">&quot;type&quot;</span>: <span class="hljs-string">&quot;length&quot;</span>, <span class="hljs-comment"># Custom filter</span>
            <span class="hljs-string">&quot;max&quot;</span>: <span class="hljs-number">40</span>
        },
        {
            <span class="hljs-string">&quot;type&quot;</span>: <span class="hljs-string">&quot;stop&quot;</span>, <span class="hljs-comment"># Custom filter</span>
            <span class="hljs-string">&quot;stop_words&quot;</span>: [<span class="hljs-string">&quot;of&quot;</span>, <span class="hljs-string">&quot;to&quot;</span>]
        }
    ]
}

<span class="hljs-comment"># Add VARCHAR field `title`</span>
schema.add_field(
    field_name=<span class="hljs-string">&#x27;title&#x27;</span>, 
    datatype=DataType.VARCHAR, 
    max_length=<span class="hljs-number">1000</span>, 
    enable_analyzer=<span class="hljs-literal">True</span>,
    analyzer_params=analyzer_params_custom,
    enable_match=<span class="hljs-literal">True</span>, 
)

<span class="hljs-comment"># Add vector field</span>
schema.add_field(field_name=<span class="hljs-string">&quot;embedding&quot;</span>, datatype=DataType.FLOAT_VECTOR, dim=<span class="hljs-number">3</span>)
<span class="hljs-comment"># Add primary field</span>
schema.add_field(field_name=<span class="hljs-string">&quot;id&quot;</span>, datatype=DataType.INT64, is_primary=<span class="hljs-literal">True</span>)

<span class="hljs-comment"># Set up index params for vector field</span>
index_params = client.prepare_index_params()
index_params.add_index(field_name=<span class="hljs-string">&quot;embedding&quot;</span>, metric_type=<span class="hljs-string">&quot;COSINE&quot;</span>, index_type=<span class="hljs-string">&quot;AUTOINDEX&quot;</span>)

<span class="hljs-comment"># Create collection with defined schema</span>
client.create_collection(
    collection_name=<span class="hljs-string">&quot;YOUR_COLLECTION_NAME&quot;</span>,
    schema=schema,
    index_params=index_params
)
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.<span class="hljs-property">milvus</span>.<span class="hljs-property">v2</span>.<span class="hljs-property">client</span>.<span class="hljs-property">ConnectConfig</span>;
<span class="hljs-keyword">import</span> io.<span class="hljs-property">milvus</span>.<span class="hljs-property">v2</span>.<span class="hljs-property">client</span>.<span class="hljs-property">MilvusClientV2</span>;
<span class="hljs-keyword">import</span> io.<span class="hljs-property">milvus</span>.<span class="hljs-property">v2</span>.<span class="hljs-property">common</span>.<span class="hljs-property">DataType</span>;
<span class="hljs-keyword">import</span> io.<span class="hljs-property">milvus</span>.<span class="hljs-property">v2</span>.<span class="hljs-property">common</span>.<span class="hljs-property">IndexParam</span>;
<span class="hljs-keyword">import</span> io.<span class="hljs-property">milvus</span>.<span class="hljs-property">v2</span>.<span class="hljs-property">service</span>.<span class="hljs-property">collection</span>.<span class="hljs-property">request</span>.<span class="hljs-property">AddFieldReq</span>;
<span class="hljs-keyword">import</span> io.<span class="hljs-property">milvus</span>.<span class="hljs-property">v2</span>.<span class="hljs-property">service</span>.<span class="hljs-property">collection</span>.<span class="hljs-property">request</span>.<span class="hljs-property">CreateCollectionReq</span>;

<span class="hljs-comment">// Set up a Milvus client</span>
<span class="hljs-title class_">ConnectConfig</span> config = <span class="hljs-title class_">ConnectConfig</span>.<span class="hljs-title function_">builder</span>()
        .<span class="hljs-title function_">uri</span>(<span class="hljs-string">&quot;http://localhost:19530&quot;</span>)
        .<span class="hljs-title function_">build</span>();
<span class="hljs-title class_">MilvusClientV2</span> client = <span class="hljs-keyword">new</span> <span class="hljs-title class_">MilvusClientV2</span>(config);

<span class="hljs-comment">// Create schema</span>
<span class="hljs-title class_">CreateCollectionReq</span>.<span class="hljs-property">CollectionSchema</span> schema = <span class="hljs-title class_">CreateCollectionReq</span>.<span class="hljs-property">CollectionSchema</span>.<span class="hljs-title function_">builder</span>()
        .<span class="hljs-title function_">enableDynamicField</span>(<span class="hljs-literal">false</span>)
        .<span class="hljs-title function_">build</span>();

<span class="hljs-comment">// Add fields to schema</span>
<span class="hljs-comment">// Use a built-in analyzer</span>
<span class="hljs-title class_">Map</span>&lt;<span class="hljs-title class_">String</span>, <span class="hljs-title class_">Object</span>&gt; analyzerParamsBuiltin = <span class="hljs-keyword">new</span> <span class="hljs-title class_">HashMap</span>&lt;&gt;();
analyzerParamsBuiltin.<span class="hljs-title function_">put</span>(<span class="hljs-string">&quot;type&quot;</span>, <span class="hljs-string">&quot;english&quot;</span>);
<span class="hljs-comment">// Add VARCHAR field `title_en`</span>
schema.<span class="hljs-title function_">addField</span>(<span class="hljs-title class_">AddFieldReq</span>.<span class="hljs-title function_">builder</span>()
        .<span class="hljs-title function_">fieldName</span>(<span class="hljs-string">&quot;title_en&quot;</span>)
        .<span class="hljs-title function_">dataType</span>(<span class="hljs-title class_">DataType</span>.<span class="hljs-property">VarChar</span>)
        .<span class="hljs-title function_">maxLength</span>(<span class="hljs-number">1000</span>)
        .<span class="hljs-title function_">enableAnalyzer</span>(<span class="hljs-literal">true</span>)
        .<span class="hljs-title function_">analyzerParams</span>(analyzerParamsBuiltin)
        .<span class="hljs-title function_">enableMatch</span>(<span class="hljs-literal">true</span>)
        .<span class="hljs-title function_">build</span>());

<span class="hljs-comment">// Configure a custom analyzer</span>
<span class="hljs-title class_">Map</span>&lt;<span class="hljs-title class_">String</span>, <span class="hljs-title class_">Object</span>&gt; analyzerParams = <span class="hljs-keyword">new</span> <span class="hljs-title class_">HashMap</span>&lt;&gt;();
analyzerParams.<span class="hljs-title function_">put</span>(<span class="hljs-string">&quot;tokenizer&quot;</span>, <span class="hljs-string">&quot;standard&quot;</span>);
analyzerParams.<span class="hljs-title function_">put</span>(<span class="hljs-string">&quot;filter&quot;</span>,
        <span class="hljs-title class_">Arrays</span>.<span class="hljs-title function_">asList</span>(<span class="hljs-string">&quot;lowercase&quot;</span>,
                <span class="hljs-keyword">new</span> <span class="hljs-title class_">HashMap</span>&lt;<span class="hljs-title class_">String</span>, <span class="hljs-title class_">Object</span>&gt;() {{
                    <span class="hljs-title function_">put</span>(<span class="hljs-string">&quot;type&quot;</span>, <span class="hljs-string">&quot;length&quot;</span>);
                    <span class="hljs-title function_">put</span>(<span class="hljs-string">&quot;max&quot;</span>, <span class="hljs-number">40</span>);
                }},
                <span class="hljs-keyword">new</span> <span class="hljs-title class_">HashMap</span>&lt;<span class="hljs-title class_">String</span>, <span class="hljs-title class_">Object</span>&gt;() {{
                    <span class="hljs-title function_">put</span>(<span class="hljs-string">&quot;type&quot;</span>, <span class="hljs-string">&quot;stop&quot;</span>);
                    <span class="hljs-title function_">put</span>(<span class="hljs-string">&quot;stop_words&quot;</span>, <span class="hljs-title class_">Arrays</span>.<span class="hljs-title function_">asList</span>(<span class="hljs-string">&quot;a&quot;</span>, <span class="hljs-string">&quot;an&quot;</span>, <span class="hljs-string">&quot;for&quot;</span>));
                }}
        )
);
schema.<span class="hljs-title function_">addField</span>(<span class="hljs-title class_">AddFieldReq</span>.<span class="hljs-title function_">builder</span>()
        .<span class="hljs-title function_">fieldName</span>(<span class="hljs-string">&quot;title&quot;</span>)
        .<span class="hljs-title function_">dataType</span>(<span class="hljs-title class_">DataType</span>.<span class="hljs-property">VarChar</span>)
        .<span class="hljs-title function_">maxLength</span>(<span class="hljs-number">1000</span>)
        .<span class="hljs-title function_">enableAnalyzer</span>(<span class="hljs-literal">true</span>)
        .<span class="hljs-title function_">analyzerParams</span>(analyzerParams)
        .<span class="hljs-title function_">enableMatch</span>(<span class="hljs-literal">true</span>) <span class="hljs-comment">// must enable this if you use TextMatch</span>
        .<span class="hljs-title function_">build</span>());

<span class="hljs-comment">// Add vector field</span>
schema.<span class="hljs-title function_">addField</span>(<span class="hljs-title class_">AddFieldReq</span>.<span class="hljs-title function_">builder</span>()
        .<span class="hljs-title function_">fieldName</span>(<span class="hljs-string">&quot;embedding&quot;</span>)
        .<span class="hljs-title function_">dataType</span>(<span class="hljs-title class_">DataType</span>.<span class="hljs-property">FloatVector</span>)
        .<span class="hljs-title function_">dimension</span>(<span class="hljs-number">3</span>)
        .<span class="hljs-title function_">build</span>());
<span class="hljs-comment">// Add primary field</span>
schema.<span class="hljs-title function_">addField</span>(<span class="hljs-title class_">AddFieldReq</span>.<span class="hljs-title function_">builder</span>()
        .<span class="hljs-title function_">fieldName</span>(<span class="hljs-string">&quot;id&quot;</span>)
        .<span class="hljs-title function_">dataType</span>(<span class="hljs-title class_">DataType</span>.<span class="hljs-property">Int64</span>)
        .<span class="hljs-title function_">isPrimaryKey</span>(<span class="hljs-literal">true</span>)
        .<span class="hljs-title function_">autoID</span>(<span class="hljs-literal">true</span>)
        .<span class="hljs-title function_">build</span>());

<span class="hljs-comment">// Set up index params for vector field</span>
<span class="hljs-title class_">List</span>&lt;<span class="hljs-title class_">IndexParam</span>&gt; indexes = <span class="hljs-keyword">new</span> <span class="hljs-title class_">ArrayList</span>&lt;&gt;();
indexes.<span class="hljs-title function_">add</span>(<span class="hljs-title class_">IndexParam</span>.<span class="hljs-title function_">builder</span>()
        .<span class="hljs-title function_">fieldName</span>(<span class="hljs-string">&quot;embedding&quot;</span>)
        .<span class="hljs-title function_">indexType</span>(<span class="hljs-title class_">IndexParam</span>.<span class="hljs-property">IndexType</span>.<span class="hljs-property">AUTOINDEX</span>)
        .<span class="hljs-title function_">metricType</span>(<span class="hljs-title class_">IndexParam</span>.<span class="hljs-property">MetricType</span>.<span class="hljs-property">COSINE</span>)
        .<span class="hljs-title function_">build</span>());

<span class="hljs-comment">// Create collection with defined schema</span>
<span class="hljs-title class_">CreateCollectionReq</span> requestCreate = <span class="hljs-title class_">CreateCollectionReq</span>.<span class="hljs-title function_">builder</span>()
        .<span class="hljs-title function_">collectionName</span>(<span class="hljs-string">&quot;YOUR_COLLECTION_NAME&quot;</span>)
        .<span class="hljs-title function_">collectionSchema</span>(schema)
        .<span class="hljs-title function_">indexParams</span>(indexes)
        .<span class="hljs-title function_">build</span>();
client.<span class="hljs-title function_">createCollection</span>(requestCreate);
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-keyword">import</span> { MilvusClient, DataType } from <span class="hljs-string">&quot;@zilliz/milvus2-sdk-node&quot;</span>;

<span class="hljs-comment">// Set up a Milvus client</span>
<span class="hljs-keyword">const</span> client = <span class="hljs-built_in">new</span> MilvusClient(<span class="hljs-string">&quot;http://localhost:19530&quot;</span>);
<span class="hljs-comment">// Use a built-in analyzer for VARCHAR field `title_en`</span>
<span class="hljs-keyword">const</span> analyzerParamsBuiltIn = {
  <span class="hljs-keyword">type</span>: <span class="hljs-string">&quot;english&quot;</span>,
};

<span class="hljs-comment">// Configure a custom analyzer for VARCHAR field `title`</span>
<span class="hljs-keyword">const</span> analyzerParamsCustom = {
  tokenizer: <span class="hljs-string">&quot;standard&quot;</span>,
  filter: [
    <span class="hljs-string">&quot;lowercase&quot;</span>,
    {
      <span class="hljs-keyword">type</span>: <span class="hljs-string">&quot;length&quot;</span>,
      max: <span class="hljs-number">40</span>,
    },
    {
      <span class="hljs-keyword">type</span>: <span class="hljs-string">&quot;stop&quot;</span>,
      stop_words: [<span class="hljs-string">&quot;of&quot;</span>, <span class="hljs-string">&quot;to&quot;</span>],
    },
  ],
};

<span class="hljs-comment">// Create schema</span>
<span class="hljs-keyword">const</span> schema = {
  auto_id: <span class="hljs-literal">true</span>,
  fields: [
    {
      name: <span class="hljs-string">&quot;id&quot;</span>,
      <span class="hljs-keyword">type</span>: DataType.INT64,
      is_primary: <span class="hljs-literal">true</span>,
    },
    {
      name: <span class="hljs-string">&quot;title_en&quot;</span>,
      data_type: DataType.VARCHAR,
      max_length: <span class="hljs-number">1000</span>,
      enable_analyzer: <span class="hljs-literal">true</span>,
      analyzer_params: analyzerParamsBuiltIn,
      enable_match: <span class="hljs-literal">true</span>,
    },
    {
      name: <span class="hljs-string">&quot;title&quot;</span>,
      data_type: DataType.VARCHAR,
      max_length: <span class="hljs-number">1000</span>,
      enable_analyzer: <span class="hljs-literal">true</span>,
      analyzer_params: analyzerParamsCustom,
      enable_match: <span class="hljs-literal">true</span>,
    },
    {
      name: <span class="hljs-string">&quot;embedding&quot;</span>,
      data_type: DataType.FLOAT_VECTOR,
      dim: <span class="hljs-number">4</span>,
    },
  ],
};

<span class="hljs-comment">// Set up index params for vector field</span>
<span class="hljs-keyword">const</span> indexParams = [
  {
    name: <span class="hljs-string">&quot;embedding&quot;</span>,
    metric_type: <span class="hljs-string">&quot;COSINE&quot;</span>,
    index_type: <span class="hljs-string">&quot;AUTOINDEX&quot;</span>,
  },
];

<span class="hljs-comment">// Create collection with defined schema</span>
await client.createCollection({
  collection_name: <span class="hljs-string">&quot;YOUR_COLLECTION_NAME&quot;</span>,
  schema: schema,
  index_params: indexParams,
});

console.log(<span class="hljs-string">&quot;Collection created successfully!&quot;</span>);

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-bash"><span class="hljs-built_in">export</span> schema=<span class="hljs-string">&#x27;{
        &quot;autoId&quot;: true,
        &quot;enabledDynamicField&quot;: false,
        &quot;fields&quot;: [
            {
                &quot;fieldName&quot;: &quot;id&quot;,
                &quot;dataType&quot;: &quot;Int64&quot;,
                &quot;isPrimary&quot;: true
            },
            {
                &quot;fieldName&quot;: &quot;title_en&quot;,
                &quot;dataType&quot;: &quot;VarChar&quot;,
                &quot;elementTypeParams&quot;: {
                    &quot;max_length&quot;: 1000,
                    &quot;enable_analyzer&quot;: true,
                    &quot;enable_match&quot;: true,
                    &quot;analyzer_params&quot;: {&quot;type&quot;: &quot;english&quot;}
                }
            },
            {
                &quot;fieldName&quot;: &quot;title&quot;,
                &quot;dataType&quot;: &quot;VarChar&quot;,
                &quot;elementTypeParams&quot;: {
                    &quot;max_length&quot;: 1000,
                    &quot;enable_analyzer&quot;: true,
                    &quot;enable_match&quot;: true,
                    &quot;analyzer_params&quot;: {
                        &quot;tokenizer&quot;: &quot;standard&quot;,
                        &quot;filter&quot;:[
                            &quot;lowercase&quot;,
                            {
                                &quot;type&quot;:&quot;length&quot;,
                                &quot;max&quot;:40
                            },
                            {
                                &quot;type&quot;:&quot;stop&quot;,
                                &quot;stop_words&quot;:[&quot;of&quot;,&quot;to&quot;]
                            }
                        ]
                    }
                }
            },
            {
                &quot;fieldName&quot;: &quot;embedding&quot;,
                &quot;dataType&quot;: &quot;FloatVector&quot;,
                &quot;elementTypeParams&quot;: {
                    &quot;dim&quot;:3
                }
            }
        ]
    }&#x27;</span>
    
<span class="hljs-built_in">export</span> indexParams=<span class="hljs-string">&#x27;[
        {
            &quot;fieldName&quot;: &quot;embedding&quot;,
            &quot;metricType&quot;: &quot;COSINE&quot;,
            &quot;indexType&quot;: &quot;AUTOINDEX&quot;
        }
    ]&#x27;</span>

<span class="hljs-built_in">export</span> CLUSTER_ENDPOINT=<span class="hljs-string">&quot;http://localhost:19530&quot;</span>
<span class="hljs-built_in">export</span> TOKEN=<span class="hljs-string">&quot;root:Milvus&quot;</span>

curl --request POST \
--url <span class="hljs-string">&quot;<span class="hljs-variable">${CLUSTER_ENDPOINT}</span>/v2/vectordb/collections/create&quot;</span> \
--header <span class="hljs-string">&quot;Authorization: Bearer <span class="hljs-variable">${TOKEN}</span>&quot;</span> \
--header <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \
-d <span class="hljs-string">&quot;{
    \&quot;collectionName\&quot;: \&quot;YOUR_COLLECTION_NAME\&quot;,
    \&quot;schema\&quot;: <span class="hljs-variable">$schema</span>,
    \&quot;indexParams\&quot;: <span class="hljs-variable">$indexParams</span>
}&quot;</span>
<button class="copy-code-btn"></button></code></pre>
