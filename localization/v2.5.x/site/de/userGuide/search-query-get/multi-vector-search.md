---
id: multi-vector-search.md
order: 2
summary: >-
  In diesem Leitfaden wird gezeigt, wie man eine hybride Suche in Milvus
  durchführt und wie die Ergebnisse neu geordnet werden.
title: Hybride Suche
---
<h1 id="Hybrid-Search​" class="common-anchor-header">Hybride Suche<button data-href="#Hybrid-Search​" class="anchor-icon" translate="no">
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
    </button></h1><p>Die hybride Suche bezieht sich auf eine Suchmethode, die mehrere ANN-Suchen gleichzeitig durchführt, mehrere Ergebnissätze aus diesen ANN-Suchen neu ordnet und schließlich einen einzigen Ergebnissatz liefert. Die Verwendung von Hybrid Search kann die Suchgenauigkeit verbessern. Zilliz unterstützt die Durchführung von Hybrid Search in einer Sammlung mit mehreren Vektorfeldern. </p>
<p>Die hybride Suche wird am häufigsten in Szenarien verwendet, die spärliche und dichte Vektorsuchen und multimodale Suchen beinhalten. In diesem Leitfaden wird anhand eines konkreten Beispiels gezeigt, wie eine Hybrid-Suche in Zilliz durchgeführt werden kann.</p>
<h2 id="Scenarios​" class="common-anchor-header">Szenarien<button data-href="#Scenarios​" class="anchor-icon" translate="no">
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
    </button></h2><p>Die hybride Suche eignet sich für die folgenden beiden Szenarien.</p>
<h3 id="Sparse-Dense-Vector-Search​" class="common-anchor-header">Sparse-Dense-Vektorsuche</h3><p>Verschiedene Arten von Vektoren können unterschiedliche Informationen repräsentieren, und die Verwendung verschiedener Einbettungsmodelle kann verschiedene Merkmale und Aspekte der Daten umfassender darstellen. Zum Beispiel kann die Verwendung verschiedener Einbettungsmodelle für denselben Satz einen dichten Vektor zur Darstellung der semantischen Bedeutung und einen spärlichen Vektor zur Darstellung der Worthäufigkeit im Satz erzeugen.</p>
<ul>
<li><p><strong>Spärliche Vektoren:</strong> Spärliche Vektoren zeichnen sich durch ihre hohe Vektordimensionalität und das Vorhandensein von wenigen Werten ungleich Null aus. Aufgrund dieser Struktur eignen sie sich besonders gut für traditionelle Information Retrieval-Anwendungen. In den meisten Fällen entspricht die Anzahl der Dimensionen, die in spärlichen Vektoren verwendet werden, den verschiedenen Token in einer oder mehreren Sprachen. Jeder Dimension wird ein Wert zugewiesen, der die relative Bedeutung dieses Tokens innerhalb des Dokuments angibt. Dieses Layout erweist sich als vorteilhaft für Aufgaben, die einen Textabgleich beinhalten.</p></li>
<li><p><strong>Dichte Vektoren:</strong> Dichte Vektoren sind von neuronalen Netzen abgeleitete Einbettungen. Wenn sie in einem geordneten Array angeordnet sind, erfassen diese Vektoren das semantische Wesen des Eingabetextes. Dichte Vektoren sind nicht auf die Textverarbeitung beschränkt; sie werden auch häufig in der Computer Vision verwendet, um die Semantik von visuellen Daten darzustellen. Diese dichten Vektoren, die in der Regel durch Modelle zur Texteinbettung erzeugt werden, zeichnen sich dadurch aus, dass die meisten oder alle Elemente ungleich Null sind. Daher eignen sich dichte Vektoren besonders gut für semantische Suchanwendungen, da sie auf der Grundlage der Vektordistanz die ähnlichsten Ergebnisse liefern können, selbst wenn es keine exakten Textübereinstimmungen gibt. Diese Fähigkeit ermöglicht nuanciertere und kontextbezogene Suchergebnisse, die oft Beziehungen zwischen Konzepten erfassen, die bei schlagwortbasierten Ansätzen übersehen werden könnten.</p></li>
</ul>
<p>Weitere Einzelheiten finden Sie unter <a href="/docs/de/sparse_vector.md">Sparse Vector</a> und <a href="/docs/de/dense-vector.md">Dense Vector</a>.</p>
<h3 id="Multimodal-Search​" class="common-anchor-header">Multimodale Suche</h3><p>Multimodale Suche bezieht sich auf die Ähnlichkeitssuche von unstrukturierten Daten über mehrere Modalitäten hinweg (wie Bilder, Videos, Audio, Text usw.). Eine Person kann beispielsweise durch verschiedene Modalitäten von Daten wie Fingerabdrücke, Stimmabdrücke und Gesichtsmerkmale dargestellt werden. Die hybride Suche unterstützt mehrere Suchvorgänge gleichzeitig. Zum Beispiel die Suche nach einer Person mit ähnlichen Fingerabdrücken und Stimmbildern.</p>
<h2 id="Workflow​" class="common-anchor-header">Arbeitsablauf<button data-href="#Workflow​" class="anchor-icon" translate="no">
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
    </button></h2><p>Der Hauptarbeitsablauf für die Durchführung einer hybriden Suche sieht wie folgt aus.</p>
<ol>
<li><p>Erzeugen von dichten Vektoren durch Einbettungsmodelle wie <a href="https://zilliz.com/learn/explore-colbert-token-level-embedding-and-ranking-model-for-similarity-search#A-Quick-Recap-of-BERT">BERT</a> und <a href="https://zilliz.com/learn/NLP-essentials-understanding-transformers-in-AI">Transformers</a>.</p></li>
<li><p>Generieren Sie spärliche Vektoren durch Einbettungsmodelle wie <a href="https://zilliz.com/learn/mastering-bm25-a-deep-dive-into-the-algorithm-and-application-in-milvus">BM25</a>, <a href="https://zilliz.com/learn/bge-m3-and-splade-two-machine-learning-models-for-generating-sparse-embeddings#BGE-M3">BGE-M3</a>, <a href="https://zilliz.com/learn/bge-m3-and-splade-two-machine-learning-models-for-generating-sparse-embeddings#SPLADE">SPLADE</a> usw. In Milvus können Sie die Funktion zur Generierung spärlicher Vektoren verwenden. Weitere Informationen finden Sie unter <a href="/docs/de/full-text-search.md">Volltextsuche</a>.</p></li>
<li><p>Erstellen Sie eine Sammlung und definieren Sie das Sammlungsschema, das sowohl dichte als auch spärliche Vektorfelder enthält.</p></li>
<li><p>Fügen Sie spärlich-dichte Vektoren in die im vorherigen Schritt erstellte Sammlung ein.</p></li>
<li><p>Führen Sie eine hybride Suche durch: Die ANN-Suche in dichten Vektoren liefert eine Reihe von Top-K-Ergebnissen mit der größten Ähnlichkeit, und der Textabgleich in spärlichen Vektoren liefert ebenfalls eine Reihe von Top-K-Ergebnissen.</p></li>
<li><p>Normalisierung: Normalisieren Sie die Punktzahlen der beiden Sätze von Top-K-Ergebnissen, indem Sie die Punktzahlen in einen Bereich zwischen [0,1] umwandeln.</p></li>
<li><p>Wählen Sie eine geeignete Reranking-Strategie, um die beiden Gruppen von Top-K-Ergebnissen zusammenzuführen und neu zu ordnen und schließlich eine endgültige Gruppe von Top-K-Ergebnissen zu erhalten.</p></li>
</ol>
<p>
  
   <span class="img-wrapper"> <img translate="no" src="/docs/v2.5.x/assets/hybrid-search.png" alt="Hybrid Search Workflow" class="doc-image" id="hybrid-search-workflow" />
   </span> <span class="img-wrapper"> <span>Hybrider Such-Workflow</span> </span></p>
<h2 id="Examples​" class="common-anchor-header">Beispiele<button data-href="#Examples​" class="anchor-icon" translate="no">
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
    </button></h2><p>In diesem Abschnitt wird anhand eines konkreten Beispiels gezeigt, wie eine hybride Suche auf spärlich dichten Vektoren durchgeführt werden kann, um die Genauigkeit der Textsuche zu verbessern.</p>
<h3 id="Create-a-collection-with-multiple-vector-fields​" class="common-anchor-header">Erstellen einer Sammlung mit mehreren Vektorfeldern</h3><p>Der Prozess der Erstellung einer Sammlung umfasst drei Teile: Definieren des Schemas der Sammlung, Konfigurieren der Indexparameter und Erstellen der Sammlung.</p>
<h4 id="Define-schema​" class="common-anchor-header">Definieren des Schemas</h4><p>In diesem Beispiel müssen mehrere Vektorfelder im Schema der Sammlung definiert werden. Derzeit kann jede Sammlung standardmäßig bis zu 4 Vektorfelder enthalten. Sie können aber auch den Wert von  <a href="https://milvus.io/docs/configure_proxy.md#proxymaxVectorFieldNum"><code translate="no">proxy.maxVectorFieldNum</code></a>  ändern, um bei Bedarf bis zu 10 Vektorfelder in eine Sammlung aufzunehmen.</p>
<p>Das folgende Beispiel definiert ein Auflistungsschema, wobei <code translate="no">dense</code> und <code translate="no">sparse</code> die beiden Vektorfelder sind.</p>
<ul>
<li><p><code translate="no">id</code>: Dieses Feld dient als Primärschlüssel für die Speicherung von Text-IDs. Der Datentyp dieses Feldes ist INT64.</p></li>
<li><p><code translate="no">text</code>: Dieses Feld dient zur Speicherung von Textinhalten. Der Datentyp dieses Feldes ist VARCHAR, mit einer maximalen Länge von 1000 Zeichen.</p></li>
<li><p><code translate="no">dense</code>: In diesem Feld werden die dichten Vektoren der Texte gespeichert. Der Datentyp dieses Feldes ist FLOAT_VECTOR, mit einer Vektordimension von 768.</p></li>
<li><p><code translate="no">sparse</code>: In diesem Feld werden die spärlichen Vektoren der Texte gespeichert. Der Datentyp dieses Feldes ist SPARSE_FLOAT_VECTOR. In diesem Beispiel verwenden wir die Funktion, um spärliche Vektoren zu erzeugen.</p></li>
</ul>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a> <a href="#curl">cURL</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># Create a collection in customized setup mode​</span>
<span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> (​
    MilvusClient, DataType​
)​
​
client = MilvusClient(​
    uri=<span class="hljs-string">&quot;http://localhost:19530&quot;</span>,​
    token=<span class="hljs-string">&quot;root:Milvus&quot;</span>​
)​
​
<span class="hljs-comment"># Create schema​</span>
schema = MilvusClient.create_schema(​
    auto_id=<span class="hljs-literal">False</span>,​
    enable_dynamic_field=<span class="hljs-literal">True</span>,​
)​
<span class="hljs-comment"># Add fields to schema​</span>
schema.add_field(field_name=<span class="hljs-string">&quot;id&quot;</span>, datatype=DataType.INT64, is_primary=<span class="hljs-literal">True</span>)​
schema.add_field(field_name=<span class="hljs-string">&quot;text&quot;</span>, datatype=DataType.VARCHAR, max_length=<span class="hljs-number">1000</span>)​
<span class="hljs-comment"># Define a sparse vector field to generate spare vectors with BM25</span>
schema.add_field(field_name=<span class="hljs-string">&quot;sparse&quot;</span>, datatype=DataType.SPARSE_FLOAT_VECTOR)​
schema.add_field(field_name=<span class="hljs-string">&quot;dense&quot;</span>, datatype=DataType.FLOAT_VECTOR, dim=<span class="hljs-number">5</span>)​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.milvus.v2.client.ConnectConfig;​
<span class="hljs-keyword">import</span> io.milvus.v2.client.MilvusClientV2;​
<span class="hljs-keyword">import</span> io.milvus.v2.common.DataType;​
<span class="hljs-keyword">import</span> io.milvus.v2.service.collection.request.AddFieldReq;​
<span class="hljs-keyword">import</span> io.milvus.v2.service.collection.request.CreateCollectionReq;​
​
<span class="hljs-type">MilvusClientV2</span> <span class="hljs-variable">client</span> <span class="hljs-operator">=</span> <span class="hljs-keyword">new</span> <span class="hljs-title class_">MilvusClientV2</span>(ConnectConfig.builder()​
        .uri(<span class="hljs-string">&quot;http://localhost:19530&quot;</span>)​
        .token(<span class="hljs-string">&quot;root:Milvus&quot;</span>)​
        .build());​
​
CreateCollectionReq.<span class="hljs-type">CollectionSchema</span> <span class="hljs-variable">schema</span> <span class="hljs-operator">=</span> client.createSchema();​
schema.addField(AddFieldReq.builder()​
        .fieldName(<span class="hljs-string">&quot;id&quot;</span>)​
        .dataType(DataType.Int64)​
        .isPrimaryKey(<span class="hljs-literal">true</span>)​
        .autoID(<span class="hljs-literal">false</span>)​
        .build());​
​
schema.addField(AddFieldReq.builder()​
        .fieldName(<span class="hljs-string">&quot;text&quot;</span>)​
        .dataType(DataType.VarChar)​
        .maxLength(<span class="hljs-number">1000</span>)​
        .build());​
​
schema.addField(AddFieldReq.builder()​
        .fieldName(<span class="hljs-string">&quot;dense&quot;</span>)​
        .dataType(DataType.FloatVector)​
        .dimension(<span class="hljs-number">768</span>)​
        .build());​
​
schema.addField(AddFieldReq.builder()​
        .fieldName(<span class="hljs-string">&quot;sparse&quot;</span>)​
        .dataType(DataType.SparseFloatVector)​
        .build());​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-go"><span class="hljs-comment">// WIP​</span>

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-keyword">import</span> { <span class="hljs-title class_">MilvusClient</span>, <span class="hljs-title class_">DataType</span> } <span class="hljs-keyword">from</span> <span class="hljs-string">&quot;@zilliz/milvus2-sdk-node&quot;</span>;​
​
<span class="hljs-keyword">const</span> address = <span class="hljs-string">&quot;http://localhost:19530&quot;</span>;​
<span class="hljs-keyword">const</span> token = <span class="hljs-string">&quot;root:Milvus&quot;</span>;​
<span class="hljs-keyword">const</span> client = <span class="hljs-keyword">new</span> <span class="hljs-title class_">MilvusClient</span>({address, token});​
​
<span class="hljs-comment">// Create a collection in customized setup mode​</span>
<span class="hljs-comment">// Define fields​</span>
<span class="hljs-keyword">const</span> fields = [​
    {​
        <span class="hljs-attr">name</span>: <span class="hljs-string">&quot;id&quot;</span>,​
        <span class="hljs-attr">data_type</span>: <span class="hljs-title class_">DataType</span>.<span class="hljs-property">Int64</span>,​
        <span class="hljs-attr">is_primary_key</span>: <span class="hljs-literal">true</span>,​
        <span class="hljs-attr">auto_id</span>: <span class="hljs-literal">false</span>​
    },​
    {​
        <span class="hljs-attr">name</span>: <span class="hljs-string">&quot;text&quot;</span>,​
        <span class="hljs-attr">data_type</span>: <span class="hljs-title class_">DataType</span>.<span class="hljs-property">VarChar</span>,​
        <span class="hljs-attr">max_length</span>: <span class="hljs-number">1000</span>​
    },​
    {​
        <span class="hljs-attr">name</span>: <span class="hljs-string">&quot;sparse&quot;</span>,​
        <span class="hljs-attr">data_type</span>: <span class="hljs-title class_">DataType</span>.<span class="hljs-property">SPARSE_FLOAT_VECTOR</span>​
    },​
    {​
        <span class="hljs-attr">name</span>: <span class="hljs-string">&quot;dense&quot;</span>,​
        <span class="hljs-attr">data_type</span>: <span class="hljs-title class_">DataType</span>.<span class="hljs-property">FloatVector</span>,​
        <span class="hljs-attr">dim</span>: <span class="hljs-number">768</span>​
    }​
]​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-curl"><span class="hljs-built_in">export</span> schema=<span class="hljs-string">&#x27;{​
        &quot;autoId&quot;: false,​
        &quot;enabledDynamicField&quot;: true,​
        &quot;fields&quot;: [​
            {​
                &quot;fieldName&quot;: &quot;id&quot;,​
                &quot;dataType&quot;: &quot;Int64&quot;,​
                &quot;isPrimary&quot;: true​
            },​
            {​
                &quot;fieldName&quot;: &quot;text&quot;,​
                &quot;dataType&quot;: &quot;VarChar&quot;,​
                &quot;elementTypeParams&quot;: {​
                    &quot;max_length&quot;: 1000​
                }​
            },​
            {​
                &quot;fieldName&quot;: &quot;sparse&quot;,​
                &quot;dataType&quot;: &quot;SparseFloatVector&quot;​
            },​
            {​
                &quot;fieldName&quot;: &quot;dense&quot;,​
                &quot;dataType&quot;: &quot;FloatVector&quot;,​
                &quot;elementTypeParams&quot;: {​
                    &quot;dim&quot;: &quot;768&quot;​
                }​
            }​
        ]​
    }&#x27;</span>​

<button class="copy-code-btn"></button></code></pre>
<p>Bei der Suche nach Sparse Vectors können Sie den Prozess der Erzeugung von Sparse Embedding Vectors vereinfachen, indem Sie die Funktionen der Volltextsuche nutzen. Für weitere Details siehe <a href="/docs/de/full-text-search.md">Volltextsuche</a>.</p>
<h4 id="Define-function-to-generate-sparse-vectors​" class="common-anchor-header">Funktion zur Erzeugung von Sparse-Vektoren definieren</h4><p>Um spärliche Vektoren zu erzeugen, können Sie die Funktion "Function" in Milvus verwenden. Das folgende Beispiel definiert eine Funktion zur Erzeugung spärlicher Vektoren unter Verwendung des BM25-Algorithmus. Weitere Informationen finden Sie unter <a href="/docs/de/full-text-search.md">Volltextsuche</a>.</p>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a> <a href="#curl">cURL</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># Define function to generate sparse vectors</span>

bm25_function = Function(
    name=<span class="hljs-string">&quot;text_bm25_emb&quot;</span>, <span class="hljs-comment"># Function name</span>
    input_field_names=[<span class="hljs-string">&quot;text&quot;</span>], <span class="hljs-comment"># Name of the VARCHAR field containing raw text data</span>
    output_field_names=[<span class="hljs-string">&quot;sparse&quot;</span>], <span class="hljs-comment"># Name of the SPARSE_FLOAT_VECTOR field reserved to store generated embeddings</span>
    function_type=FunctionType.BM25,
)

schema.add_function(bm25_function)
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.milvus.common.clientenum.FunctionType;
<span class="hljs-keyword">import</span> io.milvus.v2.service.collection.request.CreateCollectionReq.Function;

<span class="hljs-keyword">import</span> java.util.*;

schema.addFunction(Function.builder()
        .functionType(FunctionType.BM25)
        .name(<span class="hljs-string">&quot;text_bm25_emb&quot;</span>)
        .inputFieldNames(Collections.singletonList(<span class="hljs-string">&quot;text&quot;</span>))
        .outputFieldNames(Collections.singletonList(<span class="hljs-string">&quot;sparse&quot;</span>))
        .build());
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript">const <span class="hljs-built_in">functions</span> = [
    {
      name: <span class="hljs-string">&#x27;text_bm25_emb&#x27;</span>,
      description: <span class="hljs-string">&#x27;bm25 function&#x27;</span>,
      <span class="hljs-built_in">type</span>: FunctionType.BM25,
      input_field_names: [<span class="hljs-string">&#x27;text&#x27;</span>],
      output_field_names: [<span class="hljs-string">&#x27;sparse&#x27;</span>],
      params: {},
    },
]；
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-curl"><span class="hljs-built_in">export</span> schema=<span class="hljs-string">&#x27;{
        &quot;autoId&quot;: true,
        &quot;enabledDynamicField&quot;: false,
        &quot;fields&quot;: [
            {
                &quot;fieldName&quot;: &quot;id&quot;,
                &quot;dataType&quot;: &quot;Int64&quot;,
                &quot;isPrimary&quot;: true
            },
            {
                &quot;fieldName&quot;: &quot;text&quot;,
                &quot;dataType&quot;: &quot;VarChar&quot;,
                &quot;elementTypeParams&quot;: {
                    &quot;max_length&quot;: 1000,
                    &quot;enable_analyzer&quot;: true
                }
            },
            {
                &quot;fieldName&quot;: &quot;sparse&quot;,
                &quot;dataType&quot;: &quot;SparseFloatVector&quot;
            }
        ],
        &quot;functions&quot;: [
            {
                &quot;name&quot;: &quot;text_bm25_emb&quot;,
                &quot;type&quot;: &quot;BM25&quot;,
                &quot;inputFieldNames&quot;: [&quot;text&quot;],
                &quot;outputFieldNames&quot;: [&quot;sparse&quot;],
                &quot;params&quot;: {}
            }
        ]
    }&#x27;</span>
<button class="copy-code-btn"></button></code></pre>
<h4 id="Create-index​" class="common-anchor-header">Index erstellen</h4><p>Nach der Definition des Sammelschemas müssen die Vektorindizes und die Ähnlichkeitsmetriken eingerichtet werden. In diesem Beispiel wird ein IVF_FLAT-Index für das dichte Vektorfeld <code translate="no">dense</code> und ein SPARSE_INVERTED_INDEX für das spärliche Vektorfeld <code translate="no">sparse</code> erstellt. Weitere Informationen zu den unterstützten Indextypen finden Sie unter <a href="https://milvus.io/docs/index.md?tab=floating">Index erklärt</a>.</p>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a> <a href="#curl">cURL</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> MilvusClient​
​
<span class="hljs-comment"># Prepare index parameters​</span>
index_params = client.prepare_index_params()​
​
<span class="hljs-comment"># Add indexes​</span>
index_params.add_index(​
    field_name=<span class="hljs-string">&quot;dense&quot;</span>,​
    index_name=<span class="hljs-string">&quot;dense_index&quot;</span>,​
    index_type=<span class="hljs-string">&quot;IVF_FLAT&quot;</span>,​
    metric_type=<span class="hljs-string">&quot;IP&quot;</span>,​
    params={<span class="hljs-string">&quot;nlist&quot;</span>: <span class="hljs-number">128</span>},​
)​
​
index_params.add_index(
    field_name=<span class="hljs-string">&quot;sparse&quot;</span>,
    index_name=<span class="hljs-string">&quot;sparse_index&quot;</span>,
    index_type=<span class="hljs-string">&quot;SPARSE_INVERTED_INDEX&quot;</span>,  <span class="hljs-comment"># Index type for sparse vectors</span>
    metric_type=<span class="hljs-string">&quot;BM25&quot;</span>,  <span class="hljs-comment"># Set to `BM25` when using function to generate sparse vectors</span>
    params={<span class="hljs-string">&quot;inverted_index_algo&quot;</span>: <span class="hljs-string">&quot;DAAT_MAXSCORE&quot;</span>},  <span class="hljs-comment"># The ratio of small vector values to be dropped during indexing</span>
)
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.<span class="hljs-property">milvus</span>.<span class="hljs-property">v2</span>.<span class="hljs-property">common</span>.<span class="hljs-property">IndexParam</span>;​
<span class="hljs-keyword">import</span> java.<span class="hljs-property">util</span>.*;​
​
<span class="hljs-title class_">Map</span>&lt;<span class="hljs-title class_">String</span>, <span class="hljs-title class_">Object</span>&gt; denseParams = <span class="hljs-keyword">new</span> <span class="hljs-title class_">HashMap</span>&lt;&gt;();​
denseParams.<span class="hljs-title function_">put</span>(<span class="hljs-string">&quot;nlist&quot;</span>, <span class="hljs-number">128</span>);​
<span class="hljs-title class_">IndexParam</span> indexParamForDenseField = <span class="hljs-title class_">IndexParam</span>.<span class="hljs-title function_">builder</span>()​
        .<span class="hljs-title function_">fieldName</span>(<span class="hljs-string">&quot;dense&quot;</span>)​
        .<span class="hljs-title function_">indexName</span>(<span class="hljs-string">&quot;dense_index&quot;</span>)​
        .<span class="hljs-title function_">indexType</span>(<span class="hljs-title class_">IndexParam</span>.<span class="hljs-property">IndexType</span>.<span class="hljs-property">IVF_FLAT</span>)​
        .<span class="hljs-title function_">metricType</span>(<span class="hljs-title class_">IndexParam</span>.<span class="hljs-property">MetricType</span>.<span class="hljs-property">IP</span>)​
        .<span class="hljs-title function_">extraParams</span>(denseParams)​
        .<span class="hljs-title function_">build</span>();​
​
<span class="hljs-title class_">Map</span>&lt;<span class="hljs-title class_">String</span>, <span class="hljs-title class_">Object</span>&gt; sparseParams = <span class="hljs-keyword">new</span> <span class="hljs-title class_">HashMap</span>&lt;&gt;();​
sparseParams.<span class="hljs-title function_">put</span>(<span class="hljs-string">&quot;inverted_index_algo&quot;</span>: <span class="hljs-string">&quot;DAAT_MAXSCORE&quot;</span>);​ <span class="hljs-comment">// Algorithm used for building and querying the index</span>
<span class="hljs-title class_">IndexParam</span> indexParamForSparseField = <span class="hljs-title class_">IndexParam</span>.<span class="hljs-title function_">builder</span>()​
        .<span class="hljs-title function_">fieldName</span>(<span class="hljs-string">&quot;sparse&quot;</span>)​
        .<span class="hljs-title function_">indexName</span>(<span class="hljs-string">&quot;sparse_index&quot;</span>)​
        .<span class="hljs-title function_">indexType</span>(<span class="hljs-title class_">IndexParam</span>.<span class="hljs-property">IndexType</span>.<span class="hljs-property">SPARSE_INVERTED_INDEX</span>)​
        .<span class="hljs-title function_">metricType</span>(<span class="hljs-title class_">IndexParam</span>.<span class="hljs-property">MetricType</span>.<span class="hljs-property">BM25</span>)​
        .<span class="hljs-title function_">extraParams</span>(sparseParams)​
        .<span class="hljs-title function_">build</span>();​
​
<span class="hljs-title class_">List</span>&lt;<span class="hljs-title class_">IndexParam</span>&gt; indexParams = <span class="hljs-keyword">new</span> <span class="hljs-title class_">ArrayList</span>&lt;&gt;();​
indexParams.<span class="hljs-title function_">add</span>(indexParamForDenseField);​
indexParams.<span class="hljs-title function_">add</span>(indexParamForSparseField);​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-keyword">const</span> index_params = [{​
    <span class="hljs-attr">field_name</span>: <span class="hljs-string">&quot;dense&quot;</span>,​
    <span class="hljs-attr">index_type</span>: <span class="hljs-string">&quot;IVF_FLAT&quot;</span>,​
    <span class="hljs-attr">metric_type</span>: <span class="hljs-string">&quot;IP&quot;</span>​
},{​
    <span class="hljs-attr">field_name</span>: <span class="hljs-string">&quot;sparse&quot;</span>,​
    <span class="hljs-attr">index_type</span>: <span class="hljs-string">&quot;SPARSE_INVERTED_INDEX&quot;</span>,​
    <span class="hljs-attr">metric_type</span>: <span class="hljs-string">&quot;BM25&quot;</span>​
}]​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-curl"><span class="hljs-built_in">export</span> indexParams=<span class="hljs-string">&#x27;[​
        {​
            &quot;fieldName&quot;: &quot;dense&quot;,​
            &quot;metricType&quot;: &quot;IP&quot;,​
            &quot;indexName&quot;: &quot;dense_index&quot;,​
            &quot;indexType&quot;:&quot;IVF_FLAT&quot;,​
            &quot;params&quot;:{&quot;nlist&quot;:128}​
        },​
        {​
            &quot;fieldName&quot;: &quot;sparse&quot;,​
            &quot;metricType&quot;: &quot;BM25&quot;,​
            &quot;indexName&quot;: &quot;sparse_index&quot;,​
            &quot;indexType&quot;: &quot;SPARSE_INVERTED_INDEX&quot;​
        }​
    ]&#x27;</span>​

<button class="copy-code-btn"></button></code></pre>
<h4 id="Create-collection​" class="common-anchor-header">Sammlung erstellen</h4><p>Erstellen Sie eine Sammlung mit dem Namen <code translate="no">demo</code> mit dem Sammlungsschema und den Indizes, die in den beiden vorherigen Schritten konfiguriert wurden.</p>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a> <a href="#curl">cURL</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> <span class="hljs-title class_">MilvusClient</span>​
​
client.<span class="hljs-title function_">create_collection</span>(​
    collection_name=<span class="hljs-string">&quot;hybrid_search_collection&quot;</span>,​
    schema=schema,​
    index_params=index_params​
)​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-type">CreateCollectionReq</span> <span class="hljs-variable">createCollectionReq</span> <span class="hljs-operator">=</span> CreateCollectionReq.builder()​
        .collectionName(<span class="hljs-string">&quot;hybrid_search_collection&quot;</span>)​
        .collectionSchema(schema)​
        .indexParams(indexParams)​
        .build();​
client.createCollection(createCollectionReq);​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript">res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">createCollection</span>({​
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;hybrid_search_collection&quot;</span>,​
    <span class="hljs-attr">fields</span>: fields,​
    <span class="hljs-attr">index_params</span>: index_params,​
})​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-curl"><span class="hljs-built_in">export</span> CLUSTER_ENDPOINT=<span class="hljs-string">&quot;http://localhost:19530&quot;</span>​
<span class="hljs-built_in">export</span> TOKEN=<span class="hljs-string">&quot;root:Milvus&quot;</span>​
​
curl --request POST \​
--url <span class="hljs-string">&quot;<span class="hljs-variable">${CLUSTER_ENDPOINT}</span>/v2/vectordb/collections/create&quot;</span> \​
--header <span class="hljs-string">&quot;Authorization: Bearer <span class="hljs-variable">${TOKEN}</span>&quot;</span> \​
--header <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \​
-d <span class="hljs-string">&quot;{​
    \&quot;collectionName\&quot;: \&quot;hybrid_search_collection\&quot;,​
    \&quot;schema\&quot;: <span class="hljs-variable">$schema</span>,​
    \&quot;indexParams\&quot;: <span class="hljs-variable">$indexParams</span>​
}&quot;</span>​

<button class="copy-code-btn"></button></code></pre>
<h3 id="Insert-data​" class="common-anchor-header">Daten einfügen</h3><p>Fügen Sie die sparse-denses Vektoren in die Sammlung <code translate="no">demo</code> ein.</p>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a> <a href="#curl">cURL</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> <span class="hljs-title class_">MilvusClient</span>​
​
docs = [
    <span class="hljs-string">&quot;Artificial intelligence was founded as an academic discipline in 1956.&quot;</span>,
    <span class="hljs-string">&quot;Alan Turing was the first person to conduct substantial research in AI.&quot;</span>,
    <span class="hljs-string">&quot;Born in Maida Vale, London, Turing was raised in southern England.&quot;</span>,
]

data = [
    {<span class="hljs-string">&quot;id&quot;</span>: <span class="hljs-number">1</span>, <span class="hljs-string">&quot;text&quot;</span>: docs[<span class="hljs-number">0</span>], <span class="hljs-string">&quot;dense&quot;</span>: [<span class="hljs-number">2.7242085933685303</span>, <span class="hljs-number">6.021071434020996</span>, <span class="hljs-number">0.4754035174846649</span>, <span class="hljs-number">9.358858108520508</span>, <span class="hljs-number">5.173221111297607</span>]},
    {<span class="hljs-string">&quot;id&quot;</span>: <span class="hljs-number">2</span>, <span class="hljs-string">&quot;text&quot;</span>: docs[<span class="hljs-number">1</span>], <span class="hljs-string">&quot;dense&quot;</span>: [<span class="hljs-number">8.584294319152832</span>, <span class="hljs-number">2.7640628814697266</span>, <span class="hljs-number">9.558855056762695</span>, <span class="hljs-number">2.584272861480713</span>, <span class="hljs-number">4.705013275146484</span>]},
    {<span class="hljs-string">&quot;id&quot;</span>: <span class="hljs-number">3</span>, <span class="hljs-string">&quot;text&quot;</span>: docs[<span class="hljs-number">2</span>], <span class="hljs-string">&quot;dense&quot;</span>: [<span class="hljs-number">2.5525057315826416</span>, <span class="hljs-number">3.8815805912017822</span>, <span class="hljs-number">9.343480110168457</span>, <span class="hljs-number">7.888997554779053</span>, <span class="hljs-number">4.500918388366699</span>]},
]
​
res = client.<span class="hljs-title function_">insert</span>(​
    collection_name=<span class="hljs-string">&quot;hybrid_search_collection&quot;</span>,​
    data=data​
)​
​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> com.google.gson.Gson;​
<span class="hljs-keyword">import</span> com.google.gson.JsonObject;​
<span class="hljs-keyword">import</span> io.milvus.v2.service.vector.request.InsertReq;​
​
<span class="hljs-type">Gson</span> <span class="hljs-variable">gson</span> <span class="hljs-operator">=</span> <span class="hljs-keyword">new</span> <span class="hljs-title class_">Gson</span>();​
<span class="hljs-type">float</span>[] dense1 = {<span class="hljs-number">2.7242086f</span>, <span class="hljs-number">6.0210714f</span>, <span class="hljs-number">0.47540352f</span>, <span class="hljs-number">9.3588581f</span>, <span class="hljs-number">5.1732211f</span>};
<span class="hljs-type">float</span>[] dense2 = {<span class="hljs-number">8.5842943f</span>, <span class="hljs-number">2.7640628f</span>, <span class="hljs-number">9.5588550f</span>, <span class="hljs-number">2.5842728f</span>, <span class="hljs-number">4.7050133f</span>};
<span class="hljs-type">float</span>[] dense3 = {<span class="hljs-number">2.5525057f</span>, <span class="hljs-number">3.8815806f</span>, <span class="hljs-number">9.3434801f</span>, <span class="hljs-number">7.8889976f</span>, <span class="hljs-number">4.5009184f</span>};
String[] docs = {
            <span class="hljs-string">&quot;Artificial intelligence was founded as an academic discipline in 1956.&quot;</span>,
            <span class="hljs-string">&quot;Alan Turing was the first person to conduct substantial research in AI.&quot;</span>,
            <span class="hljs-string">&quot;Born in Maida Vale, London, Turing was raised in southern England.&quot;</span>
};
<span class="hljs-type">JsonObject</span> <span class="hljs-variable">row1</span> <span class="hljs-operator">=</span> <span class="hljs-keyword">new</span> <span class="hljs-title class_">JsonObject</span>();
row1.addProperty(<span class="hljs-string">&quot;id&quot;</span>, <span class="hljs-number">1</span>);
row1.addProperty(<span class="hljs-string">&quot;text&quot;</span>, docs[<span class="hljs-number">0</span>]);
row1.add(<span class="hljs-string">&quot;dense&quot;</span>, gson.toJsonTree(dense1));
​
<span class="hljs-type">JsonObject</span> <span class="hljs-variable">row2</span> <span class="hljs-operator">=</span> <span class="hljs-keyword">new</span> <span class="hljs-title class_">JsonObject</span>();
row2.addProperty(<span class="hljs-string">&quot;id&quot;</span>, <span class="hljs-number">2</span>);
row2.addProperty(<span class="hljs-string">&quot;text&quot;</span>, docs[<span class="hljs-number">1</span>]);
row2.add(<span class="hljs-string">&quot;dense&quot;</span>, gson.toJsonTree(dense2));
​
<span class="hljs-type">JsonObject</span> <span class="hljs-variable">row3</span> <span class="hljs-operator">=</span> <span class="hljs-keyword">new</span> <span class="hljs-title class_">JsonObject</span>();
row3.addProperty(<span class="hljs-string">&quot;id&quot;</span>, <span class="hljs-number">3</span>);
row3.addProperty(<span class="hljs-string">&quot;text&quot;</span>, docs[<span class="hljs-number">2</span>]);
row3.add(<span class="hljs-string">&quot;dense&quot;</span>, gson.toJsonTree(dense3));
​
List&lt;JsonObject&gt; data = Arrays.asList(row1, row2, row3);​
<span class="hljs-type">InsertReq</span> <span class="hljs-variable">insertReq</span> <span class="hljs-operator">=</span> InsertReq.builder()​
        .collectionName(<span class="hljs-string">&quot;hybrid_search_collection&quot;</span>)​
        .data(data)​
        .build();​
​
<span class="hljs-type">InsertResp</span> <span class="hljs-variable">insertResp</span> <span class="hljs-operator">=</span> client.insert(insertReq);​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-keyword">const</span> { <span class="hljs-title class_">MilvusClient</span>, <span class="hljs-title class_">DataType</span> } = <span class="hljs-built_in">require</span>(<span class="hljs-string">&quot;@zilliz/milvus2-sdk-node&quot;</span>)​
​
<span class="hljs-keyword">const</span> docs = [
    <span class="hljs-string">&quot;Artificial intelligence was founded as an academic discipline in 1956.&quot;</span>,
    <span class="hljs-string">&quot;Alan Turing was the first person to conduct substantial research in AI.&quot;</span>,
    <span class="hljs-string">&quot;Born in Maida Vale, London, Turing was raised in southern England.&quot;</span>
];

<span class="hljs-keyword">const</span> data = [
    {
        <span class="hljs-attr">id</span>: <span class="hljs-number">1</span>,
        <span class="hljs-attr">text</span>: docs[<span class="hljs-number">0</span>],
        <span class="hljs-attr">dense</span>: [<span class="hljs-number">2.7242085933685303</span>, <span class="hljs-number">6.021071434020996</span>, <span class="hljs-number">0.4754035174846649</span>, <span class="hljs-number">9.358858108520508</span>, <span class="hljs-number">5.173221111297607</span>]
    },
    {
        <span class="hljs-attr">id</span>: <span class="hljs-number">2</span>,
        <span class="hljs-attr">text</span>: docs[<span class="hljs-number">1</span>],
        <span class="hljs-attr">dense</span>: [<span class="hljs-number">8.584294319152832</span>, <span class="hljs-number">2.7640628814697266</span>, <span class="hljs-number">9.558855056762695</span>, <span class="hljs-number">2.584272861480713</span>, <span class="hljs-number">4.705013275146484</span>]
    },
    {
        <span class="hljs-attr">id</span>: <span class="hljs-number">3</span>,
        <span class="hljs-attr">text</span>: docs[<span class="hljs-number">2</span>],
        <span class="hljs-attr">dense</span>: [<span class="hljs-number">2.5525057315826416</span>, <span class="hljs-number">3.8815805912017822</span>, <span class="hljs-number">9.343480110168457</span>, <span class="hljs-number">7.888997554779053</span>, <span class="hljs-number">4.500918388366699</span>]
    }
];
​
<span class="hljs-keyword">var</span> res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">insert</span>({​
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;hybrid_search_collection&quot;</span>,​
    <span class="hljs-attr">data</span>: data,​
})​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-curl">curl --request POST \​
--url <span class="hljs-string">&quot;<span class="hljs-variable">${CLUSTER_ENDPOINT}</span>/v2/vectordb/entities/insert&quot;</span> \​
--header <span class="hljs-string">&quot;Authorization: Bearer <span class="hljs-variable">${TOKEN}</span>&quot;</span> \​
--header <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \​
-d <span class="hljs-string">&#x27;{​
    &quot;data&quot;: [
            {
                &quot;id&quot;: 1,
                &quot;text&quot;: &quot;Artificial intelligence was founded as an academic discipline in 1956.&quot;,
                &quot;dense&quot;: [2.7242085933685303, 6.021071434020996, 0.4754035174846649, 9.358858108520508, 5.173221111297607]
            },
            {
                &quot;id&quot;: 2,
                &quot;text&quot;: &quot;Alan Turing was the first person to conduct substantial research in AI.&quot;,
                &quot;dense&quot;: [8.584294319152832, 2.7640628814697266, 9.558855056762695, 2.584272861480713, 4.705013275146484]
            },
            {
                &quot;id&quot;: 3,
                &quot;text&quot;: &quot;Born in Maida Vale, London, Turing was raised in southern England.&quot;,
                &quot;dense&quot;: [2.5525057315826416, 3.8815805912017822, 9.343480110168457, 7.888997554779053, 4.500918388366699]
            }
        ],​
    &quot;collectionName&quot;: &quot;hybrid_search_collection&quot;​
}&#x27;</span>​

<button class="copy-code-btn"></button></code></pre>
<h3 id="Create-multiple-AnnSearchRequest-instances​" class="common-anchor-header">Mehrere AnnSearchRequest-Instanzen erstellen</h3><p>Die hybride Suche wird durch die Erstellung mehrerer <code translate="no">AnnSearchRequest</code> in der Funktion <code translate="no">hybrid_search()</code> implementiert, wobei jede <code translate="no">AnnSearchRequest</code> eine grundlegende ANN-Suchanfrage für ein bestimmtes Vektorfeld darstellt. Daher muss vor der Durchführung einer Hybrid Search für jedes Vektorfeld eine <code translate="no">AnnSearchRequest</code> erstellt werden.</p>
<div class="alert note">
<p>Bei der hybriden Suche unterstützt jedes <code translate="no">AnnSearchRequest</code> nur einen Abfragevektor.</p>
</div>
<p>Angenommen, der Abfragetext "Wer begann mit der KI-Forschung?" wurde bereits in sparse und dense Vektoren umgewandelt. Auf dieser Grundlage werden zwei <code translate="no">AnnSearchRequest</code> Suchanfragen für die Vektorfelder <code translate="no">sparse</code> und <code translate="no">dense</code> erstellt, wie im folgenden Beispiel gezeigt.</p>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a> <a href="#curl">cURL</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> <span class="hljs-title class_">AnnSearchRequest</span>​
​
search_param_1 = {
    <span class="hljs-string">&quot;data&quot;</span>: [[<span class="hljs-number">0.7425515055656433</span>, <span class="hljs-number">7.774101734161377</span>, <span class="hljs-number">0.7397570610046387</span>, <span class="hljs-number">2.429982900619507</span>, <span class="hljs-number">3.8253049850463867</span>]],
    <span class="hljs-string">&quot;anns_field&quot;</span>: <span class="hljs-string">&quot;dense&quot;</span>,
    <span class="hljs-string">&quot;param&quot;</span>: {
        <span class="hljs-string">&quot;metric_type&quot;</span>: <span class="hljs-string">&quot;IP&quot;</span>,
        <span class="hljs-string">&quot;params&quot;</span>: {<span class="hljs-string">&quot;nprobe&quot;</span>: <span class="hljs-number">10</span>}
    },
    <span class="hljs-string">&quot;limit&quot;</span>: <span class="hljs-number">2</span>
}
request_1 = <span class="hljs-title class_">AnnSearchRequest</span>(**search_param_1)

search_param_2 = {
    <span class="hljs-string">&quot;data&quot;</span>: [<span class="hljs-string">&#x27;Who started AI research&#x27;</span>],
    <span class="hljs-string">&quot;anns_field&quot;</span>: <span class="hljs-string">&quot;sparse&quot;</span>,
    <span class="hljs-string">&quot;param&quot;</span>: {
        <span class="hljs-string">&quot;metric_type&quot;</span>: <span class="hljs-string">&quot;BM25&quot;</span>,
    },
    <span class="hljs-string">&quot;limit&quot;</span>: <span class="hljs-number">2</span>
}
request_2 = <span class="hljs-title class_">AnnSearchRequest</span>(**search_param_2)

reqs = [request_1, request_2]
​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.milvus.v2.service.vector.request.AnnSearchReq;
<span class="hljs-keyword">import</span> io.milvus.v2.service.vector.request.data.BaseVector;
<span class="hljs-keyword">import</span> io.milvus.v2.service.vector.request.data.FloatVec;
<span class="hljs-keyword">import</span> io.milvus.v2.service.vector.request.data.TextVec;
<span class="hljs-keyword">import</span> io.milvus.v2.service.index.IndexParam;

<span class="hljs-keyword">import</span> java.util.*;

<span class="hljs-keyword">public</span> <span class="hljs-keyword">class</span> <span class="hljs-title class_">MilvusSearchRequest</span> {
    <span class="hljs-keyword">public</span> <span class="hljs-keyword">static</span> <span class="hljs-keyword">void</span> <span class="hljs-title function_">main</span><span class="hljs-params">(String[] args)</span> {
        <span class="hljs-type">float</span>[] denseQueryVector = {
                <span class="hljs-number">0.7425515f</span>, <span class="hljs-number">7.7741017f</span>, <span class="hljs-number">0.73975706f</span>, <span class="hljs-number">2.4299829f</span>, <span class="hljs-number">3.825305f</span>
        };

        <span class="hljs-type">String</span> <span class="hljs-variable">sparseQueryText</span> <span class="hljs-operator">=</span> <span class="hljs-string">&quot;Who started AI research&quot;</span>;

        List&lt;BaseVector&gt; queryDenseVectors = Collections.singletonList(<span class="hljs-keyword">new</span> <span class="hljs-title class_">FloatVec</span>(denseQueryVector));

        List&lt;BaseVector&gt; querySparseVectors = Collections.singletonList(<span class="hljs-keyword">new</span> <span class="hljs-title class_">TextVec</span>(sparseQueryText));

        List&lt;AnnSearchReq&gt; searchRequests = <span class="hljs-keyword">new</span> <span class="hljs-title class_">ArrayList</span>&lt;&gt;();

        searchRequests.add(AnnSearchReq.builder()
                .vectorFieldName(<span class="hljs-string">&quot;dense&quot;</span>)  <span class="hljs-comment">// Field Name</span>
                .vectors(queryDenseVectors) <span class="hljs-comment">// Query Vector</span>
                .metricType(IndexParam.MetricType.IP) <span class="hljs-comment">// Inner Product Metric</span>
                .params(<span class="hljs-string">&quot;{\&quot;nprobe\&quot;: 10}&quot;</span>) <span class="hljs-comment">// Search Params</span>
                .topK(<span class="hljs-number">2</span>) <span class="hljs-comment">// Limit results to top 2</span>
                .build());

        searchRequests.add(AnnSearchReq.builder()
                .vectorFieldName(<span class="hljs-string">&quot;sparse&quot;</span>) <span class="hljs-comment">// Field Name</span>
                .vectors(querySparseVectors) <span class="hljs-comment">// Query Text Vector</span>
                .metricType(IndexParam.MetricType.BM25) <span class="hljs-comment">// BM25 Metric for sparse</span>
                .params(<span class="hljs-string">&quot;{}&quot;</span>) <span class="hljs-comment">// No additional parameters for BM25</span>
                .topK(<span class="hljs-number">2</span>) <span class="hljs-comment">// Limit results to top 2</span>
                .build());

        System.out.println(<span class="hljs-string">&quot;Generated Search Requests:&quot;</span>);
        searchRequests.forEach(System.out::println);
    }
}


<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-keyword">const</span> search_param_1 = {
    <span class="hljs-string">&quot;data&quot;</span>: [[<span class="hljs-number">0.7425515055656433</span>, <span class="hljs-number">7.774101734161377</span>, <span class="hljs-number">0.7397570610046387</span>, <span class="hljs-number">2.429982900619507</span>, <span class="hljs-number">3.8253049850463867</span>]], 
    <span class="hljs-string">&quot;anns_field&quot;</span>: <span class="hljs-string">&quot;dense&quot;</span>,
    <span class="hljs-string">&quot;param&quot;</span>: {
        <span class="hljs-string">&quot;metric_type&quot;</span>: <span class="hljs-string">&quot;IP&quot;</span>,
        <span class="hljs-string">&quot;params&quot;</span>: { <span class="hljs-string">&quot;nprobe&quot;</span>: <span class="hljs-number">10</span> } 
    },
    <span class="hljs-string">&quot;limit&quot;</span>: <span class="hljs-number">2</span>
};

<span class="hljs-keyword">const</span> search_param_2 = {
    <span class="hljs-string">&quot;data&quot;</span>: [<span class="hljs-string">&quot;Who started AI research&quot;</span>], 
    <span class="hljs-string">&quot;anns_field&quot;</span>: <span class="hljs-string">&quot;sparse&quot;</span>,
    <span class="hljs-string">&quot;param&quot;</span>: {
        <span class="hljs-string">&quot;metric_type&quot;</span>: <span class="hljs-string">&quot;BM25&quot;</span>,
        <span class="hljs-string">&quot;params&quot;</span>: {} <span class="hljs-comment">// BM25 does not require extra parameters</span>
    },
    <span class="hljs-string">&quot;limit&quot;</span>: <span class="hljs-number">2</span>
};

<span class="hljs-comment">// Combine both search parameters into a single request list</span>
<span class="hljs-keyword">const</span> reqs = [search_param_1, search_param_2];

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-curl"><span class="hljs-built_in">export</span> req=<span class="hljs-string">&#x27;[
    {
        &quot;data&quot;: [[0.7425515055656433, 7.774101734161377, 0.7397570610046387, 2.429982900619507, 3.8253049850463867]], 
        &quot;anns_field&quot;: &quot;dense&quot;,
        &quot;param&quot;: {
            &quot;metric_type&quot;: &quot;IP&quot;,
            &quot;params&quot;: {
                &quot;nprobe&quot;: 10
            }
        },
        &quot;limit&quot;: 2
    },
    {
        &quot;data&quot;: [&quot;Who started AI research&quot;],
        &quot;anns_field&quot;: &quot;sparse&quot;,
        &quot;param&quot;: {
            &quot;metric_type&quot;: &quot;BM25&quot;,
            &quot;params&quot;: {}
        },
        &quot;limit&quot;: 2
    }
]&#x27;</span>

curl -X POST <span class="hljs-string">&quot;http://your-milvus-server-address/v1/vector/search&quot;</span> \
     -H <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \
     -d <span class="hljs-string">&quot;<span class="hljs-variable">$req</span>&quot;</span>


<button class="copy-code-btn"></button></code></pre>
<p>Da der Parameter <code translate="no">limit</code> auf 2 gesetzt ist, liefert jede <code translate="no">AnnSearchRequest</code> 2 Suchergebnisse. In diesem Beispiel werden 2 <code translate="no">AnnSearchRequest</code> erstellt, daher werden insgesamt 4 Suchergebnisse zurückgegeben.</p>
<h3 id="Configure-a-reranking-strategy​" class="common-anchor-header">Konfigurieren Sie eine Ranglistenstrategie</h3><p>Um die beiden Gruppen von ANN-Suchergebnissen zusammenzuführen und neu zu ordnen, ist es notwendig, eine geeignete Rangordnungsstrategie zu wählen. Zilliz unterstützt zwei Arten von Reranking-Strategien: <strong>WeightedRanker</strong> und <strong>RRFRanker</strong>. Bei der Wahl der Reranking-Strategie muss unter anderem berücksichtigt werden, ob eine oder mehrere ANN-Basissuchen auf den Vektorfeldern einen Schwerpunkt bilden.</p>
<ul>
<li><p><strong>WeightedRanker</strong>: Diese Strategie wird empfohlen, wenn die Ergebnisse ein bestimmtes Vektorfeld betonen sollen. Mit dem WeightedRanker können Sie bestimmten Vektorfeldern eine höhere Gewichtung zuweisen und sie damit stärker hervorheben. Bei einer multimodalen Suche könnten beispielsweise Textbeschreibungen eines Bildes als wichtiger angesehen werden als die Farben dieses Bildes.</p></li>
<li><p><strong>RRFRanker (Reciprocal Rank Fusion Ranker)</strong>: Diese Strategie wird empfohlen, wenn es keine besondere Gewichtung gibt. Der RRF kann die Bedeutung der einzelnen Vektorfelder effektiv ausgleichen.</p></li>
</ul>
<p>Weitere Einzelheiten zu den Mechanismen dieser beiden Reranking-Strategien finden Sie unter <a href="/docs/de/reranking.md">Reranking</a>.</p>
<p>Die folgenden zwei Beispiele zeigen, wie die Reranking-Strategien WeightedRanker und RRFRanker verwendet werden können.</p>
<ol>
<li><p><strong>Beispiel 1: Verwendung von WeightedRanker</strong></p>
<p>Wenn Sie die WeightedRanker-Strategie verwenden, müssen Sie Gewichtungswerte in die Funktion <code translate="no">WeightedRanker</code> eingeben. Die Anzahl der ANN-Basissuchen in einer Hybrid Search entspricht der Anzahl der einzugebenden Werte. Die Eingabewerte sollten im Bereich [0,1] liegen, wobei Werte, die näher an 1 liegen, eine größere Wichtigkeit anzeigen.</p>
<p><div class="multipleCode">
<a href="#python">Python </a><a href="#java">Java</a><a href="#javascript">Node.js</a><a href="#curl">cURL</a></div></p>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> <span class="hljs-title class_">WeightedRanker</span>​
​
ranker = <span class="hljs-title class_">WeightedRanker</span>(<span class="hljs-number">0.8</span>, <span class="hljs-number">0.3</span>) ​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.milvus.v2.service.vector.request.ranker.BaseRanker;​
<span class="hljs-keyword">import</span> io.milvus.v2.service.vector.request.ranker.WeightedRanker;​
​
<span class="hljs-type">BaseRanker</span> <span class="hljs-variable">reranker</span> <span class="hljs-operator">=</span> <span class="hljs-keyword">new</span> <span class="hljs-title class_">WeightedRanker</span>(Arrays.asList(<span class="hljs-number">0.8f</span>, <span class="hljs-number">0.3f</span>));​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-keyword">import</span> { <span class="hljs-title class_">MilvusClient</span>, <span class="hljs-title class_">DataType</span> } <span class="hljs-keyword">from</span> <span class="hljs-string">&quot;@zilliz/milvus2-sdk-node&quot;</span>;​
​
<span class="hljs-keyword">const</span> rerank = <span class="hljs-title class_">WeightedRanker</span>(<span class="hljs-number">0.8</span>, <span class="hljs-number">0.3</span>);​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-curl"><span class="hljs-built_in">export</span> rerank=<span class="hljs-string">&#x27;{​
        &quot;strategy&quot;: &quot;ws&quot;,​
        &quot;params&quot;: {&quot;weights&quot;: [0.8,0.3]}​
    }&#x27;</span>​

<button class="copy-code-btn"></button></code></pre></li>
<li><p><strong>Beispiel 2: Verwendung von RRFRanker</strong></p>
<p>Wenn Sie die RRFRanker-Strategie verwenden, müssen Sie den Parameterwert <code translate="no">k</code> in den RRFRanker eingeben. Der Standardwert von <code translate="no">k</code> ist 60. Mit diesem Parameter wird festgelegt, wie die Ränge aus verschiedenen ANN-Suchen kombiniert werden, um die Wichtigkeit über alle Suchen hinweg auszugleichen und zu mischen.</p>
<p><div class="multipleCode">
<a href="#python">Python </a><a href="#java">Java</a><a href="#javascript">Node.js</a><a href="#curl">cURL</a></div></p>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> <span class="hljs-title class_">RRFRanker</span>​
​
ranker = <span class="hljs-title class_">RRFRanker</span>(<span class="hljs-number">100</span>)​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.milvus.v2.service.vector.request.ranker.BaseRanker;​
<span class="hljs-keyword">import</span> io.milvus.v2.service.vector.request.ranker.RRFRanker;​
​
<span class="hljs-type">BaseRanker</span> <span class="hljs-variable">reranker</span> <span class="hljs-operator">=</span> <span class="hljs-keyword">new</span> <span class="hljs-title class_">RRFRanker</span>(<span class="hljs-number">100</span>);​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-keyword">import</span> { <span class="hljs-title class_">MilvusClient</span>, <span class="hljs-title class_">DataType</span> } <span class="hljs-keyword">from</span> <span class="hljs-string">&quot;@zilliz/milvus2-sdk-node&quot;</span>;​
​
<span class="hljs-keyword">const</span> rerank = <span class="hljs-title class_">RRFRanker</span>(<span class="hljs-string">&quot;100&quot;</span>);​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-curl"><span class="hljs-built_in">export</span> rerank=<span class="hljs-string">&#x27;{​
        &quot;strategy&quot;: &quot;rrf&quot;,​
        &quot;params&quot;: { &quot;k&quot;: 100}​
    }&#x27;</span>​

<button class="copy-code-btn"></button></code></pre></li>
</ol>
<h3 id="Perform-a-Hybrid-Search​" class="common-anchor-header">Durchführen einer hybriden Suche</h3><p>Bevor eine hybride Suche durchgeführt werden kann, muss die Sammlung in den Speicher geladen werden. Wenn die Vektorfelder in der Sammlung keinen Index haben oder nicht geladen sind, tritt beim Aufruf der Methode Hybrid Search ein Fehler auf. </p>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a> <a href="#curl">cURL</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> MilvusClient​
​
res = client.hybrid_search(​
    collection_name=<span class="hljs-string">&quot;hybrid_search_collection&quot;</span>,​
    reqs=reqs,​
    ranker=ranker,​
    limit=<span class="hljs-number">2</span>​
)​
<span class="hljs-keyword">for</span> hits <span class="hljs-keyword">in</span> res:​
    <span class="hljs-built_in">print</span>(<span class="hljs-string">&quot;TopK results:&quot;</span>)​
    <span class="hljs-keyword">for</span> hit <span class="hljs-keyword">in</span> hits:​
        <span class="hljs-built_in">print</span>(hit)​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.milvus.v2.common.ConsistencyLevel;​
<span class="hljs-keyword">import</span> io.milvus.v2.service.vector.request.HybridSearchReq;​
<span class="hljs-keyword">import</span> io.milvus.v2.service.vector.response.SearchResp;​
​
<span class="hljs-type">HybridSearchReq</span> <span class="hljs-variable">hybridSearchReq</span> <span class="hljs-operator">=</span> HybridSearchReq.builder()​
        .collectionName(<span class="hljs-string">&quot;hybrid_search_collection&quot;</span>)​
        .searchRequests(searchRequests)​
        .ranker(reranker)​
        .topK(<span class="hljs-number">2</span>)​
        .consistencyLevel(ConsistencyLevel.BOUNDED)​
        .build();​
​
<span class="hljs-type">SearchResp</span> <span class="hljs-variable">searchResp</span> <span class="hljs-operator">=</span> client.hybridSearch(hybridSearchReq);​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-keyword">const</span> { <span class="hljs-title class_">MilvusClient</span>, <span class="hljs-title class_">DataType</span> } = <span class="hljs-built_in">require</span>(<span class="hljs-string">&quot;@zilliz/milvus2-sdk-node&quot;</span>)​
​
res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">loadCollection</span>({​
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;hybrid_search_collection&quot;</span>​
})​
​
<span class="hljs-keyword">import</span> { <span class="hljs-title class_">MilvusClient</span>, <span class="hljs-title class_">RRFRanker</span>, <span class="hljs-title class_">WeightedRanker</span> } <span class="hljs-keyword">from</span> <span class="hljs-string">&#x27;@zilliz/milvus2-sdk-node&#x27;</span>;​
​
<span class="hljs-keyword">const</span> search = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">search</span>({​
  <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;hybrid_search_collection&quot;</span>,​
  <span class="hljs-attr">data</span>: [search_param_1, search_param_2],​
  <span class="hljs-attr">limit</span>: <span class="hljs-number">2</span>,​
  <span class="hljs-attr">rerank</span>: <span class="hljs-title class_">RRFRanker</span>(<span class="hljs-number">100</span>)​
});​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-curl">curl --request POST \​
--url <span class="hljs-string">&quot;<span class="hljs-variable">${CLUSTER_ENDPOINT}</span>/v2/vectordb/entities/advanced_search&quot;</span> \​
--header <span class="hljs-string">&quot;Authorization: Bearer <span class="hljs-variable">${TOKEN}</span>&quot;</span> \​
--header <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \​
-d <span class="hljs-string">&quot;{​
    \&quot;collectionName\&quot;: \&quot;hybrid_search_collection\&quot;,​
    \&quot;search\&quot;: <span class="hljs-variable">${req}</span>,​
    \&quot;rerank\&quot;: {​
        \&quot;strategy\&quot;:\&quot;rrf\&quot;,​
        \&quot;params\&quot;: {​
            \&quot;k\&quot;: 10​
        }​
    },​
    \&quot;limit\&quot;: 3,​
    \&quot;outputFields\&quot;: [​
        \&quot;user_id\&quot;,​
        \&quot;word_count\&quot;,​
        \&quot;book_describe\&quot;​
    ]​
}&quot;</span>​

<button class="copy-code-btn"></button></code></pre>
<p>Es folgt die Ausgabe.</p>
<pre><code translate="no" class="language-json">[<span class="hljs-string">&quot;[&#x27;id: 844, distance: 0.006047376897186041, entity: {}&#x27;, &#x27;id: 876, distance: 0.006422005593776703, entity: {}&#x27;]&quot;</span>]​

<button class="copy-code-btn"></button></code></pre>
<p>Da <code translate="no">limit=2</code> in der Hybrid Search angegeben ist, wird Zilliz die vier Suchergebnisse aus Schritt 3 neu ordnen und schließlich nur die zwei ähnlichsten Suchergebnisse zurückgeben. </p>
