---
id: sparse_vector.md
title: スパース・ベクトル
summary: >-
  スパース・ベクトルは、情報検索や自然言語処理におけるデータ表現の重要な手法である。密なベクトルはその優れた意味理解能力で人気があるが、キーワードやフレーズの正確なマッチングを必要とするアプリケーションに関しては、疎なベクトルの方がより正確な結果を提供することが多い。
---
<h1 id="Sparse-Vector​" class="common-anchor-header">スパース・ベクトル<button data-href="#Sparse-Vector​" class="anchor-icon" translate="no">
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
    </button></h1><p>スパース・ベクトルは、情報検索や自然言語処理におけるデータ表現の重要な手法である。密なベクトルはその優れた意味理解能力で人気がありますが、キーワードやフレーズの正確なマッチングを必要とするアプリケーションに関しては、疎なベクトルの方がより正確な結果を提供することがよくあります。</p>
<h2 id="Overview​" class="common-anchor-header">概要<button data-href="#Overview​" class="anchor-icon" translate="no">
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
    </button></h2><p>スパース・ベクトルは高次元ベクトルの特殊な表現で、ほとんどの要素が0であり、0でない値を持つ次元はわずかです。この特性により、スパースベクトルは大規模で高次元の疎なデータを扱うのに特に効果的です。一般的なアプリケーションは以下の通り。</p>
<ul>
<li><p><strong>テキスト分析：</strong>各次元が単語に対応し、文書に登場する単語だけがゼロ以外の値を持つ。</p></li>
<li><p><strong>推薦システム：</strong>ユーザーとアイテムの相互作用行列。各次元は、特定のアイテムに対するユーザーの評価を表し、ほとんどのユーザーは少数のアイテムとしか相互作用しない。</p></li>
<li><p><strong>画像処理：</strong>局所特徴表現：画像の重要なポイントのみに焦点を当て、高次元の疎なベクトルを生成する。</p></li>
</ul>
<p>下図に示すように、密なベクトルは通常、各位置が値を持つ連続的な配列として表現される（例：<code translate="no">[0.3, 0.8, 0.2, 0.3, 0.1]</code> ）。対照的に、スパース・ベクトルは非ゼロ要素とそのインデックスのみを格納し、しばしばキーと値のペアとして表現されます（例：<code translate="no">[{2: 0.2}, ..., {9997: 0.5}, {9999: 0.7}]</code> ）。この表現は、特に非常に高次元のデータ（例えば10,000次元）を扱う場合に、記憶領域を大幅に削減し、計算効率を向上させます。</p>
<p>
  
   <span class="img-wrapper"> <img translate="no" src="/docs/v2.5.x/assets/sparse-vector.png" alt="Spare vector representation" class="doc-image" id="spare-vector-representation" />
   </span> <span class="img-wrapper"> <span>疎ベクトル表現</span> </span></p>
<p>スパースベクトルは、テキスト処理における<a href="https://en.wikipedia.org/wiki/Tf%E2%80%93idf">TF-IDF</a>（項頻度-逆文書頻度）や<a href="https://en.wikipedia.org/wiki/Okapi_BM25">BM25など</a>、様々な手法を用いて生成することができます。さらに、Milvusはスパースベクトルの生成と処理を支援する便利なメソッドを提供しています。詳細は<a href="/docs/ja/embeddings.md">埋め込みを</a>ご参照ください。</p>
<p>Milvusはテキストデータの全文検索機能も提供しており、スパースベクトルを生成するために外部の埋め込みモデルを使用することなく、生のテキストデータに対して直接ベクトル検索を行うことができます。詳細は<a href="/docs/ja/full-text-search.md">全文検索を</a>ご参照ください。</p>
<p>ベクトル化されたデータはMilvusに保存され、管理やベクトル検索に利用することができます。下図は基本的なプロセスを示しています。</p>
<p>
  
   <span class="img-wrapper"> <img translate="no" src="/docs/v2.5.x/assets/use-sparse-vector.png" alt="Use sparse vector in Milvus" class="doc-image" id="use-sparse-vector-in-milvus" />
   </span> <span class="img-wrapper"> <span>Milvusでスパースベクトルを使用する。</span> </span></p>
<div class="alert note">
<p>Milvusはスパースベクトル以外にも、デンスベクトルやバイナリベクトルにも対応しています。密なベクトルは深い意味的関係を把握するのに理想的であり、バイナリベクトルは迅速な類似性比較やコンテンツの重複排除などのシナリオに優れています。詳細については、<a href="/docs/ja/dense-vector.md">密なベクトルと</a> <a href="/docs/ja/binary-vector.md">バイナリベクトルを</a>参照してください。</p>
</div>
<h2 id="Use-sparse-vectors-in-Milvus​" class="common-anchor-header">Milvusでスパースベクトルを使う<button data-href="#Use-sparse-vectors-in-Milvus​" class="anchor-icon" translate="no">
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
    </button></h2><p>Milvusでは、以下のいずれかの形式でスパースベクトルを表現することができます。</p>
<ul>
<li><p>疎行列 (<code translate="no">scipy.sparse</code> クラスを使用)</p>
<p><div class="multipleCode">
<a href="#python">Python </a><a href="#java">Java</a><a href="#javascript">Node.js</a><a href="#curl">cURL</a></div></p>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> scipy.sparse <span class="hljs-keyword">import</span> csr_matrix​
​
<span class="hljs-comment"># Create a sparse matrix​</span>
row = [<span class="hljs-number">0</span>, <span class="hljs-number">0</span>, <span class="hljs-number">1</span>, <span class="hljs-number">2</span>, <span class="hljs-number">2</span>, <span class="hljs-number">2</span>]​
col = [<span class="hljs-number">0</span>, <span class="hljs-number">2</span>, <span class="hljs-number">2</span>, <span class="hljs-number">0</span>, <span class="hljs-number">1</span>, <span class="hljs-number">2</span>]​
data = [<span class="hljs-number">1</span>, <span class="hljs-number">2</span>, <span class="hljs-number">3</span>, <span class="hljs-number">4</span>, <span class="hljs-number">5</span>, <span class="hljs-number">6</span>]​
sparse_matrix = csr_matrix((data, (row, col)), shape=(<span class="hljs-number">3</span>, <span class="hljs-number">3</span>))​
​
<span class="hljs-comment"># Represent sparse vector using the sparse matrix​</span>
sparse_vector = sparse_matrix.getrow(<span class="hljs-number">0</span>)​

<button class="copy-code-btn"></button></code></pre></li>
<li><p>辞書のリスト (<code translate="no">{dimension_index: value, ...}</code> としてフォーマット)</p>
<p><div class="multipleCode">
<a href="#python">Python </a><a href="#java">Java</a><a href="#javascript">Node.js</a><a href="#curl">cURL</a></div></p>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># Represent sparse vector using a dictionary​</span>
sparse_vector = [{<span class="hljs-number">1</span>: <span class="hljs-number">0.5</span>, <span class="hljs-number">100</span>: <span class="hljs-number">0.3</span>, <span class="hljs-number">500</span>: <span class="hljs-number">0.8</span>, <span class="hljs-number">1024</span>: <span class="hljs-number">0.2</span>, <span class="hljs-number">5000</span>: <span class="hljs-number">0.6</span>}]​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-title class_">SortedMap</span>&lt;<span class="hljs-title class_">Long</span>, <span class="hljs-title class_">Float</span>&gt; sparseVector = <span class="hljs-keyword">new</span> <span class="hljs-title class_">TreeMap</span>&lt;&gt;();​
sparseVector.<span class="hljs-title function_">put</span>(1L, <span class="hljs-number">0.</span>5f);​
sparseVector.<span class="hljs-title function_">put</span>(100L, <span class="hljs-number">0.</span>3f);​
sparseVector.<span class="hljs-title function_">put</span>(500L, <span class="hljs-number">0.</span>8f);​
sparseVector.<span class="hljs-title function_">put</span>(1024L, <span class="hljs-number">0.</span>2f);​
sparseVector.<span class="hljs-title function_">put</span>(5000L, <span class="hljs-number">0.</span>6f);​

<button class="copy-code-btn"></button></code></pre></li>
<li><p>タプルイテレータのリスト（<code translate="no">[(dimension_index, value)]</code> としてフォーマットされる）</p>
<p><div class="multipleCode">
<a href="#python">Python </a><a href="#java">Java</a><a href="#javascript">Node.js</a><a href="#curl">cURL</a></div></p>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># Represent sparse vector using a list of tuples​</span>
sparse_vector = [[(<span class="hljs-number">1</span>, <span class="hljs-number">0.5</span>), (<span class="hljs-number">100</span>, <span class="hljs-number">0.3</span>), (<span class="hljs-number">500</span>, <span class="hljs-number">0.8</span>), (<span class="hljs-number">1024</span>, <span class="hljs-number">0.2</span>), (<span class="hljs-number">5000</span>, <span class="hljs-number">0.6</span>)]]​

<button class="copy-code-btn"></button></code></pre></li>
</ul>
<h3 id="Add-vector-field​" class="common-anchor-header">ベクトル・フィールドの追加</h3><p>Milvusでスパースベクトルを使用するには、コレクション作成時にスパースベクトルを格納するフィールドを定義します。このプロセスには以下が含まれます。</p>
<ol>
<li><p><code translate="no">datatype</code> をサポートされているスパースベクトルデータ型、<code translate="no">SPARSE_FLOAT_VECTOR</code> に設定します。</p></li>
<li><p>次元を指定する必要はない。</p></li>
</ol>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a> <a href="#curl">cURL</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> MilvusClient, DataType​
​
client = MilvusClient(uri=<span class="hljs-string">&quot;http://localhost:19530&quot;</span>)​
​
client.drop_collection(collection_name=<span class="hljs-string">&quot;my_sparse_collection&quot;</span>)​
​
schema = client.create_schema(​
    auto_id=<span class="hljs-literal">True</span>,​
    enable_dynamic_fields=<span class="hljs-literal">True</span>,​
)​
​
schema.add_field(field_name=<span class="hljs-string">&quot;pk&quot;</span>, datatype=DataType.VARCHAR, is_primary=<span class="hljs-literal">True</span>, max_length=<span class="hljs-number">100</span>)​
schema.add_field(field_name=<span class="hljs-string">&quot;sparse_vector&quot;</span>, datatype=DataType.SPARSE_FLOAT_VECTOR)​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.milvus.v2.client.ConnectConfig;​
<span class="hljs-keyword">import</span> io.milvus.v2.client.MilvusClientV2;​
​
<span class="hljs-keyword">import</span> io.milvus.v2.common.DataType;​
<span class="hljs-keyword">import</span> io.milvus.v2.service.collection.request.AddFieldReq;​
<span class="hljs-keyword">import</span> io.milvus.v2.service.collection.request.CreateCollectionReq;​
​
<span class="hljs-type">MilvusClientV2</span> <span class="hljs-variable">client</span> <span class="hljs-operator">=</span> <span class="hljs-keyword">new</span> <span class="hljs-title class_">MilvusClientV2</span>(ConnectConfig.builder()​
        .uri(<span class="hljs-string">&quot;http://localhost:19530&quot;</span>)​
        .build());​
        ​
CreateCollectionReq.<span class="hljs-type">CollectionSchema</span> <span class="hljs-variable">schema</span> <span class="hljs-operator">=</span> client.createSchema();​
schema.setEnableDynamicField(<span class="hljs-literal">true</span>);​
schema.addField(AddFieldReq.builder()​
        .fieldName(<span class="hljs-string">&quot;pk&quot;</span>)​
        .dataType(DataType.VarChar)​
        .isPrimaryKey(<span class="hljs-literal">true</span>)​
        .autoID(<span class="hljs-literal">true</span>)​
        .maxLength(<span class="hljs-number">100</span>)​
        .build());​
​
schema.addField(AddFieldReq.builder()​
        .fieldName(<span class="hljs-string">&quot;sparse_vector&quot;</span>)​
        .dataType(DataType.SparseFloatVector)​
        .build());​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-keyword">import</span> { <span class="hljs-title class_">DataType</span> } <span class="hljs-keyword">from</span> <span class="hljs-string">&quot;@zilliz/milvus2-sdk-node&quot;</span>;​
​
<span class="hljs-keyword">const</span> schema = [​
  {​
    <span class="hljs-attr">name</span>: <span class="hljs-string">&quot;metadata&quot;</span>,​
    <span class="hljs-attr">data_type</span>: <span class="hljs-title class_">DataType</span>.<span class="hljs-property">JSON</span>,​
  },​
  {​
    <span class="hljs-attr">name</span>: <span class="hljs-string">&quot;pk&quot;</span>,​
    <span class="hljs-attr">data_type</span>: <span class="hljs-title class_">DataType</span>.<span class="hljs-property">Int64</span>,​
    <span class="hljs-attr">is_primary_key</span>: <span class="hljs-literal">true</span>,​
  },​
  {​
    <span class="hljs-attr">name</span>: <span class="hljs-string">&quot;sparse_vector&quot;</span>,​
    <span class="hljs-attr">data_type</span>: <span class="hljs-title class_">DataType</span>.<span class="hljs-property">SparseFloatVector</span>,​
  }​
];​
​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-curl"><span class="hljs-built_in">export</span> primaryField=<span class="hljs-string">&#x27;{​
    &quot;fieldName&quot;: &quot;pk&quot;,​
    &quot;dataType&quot;: &quot;VarChar&quot;,​
    &quot;isPrimary&quot;: true,​
    &quot;elementTypeParams&quot;: {​
        &quot;max_length&quot;: 100​
    }​
}&#x27;</span>​
​
<span class="hljs-built_in">export</span> vectorField=<span class="hljs-string">&#x27;{​
    &quot;fieldName&quot;: &quot;sparse_vector&quot;,​
    &quot;dataType&quot;: &quot;SparseFloatVector&quot;​
}&#x27;</span>​
​
<span class="hljs-built_in">export</span> schema=<span class="hljs-string">&quot;{​
    \&quot;autoID\&quot;: true,​
    \&quot;fields\&quot;: [​
        <span class="hljs-variable">$primaryField</span>,​
        <span class="hljs-variable">$vectorField</span>​
    ]​
}&quot;</span>​

<button class="copy-code-btn"></button></code></pre>
<p>この例では、スパース・ベクトルを格納するために、<code translate="no">sparse_vector</code> というベクトル・ フィールドが追加されている。このフィールドのデータ型は<code translate="no">SPARSE_FLOAT_VECTOR</code> です。</p>
<h3 id="Set-index-params-for-vector-field​" class="common-anchor-header">ベクトル・フィールドにインデックス・パラメータを設定する</h3><p>スパース・ベクトルのインデックスを作成するプロセスは、<a href="/docs/ja/dense-vector.md">密な</a>ベクトルの場合と似ていますが、指定するインデックス・タイプ (<code translate="no">index_type</code>)、距離メトリック (<code translate="no">metric_type</code>)、インデックス・パラメータ (<code translate="no">params</code>)が異なります。</p>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a> <a href="#curl">cURL</a></div>
<pre><code translate="no" class="language-python">index_params = client.prepare_index_params()

index_params.add_index(
    field_name=<span class="hljs-string">&quot;sparse_vector&quot;</span>,
    index_name=<span class="hljs-string">&quot;sparse_inverted_index&quot;</span>,
    index_type=<span class="hljs-string">&quot;SPARSE_INVERTED_INDEX&quot;</span>,
    metric_type=<span class="hljs-string">&quot;IP&quot;</span>,
    params={<span class="hljs-string">&quot;inverted_index_algo&quot;</span>: <span class="hljs-string">&quot;DAAT_MAXSCORE&quot;</span>}, <span class="hljs-comment"># Algorithm used for building and querying the index</span>
)

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.<span class="hljs-property">milvus</span>.<span class="hljs-property">v2</span>.<span class="hljs-property">common</span>.<span class="hljs-property">IndexParam</span>;
<span class="hljs-keyword">import</span> java.<span class="hljs-property">util</span>.*;

<span class="hljs-title class_">List</span>&lt;<span class="hljs-title class_">IndexParam</span>&gt; indexes = <span class="hljs-keyword">new</span> <span class="hljs-title class_">ArrayList</span>&lt;&gt;();
<span class="hljs-title class_">Map</span>&lt;<span class="hljs-title class_">String</span>,<span class="hljs-title class_">Object</span>&gt; extraParams = <span class="hljs-keyword">new</span> <span class="hljs-title class_">HashMap</span>&lt;&gt;();
extraParams.<span class="hljs-title function_">put</span>(<span class="hljs-string">&quot;inverted_index_algo&quot;</span>: <span class="hljs-string">&quot;DAAT_MAXSCORE&quot;</span>); <span class="hljs-comment">// Algorithm used for building and querying the index</span>
indexes.<span class="hljs-title function_">add</span>(<span class="hljs-title class_">IndexParam</span>.<span class="hljs-title function_">builder</span>()
        .<span class="hljs-title function_">fieldName</span>(<span class="hljs-string">&quot;sparse_vector&quot;</span>)
        .<span class="hljs-title function_">indexName</span>(<span class="hljs-string">&quot;sparse_inverted_index&quot;</span>)
        .<span class="hljs-title function_">indexType</span>(<span class="hljs-title class_">IndexParam</span>.<span class="hljs-property">IndexType</span>.<span class="hljs-property">SPARSE_INVERTED_INDEX</span>)
        .<span class="hljs-title function_">metricType</span>(<span class="hljs-title class_">IndexParam</span>.<span class="hljs-property">MetricType</span>.<span class="hljs-property">IP</span>)
        .<span class="hljs-title function_">extraParams</span>(extraParams)
        .<span class="hljs-title function_">build</span>());

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-keyword">const</span> indexParams = <span class="hljs-keyword">await</span> client.createIndex({
    index_name: <span class="hljs-string">&#x27;sparse_inverted_index&#x27;</span>,
    field_name: <span class="hljs-string">&#x27;sparse_vector&#x27;</span>,
    metric_type: MetricType.IP,
    index_type: IndexType.SPARSE_INVERTED_INDEX,
    <span class="hljs-keyword">params</span>: {
      inverted_index_algo: <span class="hljs-string">&#x27;DAAT_MAXSCORE&#x27;</span>, <span class="hljs-comment">// Algorithm used for building and querying the index</span>
    },
});

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-curl"><span class="hljs-built_in">export</span> indexParams=<span class="hljs-string">&#x27;[
        {
            &quot;fieldName&quot;: &quot;sparse_vector&quot;,
            &quot;metricType&quot;: &quot;IP&quot;,
            &quot;indexName&quot;: &quot;sparse_inverted_index&quot;,
            &quot;indexType&quot;: &quot;SPARSE_INVERTED_INDEX&quot;,
            &quot;params&quot;:{&quot;inverted_index_algo&quot;: &quot;DAAT_MAXSCORE&quot;} # Algorithm used for building and querying the index
        }
    ]&#x27;</span>

<button class="copy-code-btn"></button></code></pre>
<p>上の例では</p>
<ul>
<li><p><code translate="no">index_type</code>:疎なベクトル・フィールドに作成するインデックスの型。有効な値：</p>
<ul>
<li><code translate="no">SPARSE_INVERTED_INDEX</code>:スパースベクトル用の汎用転置インデックス。</li>
</ul>
  <div class="alert note">
<p>Milvus 2.5.4以降、<code translate="no">SPARSE_WAND</code> は非推奨となります。代わりに、互換性を維持しながら同等性を保つために<code translate="no">&quot;inverted_index_algo&quot;: &quot;DAAT_WAND&quot;</code> を使用することが推奨されます。</p>
  </div>
</li>
<li><p><code translate="no">metric_type</code>:スパースベクトル間の類似度を計算するために使用されるメトリック。有効な値：</p>
<ul>
<li><p><code translate="no">IP</code> (内積)：ドット積を使用して類似度を測定する。</p></li>
<li><p><code translate="no">BM25</code>:通常、テキストの類似性に重点を置いた全文検索に使用される。</p>
<p>詳細は「<a href="/docs/ja/metric.md">メトリックタイプと</a> <a href="/docs/ja/full-text-search.md">全文検索</a>」を参照。</p></li>
</ul></li>
<li><p><code translate="no">params.inverted_index_algo</code>:インデックスの構築とクエリに使用されるアルゴリズム。有効な値：</p>
<ul>
<li><p><code translate="no">&quot;DAAT_MAXSCORE&quot;</code> (デフォルト)：MaxScoreアルゴリズムを使用した最適化されたDocument-at-a-Time（DAAT）クエリ処理。MaxScoreは、高いk値や多くの用語を含むクエリに対して、最小限の影響しか与えないと思われる用語や文書をスキップすることで、より優れたパフォーマンスを提供します。MaxScoreは、最大インパクトスコアに基づいて用語を必須グループと非必須グループに分割し、トップkの結果に貢献できる用語に焦点を当てることでこれを実現する。</p></li>
<li><p><code translate="no">&quot;DAAT_WAND&quot;</code>:WANDアルゴリズムを使用したDAATクエリ処理の最適化。WANDは非競合文書をスキップするために最大インパクトスコアを活用することで、より少ないヒット文書を評価する。このため、WANDはk値が小さいクエリや短いクエリではスキップがより効率的である。</p></li>
<li><p><code translate="no">&quot;TAAT_NAIVE&quot;</code>:Basic Term-at-a-Time (TAAT)クエリー処理。<code translate="no">DAAT_MAXSCORE</code> 、<code translate="no">DAAT_WAND</code> と比較すると遅いが、<code translate="no">TAAT_NAIVE</code> にはユニークな利点がある。グローバルコレクションパラメータ(avgdl)の変更に関係なく静的なままキャッシュされた最大インパクトスコアを使用するDAATアルゴリズムとは異なり、<code translate="no">TAAT_NAIVE</code> 、そのような変更に動的に適応する。</p></li>
</ul></li>
</ul>
<h3 id="Create-collection​" class="common-anchor-header">コレクションの作成</h3><p>スパースベクタとインデックスの設定が完了すると、スパースベクタを含むコレクションを 作成できます。以下の例では <ins><code translate="no">create_collection</code></ins>メソッドを使用して、<code translate="no">my_sparse_collection</code> という名前のコレクションを作成します。</p>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a> <a href="#curl">cURL</a></div>
<pre><code translate="no" class="language-python">client.<span class="hljs-title function_">create_collection</span>(​
    collection_name=<span class="hljs-string">&quot;my_sparse_collection&quot;</span>,​
    schema=schema,​
    index_params=index_params​
)​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.milvus.v2.client.ConnectConfig;​
<span class="hljs-keyword">import</span> io.milvus.v2.client.MilvusClientV2;​
​
<span class="hljs-type">MilvusClientV2</span> <span class="hljs-variable">client</span> <span class="hljs-operator">=</span> <span class="hljs-keyword">new</span> <span class="hljs-title class_">MilvusClientV2</span>(ConnectConfig.builder()​
        .uri(<span class="hljs-string">&quot;http://localhost:19530&quot;</span>)​
        .build());​
        ​
<span class="hljs-type">CreateCollectionReq</span> <span class="hljs-variable">requestCreate</span> <span class="hljs-operator">=</span> CreateCollectionReq.builder()​
        .collectionName(<span class="hljs-string">&quot;my_sparse_collection&quot;</span>)​
        .collectionSchema(schema)​
        .indexParams(indexes)​
        .build();​
client.createCollection(requestCreate);​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-keyword">import</span> { <span class="hljs-title class_">MilvusClient</span> } <span class="hljs-keyword">from</span> <span class="hljs-string">&quot;@zilliz/milvus2-sdk-node&quot;</span>;​
​
<span class="hljs-keyword">const</span> client = <span class="hljs-keyword">new</span> <span class="hljs-title class_">MilvusClient</span>({​
    <span class="hljs-attr">address</span>: <span class="hljs-string">&#x27;http://localhost:19530&#x27;</span>​
});​
​
<span class="hljs-keyword">await</span> client.<span class="hljs-title function_">createCollection</span>({​
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&#x27;my_sparse_collection&#x27;</span>,​
    <span class="hljs-attr">schema</span>: schema,​
    <span class="hljs-attr">index_params</span>: indexParams​
});​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-curl">curl --request POST \​
--url <span class="hljs-string">&quot;<span class="hljs-variable">${CLUSTER_ENDPOINT}</span>/v2/vectordb/collections/create&quot;</span> \​
--header <span class="hljs-string">&quot;Authorization: Bearer <span class="hljs-variable">${TOKEN}</span>&quot;</span> \​
--header <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \​
-d <span class="hljs-string">&quot;{​
    \&quot;collectionName\&quot;: \&quot;my_sparse_collection\&quot;,​
    \&quot;schema\&quot;: <span class="hljs-variable">$schema</span>,​
    \&quot;indexParams\&quot;: <span class="hljs-variable">$indexParams</span>​
}&quot;</span>​

<button class="copy-code-btn"></button></code></pre>
<h3 id="Insert-data​" class="common-anchor-header">データの挿入</h3><p>コレクションを作成したら、スパース・ベクトルを含むデータを挿入します。</p>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a> <a href="#curl">cURL</a></div>
<pre><code translate="no" class="language-python">sparse_vectors = [​
    {<span class="hljs-string">&quot;sparse_vector&quot;</span>: {<span class="hljs-number">1</span>: <span class="hljs-number">0.5</span>, <span class="hljs-number">100</span>: <span class="hljs-number">0.3</span>, <span class="hljs-number">500</span>: <span class="hljs-number">0.8</span>}},​
    {<span class="hljs-string">&quot;sparse_vector&quot;</span>: {<span class="hljs-number">10</span>: <span class="hljs-number">0.1</span>, <span class="hljs-number">200</span>: <span class="hljs-number">0.7</span>, <span class="hljs-number">1000</span>: <span class="hljs-number">0.9</span>}},​
]​
​
client.<span class="hljs-title function_">insert</span>(​
    collection_name=<span class="hljs-string">&quot;my_sparse_collection&quot;</span>,​
    data=sparse_vectors​
)​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> com.google.gson.Gson;​
<span class="hljs-keyword">import</span> com.google.gson.JsonObject;​
<span class="hljs-keyword">import</span> io.milvus.v2.service.vector.request.InsertReq;​
<span class="hljs-keyword">import</span> io.milvus.v2.service.vector.response.InsertResp;​
​
List&lt;JsonObject&gt; rows = <span class="hljs-keyword">new</span> <span class="hljs-title class_">ArrayList</span>&lt;&gt;();​
<span class="hljs-type">Gson</span> <span class="hljs-variable">gson</span> <span class="hljs-operator">=</span> <span class="hljs-keyword">new</span> <span class="hljs-title class_">Gson</span>();​
{​
    <span class="hljs-type">JsonObject</span> <span class="hljs-variable">row</span> <span class="hljs-operator">=</span> <span class="hljs-keyword">new</span> <span class="hljs-title class_">JsonObject</span>();​
    SortedMap&lt;Long, Float&gt; sparse = <span class="hljs-keyword">new</span> <span class="hljs-title class_">TreeMap</span>&lt;&gt;();​
    sparse.put(<span class="hljs-number">1L</span>, <span class="hljs-number">0.5f</span>);​
    sparse.put(<span class="hljs-number">100L</span>, <span class="hljs-number">0.3f</span>);​
    sparse.put(<span class="hljs-number">500L</span>, <span class="hljs-number">0.8f</span>);​
    row.add(<span class="hljs-string">&quot;sparse_vector&quot;</span>, gson.toJsonTree(sparse));​
    rows.add(row);​
}​
{​
    <span class="hljs-type">JsonObject</span> <span class="hljs-variable">row</span> <span class="hljs-operator">=</span> <span class="hljs-keyword">new</span> <span class="hljs-title class_">JsonObject</span>();​
    SortedMap&lt;Long, Float&gt; sparse = <span class="hljs-keyword">new</span> <span class="hljs-title class_">TreeMap</span>&lt;&gt;();​
    sparse.put(<span class="hljs-number">10L</span>, <span class="hljs-number">0.1f</span>);​
    sparse.put(<span class="hljs-number">200L</span>, <span class="hljs-number">0.7f</span>);​
    sparse.put(<span class="hljs-number">1000L</span>, <span class="hljs-number">0.9f</span>);​
    row.add(<span class="hljs-string">&quot;sparse_vector&quot;</span>, gson.toJsonTree(sparse));​
    rows.add(row);​
}​
​
<span class="hljs-type">InsertResp</span> <span class="hljs-variable">insertR</span> <span class="hljs-operator">=</span> client.insert(InsertReq.builder()​
        .collectionName(<span class="hljs-string">&quot;my_sparse_collection&quot;</span>)​
        .data(rows)​
        .build());​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-keyword">const</span> data = [​
  { <span class="hljs-attr">sparse_vector</span>: { <span class="hljs-string">&quot;1&quot;</span>: <span class="hljs-number">0.5</span>, <span class="hljs-string">&quot;100&quot;</span>: <span class="hljs-number">0.3</span>, <span class="hljs-string">&quot;500&quot;</span>: <span class="hljs-number">0.8</span> } },​
  { <span class="hljs-attr">sparse_vector</span>: { <span class="hljs-string">&quot;10&quot;</span>: <span class="hljs-number">0.1</span>, <span class="hljs-string">&quot;200&quot;</span>: <span class="hljs-number">0.7</span>, <span class="hljs-string">&quot;1000&quot;</span>: <span class="hljs-number">0.9</span> } },​
];​
client.<span class="hljs-title function_">insert</span>({​
  <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;my_sparse_collection&quot;</span>,​
  <span class="hljs-attr">data</span>: data,​
});​
​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-curl">curl --request POST \​
--url <span class="hljs-string">&quot;<span class="hljs-variable">${CLUSTER_ENDPOINT}</span>/v2/vectordb/entities/insert&quot;</span> \​
--header <span class="hljs-string">&quot;Authorization: Bearer <span class="hljs-variable">${TOKEN}</span>&quot;</span> \​
--header <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \​
-d <span class="hljs-string">&#x27;{​
    &quot;data&quot;: [​
        {&quot;sparse_vector&quot;: {&quot;1&quot;: 0.5, &quot;100&quot;: 0.3, &quot;500&quot;: 0.8}},​
        {&quot;sparse_vector&quot;: {&quot;10&quot;: 0.1, &quot;200&quot;: 0.7, &quot;1000&quot;: 0.9}}        ​
    ],​
    &quot;collectionName&quot;: &quot;my_sparse_collection&quot;​
}&#x27;</span>​
​
<span class="hljs-comment">## {&quot;code&quot;:0,&quot;cost&quot;:0,&quot;data&quot;:{&quot;insertCount&quot;:2,&quot;insertIds&quot;:[&quot;453577185629572534&quot;,&quot;453577185629572535&quot;]}}​</span>

<button class="copy-code-btn"></button></code></pre>
<h3 id="Perform-similarity-search​" class="common-anchor-header">類似検索の実行</h3><p>スパースベクトルを使って類似検索を行うには、クエリベクトルと検索パラメータを用意します。</p>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a> <a href="#curl">cURL</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># Prepare search parameters​</span>
search_params = {​
    <span class="hljs-string">&quot;params&quot;</span>: {<span class="hljs-string">&quot;drop_ratio_search&quot;</span>: <span class="hljs-number">0.2</span>},  <span class="hljs-comment"># Proportion of small vector values to ignore during the search</span>
}​
​
<span class="hljs-comment"># Prepare the query vector​</span>
query_vector = [{<span class="hljs-number">1</span>: <span class="hljs-number">0.2</span>, <span class="hljs-number">50</span>: <span class="hljs-number">0.4</span>, <span class="hljs-number">1000</span>: <span class="hljs-number">0.7</span>}]​

<button class="copy-code-btn"></button></code></pre>
<p>この例では、<code translate="no">drop_ratio_search</code> はスパース・ベクトル専用のオプション・パラメータで、検索中にクエリ・ベクトル内の小さな値を微調整できるようにします。例えば、<code translate="no">{&quot;drop_ratio_search&quot;: 0.2}</code> を指定すると、クエリベクトル内の最小20%の値は検索時に無視されます。</p>
<p>次に、<code translate="no">search</code> メソッドを使って類似検索を実行する。</p>
<div class="multipleCode">
 <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a> <a href="#curl">cURL</a></div>
<pre><code translate="no" class="language-python">res = client.search(​
    collection_name=<span class="hljs-string">&quot;my_sparse_collection&quot;</span>,​
    data=query_vector,​
    <span class="hljs-built_in">limit</span>=3,​
    output_fields=[<span class="hljs-string">&quot;pk&quot;</span>],​
    search_params=search_params,​
)​
​
<span class="hljs-built_in">print</span>(res)​
​
<span class="hljs-comment"># Output​</span>
<span class="hljs-comment"># data: [&quot;[{&#x27;id&#x27;: &#x27;453718927992172266&#x27;, &#x27;distance&#x27;: 0.6299999952316284, &#x27;entity&#x27;: {&#x27;pk&#x27;: &#x27;453718927992172266&#x27;}}, {&#x27;id&#x27;: &#x27;453718927992172265&#x27;, &#x27;distance&#x27;: 0.10000000149011612, &#x27;entity&#x27;: {&#x27;pk&#x27;: &#x27;453718927992172265&#x27;}}]&quot;]​</span>

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.<span class="hljs-property">milvus</span>.<span class="hljs-property">v2</span>.<span class="hljs-property">service</span>.<span class="hljs-property">vector</span>.<span class="hljs-property">request</span>.<span class="hljs-property">SearchReq</span>;​
<span class="hljs-keyword">import</span> io.<span class="hljs-property">milvus</span>.<span class="hljs-property">v2</span>.<span class="hljs-property">service</span>.<span class="hljs-property">vector</span>.<span class="hljs-property">request</span>.<span class="hljs-property">data</span>.<span class="hljs-property">SparseFloatVec</span>;​
<span class="hljs-keyword">import</span> io.<span class="hljs-property">milvus</span>.<span class="hljs-property">v2</span>.<span class="hljs-property">service</span>.<span class="hljs-property">vector</span>.<span class="hljs-property">response</span>.<span class="hljs-property">SearchResp</span>;​
​
<span class="hljs-title class_">Map</span>&lt;<span class="hljs-title class_">String</span>,<span class="hljs-title class_">Object</span>&gt; searchParams = <span class="hljs-keyword">new</span> <span class="hljs-title class_">HashMap</span>&lt;&gt;();​
searchParams.<span class="hljs-title function_">put</span>(<span class="hljs-string">&quot;drop_ratio_search&quot;</span>, <span class="hljs-number">0.2</span>);​ <span class="hljs-comment">// Proportion of small vector values to ignore during the search</span>
​
<span class="hljs-title class_">SortedMap</span>&lt;<span class="hljs-title class_">Long</span>, <span class="hljs-title class_">Float</span>&gt; sparse = <span class="hljs-keyword">new</span> <span class="hljs-title class_">TreeMap</span>&lt;&gt;();​
sparse.<span class="hljs-title function_">put</span>(10L, <span class="hljs-number">0.</span>1f);​
sparse.<span class="hljs-title function_">put</span>(200L, <span class="hljs-number">0.</span>7f);​
sparse.<span class="hljs-title function_">put</span>(1000L, <span class="hljs-number">0.</span>9f);​
​
<span class="hljs-title class_">SparseFloatVec</span> queryVector = <span class="hljs-keyword">new</span> <span class="hljs-title class_">SparseFloatVec</span>(sparse);​
​
<span class="hljs-title class_">SearchResp</span> searchR = client.<span class="hljs-title function_">search</span>(<span class="hljs-title class_">SearchReq</span>.<span class="hljs-title function_">builder</span>()​
        .<span class="hljs-title function_">collectionName</span>(<span class="hljs-string">&quot;my_sparse_collection&quot;</span>)​
        .<span class="hljs-title function_">data</span>(<span class="hljs-title class_">Collections</span>.<span class="hljs-title function_">singletonList</span>(queryVector))​
        .<span class="hljs-title function_">annsField</span>(<span class="hljs-string">&quot;sparse_vector&quot;</span>)​
        .<span class="hljs-title function_">searchParams</span>(searchParams)​
        .<span class="hljs-title function_">topK</span>(<span class="hljs-number">3</span>)​
        .<span class="hljs-title function_">outputFields</span>(<span class="hljs-title class_">Collections</span>.<span class="hljs-title function_">singletonList</span>(<span class="hljs-string">&quot;pk&quot;</span>))​
        .<span class="hljs-title function_">build</span>());​
        ​
<span class="hljs-title class_">System</span>.<span class="hljs-property">out</span>.<span class="hljs-title function_">println</span>(searchR.<span class="hljs-title function_">getSearchResults</span>());​
​
<span class="hljs-comment">// Output​</span>
<span class="hljs-comment">//​</span>
<span class="hljs-comment">// [[SearchResp.SearchResult(entity={pk=453444327741536759}, score=1.31, id=453444327741536759), SearchResp.SearchResult(entity={pk=453444327741536756}, score=1.31, id=453444327741536756), SearchResp.SearchResult(entity={pk=453444327741536753}, score=1.31, id=453444327741536753)]]​</span>

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript">client.search({​
    collection_name: <span class="hljs-string">&#x27;my_sparse_collection&#x27;</span>,​
    data: {1: 0.2, 50: 0.4, 1000: 0.7},​
    <span class="hljs-built_in">limit</span>: 3,​
    output_fields: [<span class="hljs-string">&#x27;pk&#x27;</span>],​
    params: {​
        drop_ratio_search: 0.2​
    }​
});​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-curl">curl --request POST \​
--url <span class="hljs-string">&quot;<span class="hljs-variable">${CLUSTER_ENDPOINT}</span>/v2/vectordb/entities/search&quot;</span> \​
--header <span class="hljs-string">&quot;Authorization: Bearer <span class="hljs-variable">${TOKEN}</span>&quot;</span> \​
--header <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \​
-d <span class="hljs-string">&#x27;{​
    &quot;collectionName&quot;: &quot;my_sparse_collection&quot;,​
    &quot;data&quot;: [​
        {&quot;1&quot;: 0.2, &quot;50&quot;: 0.4, &quot;1000&quot;: 0.7}​
    ],​
    &quot;annsField&quot;: &quot;sparse_vector&quot;,​
    &quot;limit&quot;: 3,​
    &quot;searchParams&quot;:{​
        &quot;params&quot;:{&quot;drop_ratio_search&quot;: 0.2}​ # Proportion of small vector values to ignore during the search
    },​
    &quot;outputFields&quot;: [&quot;pk&quot;]​
}&#x27;</span>​
​
<span class="hljs-comment">## {&quot;code&quot;:0,&quot;cost&quot;:0,&quot;data&quot;:[{&quot;distance&quot;:0.63,&quot;id&quot;:&quot;453577185629572535&quot;,&quot;pk&quot;:&quot;453577185629572535&quot;},{&quot;distance&quot;:0.1,&quot;id&quot;:&quot;453577185629572534&quot;,&quot;pk&quot;:&quot;453577185629572534&quot;}]}​</span>

<button class="copy-code-btn"></button></code></pre>
<p>類似検索パラメーターの詳細については、「<a href="/docs/ja/single-vector-search.md">基本的なANN検索</a>」を参照のこと。</p>
<h2 id="Limits" class="common-anchor-header">限界<button data-href="#Limits" class="anchor-icon" translate="no">
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
    </button></h2><p>Milvusでスパースベクトルを使用する場合、以下の制限を考慮してください：</p>
<ul>
<li><p>現在、スパースベクトルは<strong>IPと</strong> <strong>BM25</strong>（全文検索用）距離メトリクスのみがサポートされています。スパースベクトルは次元が高いため、L2距離と余弦距離は実用的ではありません。</p></li>
<li><p>疎なベクトル・フィールドでは、<strong>SPARSE_INVERTED_INDEX</strong>インデックス型のみがサポートされます。</p></li>
<li><p>スパース・ベクトルでサポートされるデータ型：</p>
<ul>
<li>次元部は符号なし32ビット整数でなければならない；</li>
<li>値部は非負の32ビット浮動小数点数。</li>
</ul></li>
<li><p>スパース・ベクトルは、挿入と検索に関して以下の要件を満たす必要があります：</p>
<ul>
<li>ベクトル内の少なくとも1つの値が非ゼロである；</li>
<li>ベクトルの添字が非負であること。</li>
</ul></li>
</ul>
<h2 id="FAQ" class="common-anchor-header">よくある質問<button data-href="#FAQ" class="anchor-icon" translate="no">
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
    </button></h2><ul>
<li><p><strong>スパース埋め込みの次元は、uint32空間内の任意の離散値にすることができますか？</strong></p>
<p>はい，1つ例外があります．スパース埋込みの次元は，<code translate="no">[0, maximum of uint32)</code> の範囲内の任意の値にすることができます． つまり，uint32の最大値を使うことはできません．</p></li>
<li><p><strong>成長しているセグメントの検索は、インデックスを使って行うのですか?</strong></p>
<p>成長中のセグメントを検索する際には、セグメントインデックスと同じ型のインデックスを使用します。インデックスが作成される前の新しい成長中のセグメントについては、 総当たり検索を使用します。</p></li>
<li><p><strong>1つのコレクションに、疎なベクトルと密なベクトルの両方を持つことは可能ですか?</strong></p>
<p>はい、複数のベクトル型をサポートしているため、疎なベクトル列と密なベクトル列の両方を持つコレクションを作成し、それに対してハイブリッド検索を実行することができます。</p></li>
</ul>
