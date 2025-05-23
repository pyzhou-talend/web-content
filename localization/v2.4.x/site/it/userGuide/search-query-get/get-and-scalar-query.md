---
id: get-and-scalar-query.md
order: 3
summary: >-
  Questa guida illustra come ottenere le entità per ID ed eseguire il filtraggio
  scalare.
title: Ottenere e fare una query scalare
---
<h1 id="Get--Scalar-Query" class="common-anchor-header">Ottenere e fare una query scalare<button data-href="#Get--Scalar-Query" class="anchor-icon" translate="no">
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
    </button></h1><p>Questa guida illustra come ottenere le entità per ID ed eseguire un filtraggio scalare. Un filtro scalare recupera le entità che corrispondono alle condizioni di filtraggio specificate.</p>
<h2 id="Overview" class="common-anchor-header">Panoramica<button data-href="#Overview" class="anchor-icon" translate="no">
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
    </button></h2><p>Una query scalare filtra le entità di una raccolta in base a una condizione definita utilizzando espressioni booleane. Il risultato della query è un insieme di entità che corrispondono alla condizione definita. A differenza di una ricerca vettoriale, che identifica il vettore più vicino a un dato vettore in una collezione, le query filtrano le entità in base a criteri specifici.</p>
<p>In Milvus, <strong>un filtro è sempre una stringa che comprende nomi di campi uniti da operatori</strong>. In questa guida troverete vari esempi di filtri. Per saperne di più sui dettagli degli operatori, consultare la sezione <a href="https://milvus.io/docs/get-and-scalar-query.md#Reference-on-scalar-filters">Riferimenti</a>.</p>
<h2 id="Preparations" class="common-anchor-header">Preparazione<button data-href="#Preparations" class="anchor-icon" translate="no">
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
    </button></h2><p>I passi seguenti ripropongono il codice per connettersi a Milvus, creare rapidamente una collezione e inserire oltre 1.000 entità generate casualmente nella collezione.</p>
<h3 id="Step-1-Create-a-collection" class="common-anchor-header">Passo 1: Creare una collezione</h3><div class="language-python">
<p>Utilizzare <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Client/MilvusClient.md"><code translate="no">MilvusClient</code></a> per connettersi al server Milvus e <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Collections/create_collection.md"><code translate="no">create_collection()</code></a> per creare una raccolta.</p>
</div>
<div class="language-java">
<p>Utilizzare <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Client/MilvusClientV2.md"><code translate="no">MilvusClientV2</code></a> per connettersi al server Milvus e <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Collections/createCollection.md"><code translate="no">createCollection()</code></a> per creare una raccolta.</p>
</div>
<div class="language-javascript">
<p>Usare <a href="https://milvus.io/api-reference/node/v2.4.x/Client/MilvusClient.md"><code translate="no">MilvusClient</code></a> per connettersi al server Milvus e <a href="https://milvus.io/api-reference/node/v2.4.x/Collections/createCollection.md"><code translate="no">createCollection()</code></a> per creare una raccolta.</p>
</div>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> MilvusClient

<span class="hljs-comment"># 1. Set up a Milvus client</span>
client = MilvusClient(
    uri=<span class="hljs-string">&quot;http://localhost:19530&quot;</span>
)

<span class="hljs-comment"># 2. Create a collection</span>
client.create_collection(
    collection_name=<span class="hljs-string">&quot;quick_setup&quot;</span>,
    dimension=<span class="hljs-number">5</span>,
)
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> com.google.gson.Gson;
<span class="hljs-keyword">import</span> com.google.gson.JsonObject;
<span class="hljs-keyword">import</span> io.milvus.v2.client.MilvusClientV2;
<span class="hljs-keyword">import</span> io.milvus.v2.client.ConnectConfig;
<span class="hljs-keyword">import</span> io.milvus.v2.common.ConsistencyLevel;
<span class="hljs-keyword">import</span> io.milvus.v2.service.collection.request.CreateCollectionReq;
<span class="hljs-keyword">import</span> io.milvus.v2.service.collection.request.DropCollectionReq;
<span class="hljs-keyword">import</span> io.milvus.v2.service.partition.request.CreatePartitionReq;
<span class="hljs-keyword">import</span> io.milvus.v2.service.vector.request.GetReq;
<span class="hljs-keyword">import</span> io.milvus.v2.service.vector.request.InsertReq;
<span class="hljs-keyword">import</span> io.milvus.v2.service.vector.response.GetResp;
<span class="hljs-keyword">import</span> io.milvus.v2.service.vector.response.InsertResp;

<span class="hljs-keyword">import</span> java.util.*;

<span class="hljs-type">String</span> <span class="hljs-variable">CLUSTER_ENDPOINT</span> <span class="hljs-operator">=</span> <span class="hljs-string">&quot;http://localhost:19530&quot;</span>;

<span class="hljs-comment">// 1. Connect to Milvus server</span>
<span class="hljs-type">ConnectConfig</span> <span class="hljs-variable">connectConfig</span> <span class="hljs-operator">=</span> ConnectConfig.builder()
    .uri(CLUSTER_ENDPOINT)
    .build();

<span class="hljs-type">MilvusClientV2</span> <span class="hljs-variable">client</span> <span class="hljs-operator">=</span> <span class="hljs-keyword">new</span> <span class="hljs-title class_">MilvusClientV2</span>(connectConfig);  

<span class="hljs-comment">// 2. Create a collection in quick setup mode</span>
<span class="hljs-type">CreateCollectionReq</span> <span class="hljs-variable">quickSetupReq</span> <span class="hljs-operator">=</span> CreateCollectionReq.builder()
    .collectionName(<span class="hljs-string">&quot;quick_setup&quot;</span>)
    .dimension(<span class="hljs-number">5</span>)
    .metricType(<span class="hljs-string">&quot;IP&quot;</span>)
    .build();

client.createCollection(quickSetupReq);
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-keyword">const</span> { <span class="hljs-title class_">MilvusClient</span>, <span class="hljs-title class_">DataType</span>, sleep } = <span class="hljs-built_in">require</span>(<span class="hljs-string">&quot;@zilliz/milvus2-sdk-node&quot;</span>)

<span class="hljs-keyword">const</span> address = <span class="hljs-string">&quot;http://localhost:19530&quot;</span>

<span class="hljs-comment">// 1. Set up a Milvus Client</span>
client = <span class="hljs-keyword">new</span> <span class="hljs-title class_">MilvusClient</span>({address}); 

<span class="hljs-comment">// 2. Create a collection in quick setup mode</span>
<span class="hljs-keyword">await</span> client.<span class="hljs-title function_">createCollection</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;quick_setup&quot;</span>,
    <span class="hljs-attr">dimension</span>: <span class="hljs-number">5</span>,
}); 
<button class="copy-code-btn"></button></code></pre>
<h3 id="Step-2-Insert-randomly-generated-entities" class="common-anchor-header">Passo 2: Inserire entità generate casualmente</h3><div class="language-python">
<p>Utilizzare <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Vector/insert.md"><code translate="no">insert()</code></a> per inserire le entità nell'insieme.</p>
</div>
<div class="language-java">
<p>Utilizzare <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Vector/insert.md"><code translate="no">insert()</code></a> per inserire entità nell'insieme.</p>
</div>
<div class="language-javascript">
<p>Utilizzare <a href="https://milvus.io/api-reference/node/v2.4.x/Vector/insert.md"><code translate="no">insert()</code></a> per inserire entità nell'insieme.</p>
</div>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># 3. Insert randomly generated vectors </span>
colors = [<span class="hljs-string">&quot;green&quot;</span>, <span class="hljs-string">&quot;blue&quot;</span>, <span class="hljs-string">&quot;yellow&quot;</span>, <span class="hljs-string">&quot;red&quot;</span>, <span class="hljs-string">&quot;black&quot;</span>, <span class="hljs-string">&quot;white&quot;</span>, <span class="hljs-string">&quot;purple&quot;</span>, <span class="hljs-string">&quot;pink&quot;</span>, <span class="hljs-string">&quot;orange&quot;</span>, <span class="hljs-string">&quot;brown&quot;</span>, <span class="hljs-string">&quot;grey&quot;</span>]
data = []

<span class="hljs-keyword">for</span> i <span class="hljs-keyword">in</span> <span class="hljs-built_in">range</span>(<span class="hljs-number">1000</span>):
    current_color = random.choice(colors)
    current_tag = random.randint(<span class="hljs-number">1000</span>, <span class="hljs-number">9999</span>)
    data.append({
        <span class="hljs-string">&quot;id&quot;</span>: i,
        <span class="hljs-string">&quot;vector&quot;</span>: [ random.uniform(-<span class="hljs-number">1</span>, <span class="hljs-number">1</span>) <span class="hljs-keyword">for</span> _ <span class="hljs-keyword">in</span> <span class="hljs-built_in">range</span>(<span class="hljs-number">5</span>) ],
        <span class="hljs-string">&quot;color&quot;</span>: current_color,
        <span class="hljs-string">&quot;tag&quot;</span>: current_tag,
        <span class="hljs-string">&quot;color_tag&quot;</span>: <span class="hljs-string">f&quot;<span class="hljs-subst">{current_color}</span>_<span class="hljs-subst">{<span class="hljs-built_in">str</span>(current_tag)}</span>&quot;</span>
    })

<span class="hljs-built_in">print</span>(data[<span class="hljs-number">0</span>])

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;id&quot;: 0,</span>
<span class="hljs-comment">#     &quot;vector&quot;: [</span>
<span class="hljs-comment">#         0.7371107800002366,</span>
<span class="hljs-comment">#         -0.7290389773227746,</span>
<span class="hljs-comment">#         0.38367002049157417,</span>
<span class="hljs-comment">#         0.36996000494220627,</span>
<span class="hljs-comment">#         -0.3641898951462792</span>
<span class="hljs-comment">#     ],</span>
<span class="hljs-comment">#     &quot;color&quot;: &quot;yellow&quot;,</span>
<span class="hljs-comment">#     &quot;tag&quot;: 6781,</span>
<span class="hljs-comment">#     &quot;color_tag&quot;: &quot;yellow_6781&quot;</span>
<span class="hljs-comment"># }</span>

res = client.insert(
    collection_name=<span class="hljs-string">&quot;quick_setup&quot;</span>,
    data=data
)

<span class="hljs-built_in">print</span>(res)

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;insert_count&quot;: 1000,</span>
<span class="hljs-comment">#     &quot;ids&quot;: [</span>
<span class="hljs-comment">#         0,</span>
<span class="hljs-comment">#         1,</span>
<span class="hljs-comment">#         2,</span>
<span class="hljs-comment">#         3,</span>
<span class="hljs-comment">#         4,</span>
<span class="hljs-comment">#         5,</span>
<span class="hljs-comment">#         6,</span>
<span class="hljs-comment">#         7,</span>
<span class="hljs-comment">#         8,</span>
<span class="hljs-comment">#         9,</span>
<span class="hljs-comment">#         &quot;(990 more items hidden)&quot;</span>
<span class="hljs-comment">#     ]</span>
<span class="hljs-comment"># }</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-comment">// 3. Insert randomly generated vectors into the collection</span>
List&lt;String&gt; colors = Arrays.asList(<span class="hljs-string">&quot;green&quot;</span>, <span class="hljs-string">&quot;blue&quot;</span>, <span class="hljs-string">&quot;yellow&quot;</span>, <span class="hljs-string">&quot;red&quot;</span>, <span class="hljs-string">&quot;black&quot;</span>, <span class="hljs-string">&quot;white&quot;</span>, <span class="hljs-string">&quot;purple&quot;</span>, <span class="hljs-string">&quot;pink&quot;</span>, <span class="hljs-string">&quot;orange&quot;</span>, <span class="hljs-string">&quot;brown&quot;</span>, <span class="hljs-string">&quot;grey&quot;</span>);
List&lt;JsonObject&gt; data = <span class="hljs-keyword">new</span> <span class="hljs-title class_">ArrayList</span>&lt;&gt;();
<span class="hljs-type">Gson</span> <span class="hljs-variable">gson</span> <span class="hljs-operator">=</span> <span class="hljs-keyword">new</span> <span class="hljs-title class_">Gson</span>();
<span class="hljs-keyword">for</span> (<span class="hljs-type">int</span> i=<span class="hljs-number">0</span>; i&lt;<span class="hljs-number">1000</span>; i++) {
    <span class="hljs-type">Random</span> <span class="hljs-variable">rand</span> <span class="hljs-operator">=</span> <span class="hljs-keyword">new</span> <span class="hljs-title class_">Random</span>();
    <span class="hljs-type">String</span> <span class="hljs-variable">current_color</span> <span class="hljs-operator">=</span> colors.get(rand.nextInt(colors.size()-<span class="hljs-number">1</span>));
    <span class="hljs-type">int</span> <span class="hljs-variable">current_tag</span> <span class="hljs-operator">=</span> rand.nextInt(<span class="hljs-number">8999</span>) + <span class="hljs-number">1000</span>;
    <span class="hljs-type">JsonObject</span> <span class="hljs-variable">row</span> <span class="hljs-operator">=</span> <span class="hljs-keyword">new</span> <span class="hljs-title class_">JsonObject</span>();
    row.addProperty(<span class="hljs-string">&quot;id&quot;</span>, (<span class="hljs-type">long</span>) i);
    row.add(<span class="hljs-string">&quot;vector&quot;</span>, gson.toJsonTree(Arrays.asList(rand.nextFloat(), rand.nextFloat(), rand.nextFloat(), rand.nextFloat(), rand.nextFloat())));
    row.addProperty(<span class="hljs-string">&quot;color&quot;</span>, current_color);
    row.addProperty(<span class="hljs-string">&quot;tag&quot;</span>, current_tag);
    row.addProperty(<span class="hljs-string">&quot;color_tag&quot;</span>, current_color + <span class="hljs-string">&#x27;_&#x27;</span> + String.valueOf(rand.nextInt(<span class="hljs-number">8999</span>) + <span class="hljs-number">1000</span>));
    data.add(row);
}

<span class="hljs-type">InsertReq</span> <span class="hljs-variable">insertReq</span> <span class="hljs-operator">=</span> InsertReq.builder()
        .collectionName(<span class="hljs-string">&quot;quick_setup&quot;</span>)
        .data(data)
        .build();

<span class="hljs-type">InsertResp</span> <span class="hljs-variable">insertResp</span> <span class="hljs-operator">=</span> client.insert(insertReq);

System.out.println(insertResp.getInsertCnt());

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// 1000</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-comment">// 3. Insert randomly generated vectors</span>
<span class="hljs-keyword">const</span> colors = [<span class="hljs-string">&quot;green&quot;</span>, <span class="hljs-string">&quot;blue&quot;</span>, <span class="hljs-string">&quot;yellow&quot;</span>, <span class="hljs-string">&quot;red&quot;</span>, <span class="hljs-string">&quot;black&quot;</span>, <span class="hljs-string">&quot;white&quot;</span>, <span class="hljs-string">&quot;purple&quot;</span>, <span class="hljs-string">&quot;pink&quot;</span>, <span class="hljs-string">&quot;orange&quot;</span>, <span class="hljs-string">&quot;brown&quot;</span>, <span class="hljs-string">&quot;grey&quot;</span>]
<span class="hljs-keyword">var</span> data = []

<span class="hljs-keyword">for</span> (<span class="hljs-keyword">let</span> i = <span class="hljs-number">0</span>; i &lt; <span class="hljs-number">1000</span>; i++) {
    current_color = colors[<span class="hljs-title class_">Math</span>.<span class="hljs-title function_">floor</span>(<span class="hljs-title class_">Math</span>.<span class="hljs-title function_">random</span>() * colors.<span class="hljs-property">length</span>)]
    current_tag = <span class="hljs-title class_">Math</span>.<span class="hljs-title function_">floor</span>(<span class="hljs-title class_">Math</span>.<span class="hljs-title function_">random</span>() * <span class="hljs-number">8999</span> + <span class="hljs-number">1000</span>)
    data.<span class="hljs-title function_">push</span>({
        <span class="hljs-string">&quot;id&quot;</span>: i,
        <span class="hljs-string">&quot;vector&quot;</span>: [<span class="hljs-title class_">Math</span>.<span class="hljs-title function_">random</span>(), <span class="hljs-title class_">Math</span>.<span class="hljs-title function_">random</span>(), <span class="hljs-title class_">Math</span>.<span class="hljs-title function_">random</span>(), <span class="hljs-title class_">Math</span>.<span class="hljs-title function_">random</span>(), <span class="hljs-title class_">Math</span>.<span class="hljs-title function_">random</span>()],
        <span class="hljs-string">&quot;color&quot;</span>: current_color,
        <span class="hljs-string">&quot;tag&quot;</span>: current_tag,
        <span class="hljs-string">&quot;color_tag&quot;</span>: <span class="hljs-string">`<span class="hljs-subst">${current_color}</span>_<span class="hljs-subst">${current_tag}</span>`</span>
    })
}

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(data[<span class="hljs-number">0</span>])

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// {</span>
<span class="hljs-comment">//   id: 0,</span>
<span class="hljs-comment">//   vector: [</span>
<span class="hljs-comment">//     0.16022394821966035,</span>
<span class="hljs-comment">//     0.6514875214491056,</span>
<span class="hljs-comment">//     0.18294484964044666,</span>
<span class="hljs-comment">//     0.30227694168725394,</span>
<span class="hljs-comment">//     0.47553087493572255</span>
<span class="hljs-comment">//   ],</span>
<span class="hljs-comment">//   color: &#x27;blue&#x27;,</span>
<span class="hljs-comment">//   tag: 8907,</span>
<span class="hljs-comment">//   color_tag: &#x27;blue_8907&#x27;</span>
<span class="hljs-comment">// }</span>
<span class="hljs-comment">// </span>

res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">insert</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;quick_setup&quot;</span>,
    <span class="hljs-attr">data</span>: data
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">insert_cnt</span>)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// 1000</span>
<span class="hljs-comment">// </span>
<button class="copy-code-btn"></button></code></pre>
<h3 id="Step-3-Create-partitions-and-insert-more-entities" class="common-anchor-header">Passo 3: Creare partizioni e inserire altre entità</h3><div class="language-python">
<p>Utilizzare <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Partitions/create_partition.md"><code translate="no">create_partition()</code></a> per creare partizioni e <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Vector/insert.md"><code translate="no">insert()</code></a> per inserire altre entità nell'insieme.</p>
</div>
<div class="language-java">
<p>Utilizzare <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Partitions/createPartition.md"><code translate="no">createPartition()</code></a> per creare partizioni e <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Vector/insert.md"><code translate="no">insert()</code></a> per inserire altre entità nell'insieme.</p>
</div>
<div class="language-javascript">
<p>Utilizzare <a href="https://milvus.io/api-reference/node/v2.4.x/Partitions/createPartition.md"><code translate="no">createPartition()</code></a> per creare partizioni e <a href="https://milvus.io/api-reference/node/v2.4.x/Vector/insert.md"><code translate="no">insert()</code></a> per inserire altre entità nell'insieme.</p>
</div>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># 4. Create partitions and insert more entities</span>
client.create_partition(
    collection_name=<span class="hljs-string">&quot;quick_setup&quot;</span>,
    partition_name=<span class="hljs-string">&quot;partitionA&quot;</span>
)

client.create_partition(
    collection_name=<span class="hljs-string">&quot;quick_setup&quot;</span>,
    partition_name=<span class="hljs-string">&quot;partitionB&quot;</span>
)

data = []

<span class="hljs-keyword">for</span> i <span class="hljs-keyword">in</span> <span class="hljs-built_in">range</span>(<span class="hljs-number">1000</span>, <span class="hljs-number">1500</span>):
    current_color = random.choice(colors)
    data.append({
        <span class="hljs-string">&quot;id&quot;</span>: i,
        <span class="hljs-string">&quot;vector&quot;</span>: [ random.uniform(-<span class="hljs-number">1</span>, <span class="hljs-number">1</span>) <span class="hljs-keyword">for</span> _ <span class="hljs-keyword">in</span> <span class="hljs-built_in">range</span>(<span class="hljs-number">5</span>) ],
        <span class="hljs-string">&quot;color&quot;</span>: current_color,
        <span class="hljs-string">&quot;tag&quot;</span>: current_tag,
        <span class="hljs-string">&quot;color_tag&quot;</span>: <span class="hljs-string">f&quot;<span class="hljs-subst">{current_color}</span>_<span class="hljs-subst">{<span class="hljs-built_in">str</span>(current_tag)}</span>&quot;</span>
    })

res = client.insert(
    collection_name=<span class="hljs-string">&quot;quick_setup&quot;</span>,
    data=data,
    partition_name=<span class="hljs-string">&quot;partitionA&quot;</span>
)

<span class="hljs-built_in">print</span>(res)

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;insert_count&quot;: 500,</span>
<span class="hljs-comment">#     &quot;ids&quot;: [</span>
<span class="hljs-comment">#         1000,</span>
<span class="hljs-comment">#         1001,</span>
<span class="hljs-comment">#         1002,</span>
<span class="hljs-comment">#         1003,</span>
<span class="hljs-comment">#         1004,</span>
<span class="hljs-comment">#         1005,</span>
<span class="hljs-comment">#         1006,</span>
<span class="hljs-comment">#         1007,</span>
<span class="hljs-comment">#         1008,</span>
<span class="hljs-comment">#         1009,</span>
<span class="hljs-comment">#         &quot;(490 more items hidden)&quot;</span>
<span class="hljs-comment">#     ]</span>
<span class="hljs-comment"># }</span>

data = []

<span class="hljs-keyword">for</span> i <span class="hljs-keyword">in</span> <span class="hljs-built_in">range</span>(<span class="hljs-number">1500</span>, <span class="hljs-number">2000</span>):
    current_color = random.choice(colors)
    data.append({
        <span class="hljs-string">&quot;id&quot;</span>: i,
        <span class="hljs-string">&quot;vector&quot;</span>: [ random.uniform(-<span class="hljs-number">1</span>, <span class="hljs-number">1</span>) <span class="hljs-keyword">for</span> _ <span class="hljs-keyword">in</span> <span class="hljs-built_in">range</span>(<span class="hljs-number">5</span>) ],
        <span class="hljs-string">&quot;color&quot;</span>: current_color,
        <span class="hljs-string">&quot;tag&quot;</span>: current_tag,
        <span class="hljs-string">&quot;color_tag&quot;</span>: <span class="hljs-string">f&quot;<span class="hljs-subst">{current_color}</span>_<span class="hljs-subst">{<span class="hljs-built_in">str</span>(current_tag)}</span>&quot;</span>
    })

res = client.insert(
    collection_name=<span class="hljs-string">&quot;quick_setup&quot;</span>,
    data=data,
    partition_name=<span class="hljs-string">&quot;partitionB&quot;</span>
)

<span class="hljs-built_in">print</span>(res)

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;insert_count&quot;: 500,</span>
<span class="hljs-comment">#     &quot;ids&quot;: [</span>
<span class="hljs-comment">#         1500,</span>
<span class="hljs-comment">#         1501,</span>
<span class="hljs-comment">#         1502,</span>
<span class="hljs-comment">#         1503,</span>
<span class="hljs-comment">#         1504,</span>
<span class="hljs-comment">#         1505,</span>
<span class="hljs-comment">#         1506,</span>
<span class="hljs-comment">#         1507,</span>
<span class="hljs-comment">#         1508,</span>
<span class="hljs-comment">#         1509,</span>
<span class="hljs-comment">#         &quot;(490 more items hidden)&quot;</span>
<span class="hljs-comment">#     ]</span>
<span class="hljs-comment"># }</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-comment">// 4. Create partitions and insert some more data</span>
CreatePartitionReq createPartitionReq = CreatePartitionReq.builder()
        .collectionName(<span class="hljs-string">&quot;quick_setup&quot;</span>)
        .partitionName(<span class="hljs-string">&quot;partitionA&quot;</span>)
        .build();

client.createPartition(createPartitionReq);

createPartitionReq = CreatePartitionReq.builder()
        .collectionName(<span class="hljs-string">&quot;quick_setup&quot;</span>)
        .partitionName(<span class="hljs-string">&quot;partitionB&quot;</span>)
        .build();

client.createPartition(createPartitionReq);

data.clear();

<span class="hljs-keyword">for</span> (<span class="hljs-built_in">int</span> i=<span class="hljs-number">1000</span>; i&lt;<span class="hljs-number">1500</span>; i++) {
    Random rand = <span class="hljs-keyword">new</span> Random();
    String current_color = colors.<span class="hljs-keyword">get</span>(rand.nextInt(colors.size()<span class="hljs-number">-1</span>));
    <span class="hljs-built_in">int</span> current_tag = rand.nextInt(<span class="hljs-number">8999</span>) + <span class="hljs-number">1000</span>;
    JsonObject row = <span class="hljs-keyword">new</span> JsonObject();
    row.addProperty(<span class="hljs-string">&quot;id&quot;</span>, (<span class="hljs-built_in">long</span>) i);
    row.<span class="hljs-keyword">add</span>(<span class="hljs-string">&quot;vector&quot;</span>, gson.toJsonTree(Arrays.asList(rand.nextFloat(), rand.nextFloat(), rand.nextFloat(), rand.nextFloat(), rand.nextFloat())));
    row.addProperty(<span class="hljs-string">&quot;color&quot;</span>, current_color);
    row.addProperty(<span class="hljs-string">&quot;tag&quot;</span>, current_tag);
    data.<span class="hljs-keyword">add</span>(row);
}

insertReq = InsertReq.builder()
        .collectionName(<span class="hljs-string">&quot;quick_setup&quot;</span>)
        .data(data)
        .partitionName(<span class="hljs-string">&quot;partitionA&quot;</span>)
        .build();

insertResp = client.insert(insertReq);

System.<span class="hljs-keyword">out</span>.println(insertResp.getInsertCnt());

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// 500</span>

data.clear();

<span class="hljs-keyword">for</span> (<span class="hljs-built_in">int</span> i=<span class="hljs-number">1500</span>; i&lt;<span class="hljs-number">2000</span>; i++) {
    Random rand = <span class="hljs-keyword">new</span> Random();
    String current_color = colors.<span class="hljs-keyword">get</span>(rand.nextInt(colors.size()<span class="hljs-number">-1</span>));
    <span class="hljs-built_in">int</span> current_tag = rand.nextInt(<span class="hljs-number">8999</span>) + <span class="hljs-number">1000</span>;
    JsonObject row = <span class="hljs-keyword">new</span> JsonObject();
    row.addProperty(<span class="hljs-string">&quot;id&quot;</span>, (<span class="hljs-built_in">long</span>) i);
    row.<span class="hljs-keyword">add</span>(<span class="hljs-string">&quot;vector&quot;</span>, gson.toJsonTree(Arrays.asList(rand.nextFloat(), rand.nextFloat(), rand.nextFloat(), rand.nextFloat(), rand.nextFloat())));
    row.addProperty(<span class="hljs-string">&quot;color&quot;</span>, current_color);
    row.addProperty(<span class="hljs-string">&quot;tag&quot;</span>, current_tag);
    data.<span class="hljs-keyword">add</span>(row);
}

insertReq = InsertReq.builder()
        .collectionName(<span class="hljs-string">&quot;quick_setup&quot;</span>)
        .data(data)
        .partitionName(<span class="hljs-string">&quot;partitionB&quot;</span>)
        .build();

insertResp = client.insert(insertReq);

System.<span class="hljs-keyword">out</span>.println(insertResp.getInsertCnt());

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// 500</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-comment">// 4. Create partitions and insert more entities</span>
<span class="hljs-keyword">await</span> client.<span class="hljs-title function_">createPartition</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;quick_setup&quot;</span>,
    <span class="hljs-attr">partition_name</span>: <span class="hljs-string">&quot;partitionA&quot;</span>
})

<span class="hljs-keyword">await</span> client.<span class="hljs-title function_">createPartition</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;quick_setup&quot;</span>,
    <span class="hljs-attr">partition_name</span>: <span class="hljs-string">&quot;partitionB&quot;</span>
})

data = []

<span class="hljs-keyword">for</span> (<span class="hljs-keyword">let</span> i = <span class="hljs-number">1000</span>; i &lt; <span class="hljs-number">1500</span>; i++) {
    current_color = colors[<span class="hljs-title class_">Math</span>.<span class="hljs-title function_">floor</span>(<span class="hljs-title class_">Math</span>.<span class="hljs-title function_">random</span>() * colors.<span class="hljs-property">length</span>)]
    current_tag = <span class="hljs-title class_">Math</span>.<span class="hljs-title function_">floor</span>(<span class="hljs-title class_">Math</span>.<span class="hljs-title function_">random</span>() * <span class="hljs-number">8999</span> + <span class="hljs-number">1000</span>)
    data.<span class="hljs-title function_">push</span>({
        <span class="hljs-string">&quot;id&quot;</span>: i,
        <span class="hljs-string">&quot;vector&quot;</span>: [<span class="hljs-title class_">Math</span>.<span class="hljs-title function_">random</span>(), <span class="hljs-title class_">Math</span>.<span class="hljs-title function_">random</span>(), <span class="hljs-title class_">Math</span>.<span class="hljs-title function_">random</span>(), <span class="hljs-title class_">Math</span>.<span class="hljs-title function_">random</span>(), <span class="hljs-title class_">Math</span>.<span class="hljs-title function_">random</span>()],
        <span class="hljs-string">&quot;color&quot;</span>: current_color,
        <span class="hljs-string">&quot;tag&quot;</span>: current_tag,
        <span class="hljs-string">&quot;color_tag&quot;</span>: <span class="hljs-string">`<span class="hljs-subst">${current_color}</span>_<span class="hljs-subst">${current_tag}</span>`</span>
    })
}

res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">insert</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;quick_setup&quot;</span>,
    <span class="hljs-attr">data</span>: data,
    <span class="hljs-attr">partition_name</span>: <span class="hljs-string">&quot;partitionA&quot;</span>
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">insert_cnt</span>)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// 500</span>
<span class="hljs-comment">// </span>

<span class="hljs-keyword">await</span> <span class="hljs-title function_">sleep</span>(<span class="hljs-number">5000</span>)

data = []

<span class="hljs-keyword">for</span> (<span class="hljs-keyword">let</span> i = <span class="hljs-number">1500</span>; i &lt; <span class="hljs-number">2000</span>; i++) {
    current_color = colors[<span class="hljs-title class_">Math</span>.<span class="hljs-title function_">floor</span>(<span class="hljs-title class_">Math</span>.<span class="hljs-title function_">random</span>() * colors.<span class="hljs-property">length</span>)]
    current_tag = <span class="hljs-title class_">Math</span>.<span class="hljs-title function_">floor</span>(<span class="hljs-title class_">Math</span>.<span class="hljs-title function_">random</span>() * <span class="hljs-number">8999</span> + <span class="hljs-number">1000</span>)
    data.<span class="hljs-title function_">push</span>({
        <span class="hljs-string">&quot;id&quot;</span>: i,
        <span class="hljs-string">&quot;vector&quot;</span>: [<span class="hljs-title class_">Math</span>.<span class="hljs-title function_">random</span>(), <span class="hljs-title class_">Math</span>.<span class="hljs-title function_">random</span>(), <span class="hljs-title class_">Math</span>.<span class="hljs-title function_">random</span>(), <span class="hljs-title class_">Math</span>.<span class="hljs-title function_">random</span>(), <span class="hljs-title class_">Math</span>.<span class="hljs-title function_">random</span>()],
        <span class="hljs-string">&quot;color&quot;</span>: current_color,
        <span class="hljs-string">&quot;tag&quot;</span>: current_tag,
        <span class="hljs-string">&quot;color_tag&quot;</span>: <span class="hljs-string">`<span class="hljs-subst">${current_color}</span>_<span class="hljs-subst">${current_tag}</span>`</span>
    })
}

res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">insert</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;quick_setup&quot;</span>,
    <span class="hljs-attr">data</span>: data,
    <span class="hljs-attr">partition_name</span>: <span class="hljs-string">&quot;partitionB&quot;</span>
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">insert_cnt</span>)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// 500</span>
<span class="hljs-comment">// </span>
<button class="copy-code-btn"></button></code></pre>
<h2 id="Get-Entities-by-ID" class="common-anchor-header">Ottenere entità per ID<button data-href="#Get-Entities-by-ID" class="anchor-icon" translate="no">
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
    </button></h2><div class="language-python">
<p>Se si conoscono gli ID delle entità di interesse, si può usare il metodo <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Vector/get.md"><code translate="no">get()</code></a> .</p>
</div>
<div class="language-java">
<p>Se si conoscono gli ID delle entità di interesse, è possibile utilizzare il metodo <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Vector/get.md"><code translate="no">get()</code></a> metodo.</p>
</div>
<div class="language-javascript">
<p>Se si conoscono gli ID delle entità di interesse, è possibile utilizzare il metodo <a href="https://milvus.io/api-reference/node/v2.4.x/Vector/get.md"><code translate="no">get()</code></a> metodo.</p>
</div>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># 4. Get entities by ID</span>
res = client.get(
    collection_name=<span class="hljs-string">&quot;quick_setup&quot;</span>,
    ids=[<span class="hljs-number">0</span>, <span class="hljs-number">1</span>, <span class="hljs-number">2</span>]
)

<span class="hljs-built_in">print</span>(res)

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># [</span>
<span class="hljs-comment">#     {</span>
<span class="hljs-comment">#         &quot;id&quot;: 0,</span>
<span class="hljs-comment">#         &quot;vector&quot;: [</span>
<span class="hljs-comment">#             0.68824464,</span>
<span class="hljs-comment">#             0.6552274,</span>
<span class="hljs-comment">#             0.33593303,</span>
<span class="hljs-comment">#             -0.7099536,</span>
<span class="hljs-comment">#             -0.07070546</span>
<span class="hljs-comment">#         ],</span>
<span class="hljs-comment">#         &quot;color_tag&quot;: &quot;green_2006&quot;,</span>
<span class="hljs-comment">#         &quot;color&quot;: &quot;green&quot;</span>
<span class="hljs-comment">#     },</span>
<span class="hljs-comment">#     {</span>
<span class="hljs-comment">#         &quot;id&quot;: 1,</span>
<span class="hljs-comment">#         &quot;vector&quot;: [</span>
<span class="hljs-comment">#             -0.98531723,</span>
<span class="hljs-comment">#             0.33456197,</span>
<span class="hljs-comment">#             0.2844234,</span>
<span class="hljs-comment">#             0.42886782,</span>
<span class="hljs-comment">#             0.32753858</span>
<span class="hljs-comment">#         ],</span>
<span class="hljs-comment">#         &quot;color_tag&quot;: &quot;white_9298&quot;,</span>
<span class="hljs-comment">#         &quot;color&quot;: &quot;white&quot;</span>
<span class="hljs-comment">#     },</span>
<span class="hljs-comment">#     {</span>
<span class="hljs-comment">#         &quot;id&quot;: 2,</span>
<span class="hljs-comment">#         &quot;vector&quot;: [</span>
<span class="hljs-comment">#             -0.9886812,</span>
<span class="hljs-comment">#             -0.44129863,</span>
<span class="hljs-comment">#             -0.29859528,</span>
<span class="hljs-comment">#             0.06059075,</span>
<span class="hljs-comment">#             -0.43817034</span>
<span class="hljs-comment">#         ],</span>
<span class="hljs-comment">#         &quot;color_tag&quot;: &quot;grey_5312&quot;,</span>
<span class="hljs-comment">#         &quot;color&quot;: &quot;grey&quot;</span>
<span class="hljs-comment">#     }</span>
<span class="hljs-comment"># ]</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-comment">// 5. Get entities by ID</span>
<span class="hljs-type">GetReq</span> <span class="hljs-variable">getReq</span> <span class="hljs-operator">=</span> GetReq.builder()
        .collectionName(<span class="hljs-string">&quot;quick_setup&quot;</span>)
        .ids(Arrays.asList(<span class="hljs-number">0L</span>, <span class="hljs-number">1L</span>, <span class="hljs-number">2L</span>))
        .build();

<span class="hljs-type">GetResp</span> <span class="hljs-variable">entities</span> <span class="hljs-operator">=</span> client.get(getReq);

System.out.println(entities.getGetResults());

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// [</span>
<span class="hljs-comment">//  QueryResp.QueryResult(entity={color=blue, color_tag=blue_4025, vector=[0.64311606, 0.73486423, 0.7352375, 0.7020566, 0.9885356], id=0, tag=4018}),</span>
<span class="hljs-comment">//  QueryResp.QueryResult(entity={color=red, color_tag=red_4788, vector=[0.27244627, 0.7068031, 0.25976115, 0.69258106, 0.8767045], id=1, tag=6611}),</span>
<span class="hljs-comment">//  QueryResp.QueryResult(entity={color=yellow, color_tag=yellow_8382, vector=[0.19625628, 0.40176708, 0.13231951, 0.50702184, 0.88406855], id=2, tag=5349})</span>
<span class="hljs-comment">//]</span>

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-comment">// 5. Get entities by id</span>
res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">get</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;quick_setup&quot;</span>,
    <span class="hljs-attr">ids</span>: [<span class="hljs-number">0</span>, <span class="hljs-number">1</span>, <span class="hljs-number">2</span>],
    <span class="hljs-attr">output_fields</span>: [<span class="hljs-string">&quot;vector&quot;</span>, <span class="hljs-string">&quot;color_tag&quot;</span>]
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">data</span>)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// [</span>
<span class="hljs-comment">//   {</span>
<span class="hljs-comment">//     vector: [</span>
<span class="hljs-comment">//       0.16022394597530365,</span>
<span class="hljs-comment">//       0.6514875292778015,</span>
<span class="hljs-comment">//       0.18294484913349152,</span>
<span class="hljs-comment">//       0.30227693915367126,</span>
<span class="hljs-comment">//       0.47553086280822754</span>
<span class="hljs-comment">//     ],</span>
<span class="hljs-comment">//     &#x27;$meta&#x27;: { color: &#x27;blue&#x27;, tag: 8907, color_tag: &#x27;blue_8907&#x27; },</span>
<span class="hljs-comment">//     id: &#x27;0&#x27;</span>
<span class="hljs-comment">//   },</span>
<span class="hljs-comment">//   {</span>
<span class="hljs-comment">//     vector: [</span>
<span class="hljs-comment">//       0.2459285855293274,</span>
<span class="hljs-comment">//       0.4974019527435303,</span>
<span class="hljs-comment">//       0.2154673933982849,</span>
<span class="hljs-comment">//       0.03719571232795715,</span>
<span class="hljs-comment">//       0.8348019123077393</span>
<span class="hljs-comment">//     ],</span>
<span class="hljs-comment">//     &#x27;$meta&#x27;: { color: &#x27;grey&#x27;, tag: 3710, color_tag: &#x27;grey_3710&#x27; },</span>
<span class="hljs-comment">//     id: &#x27;1&#x27;</span>
<span class="hljs-comment">//   },</span>
<span class="hljs-comment">//   {</span>
<span class="hljs-comment">//     vector: [</span>
<span class="hljs-comment">//       0.9404329061508179,</span>
<span class="hljs-comment">//       0.49662265181541443,</span>
<span class="hljs-comment">//       0.8088793158531189,</span>
<span class="hljs-comment">//       0.9337621331214905,</span>
<span class="hljs-comment">//       0.8269071578979492</span>
<span class="hljs-comment">//     ],</span>
<span class="hljs-comment">//     &#x27;$meta&#x27;: { color: &#x27;blue&#x27;, tag: 2993, color_tag: &#x27;blue_2993&#x27; },</span>
<span class="hljs-comment">//     id: &#x27;2&#x27;</span>
<span class="hljs-comment">//   }</span>
<span class="hljs-comment">// ]</span>
<span class="hljs-comment">// </span>
<button class="copy-code-btn"></button></code></pre>
<h3 id="Get-entities-from-partitions" class="common-anchor-header">Ottenere entità da partizioni</h3><p>È anche possibile ottenere entità da partizioni specifiche.</p>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># 5. Get entities from partitions</span>
res = client.get(
    collection_name=<span class="hljs-string">&quot;quick_setup&quot;</span>,
    ids=[<span class="hljs-number">1000</span>, <span class="hljs-number">1001</span>, <span class="hljs-number">1002</span>],
    partition_names=[<span class="hljs-string">&quot;partitionA&quot;</span>]
)

<span class="hljs-built_in">print</span>(res)

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># [</span>
<span class="hljs-comment">#     {</span>
<span class="hljs-comment">#         &quot;color&quot;: &quot;green&quot;,</span>
<span class="hljs-comment">#         &quot;tag&quot;: 1995,</span>
<span class="hljs-comment">#         &quot;color_tag&quot;: &quot;green_1995&quot;,</span>
<span class="hljs-comment">#         &quot;id&quot;: 1000,</span>
<span class="hljs-comment">#         &quot;vector&quot;: [</span>
<span class="hljs-comment">#             0.7807706,</span>
<span class="hljs-comment">#             0.8083741,</span>
<span class="hljs-comment">#             0.17276904,</span>
<span class="hljs-comment">#             -0.8580777,</span>
<span class="hljs-comment">#             0.024156934</span>
<span class="hljs-comment">#         ]</span>
<span class="hljs-comment">#     },</span>
<span class="hljs-comment">#     {</span>
<span class="hljs-comment">#         &quot;color&quot;: &quot;red&quot;,</span>
<span class="hljs-comment">#         &quot;tag&quot;: 1995,</span>
<span class="hljs-comment">#         &quot;color_tag&quot;: &quot;red_1995&quot;,</span>
<span class="hljs-comment">#         &quot;id&quot;: 1001,</span>
<span class="hljs-comment">#         &quot;vector&quot;: [</span>
<span class="hljs-comment">#             0.065074645,</span>
<span class="hljs-comment">#             -0.44882354,</span>
<span class="hljs-comment">#             -0.29479212,</span>
<span class="hljs-comment">#             -0.19798489,</span>
<span class="hljs-comment">#             -0.77542555</span>
<span class="hljs-comment">#         ]</span>
<span class="hljs-comment">#     },</span>
<span class="hljs-comment">#     {</span>
<span class="hljs-comment">#         &quot;color&quot;: &quot;green&quot;,</span>
<span class="hljs-comment">#         &quot;tag&quot;: 1995,</span>
<span class="hljs-comment">#         &quot;color_tag&quot;: &quot;green_1995&quot;,</span>
<span class="hljs-comment">#         &quot;id&quot;: 1002,</span>
<span class="hljs-comment">#         &quot;vector&quot;: [</span>
<span class="hljs-comment">#             0.027934508,</span>
<span class="hljs-comment">#             -0.44199976,</span>
<span class="hljs-comment">#             -0.40262738,</span>
<span class="hljs-comment">#             -0.041511405,</span>
<span class="hljs-comment">#             0.024782438</span>
<span class="hljs-comment">#         ]</span>
<span class="hljs-comment">#     }</span>
<span class="hljs-comment"># ]</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-comment">// 5. Get entities by ID in a partition</span>
getReq = GetReq.builder()
        .collectionName(<span class="hljs-string">&quot;quick_setup&quot;</span>)
        .ids(Arrays.asList(<span class="hljs-number">1001L</span>, <span class="hljs-number">1002L</span>, <span class="hljs-number">1003L</span>))
        .partitionName(<span class="hljs-string">&quot;partitionA&quot;</span>)
        .build();

entities = client.<span class="hljs-keyword">get</span>(getReq);

System.<span class="hljs-keyword">out</span>.println(entities.getGetResults());

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// [</span>
<span class="hljs-comment">//  QueryResp.QueryResult(entity={color=pink, vector=[0.28847772, 0.5116072, 0.5695933, 0.49643654, 0.3461541], id=1001, tag=9632}), </span>
<span class="hljs-comment">//  QueryResp.QueryResult(entity={color=blue, vector=[0.22428268, 0.8648047, 0.78426147, 0.84020555, 0.60779166], id=1002, tag=4523}), </span>
<span class="hljs-comment">//  QueryResp.QueryResult(entity={color=white, vector=[0.4081068, 0.9027214, 0.88685805, 0.38036376, 0.27950126], id=1003, tag=9321})</span>
<span class="hljs-comment">// ]</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-comment">// 5.1 Get entities by id in a partition</span>
res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">get</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;quick_setup&quot;</span>,
    <span class="hljs-attr">ids</span>: [<span class="hljs-number">1000</span>, <span class="hljs-number">1001</span>, <span class="hljs-number">1002</span>],
    <span class="hljs-attr">partition_names</span>: [<span class="hljs-string">&quot;partitionA&quot;</span>],
    <span class="hljs-attr">output_fields</span>: [<span class="hljs-string">&quot;vector&quot;</span>, <span class="hljs-string">&quot;color_tag&quot;</span>]
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">data</span>)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// [</span>
<span class="hljs-comment">//   {</span>
<span class="hljs-comment">//     id: &#x27;1000&#x27;,</span>
<span class="hljs-comment">//     vector: [</span>
<span class="hljs-comment">//       0.014254206791520119,</span>
<span class="hljs-comment">//       0.5817716121673584,</span>
<span class="hljs-comment">//       0.19793470203876495,</span>
<span class="hljs-comment">//       0.8064294457435608,</span>
<span class="hljs-comment">//       0.7745839357376099</span>
<span class="hljs-comment">//     ],</span>
<span class="hljs-comment">//     &#x27;$meta&#x27;: { color: &#x27;white&#x27;, tag: 5996, color_tag: &#x27;white_5996&#x27; }</span>
<span class="hljs-comment">//   },</span>
<span class="hljs-comment">//   {</span>
<span class="hljs-comment">//     id: &#x27;1001&#x27;,</span>
<span class="hljs-comment">//     vector: [</span>
<span class="hljs-comment">//       0.6073881983757019,</span>
<span class="hljs-comment">//       0.05214758217334747,</span>
<span class="hljs-comment">//       0.730999231338501,</span>
<span class="hljs-comment">//       0.20900958776474,</span>
<span class="hljs-comment">//       0.03665429726243019</span>
<span class="hljs-comment">//     ],</span>
<span class="hljs-comment">//     &#x27;$meta&#x27;: { color: &#x27;grey&#x27;, tag: 2834, color_tag: &#x27;grey_2834&#x27; }</span>
<span class="hljs-comment">//   },</span>
<span class="hljs-comment">//   {</span>
<span class="hljs-comment">//     id: &#x27;1002&#x27;,</span>
<span class="hljs-comment">//     vector: [</span>
<span class="hljs-comment">//       0.48877206444740295,</span>
<span class="hljs-comment">//       0.34028753638267517,</span>
<span class="hljs-comment">//       0.6527213454246521,</span>
<span class="hljs-comment">//       0.9763909578323364,</span>
<span class="hljs-comment">//       0.8031482100486755</span>
<span class="hljs-comment">//     ],</span>
<span class="hljs-comment">//     &#x27;$meta&#x27;: { color: &#x27;pink&#x27;, tag: 9107, color_tag: &#x27;pink_9107&#x27; }</span>
<span class="hljs-comment">//   }</span>
<span class="hljs-comment">// ]</span>
<span class="hljs-comment">// </span>
<button class="copy-code-btn"></button></code></pre>
<h2 id="Use-Basic-Operators" class="common-anchor-header">Utilizzare gli operatori di base<button data-href="#Use-Basic-Operators" class="anchor-icon" translate="no">
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
    </button></h2><p>In questa sezione sono riportati esempi di utilizzo degli operatori di base nel filtraggio scalare. È possibile applicare questi filtri anche alle <a href="https://milvus.io/docs/single-vector-search.md#Filtered-search">ricerche vettoriali</a> e alle <a href="https://milvus.io/docs/insert-update-delete.md#Delete-entities">cancellazioni di dati</a>.</p>
<div class="language-python">
<p>Per ulteriori informazioni, fare riferimento a <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Vector/query.md"><code translate="no">query()</code></a> nel riferimento dell'SDK.</p>
</div>
<div class="language-java">
<p>Per ulteriori informazioni, fare riferimento a <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Vector/query.md"><code translate="no">query()</code></a> nel riferimento dell'SDK.</p>
</div>
<div class="language-javascript">
<p>Per ulteriori informazioni, fare riferimento a <a href="https://milvus.io/api-reference/node/v2.4.x/Vector/query.md"><code translate="no">query()</code></a> nel riferimento dell'SDK.</p>
</div>
<ul>
<li><p>Filtra le entità con valori di tag compresi tra 1.000 e 1.500.</p>
<p><div class="multipleCode">
<a href="#python">Python </a><a href="#java">Java</a><a href="#javascript">Node.js</a></div></p>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># 6. Use basic operators</span>

res = client.query(
    collection_name=<span class="hljs-string">&quot;quick_setup&quot;</span>,
    <span class="hljs-built_in">filter</span>=<span class="hljs-string">&quot;1000 &lt; tag &lt; 1500&quot;</span>,
    output_fields=[<span class="hljs-string">&quot;color_tag&quot;</span>],
    limit=<span class="hljs-number">3</span>
)

<span class="hljs-built_in">print</span>(res)

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># [</span>
<span class="hljs-comment">#     {</span>
<span class="hljs-comment">#         &quot;id&quot;: 1,</span>
<span class="hljs-comment">#         &quot;color_tag&quot;: &quot;pink_1023&quot;</span>
<span class="hljs-comment">#     },</span>
<span class="hljs-comment">#     {</span>
<span class="hljs-comment">#         &quot;id&quot;: 41,</span>
<span class="hljs-comment">#         &quot;color_tag&quot;: &quot;red_1483&quot;</span>
<span class="hljs-comment">#     },</span>
<span class="hljs-comment">#     {</span>
<span class="hljs-comment">#         &quot;id&quot;: 44,</span>
<span class="hljs-comment">#         &quot;color_tag&quot;: &quot;grey_1146&quot;</span>
<span class="hljs-comment">#     }</span>
<span class="hljs-comment"># ]</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-comment">// 6. Use basic operators</span>

<span class="hljs-title class_">QueryReq</span> queryReq = <span class="hljs-title class_">QueryReq</span>.<span class="hljs-title function_">builder</span>()
    .<span class="hljs-title function_">collectionName</span>(<span class="hljs-string">&quot;quick_setup&quot;</span>)
    .<span class="hljs-title function_">filter</span>(<span class="hljs-string">&quot;1000 &lt; tag &lt; 1500&quot;</span>)
    .<span class="hljs-title function_">outputFields</span>(<span class="hljs-title class_">Arrays</span>.<span class="hljs-title function_">asList</span>(<span class="hljs-string">&quot;color_tag&quot;</span>))
    .<span class="hljs-title function_">limit</span>(<span class="hljs-number">3</span>)
    .<span class="hljs-title function_">build</span>();

<span class="hljs-title class_">QueryResp</span> queryResp = client.<span class="hljs-title function_">query</span>(queryReq);

<span class="hljs-title class_">System</span>.<span class="hljs-property">out</span>.<span class="hljs-title function_">println</span>(<span class="hljs-title class_">JSON</span><span class="hljs-built_in">Object</span>.<span class="hljs-title function_">toJSON</span>(queryResp));

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// {&quot;queryResults&quot;: [</span>
<span class="hljs-comment">//     {&quot;entity&quot;: {</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: &quot;white_7588&quot;,</span>
<span class="hljs-comment">//         &quot;id&quot;: 34</span>
<span class="hljs-comment">//     }},</span>
<span class="hljs-comment">//     {&quot;entity&quot;: {</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: &quot;orange_4989&quot;,</span>
<span class="hljs-comment">//         &quot;id&quot;: 64</span>
<span class="hljs-comment">//     }},</span>
<span class="hljs-comment">//     {&quot;entity&quot;: {</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: &quot;white_3415&quot;,</span>
<span class="hljs-comment">//         &quot;id&quot;: 73</span>
<span class="hljs-comment">//     }}</span>
<span class="hljs-comment">// ]}</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-comment">// 6. Use basic operators</span>
res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">query</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;quick_setup&quot;</span>,
    <span class="hljs-attr">filter</span>: <span class="hljs-string">&quot;1000 &lt; tag &lt; 1500&quot;</span>,
    <span class="hljs-attr">output_fields</span>: [<span class="hljs-string">&quot;color_tag&quot;</span>],
    <span class="hljs-attr">limit</span>: <span class="hljs-number">3</span>
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">data</span>)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// [</span>
<span class="hljs-comment">//   {</span>
<span class="hljs-comment">//     &#x27;$meta&#x27;: { color: &#x27;pink&#x27;, tag: 1050, color_tag: &#x27;pink_1050&#x27; },</span>
<span class="hljs-comment">//     id: &#x27;6&#x27;</span>
<span class="hljs-comment">//   },</span>
<span class="hljs-comment">//   {</span>
<span class="hljs-comment">//     &#x27;$meta&#x27;: { color: &#x27;purple&#x27;, tag: 1174, color_tag: &#x27;purple_1174&#x27; },</span>
<span class="hljs-comment">//     id: &#x27;24&#x27;</span>
<span class="hljs-comment">//   },</span>
<span class="hljs-comment">//   {</span>
<span class="hljs-comment">//     &#x27;$meta&#x27;: { color: &#x27;orange&#x27;, tag: 1023, color_tag: &#x27;orange_1023&#x27; },</span>
<span class="hljs-comment">//     id: &#x27;40&#x27;</span>
<span class="hljs-comment">//   }</span>
<span class="hljs-comment">// ]</span>
<span class="hljs-comment">// </span>
<button class="copy-code-btn"></button></code></pre></li>
<li><p>Filtra le entità i cui valori di <strong>colore</strong> sono impostati su <strong>marrone</strong>.</p>
<p><div class="multipleCode">
<a href="#python">Python </a><a href="#java">Java</a><a href="#javascript">Node.js</a></div></p>
<pre><code translate="no" class="language-python">res = client.query(
    collection_name=<span class="hljs-string">&quot;quick_setup&quot;</span>,
    <span class="hljs-built_in">filter</span>=<span class="hljs-string">&#x27;color == &quot;brown&quot;&#x27;</span>,
    output_fields=[<span class="hljs-string">&quot;color_tag&quot;</span>],
    limit=<span class="hljs-number">3</span>
)

<span class="hljs-built_in">print</span>(res)

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># [</span>
<span class="hljs-comment">#     {</span>
<span class="hljs-comment">#         &quot;color_tag&quot;: &quot;brown_5343&quot;,</span>
<span class="hljs-comment">#         &quot;id&quot;: 15</span>
<span class="hljs-comment">#     },</span>
<span class="hljs-comment">#     {</span>
<span class="hljs-comment">#         &quot;color_tag&quot;: &quot;brown_3167&quot;,</span>
<span class="hljs-comment">#         &quot;id&quot;: 27</span>
<span class="hljs-comment">#     },</span>
<span class="hljs-comment">#     {</span>
<span class="hljs-comment">#         &quot;color_tag&quot;: &quot;brown_3100&quot;,</span>
<span class="hljs-comment">#         &quot;id&quot;: 30</span>
<span class="hljs-comment">#     }</span>
<span class="hljs-comment"># ]</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java">queryReq = <span class="hljs-title class_">QueryReq</span>.<span class="hljs-title function_">builder</span>()
    .<span class="hljs-title function_">collectionName</span>(<span class="hljs-string">&quot;quick_setup&quot;</span>)
    .<span class="hljs-title function_">filter</span>(<span class="hljs-string">&quot;color == \&quot;brown\&quot;&quot;</span>)
    .<span class="hljs-title function_">outputFields</span>(<span class="hljs-title class_">Arrays</span>.<span class="hljs-title function_">asList</span>(<span class="hljs-string">&quot;color_tag&quot;</span>))
    .<span class="hljs-title function_">limit</span>(<span class="hljs-number">3</span>)
    .<span class="hljs-title function_">build</span>();

queryResp = client.<span class="hljs-title function_">query</span>(queryReq);

<span class="hljs-title class_">System</span>.<span class="hljs-property">out</span>.<span class="hljs-title function_">println</span>(<span class="hljs-title class_">JSON</span><span class="hljs-built_in">Object</span>.<span class="hljs-title function_">toJSON</span>(queryResp));

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// {&quot;queryResults&quot;: [</span>
<span class="hljs-comment">//     {&quot;entity&quot;: {</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: &quot;brown_7792&quot;,</span>
<span class="hljs-comment">//         &quot;id&quot;: 3</span>
<span class="hljs-comment">//     }},</span>
<span class="hljs-comment">//     {&quot;entity&quot;: {</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: &quot;brown_9695&quot;,</span>
<span class="hljs-comment">//         &quot;id&quot;: 7</span>
<span class="hljs-comment">//     }},</span>
<span class="hljs-comment">//     {&quot;entity&quot;: {</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: &quot;brown_2551&quot;,</span>
<span class="hljs-comment">//         &quot;id&quot;: 15</span>
<span class="hljs-comment">//     }}</span>
<span class="hljs-comment">// ]}</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript">res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">query</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;quick_setup&quot;</span>,
    <span class="hljs-attr">filter</span>: <span class="hljs-string">&#x27;color == &quot;brown&quot;&#x27;</span>,
    <span class="hljs-attr">output_fields</span>: [<span class="hljs-string">&quot;color_tag&quot;</span>],
    <span class="hljs-attr">limit</span>: <span class="hljs-number">3</span>
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">data</span>)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// [</span>
<span class="hljs-comment">//   {</span>
<span class="hljs-comment">//     &#x27;$meta&#x27;: { color: &#x27;brown&#x27;, tag: 6839, color_tag: &#x27;brown_6839&#x27; },</span>
<span class="hljs-comment">//     id: &#x27;22&#x27;</span>
<span class="hljs-comment">//   },</span>
<span class="hljs-comment">//   {</span>
<span class="hljs-comment">//     &#x27;$meta&#x27;: { color: &#x27;brown&#x27;, tag: 7849, color_tag: &#x27;brown_7849&#x27; },</span>
<span class="hljs-comment">//     id: &#x27;32&#x27;</span>
<span class="hljs-comment">//   },</span>
<span class="hljs-comment">//   {</span>
<span class="hljs-comment">//     &#x27;$meta&#x27;: { color: &#x27;brown&#x27;, tag: 7855, color_tag: &#x27;brown_7855&#x27; },</span>
<span class="hljs-comment">//     id: &#x27;33&#x27;</span>
<span class="hljs-comment">//   }</span>
<span class="hljs-comment">// ]</span>
<span class="hljs-comment">// </span>
<button class="copy-code-btn"></button></code></pre></li>
<li><p>Filtra le entità i cui valori di <strong>colore</strong> non sono impostati su <strong>verde</strong> e <strong>viola</strong>.</p>
<p><div class="multipleCode">
<a href="#python">Python </a><a href="#java">Java</a><a href="#javascript">Node.js</a></div></p>
<pre><code translate="no" class="language-python">res = client.query(
    collection_name=<span class="hljs-string">&quot;quick_setup&quot;</span>,
    <span class="hljs-built_in">filter</span>=<span class="hljs-string">&#x27;color not in [&quot;green&quot;, &quot;purple&quot;]&#x27;</span>,
    output_fields=[<span class="hljs-string">&quot;color_tag&quot;</span>],
    limit=<span class="hljs-number">3</span>
)

<span class="hljs-built_in">print</span>(res)

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># [</span>
<span class="hljs-comment">#     {</span>
<span class="hljs-comment">#         &quot;color_tag&quot;: &quot;yellow_6781&quot;,</span>
<span class="hljs-comment">#         &quot;id&quot;: 0</span>
<span class="hljs-comment">#     },</span>
<span class="hljs-comment">#     {</span>
<span class="hljs-comment">#         &quot;color_tag&quot;: &quot;pink_1023&quot;,</span>
<span class="hljs-comment">#         &quot;id&quot;: 1</span>
<span class="hljs-comment">#     },</span>
<span class="hljs-comment">#     {</span>
<span class="hljs-comment">#         &quot;color_tag&quot;: &quot;blue_3972&quot;,</span>
<span class="hljs-comment">#         &quot;id&quot;: 2</span>
<span class="hljs-comment">#     }</span>
<span class="hljs-comment"># ]</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java">queryReq = <span class="hljs-title class_">QueryReq</span>.<span class="hljs-title function_">builder</span>()
    .<span class="hljs-title function_">collectionName</span>(<span class="hljs-string">&quot;quick_setup&quot;</span>)
    .<span class="hljs-title function_">filter</span>(<span class="hljs-string">&quot;color not in [\&quot;green\&quot;, \&quot;purple\&quot;]&quot;</span>)
    .<span class="hljs-title function_">outputFields</span>(<span class="hljs-title class_">Arrays</span>.<span class="hljs-title function_">asList</span>(<span class="hljs-string">&quot;color_tag&quot;</span>))
    .<span class="hljs-title function_">limit</span>(<span class="hljs-number">3</span>)
    .<span class="hljs-title function_">build</span>();

queryResp = client.<span class="hljs-title function_">query</span>(queryReq);

<span class="hljs-title class_">System</span>.<span class="hljs-property">out</span>.<span class="hljs-title function_">println</span>(<span class="hljs-title class_">JSON</span><span class="hljs-built_in">Object</span>.<span class="hljs-title function_">toJSON</span>(queryResp));   

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// {&quot;queryResults&quot;: [</span>
<span class="hljs-comment">//     {&quot;entity&quot;: {</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: &quot;white_4597&quot;,</span>
<span class="hljs-comment">//         &quot;id&quot;: 0</span>
<span class="hljs-comment">//     }},</span>
<span class="hljs-comment">//     {&quot;entity&quot;: {</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: &quot;white_8708&quot;,</span>
<span class="hljs-comment">//         &quot;id&quot;: 2</span>
<span class="hljs-comment">//     }},</span>
<span class="hljs-comment">//     {&quot;entity&quot;: {</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: &quot;brown_7792&quot;,</span>
<span class="hljs-comment">//         &quot;id&quot;: 3</span>
<span class="hljs-comment">//     }}</span>
<span class="hljs-comment">// ]}</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript">res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">query</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;quick_setup&quot;</span>,
    <span class="hljs-attr">filter</span>: <span class="hljs-string">&#x27;color not in [&quot;green&quot;, &quot;purple&quot;]&#x27;</span>,
    <span class="hljs-attr">output_fields</span>: [<span class="hljs-string">&quot;color_tag&quot;</span>],
    <span class="hljs-attr">limit</span>: <span class="hljs-number">3</span>
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">data</span>)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// [</span>
<span class="hljs-comment">//   {</span>
<span class="hljs-comment">//     &#x27;$meta&#x27;: { color: &#x27;blue&#x27;, tag: 8907, color_tag: &#x27;blue_8907&#x27; },</span>
<span class="hljs-comment">//     id: &#x27;0&#x27;</span>
<span class="hljs-comment">//   },</span>
<span class="hljs-comment">//   {</span>
<span class="hljs-comment">//     &#x27;$meta&#x27;: { color: &#x27;grey&#x27;, tag: 3710, color_tag: &#x27;grey_3710&#x27; },</span>
<span class="hljs-comment">//     id: &#x27;1&#x27;</span>
<span class="hljs-comment">//   },</span>
<span class="hljs-comment">//   {</span>
<span class="hljs-comment">//     &#x27;$meta&#x27;: { color: &#x27;blue&#x27;, tag: 2993, color_tag: &#x27;blue_2993&#x27; },</span>
<span class="hljs-comment">//     id: &#x27;2&#x27;</span>
<span class="hljs-comment">//   }</span>
<span class="hljs-comment">// ]</span>
<span class="hljs-comment">// </span>
<button class="copy-code-btn"></button></code></pre></li>
<li><p>Filtra gli articoli i cui tag colore iniziano con il <strong>rosso</strong>.</p>
<p><div class="multipleCode">
<a href="#python">Python </a><a href="#java">Java</a><a href="#javascript">Node.js</a></div></p>
<pre><code translate="no" class="language-python">res = client.query(
    collection_name=<span class="hljs-string">&quot;quick_setup&quot;</span>,
    <span class="hljs-built_in">filter</span>=<span class="hljs-string">&#x27;color_tag like &quot;red%&quot;&#x27;</span>,
    output_fields=[<span class="hljs-string">&quot;color_tag&quot;</span>],
    limit=<span class="hljs-number">3</span>
)

<span class="hljs-built_in">print</span>(res)

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># [</span>
<span class="hljs-comment">#     {</span>
<span class="hljs-comment">#         &quot;color_tag&quot;: &quot;red_6443&quot;,</span>
<span class="hljs-comment">#         &quot;id&quot;: 17</span>
<span class="hljs-comment">#     },</span>
<span class="hljs-comment">#     {</span>
<span class="hljs-comment">#         &quot;color_tag&quot;: &quot;red_1483&quot;,</span>
<span class="hljs-comment">#         &quot;id&quot;: 41</span>
<span class="hljs-comment">#     },</span>
<span class="hljs-comment">#     {</span>
<span class="hljs-comment">#         &quot;color_tag&quot;: &quot;red_4348&quot;,</span>
<span class="hljs-comment">#         &quot;id&quot;: 47</span>
<span class="hljs-comment">#     }</span>
<span class="hljs-comment"># ]</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java">queryReq = <span class="hljs-title class_">QueryReq</span>.<span class="hljs-title function_">builder</span>()
    .<span class="hljs-title function_">collectionName</span>(<span class="hljs-string">&quot;quick_setup&quot;</span>)
    .<span class="hljs-title function_">filter</span>(<span class="hljs-string">&quot;color_tag like \&quot;red%\&quot;&quot;</span>)
    .<span class="hljs-title function_">outputFields</span>(<span class="hljs-title class_">Arrays</span>.<span class="hljs-title function_">asList</span>(<span class="hljs-string">&quot;color_tag&quot;</span>))
    .<span class="hljs-title function_">limit</span>(<span class="hljs-number">3</span>)
    .<span class="hljs-title function_">build</span>();

queryResp = client.<span class="hljs-title function_">query</span>(queryReq);

<span class="hljs-title class_">System</span>.<span class="hljs-property">out</span>.<span class="hljs-title function_">println</span>(<span class="hljs-title class_">JSON</span><span class="hljs-built_in">Object</span>.<span class="hljs-title function_">toJSON</span>(queryResp));  

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// {&quot;queryResults&quot;: [</span>
<span class="hljs-comment">//     {&quot;entity&quot;: {</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: &quot;red_4929&quot;,</span>
<span class="hljs-comment">//         &quot;id&quot;: 9</span>
<span class="hljs-comment">//     }},</span>
<span class="hljs-comment">//     {&quot;entity&quot;: {</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: &quot;red_8284&quot;,</span>
<span class="hljs-comment">//         &quot;id&quot;: 13</span>
<span class="hljs-comment">//     }},</span>
<span class="hljs-comment">//     {&quot;entity&quot;: {</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: &quot;red_3021&quot;,</span>
<span class="hljs-comment">//         &quot;id&quot;: 44</span>
<span class="hljs-comment">//     }}</span>
<span class="hljs-comment">// ]}</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript">res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">query</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;quick_setup&quot;</span>,
    <span class="hljs-attr">filter</span>: <span class="hljs-string">&#x27;color_tag like &quot;red%&quot;&#x27;</span>,
    <span class="hljs-attr">output_fields</span>: [<span class="hljs-string">&quot;color_tag&quot;</span>],
    <span class="hljs-attr">limit</span>: <span class="hljs-number">3</span>
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">data</span>)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// [</span>
<span class="hljs-comment">//   {</span>
<span class="hljs-comment">//     &#x27;$meta&#x27;: { color: &#x27;red&#x27;, tag: 8773, color_tag: &#x27;red_8773&#x27; },</span>
<span class="hljs-comment">//     id: &#x27;17&#x27;</span>
<span class="hljs-comment">//   },</span>
<span class="hljs-comment">//   {</span>
<span class="hljs-comment">//     &#x27;$meta&#x27;: { color: &#x27;red&#x27;, tag: 9197, color_tag: &#x27;red_9197&#x27; },</span>
<span class="hljs-comment">//     id: &#x27;34&#x27;</span>
<span class="hljs-comment">//   },</span>
<span class="hljs-comment">//   {</span>
<span class="hljs-comment">//     &#x27;$meta&#x27;: { color: &#x27;red&#x27;, tag: 7914, color_tag: &#x27;red_7914&#x27; },</span>
<span class="hljs-comment">//     id: &#x27;46&#x27;</span>
<span class="hljs-comment">//   }</span>
<span class="hljs-comment">// ]</span>
<span class="hljs-comment">// </span>
<button class="copy-code-btn"></button></code></pre></li>
<li><p>Filtra le entità i cui colori sono impostati su rosso e i cui valori dei tag sono compresi nell'intervallo tra 1.000 e 1.500.</p>
<p><div class="multipleCode">
<a href="#python">Python </a><a href="#java">Java</a><a href="#javascript">Node.js</a></div></p>
<pre><code translate="no" class="language-python">res = client.query(
    collection_name=<span class="hljs-string">&quot;quick_setup&quot;</span>,
    <span class="hljs-built_in">filter</span>=<span class="hljs-string">&#x27;(color == &quot;red&quot;) and (1000 &lt; tag &lt; 1500)&#x27;</span>,
    output_fields=[<span class="hljs-string">&quot;color_tag&quot;</span>],
    limit=<span class="hljs-number">3</span>
)

<span class="hljs-built_in">print</span>(res)

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># [</span>
<span class="hljs-comment">#     {</span>
<span class="hljs-comment">#         &quot;color_tag&quot;: &quot;red_1483&quot;,</span>
<span class="hljs-comment">#         &quot;id&quot;: 41</span>
<span class="hljs-comment">#     },</span>
<span class="hljs-comment">#     {</span>
<span class="hljs-comment">#         &quot;color_tag&quot;: &quot;red_1100&quot;,</span>
<span class="hljs-comment">#         &quot;id&quot;: 94</span>
<span class="hljs-comment">#     },</span>
<span class="hljs-comment">#     {</span>
<span class="hljs-comment">#         &quot;color_tag&quot;: &quot;red_1343&quot;,</span>
<span class="hljs-comment">#         &quot;id&quot;: 526</span>
<span class="hljs-comment">#     }</span>
<span class="hljs-comment"># ]</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java">queryReq = <span class="hljs-title class_">QueryReq</span>.<span class="hljs-title function_">builder</span>()
    .<span class="hljs-title function_">collectionName</span>(<span class="hljs-string">&quot;quick_setup&quot;</span>)
    .<span class="hljs-title function_">filter</span>(<span class="hljs-string">&quot;(color == \&quot;red\&quot;) and (1000 &lt; tag &lt; 1500)&quot;</span>)
    .<span class="hljs-title function_">outputFields</span>(<span class="hljs-title class_">Arrays</span>.<span class="hljs-title function_">asList</span>(<span class="hljs-string">&quot;color_tag&quot;</span>))
    .<span class="hljs-title function_">limit</span>(<span class="hljs-number">3</span>)
    .<span class="hljs-title function_">build</span>();

queryResp = client.<span class="hljs-title function_">query</span>(queryReq);

<span class="hljs-title class_">System</span>.<span class="hljs-property">out</span>.<span class="hljs-title function_">println</span>(<span class="hljs-title class_">JSON</span><span class="hljs-built_in">Object</span>.<span class="hljs-title function_">toJSON</span>(queryResp));  

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// {&quot;queryResults&quot;: [</span>
<span class="hljs-comment">//     {&quot;entity&quot;: {</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: &quot;red_8124&quot;,</span>
<span class="hljs-comment">//         &quot;id&quot;: 83</span>
<span class="hljs-comment">//     }},</span>
<span class="hljs-comment">//     {&quot;entity&quot;: {</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: &quot;red_5358&quot;,</span>
<span class="hljs-comment">//         &quot;id&quot;: 501</span>
<span class="hljs-comment">//     }},</span>
<span class="hljs-comment">//     {&quot;entity&quot;: {</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: &quot;red_3564&quot;,</span>
<span class="hljs-comment">//         &quot;id&quot;: 638</span>
<span class="hljs-comment">//     }}</span>
<span class="hljs-comment">// ]}</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript">res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">query</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;quick_setup&quot;</span>,
    <span class="hljs-attr">filter</span>: <span class="hljs-string">&#x27;(color == &quot;red&quot;) and (1000 &lt; tag &lt; 1500)&#x27;</span>,
    <span class="hljs-attr">output_fields</span>: [<span class="hljs-string">&quot;color_tag&quot;</span>],
    <span class="hljs-attr">limit</span>: <span class="hljs-number">3</span>
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">data</span>)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// [</span>
<span class="hljs-comment">//   {</span>
<span class="hljs-comment">//     &#x27;$meta&#x27;: { color: &#x27;red&#x27;, tag: 1436, color_tag: &#x27;red_1436&#x27; },</span>
<span class="hljs-comment">//     id: &#x27;67&#x27;</span>
<span class="hljs-comment">//   },</span>
<span class="hljs-comment">//   {</span>
<span class="hljs-comment">//     &#x27;$meta&#x27;: { color: &#x27;red&#x27;, tag: 1463, color_tag: &#x27;red_1463&#x27; },</span>
<span class="hljs-comment">//     id: &#x27;160&#x27;</span>
<span class="hljs-comment">//   },</span>
<span class="hljs-comment">//   {</span>
<span class="hljs-comment">//     &#x27;$meta&#x27;: { color: &#x27;red&#x27;, tag: 1073, color_tag: &#x27;red_1073&#x27; },</span>
<span class="hljs-comment">//     id: &#x27;291&#x27;</span>
<span class="hljs-comment">//   }</span>
<span class="hljs-comment">// ]</span>
<span class="hljs-comment">// </span>
<button class="copy-code-btn"></button></code></pre></li>
</ul>
<h2 id="Use-Advanced-Operators" class="common-anchor-header">Utilizzare gli operatori avanzati<button data-href="#Use-Advanced-Operators" class="anchor-icon" translate="no">
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
    </button></h2><p>In questa sezione sono riportati esempi di utilizzo di operatori avanzati nel filtraggio scalare. È possibile applicare questi filtri anche alle <a href="https://milvus.io/docs/single-vector-search.md#Filtered-search">ricerche vettoriali</a> e alle <a href="https://milvus.io/docs/insert-update-delete.md#Delete-entities">cancellazioni di dati</a>.</p>
<h3 id="Count-entities" class="common-anchor-header">Conta entità</h3><ul>
<li><p>Conta il numero totale di entità in un insieme.</p>
<p><div class="multipleCode">
<a href="#python">Python </a><a href="#java">Java</a><a href="#javascript">Node.js</a></div></p>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># 7. Use advanced operators</span>

<span class="hljs-comment"># Count the total number of entities in a collection</span>
res = client.query(
    collection_name=<span class="hljs-string">&quot;quick_setup&quot;</span>,
    output_fields=[<span class="hljs-string">&quot;count(*)&quot;</span>]
)

<span class="hljs-built_in">print</span>(res)

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># [</span>
<span class="hljs-comment">#     {</span>
<span class="hljs-comment">#         &quot;count(*)&quot;: 2000</span>
<span class="hljs-comment">#     }</span>
<span class="hljs-comment"># ]</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-comment">// 7. Use advanced operators</span>
<span class="hljs-comment">// Count the total number of entities in the collection</span>
queryReq = <span class="hljs-title class_">QueryReq</span>.<span class="hljs-title function_">builder</span>()
    .<span class="hljs-title function_">collectionName</span>(<span class="hljs-string">&quot;quick_setup&quot;</span>)
    .<span class="hljs-title function_">filter</span>(<span class="hljs-string">&quot;&quot;</span>)
    .<span class="hljs-title function_">outputFields</span>(<span class="hljs-title class_">Arrays</span>.<span class="hljs-title function_">asList</span>(<span class="hljs-string">&quot;count(*)&quot;</span>))
    .<span class="hljs-title function_">build</span>();

queryResp = client.<span class="hljs-title function_">query</span>(queryReq);

<span class="hljs-title class_">System</span>.<span class="hljs-property">out</span>.<span class="hljs-title function_">println</span>(<span class="hljs-title class_">JSON</span><span class="hljs-built_in">Object</span>.<span class="hljs-title function_">toJSON</span>(queryResp));

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// {&quot;queryResults&quot;: [{&quot;entity&quot;: {&quot;count(*)&quot;: 2000}}]}</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-comment">// 7. Use advanced operators</span>
<span class="hljs-comment">// Count the total number of entities in a collection</span>
res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">query</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;quick_setup&quot;</span>,
    <span class="hljs-attr">output_fields</span>: [<span class="hljs-string">&quot;count(*)&quot;</span>]
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">data</span>)   

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// [ { &#x27;count(*)&#x27;: &#x27;2000&#x27; } ]</span>
<span class="hljs-comment">// </span>
<button class="copy-code-btn"></button></code></pre></li>
<li><p>Conta il numero totale di entità in partizioni specifiche.</p>
<p><div class="multipleCode">
<a href="#python">Python </a><a href="#java">Java</a><a href="#javascript">Node.js</a></div></p>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># Count the number of entities in a partition</span>
res = client.query(
    collection_name=<span class="hljs-string">&quot;quick_setup&quot;</span>,
    output_fields=[<span class="hljs-string">&quot;count(*)&quot;</span>],
    partition_names=[<span class="hljs-string">&quot;partitionA&quot;</span>]
)

<span class="hljs-built_in">print</span>(res)

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># [</span>
<span class="hljs-comment">#     {</span>
<span class="hljs-comment">#         &quot;count(*)&quot;: 500</span>
<span class="hljs-comment">#     }</span>
<span class="hljs-comment"># ]</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-comment">// Count the number of entities in a partition</span>
queryReq = <span class="hljs-title class_">QueryReq</span>.<span class="hljs-title function_">builder</span>()
    .<span class="hljs-title function_">collectionName</span>(<span class="hljs-string">&quot;quick_setup&quot;</span>)
    .<span class="hljs-title function_">partitionNames</span>(<span class="hljs-title class_">Arrays</span>.<span class="hljs-title function_">asList</span>(<span class="hljs-string">&quot;partitionA&quot;</span>))
    .<span class="hljs-title function_">filter</span>(<span class="hljs-string">&quot;&quot;</span>)
    .<span class="hljs-title function_">outputFields</span>(<span class="hljs-title class_">Arrays</span>.<span class="hljs-title function_">asList</span>(<span class="hljs-string">&quot;count(*)&quot;</span>))
    .<span class="hljs-title function_">build</span>();

queryResp = client.<span class="hljs-title function_">query</span>(queryReq);

<span class="hljs-title class_">System</span>.<span class="hljs-property">out</span>.<span class="hljs-title function_">println</span>(<span class="hljs-title class_">JSON</span><span class="hljs-built_in">Object</span>.<span class="hljs-title function_">toJSON</span>(queryResp));

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// {&quot;queryResults&quot;: [{&quot;entity&quot;: {&quot;count(*)&quot;: 500}}]}</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-comment">// Count the number of entities in a partition</span>
res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">query</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;quick_setup&quot;</span>,
    <span class="hljs-attr">output_fields</span>: [<span class="hljs-string">&quot;count(*)&quot;</span>],
    <span class="hljs-attr">partition_names</span>: [<span class="hljs-string">&quot;partitionA&quot;</span>]
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">data</span>)     

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// [ { &#x27;count(*)&#x27;: &#x27;500&#x27; } ]</span>
<span class="hljs-comment">// </span>
<button class="copy-code-btn"></button></code></pre></li>
<li><p>Conta il numero di entità che corrispondono a una condizione di filtraggio.</p>
<p><div class="multipleCode">
<a href="#python">Python </a><a href="#java">Java</a><a href="#javascript">Node.js</a></div></p>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># Count the number of entities that match a specific filter</span>
res = client.query(
    collection_name=<span class="hljs-string">&quot;quick_setup&quot;</span>,
    <span class="hljs-built_in">filter</span>=<span class="hljs-string">&#x27;(color == &quot;red&quot;) and (1000 &lt; tag &lt; 1500)&#x27;</span>,
    output_fields=[<span class="hljs-string">&quot;count(*)&quot;</span>],
)

<span class="hljs-built_in">print</span>(res)

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># [</span>
<span class="hljs-comment">#     {</span>
<span class="hljs-comment">#         &quot;count(*)&quot;: 3</span>
<span class="hljs-comment">#     }</span>
<span class="hljs-comment"># ]</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-comment">// Count the number of entities that match a specific filter</span>
queryReq = <span class="hljs-title class_">QueryReq</span>.<span class="hljs-title function_">builder</span>()
    .<span class="hljs-title function_">collectionName</span>(<span class="hljs-string">&quot;quick_setup&quot;</span>)
    .<span class="hljs-title function_">filter</span>(<span class="hljs-string">&quot;(color == \&quot;red\&quot;) and (1000 &lt; tag &lt; 1500)&quot;</span>)
    .<span class="hljs-title function_">outputFields</span>(<span class="hljs-title class_">Arrays</span>.<span class="hljs-title function_">asList</span>(<span class="hljs-string">&quot;count(*)&quot;</span>))
    .<span class="hljs-title function_">build</span>();

queryResp = client.<span class="hljs-title function_">query</span>(queryReq);

<span class="hljs-title class_">System</span>.<span class="hljs-property">out</span>.<span class="hljs-title function_">println</span>(<span class="hljs-title class_">JSON</span><span class="hljs-built_in">Object</span>.<span class="hljs-title function_">toJSON</span>(queryResp));

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// {&quot;queryResults&quot;: [{&quot;entity&quot;: {&quot;count(*)&quot;: 7}}]}</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-comment">// Count the number of entities that match a specific filter</span>
res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">query</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;quick_setup&quot;</span>,
    <span class="hljs-attr">filter</span>: <span class="hljs-string">&#x27;(color == &quot;red&quot;) and (1000 &lt; tag &lt; 1500)&#x27;</span>,
    <span class="hljs-attr">output_fields</span>: [<span class="hljs-string">&quot;count(*)&quot;</span>]
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">data</span>)   

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// [ { &#x27;count(*)&#x27;: &#x27;10&#x27; } ]</span>
<span class="hljs-comment">// </span>
<button class="copy-code-btn"></button></code></pre></li>
</ul>
<h2 id="Reference-on-scalar-filters" class="common-anchor-header">Riferimento ai filtri scalari<button data-href="#Reference-on-scalar-filters" class="anchor-icon" translate="no">
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
    </button></h2><h3 id="Basic-Operators" class="common-anchor-header">Operatori di base</h3><p>Un'<strong>espressione booleana</strong> è sempre <strong>una stringa composta da nomi di campi uniti da operatori</strong>. In questa sezione, si apprenderà di più sugli operatori di base.</p>
<table>
<thead>
<tr><th><strong>Operatore</strong></th><th><strong>Descrizione</strong></th></tr>
</thead>
<tbody>
<tr><td><strong>e (&amp;&amp;)</strong></td><td>È vero se entrambi gli operandi sono veri</td></tr>
<tr><td><strong>o (||)</strong></td><td>Vero se uno dei due operandi è vero</td></tr>
<tr><td><strong>+, -, *, /</strong></td><td>Addizione, sottrazione, moltiplicazione e divisione</td></tr>
<tr><td><strong>**</strong></td><td>Esponente</td></tr>
<tr><td><strong>%</strong></td><td>Modulo</td></tr>
<tr><td><strong>&lt;, &gt;</strong></td><td>Minore di, maggiore di</td></tr>
<tr><td><strong>==, !=</strong></td><td>Uguale a, non uguale a</td></tr>
<tr><td><strong>&lt;=, &gt;=</strong></td><td>Inferiore o uguale a, maggiore o uguale a</td></tr>
<tr><td><strong>non</strong></td><td>Inverte il risultato di una determinata condizione.</td></tr>
<tr><td><strong>come</strong></td><td>Confronta un valore con valori simili utilizzando gli operatori jolly.<br/> Ad esempio, like &quot;prefix%&quot; corrisponde alle stringhe che iniziano con &quot;prefix&quot;.</td></tr>
<tr><td><strong>in</strong></td><td>Verifica se un'espressione corrisponde a qualsiasi valore in un elenco di valori.</td></tr>
</tbody>
</table>
<h3 id="Advanced-operators" class="common-anchor-header">Operatori avanzati</h3><ul>
<li><p><code translate="no">count(*)</code></p>
<p>Conta il numero esatto di entità nell'insieme. Si può usare come campo di output per ottenere il numero esatto di entità in un insieme o in una partizione.</p>
<p><div class="admonition note"></p>
<p><p><b>note</b></p></p>
<p><p>Si applica alle raccolte caricate. Dovreste usarlo come unico campo di output.</p></p>
<p></div></p></li>
</ul>
