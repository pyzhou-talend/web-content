---
id: with-iterators.md
order: 4
summary: >-
  Milvus proporciona iteradores de búsqueda y consulta para iterar resultados
  con un gran volumen de entidades.
title: Con iteradores
---
<h1 id="With-Iterators" class="common-anchor-header">Con iteradores<button data-href="#With-Iterators" class="anchor-icon" translate="no">
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
    </button></h1><p>Milvus proporciona iteradores de búsqueda y consulta para iterar a través de un gran volumen de entidades. Dado que Milvus limita TopK a 16384, los usuarios pueden utilizar iteradores para devolver grandes números o incluso entidades enteras en una colección en modo por lotes.</p>
<h2 id="Overview" class="common-anchor-header">Visión general<button data-href="#Overview" class="anchor-icon" translate="no">
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
    </button></h2><p>Los iteradores son una herramienta eficaz para escanear una colección completa o iterar a través de un gran volumen de entidades especificando valores de clave primaria o una expresión de filtro. En comparación con una llamada de búsqueda o consulta con parámetros de <strong>desplazamiento</strong> y <strong>límite</strong>, el uso de iteradores es más eficiente y escalable.</p>
<h3 id="Benefits-of-using-iterators" class="common-anchor-header">Ventajas del uso de iteradores</h3><ul>
<li><p><strong>Simplicidad</strong>: Elimina los complejos parámetros de <strong>desplazamiento</strong> y <strong>límite</strong>.</p></li>
<li><p><strong>Eficacia</strong>: Proporciona una recuperación de datos escalable al obtener sólo los datos necesarios.</p></li>
<li><p><strong>Coherencia</strong>: Garantiza un tamaño coherente del conjunto de datos con filtros booleanos.</p></li>
</ul>
<div class="admonition note">
<p><b>notas</b></p>
<ul>
<li>Esta función está disponible para Milvus 2.3.x o posterior.</li>
</ul>
</div>
<h2 id="Preparations" class="common-anchor-header">Preparativos<button data-href="#Preparations" class="anchor-icon" translate="no">
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
    </button></h2><p>El siguiente paso de preparación se conecta a Milvus e inserta entidades generadas aleatoriamente en una colección.</p>
<h3 id="Step-1-Create-a-collection" class="common-anchor-header">Paso 1: Crear una colección</h3><div class="language-python">
<p>Utilice <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Client/MilvusClient.md"><code translate="no">MilvusClient</code></a> para conectarse al servidor Milvus y <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Collections/create_collection.md"><code translate="no">create_collection()</code></a> para crear una colección.</p>
</div>
<div class="language-java">
<p>Utilice <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Client/MilvusClientV2.md"><code translate="no">MilvusClientV2</code></a> para conectarse al servidor Milvus y <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Collections/createCollection.md"><code translate="no">createCollection()</code></a> para crear una colección.</p>
</div>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a></div>
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
<span class="hljs-keyword">import</span> io.milvus.orm.iterator.QueryIterator;
<span class="hljs-keyword">import</span> io.milvus.orm.iterator.SearchIterator;
<span class="hljs-keyword">import</span> io.milvus.response.QueryResultsWrapper;
<span class="hljs-keyword">import</span> io.milvus.v2.client.MilvusClientV2;
<span class="hljs-keyword">import</span> io.milvus.v2.client.ConnectConfig;
<span class="hljs-keyword">import</span> io.milvus.v2.common.ConsistencyLevel;
<span class="hljs-keyword">import</span> io.milvus.v2.common.IndexParam;
<span class="hljs-keyword">import</span> io.milvus.v2.service.collection.request.CreateCollectionReq;
<span class="hljs-keyword">import</span> io.milvus.v2.service.collection.request.DropCollectionReq;
<span class="hljs-keyword">import</span> io.milvus.v2.service.vector.request.*;
<span class="hljs-keyword">import</span> io.milvus.v2.service.vector.request.data.FloatVec;
<span class="hljs-keyword">import</span> io.milvus.v2.service.vector.response.InsertResp;
<span class="hljs-keyword">import</span> io.milvus.v2.service.vector.response.QueryResp;

<span class="hljs-keyword">import</span> java.util.*;

<span class="hljs-type">String</span> <span class="hljs-variable">CLUSTER_ENDPOINT</span> <span class="hljs-operator">=</span> <span class="hljs-string">&quot;http://localhost:19530&quot;</span>;

<span class="hljs-comment">// 1. Connect to Milvus server</span>
<span class="hljs-type">ConnectParam</span> <span class="hljs-variable">connectParam</span> <span class="hljs-operator">=</span> ConnectParam.newBuilder()
        .withUri(CLUSTER_ENDPOINT)
        .build();

<span class="hljs-type">MilvusServiceClient</span> <span class="hljs-variable">client</span>  <span class="hljs-operator">=</span> <span class="hljs-keyword">new</span> <span class="hljs-title class_">MilvusServiceClient</span>(connectParam);

<span class="hljs-comment">// 2. Create a collection</span>
<span class="hljs-type">CreateCollectionReq</span> <span class="hljs-variable">quickSetupReq</span> <span class="hljs-operator">=</span> CreateCollectionReq.builder()
        .collectionName(<span class="hljs-string">&quot;quick_setup&quot;</span>)
        .dimension(<span class="hljs-number">5</span>)
        .build();
client.createCollection(quickSetupReq);
<button class="copy-code-btn"></button></code></pre>
<h3 id="Step-2-Insert-randomly-generated-entities" class="common-anchor-header">Paso 2: Insertar entidades generadas aleatoriamente</h3><div class="language-python">
<p>Utilice <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Vector/insert.md"><code translate="no">insert()</code></a> para insertar entidades en la colección.</p>
</div>
<div class="language-java">
<p>Utilice <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Vector/insert.md"><code translate="no">insert()</code></a> para insertar entidades en la colección.</p>
</div>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># 3. Insert randomly generated vectors </span>
colors = [<span class="hljs-string">&quot;green&quot;</span>, <span class="hljs-string">&quot;blue&quot;</span>, <span class="hljs-string">&quot;yellow&quot;</span>, <span class="hljs-string">&quot;red&quot;</span>, <span class="hljs-string">&quot;black&quot;</span>, <span class="hljs-string">&quot;white&quot;</span>, <span class="hljs-string">&quot;purple&quot;</span>, <span class="hljs-string">&quot;pink&quot;</span>, <span class="hljs-string">&quot;orange&quot;</span>, <span class="hljs-string">&quot;brown&quot;</span>, <span class="hljs-string">&quot;grey&quot;</span>]
data = []

<span class="hljs-keyword">for</span> i <span class="hljs-keyword">in</span> <span class="hljs-built_in">range</span>(<span class="hljs-number">10000</span>):
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
<span class="hljs-comment">#         -0.5705990742218152,</span>
<span class="hljs-comment">#         0.39844925120642083,</span>
<span class="hljs-comment">#         -0.8791287928610869,</span>
<span class="hljs-comment">#         0.024163154953680932,</span>
<span class="hljs-comment">#         0.6837669917169638</span>
<span class="hljs-comment">#     ],</span>
<span class="hljs-comment">#     &quot;color&quot;: &quot;purple&quot;,</span>
<span class="hljs-comment">#     &quot;tag&quot;: 7774,</span>
<span class="hljs-comment">#     &quot;color_tag&quot;: &quot;purple_7774&quot;</span>
<span class="hljs-comment"># }</span>

res = client.insert(
    collection_name=<span class="hljs-string">&quot;quick_setup&quot;</span>,
    data=data,
)

<span class="hljs-built_in">print</span>(res)

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;insert_count&quot;: 10000,</span>
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
<span class="hljs-comment">#         &quot;(9990 more items hidden)&quot;</span>
<span class="hljs-comment">#     ]</span>
<span class="hljs-comment"># }</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-comment">// 3. Insert randomly generated vectors into the collection</span>
List&lt;String&gt; colors = Arrays.asList(<span class="hljs-string">&quot;green&quot;</span>, <span class="hljs-string">&quot;blue&quot;</span>, <span class="hljs-string">&quot;yellow&quot;</span>, <span class="hljs-string">&quot;red&quot;</span>, <span class="hljs-string">&quot;black&quot;</span>, <span class="hljs-string">&quot;white&quot;</span>, <span class="hljs-string">&quot;purple&quot;</span>, <span class="hljs-string">&quot;pink&quot;</span>, <span class="hljs-string">&quot;orange&quot;</span>, <span class="hljs-string">&quot;brown&quot;</span>, <span class="hljs-string">&quot;grey&quot;</span>);
List&lt;JsonObject&gt; data = <span class="hljs-keyword">new</span> <span class="hljs-title class_">ArrayList</span>&lt;&gt;();
<span class="hljs-type">Gson</span> <span class="hljs-variable">gson</span> <span class="hljs-operator">=</span> <span class="hljs-keyword">new</span> <span class="hljs-title class_">Gson</span>();
<span class="hljs-keyword">for</span> (<span class="hljs-type">int</span> i=<span class="hljs-number">0</span>; i&lt;<span class="hljs-number">10000</span>; i++) {
    <span class="hljs-type">Random</span> <span class="hljs-variable">rand</span> <span class="hljs-operator">=</span> <span class="hljs-keyword">new</span> <span class="hljs-title class_">Random</span>();
    <span class="hljs-type">String</span> <span class="hljs-variable">current_color</span> <span class="hljs-operator">=</span> colors.get(rand.nextInt(colors.size()-<span class="hljs-number">1</span>));
    <span class="hljs-type">JsonObject</span> <span class="hljs-variable">row</span> <span class="hljs-operator">=</span> <span class="hljs-keyword">new</span> <span class="hljs-title class_">JsonObject</span>();
    row.addProperty(<span class="hljs-string">&quot;id&quot;</span>, (<span class="hljs-type">long</span>) i);
    row.add(<span class="hljs-string">&quot;vector&quot;</span>, gson.toJsonTree(Arrays.asList(rand.nextFloat(), rand.nextFloat(), rand.nextFloat(), rand.nextFloat(), rand.nextFloat())));
    row.addProperty(<span class="hljs-string">&quot;color_tag&quot;</span>, current_color + <span class="hljs-string">&quot;_&quot;</span> + (rand.nextInt(<span class="hljs-number">8999</span>) + <span class="hljs-number">1000</span>));
    data.add(row);
}

<span class="hljs-type">InsertResp</span> <span class="hljs-variable">insertR</span> <span class="hljs-operator">=</span> client.insert(InsertReq.builder()
        .collectionName(<span class="hljs-string">&quot;quick_setup&quot;</span>)
        .data(data)
        .build());
System.out.println(insertR.getInsertCnt());

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// 10000</span>
<button class="copy-code-btn"></button></code></pre>
<h2 id="Search-with-iterator" class="common-anchor-header">Búsqueda con iterador<button data-href="#Search-with-iterator" class="anchor-icon" translate="no">
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
    </button></h2><p>Los iteradores hacen que las búsquedas por similitud sean más escalables.</p>
<div class="language-python">
<p>Para buscar con un iterador, llama al método <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/ORM/Collection/search_iterator.md">search_iterator()</a>:</p>
</div>
<div class="language-java">
<p>Para buscar con un iterador, llame al método <a href="https://milvus.io/api-reference/java/v2.4.x/v1/QuerySearch/searchIterator.md">searchIterator()</a>:</p>
</div>
<ol>
<li><p>Inicialice el iterador de búsqueda para definir los parámetros de búsqueda y los campos de salida.</p></li>
<li><p>Utilice el método <strong>next()</strong> dentro de un bucle para paginar los resultados de la búsqueda.</p>
<ul>
<li><p>Si el método devuelve un array vacío, el bucle finaliza y no hay más páginas disponibles.</p></li>
<li><p>Todos los resultados llevan los campos de salida especificados.</p></li>
</ul></li>
<li><p>Llame manualmente al método <strong>close()</strong> para cerrar el iterador una vez que se hayan recuperado todos los datos.</p></li>
</ol>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> Collection,connections

<span class="hljs-comment"># 4. Search with iterator</span>
connections.connect(host=<span class="hljs-string">&quot;127.0.0.1&quot;</span>, port=<span class="hljs-number">19530</span>)
collection = Collection(<span class="hljs-string">&quot;quick_setup&quot;</span>)

query_vectors = [[<span class="hljs-number">0.3580376395471989</span>, -<span class="hljs-number">0.6023495712049978</span>, <span class="hljs-number">0.18414012509913835</span>, -<span class="hljs-number">0.26286205330961354</span>, <span class="hljs-number">0.9029438446296592</span>]]
search_params = {
    <span class="hljs-string">&quot;metric_type&quot;</span>: <span class="hljs-string">&quot;IP&quot;</span>,
    <span class="hljs-string">&quot;params&quot;</span>: {<span class="hljs-string">&quot;nprobe&quot;</span>: <span class="hljs-number">10</span>}
}

iterator = collection.search_iterator(
    data=query_vectors,
    anns_field=<span class="hljs-string">&quot;vector&quot;</span>,
    batch_size=<span class="hljs-number">10</span>,
    param=search_params,
    output_fields=[<span class="hljs-string">&quot;color_tag&quot;</span>],
    limit=<span class="hljs-number">300</span>
)
<span class="hljs-comment"># search 300 entities totally with 10 entities per page</span>

results = []

<span class="hljs-keyword">while</span> <span class="hljs-literal">True</span>:
    result = iterator.<span class="hljs-built_in">next</span>()
    <span class="hljs-keyword">if</span> <span class="hljs-keyword">not</span> result:
        iterator.close()
        <span class="hljs-keyword">break</span>
        
    results.extend(result)
    
    <span class="hljs-keyword">for</span> hit <span class="hljs-keyword">in</span> result:
        results.append(hit.to_dict())

<span class="hljs-built_in">print</span>(results)

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># [</span>
<span class="hljs-comment">#     {</span>
<span class="hljs-comment">#         &quot;id&quot;: 1756,</span>
<span class="hljs-comment">#         &quot;distance&quot;: 2.0642056465148926,</span>
<span class="hljs-comment">#         &quot;entity&quot;: {</span>
<span class="hljs-comment">#             &quot;color_tag&quot;: &quot;black_9109&quot;</span>
<span class="hljs-comment">#         }</span>
<span class="hljs-comment">#     },</span>
<span class="hljs-comment">#     {</span>
<span class="hljs-comment">#         &quot;id&quot;: 6488,</span>
<span class="hljs-comment">#         &quot;distance&quot;: 1.9437453746795654,</span>
<span class="hljs-comment">#         &quot;entity&quot;: {</span>
<span class="hljs-comment">#             &quot;color_tag&quot;: &quot;purple_8164&quot;</span>
<span class="hljs-comment">#         }</span>
<span class="hljs-comment">#     },</span>
<span class="hljs-comment">#     {</span>
<span class="hljs-comment">#         &quot;id&quot;: 3338,</span>
<span class="hljs-comment">#         &quot;distance&quot;: 1.9107104539871216,</span>
<span class="hljs-comment">#         &quot;entity&quot;: {</span>
<span class="hljs-comment">#             &quot;color_tag&quot;: &quot;brown_8121&quot;</span>
<span class="hljs-comment">#         }</span>
<span class="hljs-comment">#     }</span>
<span class="hljs-comment"># ]</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-comment">// 4. Search with iterators</span>
<span class="hljs-type">SearchIteratorReq</span> <span class="hljs-variable">iteratorReq</span> <span class="hljs-operator">=</span> SearchIteratorReq.builder()
        .collectionName(<span class="hljs-string">&quot;quick_setup&quot;</span>)
        .vectorFieldName(<span class="hljs-string">&quot;vector&quot;</span>)
        .batchSize(<span class="hljs-number">10L</span>)
        .vectors(Collections.singletonList(<span class="hljs-keyword">new</span> <span class="hljs-title class_">FloatVec</span>(Arrays.asList(<span class="hljs-number">0.3580376395471989f</span>, -<span class="hljs-number">0.6023495712049978f</span>, <span class="hljs-number">0.18414012509913835f</span>, -<span class="hljs-number">0.26286205330961354f</span>, <span class="hljs-number">0.9029438446296592f</span>))))
        .params(<span class="hljs-string">&quot;{\&quot;level\&quot;: 1}&quot;</span>)
        .metricType(IndexParam.MetricType.COSINE)
        .outputFields(Collections.singletonList(<span class="hljs-string">&quot;color_tag&quot;</span>))
        .topK(<span class="hljs-number">300</span>)
        .build();

<span class="hljs-type">SearchIterator</span> <span class="hljs-variable">searchIterator</span> <span class="hljs-operator">=</span> client.searchIterator(iteratorReq);

List&lt;QueryResultsWrapper.RowRecord&gt; results = <span class="hljs-keyword">new</span> <span class="hljs-title class_">ArrayList</span>&lt;&gt;();
<span class="hljs-keyword">while</span> (<span class="hljs-literal">true</span>) {
    List&lt;QueryResultsWrapper.RowRecord&gt; batchResults = searchIterator.next();
    <span class="hljs-keyword">if</span> (batchResults.isEmpty()) {
        searchIterator.close();
        <span class="hljs-keyword">break</span>;
    }

    results.addAll(batchResults);
}
System.out.println(results.size());

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// 300</span>
<button class="copy-code-btn"></button></code></pre>
<table class="language-python">
  <thead>
    <tr>
      <th>Parámetro</th>
      <th>Descripción</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code translate="no">data</code></td>
      <td>Una lista de incrustaciones vectoriales.<br/>Milvus busca las incrustaciones vectoriales más similares a las especificadas.</td>
    </tr>
    <tr>
      <td><code translate="no">anns_field</code></td>
      <td>El nombre del campo vectorial en la colección actual.</td>
    </tr>
    <tr>
      <td><code translate="no">batch_size</code></td>
      <td>El número de entidades a devolver cada vez que se llama a <code translate="no">next()</code> en el iterador actual.<br/>El valor por defecto es <strong>1000</strong>. Ajústelo a un valor adecuado para controlar el número de entidades a devolver por iteración.</td>
    </tr>
    <tr>
      <td><code translate="no">param</code></td>
      <td>Los parámetros específicos de esta operación.<br/><ul><li><code translate="no">metric_type</code>: El tipo de métrica aplicado a esta operación. Debe ser el mismo que el utilizado al indexar el campo vectorial especificado anteriormente. Los valores posibles son <strong>L2</strong>, <strong>IP</strong>, <strong>COSINE</strong>, <strong>JACCARD</strong>, <strong>HAMMING</strong>.</li><li><code translate="no">params</code>: Parámetros adicionales. Para más detalles, consulte <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/ORM/Collection/search_iterator.md">search_iterator()</a>.</li></ul></td>
    </tr>
    <tr>
      <td><code translate="no">output_fields</code></td>
      <td>Una lista de nombres de campo para incluir en cada entidad devuelta.<br/>El valor por defecto es <strong>None</strong>. Si no se especifica, sólo se incluye el campo principal.</td>
    </tr>
    <tr>
      <td><code translate="no">limit</code></td>
      <td>El número total de entidades que se devolverán.<br/>El valor predeterminado es <strong>-1</strong>, lo que indica que se devolverán todas las entidades coincidentes.</td>
    </tr>
  </tbody>
</table>
<table class="language-java">
  <thead>
    <tr>
      <th>Parámetro</th>
      <th>Descripción</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code translate="no">withCollectionName</code></td>
      <td>Establece el nombre de la colección. El nombre de la colección no puede estar vacío ni ser nulo.</td>
    </tr>
    <tr>
      <td><code translate="no">withVectorFieldName</code></td>
      <td>Establezca el nombre del campo del vector de destino. El nombre del campo no puede estar vacío ni ser nulo.</td>
    </tr>
    <tr>
      <td><code translate="no">withVectors</code></td>
      <td>Defina los vectores de destino. Se permiten hasta 16384 vectores.</td>
    </tr>
    <tr>
      <td><code translate="no">withBatchSize</code></td>
      <td>El número de entidades a devolver cada vez que se llama a <code translate="no">next()</code> en el iterador actual.<br/>El valor por defecto es <strong>1000</strong>. Establézcalo a un valor apropiado para controlar el número de entidades a devolver por iteración.</td>
    </tr>
    <tr>
      <td><code translate="no">withParams</code></td>
      <td>Especifica los parámetros de búsqueda en formato JSON. Para más información, consulte <a href="https://milvus.io/api-reference/java/v2.4.x/v1/QuerySearch/searchIterator.md">searchIterator()</a>.</td>
    </tr>
  </tbody>
</table>
<h2 id="Query-with-an-iterator" class="common-anchor-header">Consulta con un iterador<button data-href="#Query-with-an-iterator" class="anchor-icon" translate="no">
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
<p>Para consultar con un iterador, llame al método <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/ORM/Collection/query_iterator.md">query_iterator()</a>:</p>
</div>
<div class="language-java">
<p>Para buscar con un iterador, llame al método <a href="https://milvus.io/api-reference/java/v2.4.x/v1/QuerySearch/queryIterator.md">queryIterator()</a>:</p>
</div>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># 6. Query with iterator</span>
iterator = collection.query_iterator(
    batch_size=<span class="hljs-number">10</span>, <span class="hljs-comment"># Controls the size of the return each time you call next()</span>
    expr=<span class="hljs-string">&quot;color_tag like \&quot;brown_8\&quot;&quot;</span>,
    output_fields=[<span class="hljs-string">&quot;color_tag&quot;</span>]
)

results = []

<span class="hljs-keyword">while</span> <span class="hljs-literal">True</span>:
    result = iterator.<span class="hljs-built_in">next</span>()
    <span class="hljs-keyword">if</span> <span class="hljs-keyword">not</span> result:
        iterator.close()
        <span class="hljs-keyword">break</span>
        
    results.extend(result)
    
<span class="hljs-comment"># 8. Check the search results</span>
<span class="hljs-built_in">print</span>(<span class="hljs-built_in">len</span>(results))

<span class="hljs-built_in">print</span>(results[:<span class="hljs-number">3</span>])

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># [</span>
<span class="hljs-comment">#     {</span>
<span class="hljs-comment">#         &quot;color_tag&quot;: &quot;brown_8785&quot;,</span>
<span class="hljs-comment">#         &quot;id&quot;: 94</span>
<span class="hljs-comment">#     },</span>
<span class="hljs-comment">#     {</span>
<span class="hljs-comment">#         &quot;color_tag&quot;: &quot;brown_8568&quot;,</span>
<span class="hljs-comment">#         &quot;id&quot;: 176</span>
<span class="hljs-comment">#     },</span>
<span class="hljs-comment">#     {</span>
<span class="hljs-comment">#         &quot;color_tag&quot;: &quot;brown_8721&quot;,</span>
<span class="hljs-comment">#         &quot;id&quot;: 289</span>
<span class="hljs-comment">#     }</span>
<span class="hljs-comment"># ]</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-comment">// 5. Query with iterators</span>
<span class="hljs-type">QueryIterator</span> <span class="hljs-variable">queryIterator</span> <span class="hljs-operator">=</span> client.queryIterator(QueryIteratorReq.builder()
        .collectionName(<span class="hljs-string">&quot;quick_setup&quot;</span>)
        .expr(<span class="hljs-string">&quot;color_tag like \&quot;brown_8%\&quot;&quot;</span>)
        .batchSize(<span class="hljs-number">50L</span>)
        .outputFields(Arrays.asList(<span class="hljs-string">&quot;vector&quot;</span>, <span class="hljs-string">&quot;color_tag&quot;</span>))
        .build());

results.clear();
<span class="hljs-keyword">while</span> (<span class="hljs-literal">true</span>) {
    List&lt;QueryResultsWrapper.RowRecord&gt; batchResults = queryIterator.next();
    <span class="hljs-keyword">if</span> (batchResults.isEmpty()) {
        queryIterator.close();
        <span class="hljs-keyword">break</span>;
    }

    results.addAll(batchResults);
}

System.out.println(results.subList(<span class="hljs-number">0</span>, <span class="hljs-number">3</span>));

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// [</span>
<span class="hljs-comment">//  [color_tag:brown_8975, vector:[0.93425006, 0.42161798, 0.1603949, 0.86406225, 0.30063087], id:104],</span>
<span class="hljs-comment">//  [color_tag:brown_8292, vector:[0.075261295, 0.51725155, 0.13842249, 0.13178307, 0.90713704], id:793],</span>
<span class="hljs-comment">//  [color_tag:brown_8763, vector:[0.80366623, 0.6534371, 0.6446101, 0.094082, 0.1318503], id:1157]</span>
<span class="hljs-comment">// ]</span>

<button class="copy-code-btn"></button></code></pre>
<table class="language-python">
  <thead>
    <tr>
      <th>Parámetro</th>
      <th>Descripción</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code translate="no">batch_size</code></td>
      <td>El número de entidades a devolver cada vez que se llama a <code translate="no">next()</code> en el iterador actual.<br/>El valor por defecto es <strong>1000</strong>. Establézcalo a un valor apropiado para controlar el número de entidades a devolver por iteración.</td>
    </tr>
    <tr>
      <td><code translate="no">expr</code></td>
      <td>Una condición de filtrado escalar para filtrar las entidades coincidentes.<br/>El valor predeterminado es <strong>None</strong>, lo que indica que se ignora el filtrado escalar. Para crear una condición de filtrado escalar, consulte <a href="https://milvus.io/docs/boolean.md">Reglas de expresión booleana</a>.</td>
    </tr>
    <tr>
      <td><code translate="no">output_fields</code></td>
      <td>Una lista de nombres de campo para incluir en cada entidad devuelta.<br/>El valor por defecto es <strong>Ninguno</strong>. Si no se especifica, sólo se incluye el campo principal.</td>
    </tr>
    <tr>
      <td><code translate="no">limit</code></td>
      <td>El número total de entidades que se devolverán.<br/>El valor predeterminado es <strong>-1</strong>, lo que indica que se devolverán todas las entidades coincidentes.</td>
    </tr>
  </tbody>
</table>
<table class="language-java">
  <thead>
    <tr>
      <th>Parámetro</th>
      <th>Descripción</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code translate="no">withCollectionName</code></td>
      <td>Establece el nombre de la colección. El nombre de la colección no puede estar vacío ni ser nulo.</td>
    </tr>
    <tr>
      <td><code translate="no">withExpr</code></td>
      <td>Establezca la expresión para consultar las entidades. Para crear una condición de filtrado escalar, consulte <a href="https://milvus.io/docs/boolean.md">Reglas de expresión booleana</a>.</td>
    </tr>
    <tr>
      <td><code translate="no">withBatchSize</code></td>
      <td>El número de entidades a devolver cada vez que se llama a <code translate="no">next()</code> en el iterador actual.<br/>El valor por defecto es <strong>1000</strong>. Establézcalo a un valor apropiado para controlar el número de entidades a devolver por iteración.</td>
    </tr>
    <tr>
      <td><code translate="no">addOutField</code></td>
      <td>Especifica un campo escalar de salida (Opcional).</td>
    </tr>
  </tbody>
</table>
