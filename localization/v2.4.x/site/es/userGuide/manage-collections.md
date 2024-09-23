---
id: manage-collections.md
title: Gestionar cobros
---
<h1 id="Manage-Collections" class="common-anchor-header">Gestionar colecciones<button data-href="#Manage-Collections" class="anchor-icon" translate="no">
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
    </button></h1><p>Esta guía le guiará a través de la creación y gestión de colecciones utilizando el SDK de su elección.</p>
<h2 id="Before-you-start" class="common-anchor-header">Antes de empezar<button data-href="#Before-you-start" class="anchor-icon" translate="no">
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
<li><p>Ha instalado <a href="https://milvus.io/docs/install_standalone-docker.md">Milvus standalone</a> o <a href="https://milvus.io/docs/install_cluster-milvusoperator.md">Milvus cluster</a>.</p></li>
<li><p>Ha instalado los SDK preferidos. Puede elegir entre varios lenguajes, incluyendo <a href="https://milvus.io/docs/install-pymilvus.md">Python</a>, <a href="https://milvus.io/docs/install-java.md">Java</a>, <a href="https://milvus.io/docs/install-go.md">Go</a> y <a href="https://milvus.io/docs/install-node.md">Node.js</a>.</p></li>
</ul>
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
    </button></h2><p>En Milvus, usted almacena sus incrustaciones vectoriales en colecciones. Todas las incrustaciones vectoriales dentro de una colección comparten la misma dimensionalidad y métrica de distancia para medir la similitud.</p>
<p>Las colecciones Milvus soportan campos dinámicos (es decir, campos no predefinidos en el esquema) e incremento automático de claves primarias.</p>
<p>Para adaptarse a las distintas preferencias, Milvus ofrece dos métodos para crear una colección. Uno proporciona una configuración rápida, mientras que el otro permite una personalización detallada del esquema de la colección y de los parámetros del índice.</p>
<p>Además, puede ver, cargar, liberar y soltar una colección cuando sea necesario.</p>
<h2 id="Create-Collection" class="common-anchor-header">Crear colección<button data-href="#Create-Collection" class="anchor-icon" translate="no">
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
    </button></h2><p>Puede crear una colección de cualquiera de las siguientes maneras:</p>
<ul>
<li><p><strong>Configuración rápida</strong></p>
<p>De esta manera, puede crear una colección simplemente dándole un nombre y especificando el número de dimensiones de las incrustaciones vectoriales que se almacenarán en esta colección. Para más información, consulte <a href="/docs/es/manage-collections.md">Configuración rápida</a>.</p></li>
<li><p><strong>Configuración personalizada</strong></p>
<p>En lugar de dejar que In Milvus decida casi todo para su colección, puede determinar el <strong>esquema</strong> y los <strong>parámetros de índice</strong> de la colección por su cuenta. Para obtener más información, consulte <a href="/docs/es/manage-collections.md">Configuración personalizada</a>.</p></li>
</ul>
<h3 id="Quick-setup" class="common-anchor-header">Configuración rápida</h3><p>Con el gran salto en la industria de la IA como telón de fondo, la mayoría de los desarrolladores sólo necesitan una colección sencilla pero dinámica para empezar. Milvus permite una configuración rápida de dicha colección con sólo tres argumentos:</p>
<ul>
<li><p>Nombre de la colección a crear,</p></li>
<li><p>Dimensión de las incrustaciones vectoriales a insertar, y</p></li>
<li><p>Tipo de métrica utilizada para medir las similitudes entre las incrustaciones vectoriales.</p></li>
</ul>
<div class="language-python">
<p>Para una configuración rápida, utilice el método <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Collections/create_collection.md"><code translate="no">create_collection()</code></a> de la clase <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Client/MilvusClient.md"><code translate="no">MilvusClient</code></a> para crear una colección con el nombre y la dimensión especificados.</p>
</div>
<div class="language-java">
<p>Para una configuración rápida, utilice el método <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Collections/createCollection.md"><code translate="no">createCollection()</code></a> de la clase <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Client/MilvusClientV2.md"><code translate="no">MilvusClientV2</code></a> para crear una colección con el nombre y la dimensión especificados.</p>
</div>
<div class="language-javascript">
<p>Para una configuración rápida, utilice el método <a href="https://milvus.io/api-reference/node/v2.4.x/Collections/createCollection.md"><code translate="no">createCollection()</code></a> de la clase <a href="https://milvus.io/api-reference/node/v2.4.x/Client/MilvusClient.md"><code translate="no">MilvusClient</code></a> para crear una colección con el nombre y la dimensión especificados.</p>
</div>
<div class="language-shell">
<p>Para una configuración rápida, utilice el <a href="https://milvus.io/api-reference/restful/v2.4.x/v2/Collection%20(v2)/Create.md"><code translate="no">POST /v2/vectordb/collections/create</code></a> para crear una colección con el nombre y la dimensión especificados.</p>
</div>
<div class="multipleCode">
 <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a> <a href="#shell">cURL</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> MilvusClient, DataType

<span class="hljs-comment"># 1. Set up a Milvus client</span>
client = MilvusClient(
    uri=<span class="hljs-string">&quot;http://localhost:19530&quot;</span>
)

<span class="hljs-comment"># 2. Create a collection in quick setup mode</span>
client.create_collection(
    collection_name=<span class="hljs-string">&quot;quick_setup&quot;</span>,
    dimension=<span class="hljs-number">5</span>
)

res = client.get_load_state(
    collection_name=<span class="hljs-string">&quot;quick_setup&quot;</span>
)

<span class="hljs-built_in">print</span>(res)

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;state&quot;: &quot;&lt;LoadState: Loaded&gt;&quot;</span>
<span class="hljs-comment"># }</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.milvus.v2.client.ConnectConfig;
<span class="hljs-keyword">import</span> io.milvus.v2.client.MilvusClientV2;
<span class="hljs-keyword">import</span> io.milvus.v2.service.collection.request.GetLoadStateReq;
<span class="hljs-keyword">import</span> io.milvus.v2.service.collection.request.CreateCollectionReq;

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
    .build();

client.createCollection(quickSetupReq);

<span class="hljs-comment">// Thread.sleep(5000);</span>

<span class="hljs-type">GetLoadStateReq</span> <span class="hljs-variable">quickSetupLoadStateReq</span> <span class="hljs-operator">=</span> GetLoadStateReq.builder()
    .collectionName(<span class="hljs-string">&quot;quick_setup&quot;</span>)
    .build();

<span class="hljs-type">Boolean</span> <span class="hljs-variable">res</span> <span class="hljs-operator">=</span> client.getLoadState(quickSetupLoadStateReq);

System.out.println(res);

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// true</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript">address = <span class="hljs-string">&quot;http://localhost:19530&quot;</span>

<span class="hljs-comment">// 1. Set up a Milvus Client</span>
client = <span class="hljs-keyword">new</span> <span class="hljs-title class_">MilvusClient</span>({address});

<span class="hljs-comment">// 2. Create a collection in quick setup mode</span>
<span class="hljs-keyword">let</span> res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">createCollection</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;quick_setup&quot;</span>,
    <span class="hljs-attr">dimension</span>: <span class="hljs-number">5</span>,
});  

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">error_code</span>)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// Success</span>
<span class="hljs-comment">// </span>

res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">getLoadState</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;quick_setup&quot;</span>
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">state</span>)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// LoadStateLoaded</span>
<span class="hljs-comment">// </span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-shell">$ <span class="hljs-built_in">export</span> MILVUS_URI=<span class="hljs-string">&quot;localhost:19530&quot;</span>

$ curl -X POST <span class="hljs-string">&quot;http://<span class="hljs-variable">${MILVUS_URI}</span>/v2/vectordb/collections/create&quot;</span> \
-H <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \
-d <span class="hljs-string">&#x27;{
  &quot;collectionName&quot;: &quot;quick_setup&quot;,
  &quot;dimension&quot;: 5
}&#x27;</span>

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;code&quot;: 0,</span>
<span class="hljs-comment">#     &quot;data&quot;: {},</span>
<span class="hljs-comment"># }</span>

$ curl -X POST <span class="hljs-string">&quot;http://<span class="hljs-variable">${MILVUS_URI}</span>/v2/vectordb/collections/get_load_state&quot;</span> \
-H <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \
-d <span class="hljs-string">&#x27;{
  &quot;collectionName&quot;: &quot;quick_setup&quot;
}&#x27;</span>

<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;code&quot;: 0,</span>
<span class="hljs-comment">#     &quot;data&quot;: {</span>
<span class="hljs-comment">#         &quot;loadProgress&quot;: 100,</span>
<span class="hljs-comment">#         &quot;loadState&quot;: &quot;LoadStateLoaded&quot;</span>
<span class="hljs-comment">#     }</span>
<span class="hljs-comment"># }</span>
<button class="copy-code-btn"></button></code></pre>
<p>La colección generada en el código anterior contiene sólo dos campos: <code translate="no">id</code> (como clave primaria) y <code translate="no">vector</code> (como campo vectorial), con las opciones <code translate="no">auto_id</code> y <code translate="no">enable_dynamic_field</code> activadas por defecto.</p>
<ul>
<li><p><code translate="no">auto_id</code></p>
<p>Activar esta configuración garantiza que la clave primaria se incremente automáticamente. No es necesario proporcionar manualmente claves primarias durante la inserción de datos.</p></li>
<li><p><code translate="no">enable_dynamic_field</code></p>
<p>Cuando está activada, todos los campos, excepto <code translate="no">id</code> y <code translate="no">vector</code> en los datos que se van a insertar, se tratan como campos dinámicos. Estos campos adicionales se guardan como pares clave-valor dentro de un campo especial denominado <code translate="no">$meta</code>. Esta función permite incluir campos adicionales durante la inserción de datos.</p></li>
</ul>
<p>La colección indexada y cargada automáticamente a partir del código proporcionado está lista para la inserción inmediata de datos.</p>
<h3 id="Customized-setup" class="common-anchor-header">Configuración personalizada</h3><p>En lugar de dejar que Milvus decida casi todo para su colección, puede determinar el <strong>esquema</strong> y los <strong>parámetros de indexación</strong> de la colección por su cuenta.</p>
<h4 id="Step-1-Set-up-schema" class="common-anchor-header">Paso 1: Configurar el esquema</h4><p>Un esquema define la estructura de una colección. Dentro del esquema, tiene la opción de activar o desactivar <code translate="no">enable_dynamic_field</code>, añadir campos predefinidos y establecer atributos para cada campo. Para obtener una explicación detallada del concepto y de los tipos de datos disponibles, consulte <a href="/docs/es/schema.md">Explicación del esquema</a>.</p>
<div class="language-python">
<p>Para configurar un esquema, utilice <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Collections/create_schema.md"><code translate="no">create_schema()</code></a> para crear un objeto de esquema y <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/CollectionSchema/add_field.md"><code translate="no">add_field()</code></a> para añadir campos al esquema.</p>
</div>
<div class="language-java">
<p>Para configurar un esquema, utilice <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Collections/createSchema.md"><code translate="no">createSchema()</code></a> para crear un objeto de esquema y <a href="https://milvus.io/api-reference/java/v2.4.x/v2/CollectionSchema/addField.md"><code translate="no">addField()</code></a> para añadir campos al esquema.</p>
</div>
<div class="language-javascript">
<p>Para configurar un esquema, utilice <a href="https://milvus.io/api-reference/node/v2.4.x/Collections/createCollection.md"><code translate="no">createCollection()</code></a>.</p>
</div>
<div class="language-shell">
<p>Para configurar un esquema, debe definir un objeto JSON que siga el formato de esquema que se muestra en la página de referencia del punto final de la API <a href="https://milvus.io/api-reference/restful/v2.4.x/v2/Collection%20(v2)/Create.md"><code translate="no">POST /v2/vectordb/collections/create</code></a> página de referencia del punto final de la API.</p>
</div>
<div class="multipleCode">
 <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a> <a href="#shell">cURL</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># 3. Create a collection in customized setup mode</span>

<span class="hljs-comment"># 3.1. Create schema</span>
schema = MilvusClient.create_schema(
    auto_id=<span class="hljs-literal">False</span>,
    enable_dynamic_field=<span class="hljs-literal">True</span>,
)

<span class="hljs-comment"># 3.2. Add fields to schema</span>
schema.add_field(field_name=<span class="hljs-string">&quot;my_id&quot;</span>, datatype=DataType.INT64, is_primary=<span class="hljs-literal">True</span>)
schema.add_field(field_name=<span class="hljs-string">&quot;my_vector&quot;</span>, datatype=DataType.FLOAT_VECTOR, dim=<span class="hljs-number">5</span>)
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.milvus.v2.common.DataType;
<span class="hljs-keyword">import</span> io.milvus.v2.service.collection.request.CreateCollectionReq;

<span class="hljs-comment">// 3. Create a collection in customized setup mode</span>

<span class="hljs-comment">// 3.1 Create schema</span>
CreateCollectionReq.<span class="hljs-type">CollectionSchema</span> <span class="hljs-variable">schema</span> <span class="hljs-operator">=</span> client.createSchema();

<span class="hljs-comment">// 3.2 Add fields to schema</span>
schema.addField(AddFieldReq.builder()
    .fieldName(<span class="hljs-string">&quot;my_id&quot;</span>)
    .dataType(DataType.Int64)
    .isPrimaryKey(<span class="hljs-literal">true</span>)
    .autoID(<span class="hljs-literal">false</span>)
    .build());

schema.addField(AddFieldReq.builder()
    .fieldName(<span class="hljs-string">&quot;my_vector&quot;</span>)
    .dataType(DataType.FloatVector)
    .dimension(<span class="hljs-number">5</span>)
    .build());
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-comment">// 3. Create a collection in customized setup mode</span>
<span class="hljs-comment">// 3.1 Define fields</span>
<span class="hljs-keyword">const</span> fields = [
    {
        <span class="hljs-attr">name</span>: <span class="hljs-string">&quot;my_id&quot;</span>,
        <span class="hljs-attr">data_type</span>: <span class="hljs-title class_">DataType</span>.<span class="hljs-property">Int64</span>,
        <span class="hljs-attr">is_primary_key</span>: <span class="hljs-literal">true</span>,
        <span class="hljs-attr">auto_id</span>: <span class="hljs-literal">false</span>
    },
    {
        <span class="hljs-attr">name</span>: <span class="hljs-string">&quot;my_vector&quot;</span>,
        <span class="hljs-attr">data_type</span>: <span class="hljs-title class_">DataType</span>.<span class="hljs-property">FloatVector</span>,
        <span class="hljs-attr">dim</span>: <span class="hljs-number">5</span>
    },
]
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-shell"><span class="hljs-keyword">export</span> fields=<span class="hljs-string">&#x27;[{ \
    &quot;fieldName&quot;: &quot;my_id&quot;, \
    &quot;dataType&quot;: &quot;Int64&quot;, \
    &quot;isPrimary&quot;: true \
}, \
{ \
    &quot;fieldName&quot;: &quot;my_vector&quot;, \
    &quot;dataType&quot;: &quot;FloatVector&quot;, \
    &quot;elementTypeParams&quot;: { \
        &quot;dim&quot;: 5 \
    } \
}]&#x27;</span>
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
      <td><code translate="no">auto_id</code></td>
      <td>Determina si el campo primario se incrementa automáticamente.<br/>Si se establece en <strong>True</strong>, el campo primario se incrementa automáticamente. En este caso, el campo primario no debe incluirse en los datos a insertar para evitar errores. Los IDs autogenerados tienen una longitud fija y no pueden ser alterados.</td>
    </tr>
    <tr>
      <td><code translate="no">enable_dynamic_field</code></td>
      <td>Determina si Milvus guarda los valores de los campos no definidos en un campo dinámico si los datos que se insertan en la colección de destino incluyen campos que no están definidos en el esquema de la colección.<br/>Cuando se establece en <strong>True</strong>, Milvus creará un campo llamado <strong>$meta</strong> para almacenar cualquier campo no definido y sus valores de los datos que se insertan.</td>
    </tr>
    <tr>
      <td><code translate="no">field_name</code></td>
      <td>El nombre del campo.</td>
    </tr>
    <tr>
      <td><code translate="no">datatype</code></td>
      <td>El tipo de datos del campo. Para obtener una lista de los tipos de datos disponibles, consulte <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Collections/DataType.md">Tipo de datos</a>.</td>
    </tr>
    <tr>
      <td><code translate="no">is_primary</code></td>
      <td>Si el campo actual es el campo primario de una colección.<br/>Cada colección sólo tiene un campo primario. Un campo primario debe ser del tipo <strong>DataType</strong> <strong>.INT64</strong> o del tipo <strong>DataType.VARCHAR</strong>.</td>
    </tr>
    <tr>
      <td><code translate="no">dim</code></td>
      <td>La dimensión de las incrustaciones vectoriales.<br/>Es obligatorio para un campo de tipo <strong>DataType</strong> <strong>.FLOAT_VECTOR</strong>, <strong>DataType.BINARY_VECTOR</strong>, <strong>DataType.FLOAT16_VECTOR</strong> o <strong>DataType.BFLOAT16_VECTOR</strong>. Si utiliza <strong>DataType.SPARSE_FLOAT_VECTOR</strong>, omita este parámetro.</td>
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
      <td><code translate="no">fieldName</code></td>
      <td>Nombre del campo.</td>
    </tr>
    <tr>
      <td><code translate="no">dataType</code></td>
      <td>Tipo de datos del campo. Para obtener una lista de los tipos de datos disponibles, consulte <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Collections/DataType.md">TipoDatos</a>.</td>
    </tr>
    <tr>
      <td><code translate="no">isPrimaryKey</code></td>
      <td>Si el campo actual es el campo primario de una colección.<br/>Cada colección sólo tiene un campo primario. Un campo primario debe ser del tipo <strong>DataType</strong> <strong>.Int64</strong> o del tipo <strong>DataType.VarChar</strong>.</td>
    </tr>
    <tr>
      <td><code translate="no">autoID</code></td>
      <td>Si permite que el campo primario se incremente automáticamente.<br/>Si se establece en <strong>true</strong>, el campo primario se incrementa automáticamente. En este caso, el campo primario no debe incluirse en los datos a insertar para evitar errores.</td>
    </tr>
    <tr>
      <td><code translate="no">dimension</code></td>
      <td>La dimensión de las incrustaciones vectoriales.<br/>Es obligatorio para un campo de tipo <strong>DataType</strong> <strong>.FloatVector</strong>, <strong>DataType.BinaryVector</strong>, <strong>DataType.Float16Vector</strong> o <strong>DataType.BFloat16Vector</strong>.</td>
    </tr>
  </tbody>
</table>
<table class="language-javascript">
  <thead>
    <tr>
      <th>Parámetro</th>
      <th>Descripción</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code translate="no">name</code></td>
      <td>Nombre del campo.</td>
    </tr>
    <tr>
      <td><code translate="no">data_type</code></td>
      <td>Tipo de datos del campo. Para obtener una enumeración de todos los tipos de datos disponibles, consulte <a href="https://milvus.io/api-reference/node/v2.4.x/Collections/DataType.md">TipoDatos</a>.</td>
    </tr>
    <tr>
      <td><code translate="no">is_primary_key</code></td>
      <td>Si el campo actual es el campo primario de una colección.<br/>Cada colección sólo tiene un campo primario. Un campo primario debe ser del tipo <strong>DataType</strong> <strong>.INT64</strong> o del tipo <strong>DataType.VARCHAR</strong>.</td>
    </tr>
    <tr>
      <td><code translate="no">auto_id</code></td>
      <td>Si el campo primario se incrementa automáticamente al insertar datos en esta colección.<br/>El valor por defecto es <strong>False</strong>. Si se establece en <strong>True</strong>, el campo primario se incrementa automáticamente. Omita este parámetro si necesita configurar una colección con un esquema personalizado.</td>
    </tr>
    <tr>
      <td><code translate="no">dim</code></td>
      <td>La dimensionalidad del campo de la colección que contiene las incrustaciones vectoriales.<br/>El valor debe ser un número entero mayor que 1 y suele estar determinado por el modelo que se utiliza para generar incrustaciones vectoriales.</td>
    </tr>
  </tbody>
</table>
<table class="language-shell">
  <thead>
    <tr>
      <th>Parámetro</th>
      <th>Descripción</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code translate="no">fieldName</code></td>
      <td>El nombre del campo que se va a crear en la colección de destino.</td>
    </tr>
    <tr>
      <td><code translate="no">dataType</code></td>
      <td>El tipo de datos de los valores del campo.</td>
    </tr>
    <tr>
      <td><code translate="no">isPrimary</code></td>
      <td>Si el campo actual es el campo primario. Si se establece en <code translate="no">True</code>, el campo actual será el campo primario.</td>
    </tr>
    <tr>
      <td><code translate="no">elementTypeParams</code></td>
      <td>Parámetros de campo adicionales.</td>
    </tr>
    <tr>
      <td><code translate="no">dim</code></td>
      <td>Un parámetro opcional para los campos FloatVector o BinaryVector que determina la dimensión del vector.</td>
    </tr>
  </tbody>
</table>
<h4 id="Step-2-Set-up-index-parameters" class="common-anchor-header">Paso 2: Configurar parámetros de índice</h4><p>Los parámetros de índice dictan cómo Milvus organiza sus datos dentro de una colección. Puede adaptar el proceso de indexación para campos específicos ajustando sus <code translate="no">metric_type</code> y <code translate="no">index_type</code>. Para el campo vectorial, tiene la flexibilidad de seleccionar <code translate="no">COSINE</code>, <code translate="no">L2</code>, <code translate="no">IP</code>, <code translate="no">HAMMING</code>, o <code translate="no">JACCARD</code> como <code translate="no">metric_type</code>, dependiendo del tipo de vectores con los que esté trabajando. Para más información, consulte <a href="/docs/es/metric.md">Métricas de similitud</a>.</p>
<div class="language-python">
<p>Para configurar los parámetros de índice, utilice <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Management/prepare_index_params.md"><code translate="no">prepare_index_params()</code></a> para preparar los parámetros del índice y <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Management/add_index.md"><code translate="no">add_index()</code></a> para añadir el índice.</p>
</div>
<div class="language-java">
<p>Para configurar parámetros de índice, utilice <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Management/IndexParam.md">IndexParam</a>.</p>
</div>
<div class="language-javascript">
<p>Para configurar parámetros de índice, utilice <a href="https://milvus.io/api-reference/node/v2.4.x/Management/createIndex.md"><code translate="no">createIndex()</code></a>.</p>
</div>
<div class="language-shell">
<p>Para configurar parámetros de índice, debe definir un objeto JSON que siga el formato de parámetros de índice que se muestra en la página de referencia del punto final de la API <a href="https://milvus.io/api-reference/restful/v2.4.x/v2/Collection%20(v2)/Create.md"><code translate="no">POST /v2/vectordb/collections/create</code></a> página de referencia del punto final de la API.</p>
</div>
<div class="multipleCode">
 <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a> <a href="#shell">cURL</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-meta"># 3.3. Prepare index parameters</span>
index_params = client.prepare_index_params()

<span class="hljs-meta"># 3.4. Add indexes</span>
index_params.add_index(
    field_name=<span class="hljs-string">&quot;my_id&quot;</span>,
    index_type=<span class="hljs-string">&quot;STL_SORT&quot;</span>
)

index_params.add_index(
    field_name=<span class="hljs-string">&quot;my_vector&quot;</span>, 
    index_type=<span class="hljs-string">&quot;IVF_FLAT&quot;</span>,
    metric_type=<span class="hljs-string">&quot;IP&quot;</span>,
    <span class="hljs-keyword">params</span>={ <span class="hljs-string">&quot;nlist&quot;</span>: <span class="hljs-number">128</span> }
)
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.milvus.v2.common.IndexParam;

<span class="hljs-comment">// 3.3 Prepare index parameters</span>
<span class="hljs-type">IndexParam</span> <span class="hljs-variable">indexParamForIdField</span> <span class="hljs-operator">=</span> IndexParam.builder()
    .fieldName(<span class="hljs-string">&quot;my_id&quot;</span>)
    .indexType(IndexParam.IndexType.STL_SORT)
    .build();

<span class="hljs-type">IndexParam</span> <span class="hljs-variable">indexParamForVectorField</span> <span class="hljs-operator">=</span> IndexParam.builder()
    .fieldName(<span class="hljs-string">&quot;my_vector&quot;</span>)
    .indexType(IndexParam.IndexType.IVF_FLAT)
    .metricType(IndexParam.MetricType.L2)
    .extraParams(Map.of(<span class="hljs-string">&quot;nlist&quot;</span>, <span class="hljs-number">1024</span>))
    .build();

List&lt;IndexParam&gt; indexParams = <span class="hljs-keyword">new</span> <span class="hljs-title class_">ArrayList</span>&lt;&gt;();
indexParams.add(indexParamForIdField);
indexParams.add(indexParamForVectorField);
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-comment">// 3.2 Prepare index parameters</span>
<span class="hljs-keyword">const</span> index_params = [{
    field_name: <span class="hljs-string">&quot;my_id&quot;</span>,
    index_type: <span class="hljs-string">&quot;STL_SORT&quot;</span>
},{
    field_name: <span class="hljs-string">&quot;my_vector&quot;</span>,
    index_type: <span class="hljs-string">&quot;IVF_FLAT&quot;</span>,
    metric_type: <span class="hljs-string">&quot;IP&quot;</span>,
    <span class="hljs-keyword">params</span>: { nlist: <span class="hljs-number">1024</span>}
}]
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-shell"><span class="hljs-keyword">export</span> indexParams=<span class="hljs-string">&#x27;[{ \
    &quot;fieldName&quot;: &quot;my_id&quot;, \
    &quot;indexName&quot;: &quot;my_id&quot;, \
    &quot;params&quot;: { \
        &quot;index_type&quot;: &quot;SLT_SORT&quot; \
  } \
}, { \
    &quot;fieldName&quot;: &quot;my_vector&quot;, \
    &quot;metricType&quot;: &quot;COSINE&quot;, \
    &quot;indexName&quot;: &quot;my_vector&quot;, \
    &quot;params&quot;: { \
        &quot;index_type&quot;: &quot;IVF_FLAT&quot;, \
        &quot;nlist&quot;: 1024 \
  } \
}]&#x27;</span>
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
      <td><code translate="no">field_name</code></td>
      <td>El nombre del archivo de destino al que se aplica este objeto.</td>
    </tr>
    <tr>
      <td><code translate="no">index_type</code></td>
      <td>El nombre del algoritmo utilizado para ordenar los datos en el campo específico. Para conocer los algoritmos aplicables, consulte <a href="https://milvus.io/docs/index.md">Índice en memoria</a> e <a href="https://milvus.io/docs/disk_index.md">Índice en disco</a>.</td>
    </tr>
    <tr>
      <td><code translate="no">metric_type</code></td>
      <td>El algoritmo que se utiliza para medir la similitud entre vectores. Los valores posibles son <strong>IP</strong>, <strong>L2</strong>, <strong>COSINE</strong>, <strong>JACCARD</strong>, <strong>HAMMING</strong>. Sólo está disponible cuando el campo especificado es un campo vectorial. Para más información, consulte <a href="https://milvus.io/docs/index.md#Indexes-supported-in-Milvus">Índices soportados en Milvus</a>.</td>
    </tr>
    <tr>
      <td><code translate="no">params</code></td>
      <td>Los parámetros de ajuste fino para el tipo de índice especificado. Para más información sobre posibles claves y rangos de valores, consulte <a href="https://milvus.io/docs/index.md">Índice en memoria</a>.</td>
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
      <td><code translate="no">fieldName</code></td>
      <td>El nombre del campo de destino al que se aplica este objeto IndexParam.</td>
    </tr>
    <tr>
      <td><code translate="no">indexType</code></td>
      <td>El nombre del algoritmo utilizado para ordenar los datos en el campo específico. Para conocer los algoritmos aplicables, consulte <a href="https://milvus.io/docs/index.md">Índice en memoria</a> e <a href="https://milvus.io/docs/disk_index.md">Índice en disco</a>.</td>
    </tr>
    <tr>
      <td><code translate="no">metricType</code></td>
      <td>La métrica de distancia que se utilizará para el índice. Los valores posibles son <strong>IP</strong>, <strong>L2</strong>, <strong>COSINE</strong>, <strong>JACCARD</strong>, <strong>HAMMING</strong>.</td>
    </tr>
    <tr>
      <td><code translate="no">extraParams</code></td>
      <td>Parámetros de índice adicionales. Para más información, consulte <a href="https://milvus.io/docs/index.md">Índice en memoria</a> e <a href="https://milvus.io/docs/disk_index.md">Índice en disco</a>.</td>
    </tr>
  </tbody>
</table>
<table class="language-javascript">
  <thead>
    <tr>
      <th>Parámetro</th>
      <th>Descripción</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code translate="no">field_name</code></td>
      <td>Nombre del campo de destino sobre el que se va a crear un índice.</td>
    </tr>
    <tr>
      <td><code translate="no">index_type</code></td>
      <td>El nombre del algoritmo utilizado para ordenar los datos en el campo específico. Para conocer los algoritmos aplicables, consulte <a href="https://milvus.io/docs/index.md">Índice en memoria</a> e <a href="https://milvus.io/docs/disk_index.md">Índice en disco</a>.</td>
    </tr>
    <tr>
      <td><code translate="no">metric_type</code></td>
      <td>El algoritmo que se utiliza para medir la similitud entre vectores. Los valores posibles son <strong>IP</strong>, <strong>L2</strong>, <strong>COSINE</strong>, <strong>JACCARD</strong>, <strong>HAMMING</strong>. Sólo está disponible cuando el campo especificado es un campo vectorial. Para más información, consulte <a href="https://milvus.io/docs/index.md#Indexes-supported-in-Milvus">Índices soportados en Milvus</a>.</td>
    </tr>
    <tr>
      <td><code translate="no">params</code></td>
      <td>Los parámetros de ajuste fino para el tipo de índice especificado. Para más información sobre posibles claves y rangos de valores, consulte <a href="https://milvus.io/docs/index.md">Índice en memoria</a>.</td>
    </tr>
  </tbody>
</table>
<table class="language-shell">
  <thead>
    <tr>
      <th>Parámetro</th>
      <th>Descripción</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code translate="no">fieldName</code></td>
      <td>El nombre del campo de destino sobre el que se va a crear un índice.</td>
    </tr>
    <tr>
      <td><code translate="no">indexName</code></td>
      <td>Nombre del índice que se va a crear. El valor predeterminado es el nombre del campo de destino.</td>
    </tr>
    <tr>
      <td><code translate="no">metricType</code></td>
      <td>El algoritmo que se utiliza para medir la similitud entre vectores. Los valores posibles son <strong>IP</strong>, <strong>L2</strong>, <strong>COSINE</strong>, <strong>JACCARD</strong>, <strong>HAMMING</strong>. Sólo está disponible cuando el campo especificado es un campo vectorial. Para más información, consulte <a href="https://milvus.io/docs/index.md#Indexes-supported-in-Milvus">Índices soportados en Milvus</a>.</td>
    </tr>
    <tr>
      <td><code translate="no">params</code></td>
      <td>El tipo de índice y los ajustes relacionados. Para más detalles, consulte <a href="https://milvus.io/docs/index.md">Índice en memoria</a>.</td>
    </tr>
    <tr>
      <td><code translate="no">params.index_type</code></td>
      <td>El tipo de índice a crear.</td>
    </tr>
    <tr>
      <td><code translate="no">params.nlist</code></td>
      <td>El número de unidades de cluster. Esto se aplica a los tipos de índice relacionados con IVF.</td>
    </tr>
  </tbody>
</table>
<p>El fragmento de código anterior muestra cómo configurar los parámetros de índice para un campo vectorial y un campo escalar, respectivamente. Para el campo vectorial, establezca tanto el tipo métrico como el tipo de índice. Para un campo escalar, establezca sólo el tipo de índice. Se recomienda crear un índice para el campo vectorial y cualquier campo escalar que se utilice con frecuencia para filtrar.</p>
<h4 id="Step-3-Create-the-collection" class="common-anchor-header">Paso 3: Crear la colección</h4><p>Tiene la opción de crear una colección y un archivo de índice por separado o crear una colección con el índice cargado simultáneamente en el momento de la creación.</p>
<div class="language-python">
<p>Utilice <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Collections/create_collection.md">create_collection()</a> para crear una colección con los parámetros de esquema e índice especificados y <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Management/get_load_state.md">get_load_state()</a> para comprobar el estado de carga de la colección.</p>
</div>
<div class="language-java">
<p>Utilice <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Collections/createCollection.md">createCollection()</a> para crear una colección con los parámetros de esquema e índice especificados y <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Management/getLoadState.md">getLoadState()</a> para comprobar el estado de carga de la colección.</p>
</div>
<div class="language-javascript">
<p>Utilice <a href="https://milvus.io/api-reference/node/v2.4.x/Collections/createCollection.md">createCollection()</a> para crear una colección con los parámetros de esquema e índice especificados y <a href="https://milvus.io/api-reference/node/v2.4.x/Management/getLoadState.md">getLoadState()</a> para comprobar el estado de carga de la colección.</p>
</div>
<ul>
<li><p><strong>Crear una colección con el índice cargado simultáneamente a la creación.</strong></p>
<p><div class="multipleCode">
<a href="#python">Python </a><a href="#java">Java</a><a href="#javascript">Node.js</a><a href="#shell">cURL</a></div></p>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># 3.5. Create a collection with the index loaded simultaneously</span>
client.create_collection(
    collection_name=<span class="hljs-string">&quot;customized_setup_1&quot;</span>,
    schema=schema,
    index_params=index_params
)

time.sleep(<span class="hljs-number">5</span>)

res = client.get_load_state(
    collection_name=<span class="hljs-string">&quot;customized_setup_1&quot;</span>
)

<span class="hljs-built_in">print</span>(res)

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;state&quot;: &quot;&lt;LoadState: Loaded&gt;&quot;</span>
<span class="hljs-comment"># }</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.milvus.v2.service.collection.request.CreateCollectionReq;
<span class="hljs-keyword">import</span> io.milvus.v2.service.collection.request.GetLoadStateReq;

<span class="hljs-comment">// 3.4 Create a collection with schema and index parameters</span>
<span class="hljs-type">CreateCollectionReq</span> <span class="hljs-variable">customizedSetupReq1</span> <span class="hljs-operator">=</span> CreateCollectionReq.builder()
    .collectionName(<span class="hljs-string">&quot;customized_setup_1&quot;</span>)
    .collectionSchema(schema)
    .indexParams(indexParams)
    .build();

client.createCollection(customizedSetupReq1);

<span class="hljs-comment">// Thread.sleep(5000);</span>

<span class="hljs-comment">// 3.5 Get load state of the collection</span>
<span class="hljs-type">GetLoadStateReq</span> <span class="hljs-variable">customSetupLoadStateReq1</span> <span class="hljs-operator">=</span> GetLoadStateReq.builder()
    .collectionName(<span class="hljs-string">&quot;customized_setup_1&quot;</span>)
    .build();

res = client.getLoadState(customSetupLoadStateReq1);

System.out.println(res);

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// true</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-comment">// 3.3 Create a collection with fields and index parameters</span>
res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">createCollection</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;customized_setup_1&quot;</span>,
    <span class="hljs-attr">fields</span>: fields,
    <span class="hljs-attr">index_params</span>: index_params,
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">error_code</span>)  

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// Success</span>
<span class="hljs-comment">// </span>

res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">getLoadState</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;customized_setup_1&quot;</span>
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">state</span>)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// LoadStateLoaded</span>
<span class="hljs-comment">//   </span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-shell">$ curl -X POST <span class="hljs-string">&quot;http://<span class="hljs-variable">${MILVUS_URI}</span>/v2/vectordb/collections/create&quot;</span> \
-H <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \
-d <span class="hljs-string">&#x27;{
    &quot;collectionName&quot;: &quot;customized_setup_1&quot;,
    &quot;schema&quot;: {
        &quot;autoId&quot;: false,
        &quot;enabledDynamicField&quot;: false,
        &quot;fields&quot;: [
            {
                &quot;fieldName&quot;: &quot;my_id&quot;,
                &quot;dataType&quot;: &quot;Int64&quot;,
                &quot;isPrimary&quot;: true
            },
            {
                &quot;fieldName&quot;: &quot;my_vector&quot;,
                &quot;dataType&quot;: &quot;FloatVector&quot;,
                &quot;elementTypeParams&quot;: {
                    &quot;dim&quot;: &quot;5&quot;
                }
            }
        ]
    },
    &quot;indexParams&quot;: [
        {
            &quot;fieldName&quot;: &quot;my_vector&quot;,
            &quot;metricType&quot;: &quot;COSINE&quot;,
            &quot;indexName&quot;: &quot;my_vector&quot;,
            &quot;params&quot;: {
                &quot;index_type&quot;: &quot;IVF_FLAT&quot;,
                &quot;nlist&quot;: &quot;1024&quot;
            }
        },
        {
            &quot;fieldName&quot;: &quot;my_id&quot;,
            &quot;indexName&quot;: &quot;my_id&quot;,
            &quot;params&quot;: {
                &quot;index_type&quot;: &quot;STL_SORT&quot;
            }            
        }
    ]
}&#x27;</span>

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;code&quot;: 0,</span>
<span class="hljs-comment">#     &quot;data&quot;: {},</span>
<span class="hljs-comment"># }</span>

$ curl -X POST <span class="hljs-string">&quot;http://<span class="hljs-variable">${MILVUS_URI}</span>/v2/vectordb/collections/get_load_state&quot;</span> \
-H <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \
-d <span class="hljs-string">&#x27;{
    &quot;collectionName&quot;: &quot;customized_setup_1&quot;
}&#x27;</span>

<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;code&quot;: 0,</span>
<span class="hljs-comment">#     &quot;data&quot;: {</span>
<span class="hljs-comment">#         &quot;loadProgress&quot;: 100,</span>
<span class="hljs-comment">#         &quot;loadState&quot;: &quot;LoadStateLoaded&quot;</span>
<span class="hljs-comment">#     }</span>
<span class="hljs-comment"># }</span>
<button class="copy-code-btn"></button></code></pre>
<p>La colección creada anteriormente se carga automáticamente. Para obtener más información sobre cómo cargar y liberar una colección, consulte <a href="/docs/es/manage-collections.md#Load--Release-Collection">Cargar y liberar colección</a>.</p></li>
<li><p><strong>Cree una colección y un archivo de índice por separado.</strong></p>
<p><div class="multipleCode">
<a href="#python">Python </a><a href="#java">Java</a><a href="#javascript">Node.js</a><a href="#shell">cURL</a></div></p>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># 3.6. Create a collection and index it separately</span>
client.create_collection(
    collection_name=<span class="hljs-string">&quot;customized_setup_2&quot;</span>,
    schema=schema,
)

res = client.get_load_state(
    collection_name=<span class="hljs-string">&quot;customized_setup_2&quot;</span>
)

<span class="hljs-built_in">print</span>(res)

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;state&quot;: &quot;&lt;LoadState: NotLoad&gt;&quot;</span>
<span class="hljs-comment"># }</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-comment">// 3.6 Create a collection and index it separately</span>
<span class="hljs-type">CreateCollectionReq</span> <span class="hljs-variable">customizedSetupReq2</span> <span class="hljs-operator">=</span> CreateCollectionReq.builder()
    .collectionName(<span class="hljs-string">&quot;customized_setup_2&quot;</span>)
    .collectionSchema(schema)
    .build();

client.createCollection(customizedSetupReq2);
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-comment">// 3.4 Create a collection and index it seperately</span>
res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">createCollection</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;customized_setup_2&quot;</span>,
    <span class="hljs-attr">fields</span>: fields,
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">error_code</span>)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// Success</span>
<span class="hljs-comment">// </span>

res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">getLoadState</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;customized_setup_2&quot;</span>
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">state</span>)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// LoadStateNotLoad</span>
<span class="hljs-comment">// </span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-shell">$ curl -X POST <span class="hljs-string">&quot;http://<span class="hljs-variable">${MILVUS_URI}</span>/v2/vectordb/collections/create&quot;</span> \
-H <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \
-d <span class="hljs-string">&#x27;{
    &quot;collectionName&quot;: &quot;customized_setup_2&quot;,
    &quot;schema&quot;: {
        &quot;autoId&quot;: false,
        &quot;enabledDynamicField&quot;: false,
        &quot;fields&quot;: [
            {
                &quot;fieldName&quot;: &quot;my_id&quot;,
                &quot;dataType&quot;: &quot;Int64&quot;,
                &quot;isPrimary&quot;: true
            },
            {
                &quot;fieldName&quot;: &quot;my_vector&quot;,
                &quot;dataType&quot;: &quot;FloatVector&quot;,
                &quot;elementTypeParams&quot;: {
                    &quot;dim&quot;: &quot;5&quot;
                }
            }
        ]
        
    }
}&#x27;</span>

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;code&quot;: 0,</span>
<span class="hljs-comment">#     &quot;data&quot;: {},</span>
<span class="hljs-comment"># }</span>

$ curl -X POST <span class="hljs-string">&quot;http://<span class="hljs-variable">${MILVUS_URI}</span>/v2/vectordb/collections/get_load_state&quot;</span> \
-H <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \
-d <span class="hljs-string">&#x27;{
    &quot;collectionName&quot;: &quot;customized_setup_2&quot;
}&#x27;</span>

<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;code&quot;: 0,</span>
<span class="hljs-comment">#     &quot;data&quot;: {</span>
<span class="hljs-comment">#         &quot;loadState&quot;: &quot;LoadStateNotLoaded&quot;</span>
<span class="hljs-comment">#     }</span>
<span class="hljs-comment"># }</span>
<button class="copy-code-btn"></button></code></pre>
<p>La colección creada anteriormente no se carga automáticamente. Puede crear un índice para la colección de la siguiente manera. La creación de un índice para la colección de forma independiente no carga automáticamente la colección. Para más detalles, consulte <a href="/docs/es/manage-collections.md#Load--Release-Collection">Cargar y liberar colección</a>.</p>
<p><table class="language-python">
<thead>
<tr>
<th>Parámetro</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td><code translate="no">collection_name</code></td>
<td>El nombre de la colección.</td>
</tr>
<tr>
<td><code translate="no">schema</code></td>
<td>El esquema de esta colección.<br/>Establecerlo como <strong>Ninguno</strong> indica que esta colección se creará con la configuración predeterminada.<br/>Para configurar una colección con un esquema personalizado, debe crear un objeto <strong>CollectionSchema</strong> y referenciarlo aquí. En este caso, Milvus ignora todos los demás parámetros relacionados con el esquema que se incluyen en la solicitud.</td>
</tr>
<tr>
<td><code translate="no">index_params</code></td>
<td>Los parámetros para construir el índice sobre el campo vectorial en esta colección. Para configurar una colección con un esquema personalizado y cargar automáticamente la colección en memoria, necesita crear un objeto IndexParams y referenciarlo aquí.<br/>Debería añadir al menos un índice para el campo vectorial en esta colección. También puedes omitir este parámetro si prefieres configurar los parámetros del índice más adelante.</td>
</tr>
</tbody>
</table></p>
<p><table class="language-java">
<thead>
<tr>
<th>Parámetro</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td><code translate="no">collectionName</code></td>
<td>El nombre de la colección.</td>
</tr>
<tr>
<td><code translate="no">collectionSchema</code></td>
<td>El esquema de esta colección.<br/>Dejarlo vacío indica que esta colección se creará con la configuración por defecto. Para configurar una colección con un esquema personalizado, debe crear un objeto <strong>CollectionSchema</strong> y referenciarlo aquí.</td>
</tr>
<tr>
<td><code translate="no">indexParams</code></td>
<td>Los parámetros para construir el índice sobre el campo vectorial en esta colección. Para configurar una colección con un esquema personalizado y cargar automáticamente la colección en memoria, cree un objeto <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Management/IndexParam.md">IndexParams</a> con una lista de objetos IndexParam y haga referencia a él aquí.</td>
</tr>
</tbody>
</table></p>
<p><table class="language-javascript">
<thead>
<tr>
<th>Parámetro</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td><code translate="no">collection_name</code></td>
<td>El nombre de la colección.</td>
</tr>
<tr>
<td><code translate="no">fields</code></td>
<td>Los campos de la colección.</td>
</tr>
<tr>
<td><code translate="no">index_params</code></td>
<td>Los parámetros de índice de la colección a crear.</td>
</tr>
</tbody>
</table></p>
<p><table class="language-shell">
<thead>
<tr>
<th>Parámetro</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td><code translate="no">collectionName</code></td>
<td>El nombre de la colección.</td>
</tr>
<tr>
<td><code translate="no">schema</code></td>
<td>El esquema se encarga de organizar los datos en la colección de destino. Un esquema válido debe tener múltiples campos, que deben incluir una clave primaria, un campo vectorial y varios campos escalares.</td>
</tr>
<tr>
<td><code translate="no">schema.autoID</code></td>
<td>Si permite que el campo primario se incremente automáticamente. Si se establece en True, el campo primario se incrementa automáticamente. En este caso, el campo primario no debe incluirse en los datos a insertar para evitar errores. Establezca este parámetro en el campo con is_primary a True.</td>
</tr>
<tr>
<td><code translate="no">schema.enableDynamicField</code></td>
<td>Si permite utilizar el campo reservado $meta para contener campos no definidos por el esquema en pares clave-valor.</td>
</tr>
<tr>
<td><code translate="no">fields</code></td>
<td>Una lista de objetos de campo.</td>
</tr>
<tr>
<td><code translate="no">fields.fieldName</code></td>
<td>El nombre del campo a crear en la colección de destino.</td>
</tr>
<tr>
<td><code translate="no">fields.dataType</code></td>
<td>El tipo de datos de los valores del campo.</td>
</tr>
<tr>
<td><code translate="no">fields.isPrimary</code></td>
<td>Si el campo actual es el campo primario. Si se establece en True, el campo actual será el campo primario.</td>
</tr>
<tr>
<td><code translate="no">fields.elementTypeParams</code></td>
<td>Parámetros de campo adicionales.</td>
</tr>
<tr>
<td><code translate="no">fields.elementTypeParams.dim</code></td>
<td>Un parámetro opcional para los campos FloatVector o BinaryVector que determina la dimensión del vector.</td>
</tr>
</tbody>
</table></p>
<p>La colección creada anteriormente no se carga automáticamente. Puede crear un índice para la colección de la siguiente manera. La creación de un índice para la colección de forma independiente no carga automáticamente la colección. Para más detalles, consulte <a href="/docs/es/manage-collections.md">Cargar y liberar colección</a>.</p>
<p><div class="multipleCode">
<a href="#python">Python </a><a href="#java">Java</a><a href="#javascript">Node.js</a><a href="#shell">cURL</a></div></p>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># 3.6 Create index</span>
client.create_index(
    collection_name=<span class="hljs-string">&quot;customized_setup_2&quot;</span>,
    index_params=index_params
)

res = client.get_load_state(
    collection_name=<span class="hljs-string">&quot;customized_setup_2&quot;</span>
)

<span class="hljs-built_in">print</span>(res)

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;state&quot;: &quot;&lt;LoadState: NotLoad&gt;&quot;</span>
<span class="hljs-comment"># }</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-type">CreateIndexReq</span>  <span class="hljs-variable">createIndexReq</span> <span class="hljs-operator">=</span> CreateIndexReq.builder()
    .collectionName(<span class="hljs-string">&quot;customized_setup_2&quot;</span>)
    .indexParams(indexParams)
    .build();

client.createIndex(createIndexReq);

<span class="hljs-comment">// Thread.sleep(1000);</span>

<span class="hljs-comment">// 3.7 Get load state of the collection</span>
<span class="hljs-type">GetLoadStateReq</span> <span class="hljs-variable">customSetupLoadStateReq2</span> <span class="hljs-operator">=</span> GetLoadStateReq.builder()
    .collectionName(<span class="hljs-string">&quot;customized_setup_2&quot;</span>)
    .build();

res = client.getLoadState(customSetupLoadStateReq2);

System.out.println(res);

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// false</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-comment">// 3.5 Create index</span>
res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">createIndex</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;customized_setup_2&quot;</span>,
    <span class="hljs-attr">field_name</span>: <span class="hljs-string">&quot;my_vector&quot;</span>,
    <span class="hljs-attr">index_type</span>: <span class="hljs-string">&quot;IVF_FLAT&quot;</span>,
    <span class="hljs-attr">metric_type</span>: <span class="hljs-string">&quot;IP&quot;</span>,
    <span class="hljs-attr">params</span>: { <span class="hljs-attr">nlist</span>: <span class="hljs-number">1024</span>}
})

res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">getLoadState</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;customized_setup_2&quot;</span>
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">state</span>)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// LoadStateNotLoad</span>
<span class="hljs-comment">//</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-shell">$ curl -X POST <span class="hljs-string">&quot;http://<span class="hljs-variable">${MILVUS_URI}</span>/v2/vectordb/indexes/create&quot;</span> \
-H <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \
-d <span class="hljs-string">&#x27;{
    &quot;collectionName&quot;: &quot;customized_setup_2&quot;,
    &quot;indexParams&quot;: [
        {
            &quot;metricType&quot;: &quot;L2&quot;,
            &quot;fieldName&quot;: &quot;my_vector&quot;,
            &quot;indexName&quot;: &quot;my_vector&quot;,
            &quot;indexConfig&quot;: {
                &quot;index_type&quot;: &quot;IVF_FLAT&quot;,
                &quot;nlist&quot;: &quot;1024&quot;
            }
        }
    ]
}&#x27;</span>

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;code&quot;: 0,</span>
<span class="hljs-comment">#     &quot;data&quot;: {},</span>
<span class="hljs-comment"># }</span>

$ curl -X POST <span class="hljs-string">&quot;http://<span class="hljs-variable">${MILVUS_URI}</span>/v2/vectordb/collections/get_load_state&quot;</span> \
-H <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \
-d <span class="hljs-string">&#x27;{
    &quot;collectionName&quot;: &quot;customized_setup_2&quot;
}&#x27;</span>

<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;code&quot;: 0,</span>
<span class="hljs-comment">#     &quot;data&quot;: {</span>
<span class="hljs-comment">#         &quot;loadState&quot;: &quot;LoadStateNotLoaded&quot;</span>
<span class="hljs-comment">#     }</span>
<span class="hljs-comment"># }</span>
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
      <td><code translate="no">collection_name</code></td>
      <td>El nombre de la colección.</td>
    </tr>
    <tr>
      <td><code translate="no">index_params</code></td>
      <td>Un objeto <strong>IndexParams</strong> que contiene una lista de objetos <strong>IndexParam</strong>.</td>
    </tr>
  </tbody>
</table>
</li>
</ul>
<table class="language-java">
  <thead>
    <tr>
      <th>Parámetro</th>
      <th>Descripción</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code translate="no">collectionName</code></td>
      <td>El nombre de la colección.</td>
    </tr>
    <tr>
      <td><code translate="no">indexParams</code></td>
      <td>Una lista de objetos <strong>IndexParam</strong>.</td>
    </tr>
  </tbody>
</table>
<table class="language-javascript">
  <thead>
    <tr>
      <th>Parámetro</th>
      <th>Descripción</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code translate="no">collection_name</code></td>
      <td>El nombre de la colección.</td>
    </tr>
    <tr>
      <td><code translate="no">field_name</code></td>
      <td>El nombre del campo en el que crear un índice.</td>
    </tr>
    <tr>
      <td><code translate="no">index_type</code></td>
      <td>El nombre del algoritmo utilizado para ordenar los datos en el campo específico. Para conocer los algoritmos aplicables, consulte <a href="https://milvus.io/docs/index.md">Índice en memoria</a> e <a href="https://milvus.io/docs/disk_index.md">Índice en disco</a>.</td>
    </tr>
    <tr>
      <td><code translate="no">metric_type</code></td>
      <td>El algoritmo que se utiliza para medir la similitud entre vectores. Los valores posibles son <strong>IP</strong>, <strong>L2</strong>, <strong>COSINE</strong>, <strong>JACCARD</strong>, <strong>HAMMING</strong>. Sólo está disponible cuando el campo especificado es un campo vectorial. Para más información, consulte <a href="https://milvus.io/docs/index.md#Indexes-supported-in-Milvus">Índices soportados en Milvus</a>.</td>
    </tr>
    <tr>
      <td><code translate="no">params</code></td>
      <td>Los parámetros de ajuste fino para el tipo de índice especificado. Para más información sobre posibles claves y rangos de valores, consulte <a href="https://milvus.io/docs/index.md">Índice en memoria</a>.</td>
    </tr>
  </tbody>
</table>
<table class="language-shell">
    <thead>
        <tr>
        <th>Parámetro</th>
        <th>Descripción</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        <td><code translate="no">collectionName</code></td>
        <td>El nombre de la colección.</td>
        </tr>
        <tr>
        <td><code translate="no">indexParams</code></td>
        <td>Los parámetros de índice para la colección que se va a crear.</td>
        </tr>
        <tr>
        <td><code translate="no">indexParams.metricType</code></td>
        <td>El tipo de métrica de similitud utilizado para crear el índice. El valor por defecto es COSINE.</td>
        </tr>
        <tr>
        <td><code translate="no">indexParams.fieldName</code></td>
        <td>El nombre del campo de destino sobre el que se va a crear un índice.</td>
        </tr>
        <tr>
        <td><code translate="no">indexParams.indexName</code></td>
        <td>El nombre del índice que se va a crear; el valor por defecto es el nombre del campo de destino.</td>
        </tr>
        <tr>
        <td><code translate="no">indexParams.indexConfig.index_type</code></td>
        <td>El tipo de índice a crear.</td>
        </tr>
        <tr>
        <td><code translate="no">indexParams.indexConfig.nlist</code></td>
        <td>El número de unidades de cluster. Esto se aplica a los tipos de índice relacionados con FIV.</td>
        </tr>
    </tbody>
</table>
<h2 id="View-Collections" class="common-anchor-header">Ver colecciones<button data-href="#View-Collections" class="anchor-icon" translate="no">
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
<p>Para comprobar los detalles de una colección existente, utilice <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Collections/describe_collection.md">describe_collection()</a>.</p>
</div>
<div class="language-java">
<p>Para comprobar los detalles de una colección existente, utilice <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Collections/describeCollection.md">describeCollection()</a>.</p>
</div>
<div class="language-javascript">
<p>Para comprobar los detalles de una colección existente, utilice <a href="https://milvus.io/api-reference/node/v2.4.x/Collections/describeCollection.md">describeCollection()</a>.</p>
</div>
<div class="language-shell">
<p>Para ver la definición de una colección, puede utilizar los botones <a href="https://milvus.io/api-reference/restful/v2.4.x/v2/Collection%20(v2)/Describe.md"><code translate="no">POST /v2/vectordb/collections/describe</code></a> y el <a href="https://milvus.io/api-reference/restful/v2.4.x/v2/Collection%20(v2)/List.md"><code translate="no">POST /v2/vectordb/collections/list</code></a> puntos finales de la API.</p>
</div>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a> <a href="#shell">cURL</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># 5. View Collections</span>
res = client.describe_collection(
    collection_name=<span class="hljs-string">&quot;customized_setup_2&quot;</span>
)

<span class="hljs-built_in">print</span>(res)

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;collection_name&quot;: &quot;customized_setup_2&quot;,</span>
<span class="hljs-comment">#     &quot;auto_id&quot;: false,</span>
<span class="hljs-comment">#     &quot;num_shards&quot;: 1,</span>
<span class="hljs-comment">#     &quot;description&quot;: &quot;&quot;,</span>
<span class="hljs-comment">#     &quot;fields&quot;: [</span>
<span class="hljs-comment">#         {</span>
<span class="hljs-comment">#             &quot;field_id&quot;: 100,</span>
<span class="hljs-comment">#             &quot;name&quot;: &quot;my_id&quot;,</span>
<span class="hljs-comment">#             &quot;description&quot;: &quot;&quot;,</span>
<span class="hljs-comment">#             &quot;type&quot;: 5,</span>
<span class="hljs-comment">#             &quot;params&quot;: {},</span>
<span class="hljs-comment">#             &quot;element_type&quot;: 0,</span>
<span class="hljs-comment">#             &quot;is_primary&quot;: true</span>
<span class="hljs-comment">#         },</span>
<span class="hljs-comment">#         {</span>
<span class="hljs-comment">#             &quot;field_id&quot;: 101,</span>
<span class="hljs-comment">#             &quot;name&quot;: &quot;my_vector&quot;,</span>
<span class="hljs-comment">#             &quot;description&quot;: &quot;&quot;,</span>
<span class="hljs-comment">#             &quot;type&quot;: 101,</span>
<span class="hljs-comment">#             &quot;params&quot;: {</span>
<span class="hljs-comment">#                 &quot;dim&quot;: 5</span>
<span class="hljs-comment">#             },</span>
<span class="hljs-comment">#             &quot;element_type&quot;: 0</span>
<span class="hljs-comment">#         }</span>
<span class="hljs-comment">#     ],</span>
<span class="hljs-comment">#     &quot;aliases&quot;: [],</span>
<span class="hljs-comment">#     &quot;collection_id&quot;: 448143479230158446,</span>
<span class="hljs-comment">#     &quot;consistency_level&quot;: 2,</span>
<span class="hljs-comment">#     &quot;properties&quot;: {},</span>
<span class="hljs-comment">#     &quot;num_partitions&quot;: 1,</span>
<span class="hljs-comment">#     &quot;enable_dynamic_field&quot;: true</span>
<span class="hljs-comment"># }</span>

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java">import io.milvus.v2.service.collection.request.DescribeCollectionReq;
import io.milvus.v2.service.collection.response.DescribeCollectionResp;

// 4. View collections
DescribeCollectionReq describeCollectionReq = DescribeCollectionReq.builder()
    .collectionName(<span class="hljs-string">&quot;customized_setup_2&quot;</span>)
    .build();

DescribeCollectionResp describeCollectionRes = client.describeCollection(describeCollectionReq);

System.out.println(JSONObject.toJSON(describeCollectionRes));

// Output:
// {
//     <span class="hljs-string">&quot;createTime&quot;</span>: 449005822816026627,
//     <span class="hljs-string">&quot;collectionSchema&quot;</span>: {<span class="hljs-string">&quot;fieldSchemaList&quot;</span>: [
//         {
//             <span class="hljs-string">&quot;autoID&quot;</span>: <span class="hljs-literal">false</span>,
//             <span class="hljs-string">&quot;dataType&quot;</span>: <span class="hljs-string">&quot;Int64&quot;</span>,
//             <span class="hljs-string">&quot;name&quot;</span>: <span class="hljs-string">&quot;my_id&quot;</span>,
//             <span class="hljs-string">&quot;description&quot;</span>: <span class="hljs-string">&quot;&quot;</span>,
//             <span class="hljs-string">&quot;isPrimaryKey&quot;</span>: <span class="hljs-literal">true</span>,
//             <span class="hljs-string">&quot;maxLength&quot;</span>: 65535,
//             <span class="hljs-string">&quot;isPartitionKey&quot;</span>: <span class="hljs-literal">false</span>
//         },
//         {
//             <span class="hljs-string">&quot;autoID&quot;</span>: <span class="hljs-literal">false</span>,
//             <span class="hljs-string">&quot;dataType&quot;</span>: <span class="hljs-string">&quot;FloatVector&quot;</span>,
//             <span class="hljs-string">&quot;name&quot;</span>: <span class="hljs-string">&quot;my_vector&quot;</span>,
//             <span class="hljs-string">&quot;description&quot;</span>: <span class="hljs-string">&quot;&quot;</span>,
//             <span class="hljs-string">&quot;isPrimaryKey&quot;</span>: <span class="hljs-literal">false</span>,
//             <span class="hljs-string">&quot;dimension&quot;</span>: 5,
//             <span class="hljs-string">&quot;maxLength&quot;</span>: 65535,
//             <span class="hljs-string">&quot;isPartitionKey&quot;</span>: <span class="hljs-literal">false</span>
//         }
//     ]},
//     <span class="hljs-string">&quot;vectorFieldName&quot;</span>: [<span class="hljs-string">&quot;my_vector&quot;</span>],
//     <span class="hljs-string">&quot;autoID&quot;</span>: <span class="hljs-literal">false</span>,
//     <span class="hljs-string">&quot;fieldNames&quot;</span>: [
//         <span class="hljs-string">&quot;my_id&quot;</span>,
//         <span class="hljs-string">&quot;my_vector&quot;</span>
//     ],
//     <span class="hljs-string">&quot;description&quot;</span>: <span class="hljs-string">&quot;&quot;</span>,
//     <span class="hljs-string">&quot;numOfPartitions&quot;</span>: 1,
//     <span class="hljs-string">&quot;primaryFieldName&quot;</span>: <span class="hljs-string">&quot;my_id&quot;</span>,
//     <span class="hljs-string">&quot;enableDynamicField&quot;</span>: <span class="hljs-literal">true</span>,
//     <span class="hljs-string">&quot;collectionName&quot;</span>: <span class="hljs-string">&quot;customized_setup_2&quot;</span>
// }
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-comment">// 5. View Collections</span>
res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">describeCollection</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;customized_setup_2&quot;</span>
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// {</span>
<span class="hljs-comment">//   virtual_channel_names: [ &#x27;by-dev-rootcoord-dml_13_449007919953017716v0&#x27; ],</span>
<span class="hljs-comment">//   physical_channel_names: [ &#x27;by-dev-rootcoord-dml_13&#x27; ],</span>
<span class="hljs-comment">//   aliases: [],</span>
<span class="hljs-comment">//   start_positions: [],</span>
<span class="hljs-comment">//   properties: [],</span>
<span class="hljs-comment">//   status: {</span>
<span class="hljs-comment">//     extra_info: {},</span>
<span class="hljs-comment">//     error_code: &#x27;Success&#x27;,</span>
<span class="hljs-comment">//     reason: &#x27;&#x27;,</span>
<span class="hljs-comment">//     code: 0,</span>
<span class="hljs-comment">//     retriable: false,</span>
<span class="hljs-comment">//     detail: &#x27;&#x27;</span>
<span class="hljs-comment">//   },</span>
<span class="hljs-comment">//   schema: {</span>
<span class="hljs-comment">//     fields: [ [Object], [Object] ],</span>
<span class="hljs-comment">//     properties: [],</span>
<span class="hljs-comment">//     name: &#x27;customized_setup_2&#x27;,</span>
<span class="hljs-comment">//     description: &#x27;&#x27;,</span>
<span class="hljs-comment">//     autoID: false,</span>
<span class="hljs-comment">//     enable_dynamic_field: false</span>
<span class="hljs-comment">//   },</span>
<span class="hljs-comment">//   collectionID: &#x27;449007919953017716&#x27;,</span>
<span class="hljs-comment">//   created_timestamp: &#x27;449024569603784707&#x27;,</span>
<span class="hljs-comment">//   created_utc_timestamp: &#x27;1712892797866&#x27;,</span>
<span class="hljs-comment">//   shards_num: 1,</span>
<span class="hljs-comment">//   consistency_level: &#x27;Bounded&#x27;,</span>
<span class="hljs-comment">//   collection_name: &#x27;customized_setup_2&#x27;,</span>
<span class="hljs-comment">//   db_name: &#x27;default&#x27;,</span>
<span class="hljs-comment">//   num_partitions: &#x27;1&#x27;</span>
<span class="hljs-comment">// }</span>
<span class="hljs-comment">// </span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-shell">curl -X POST <span class="hljs-string">&quot;http://<span class="hljs-variable">${MILVUS_URI}</span>/v2/vectordb/collections/describe&quot;</span> \
-H <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \
-d <span class="hljs-string">&#x27;{
    &quot;dbName&quot;: &quot;default&quot;,
    &quot;collectionName&quot;: &quot;test_collection&quot;
}&#x27;</span>

<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;code&quot;: 0,</span>
<span class="hljs-comment">#     &quot;data&quot;: {</span>
<span class="hljs-comment">#         &quot;aliases&quot;: [],</span>
<span class="hljs-comment">#         &quot;autoId&quot;: false,</span>
<span class="hljs-comment">#         &quot;collectionID&quot;: 448707763883002014,</span>
<span class="hljs-comment">#         &quot;collectionName&quot;: &quot;test_collection&quot;,</span>
<span class="hljs-comment">#         &quot;consistencyLevel&quot;: &quot;Bounded&quot;,</span>
<span class="hljs-comment">#         &quot;description&quot;: &quot;&quot;,</span>
<span class="hljs-comment">#         &quot;enableDynamicField&quot;: true,</span>
<span class="hljs-comment">#         &quot;fields&quot;: [</span>
<span class="hljs-comment">#             {</span>
<span class="hljs-comment">#                 &quot;autoId&quot;: false,</span>
<span class="hljs-comment">#                 &quot;description&quot;: &quot;&quot;,</span>
<span class="hljs-comment">#                 &quot;id&quot;: 100,</span>
<span class="hljs-comment">#                 &quot;name&quot;: &quot;id&quot;,</span>
<span class="hljs-comment">#                 &quot;partitionKey&quot;: false,</span>
<span class="hljs-comment">#                 &quot;primaryKey&quot;: true,</span>
<span class="hljs-comment">#                 &quot;type&quot;: &quot;Int64&quot;</span>
<span class="hljs-comment">#             },</span>
<span class="hljs-comment">#             {</span>
<span class="hljs-comment">#                 &quot;autoId&quot;: false,</span>
<span class="hljs-comment">#                 &quot;description&quot;: &quot;&quot;,</span>
<span class="hljs-comment">#                 &quot;id&quot;: 101,</span>
<span class="hljs-comment">#                 &quot;name&quot;: &quot;vector&quot;,</span>
<span class="hljs-comment">#                 &quot;params&quot;: [</span>
<span class="hljs-comment">#                     {</span>
<span class="hljs-comment">#                         &quot;key&quot;: &quot;dim&quot;,</span>
<span class="hljs-comment">#                         &quot;value&quot;: &quot;5&quot;</span>
<span class="hljs-comment">#                     }</span>
<span class="hljs-comment">#                 ],</span>
<span class="hljs-comment">#                 &quot;partitionKey&quot;: false,</span>
<span class="hljs-comment">#                 &quot;primaryKey&quot;: false,</span>
<span class="hljs-comment">#                 &quot;type&quot;: &quot;FloatVector&quot;</span>
<span class="hljs-comment">#             }</span>
<span class="hljs-comment">#         ],</span>
<span class="hljs-comment">#         &quot;indexes&quot;: [</span>
<span class="hljs-comment">#             {</span>
<span class="hljs-comment">#                 &quot;fieldName&quot;: &quot;vector&quot;,</span>
<span class="hljs-comment">#                 &quot;indexName&quot;: &quot;vector&quot;,</span>
<span class="hljs-comment">#                 &quot;metricType&quot;: &quot;COSINE&quot;</span>
<span class="hljs-comment">#             }</span>
<span class="hljs-comment">#         ],</span>
<span class="hljs-comment">#         &quot;load&quot;: &quot;LoadStateLoaded&quot;,</span>
<span class="hljs-comment">#         &quot;partitionsNum&quot;: 1,</span>
<span class="hljs-comment">#         &quot;properties&quot;: [],</span>
<span class="hljs-comment">#         &quot;shardsNum&quot;: 1</span>
<span class="hljs-comment">#     }</span>
<span class="hljs-comment"># }</span>
<button class="copy-code-btn"></button></code></pre>
<p>Para listar todas las colecciones existentes, puedes hacer lo siguiente:</p>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a> <a href="#shell">cURL</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># 6. List all collection names</span>
res = client.list_collections()

<span class="hljs-built_in">print</span>(res)

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># [</span>
<span class="hljs-comment">#     &quot;customized_setup_2&quot;,</span>
<span class="hljs-comment">#     &quot;quick_setup&quot;,</span>
<span class="hljs-comment">#     &quot;customized_setup_1&quot;</span>
<span class="hljs-comment"># ]</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.milvus.v2.service.collection.response.ListCollectionsResp;

<span class="hljs-comment">// 5. List all collection names</span>
<span class="hljs-type">ListCollectionsResp</span> <span class="hljs-variable">listCollectionsRes</span> <span class="hljs-operator">=</span> client.listCollections();

System.out.println(listCollectionsRes.getCollectionNames());

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// [</span>
<span class="hljs-comment">//     &quot;customized_setup_2&quot;,</span>
<span class="hljs-comment">//     &quot;quick_setup&quot;,</span>
<span class="hljs-comment">//     &quot;customized_setup_1&quot;</span>
<span class="hljs-comment">// ]</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-comment">// 5. List all collection names</span>
<span class="hljs-type">ListCollectionsResp</span> <span class="hljs-variable">listCollectionsRes</span> <span class="hljs-operator">=</span> client.listCollections();

System.out.println(listCollectionsRes.getCollectionNames());

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// [</span>
<span class="hljs-comment">//     &quot;customized_setup_1&quot;,</span>
<span class="hljs-comment">//     &quot;quick_setup&quot;,</span>
<span class="hljs-comment">//     &quot;customized_setup_2&quot;</span>
<span class="hljs-comment">// ]</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-shell">$ curl -X POST <span class="hljs-string">&quot;http://<span class="hljs-variable">${MILVUS_URI}</span>/v2/vectordb/collections/list&quot;</span> \
-H <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \
-d <span class="hljs-string">&#x27;{
    &quot;dbName&quot;: &quot;default&quot;
}&#x27;</span>

<span class="hljs-comment"># {</span>
<span class="hljs-comment">#   &quot;code&quot;: 0,</span>
<span class="hljs-comment">#   &quot;data&quot;: [</span>
<span class="hljs-comment">#     &quot;quick_setup&quot;,</span>
<span class="hljs-comment">#     &quot;customized_setup_1&quot;,</span>
<span class="hljs-comment">#     &quot;customized_setup_2&quot;</span>
<span class="hljs-comment">#   ]</span>
<span class="hljs-comment"># }</span>
<button class="copy-code-btn"></button></code></pre>
<h2 id="Load--Release-Collection" class="common-anchor-header">Cargar y liberar colección<button data-href="#Load--Release-Collection" class="anchor-icon" translate="no">
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
    </button></h2><p>Durante el proceso de carga de una colección, Milvus carga el fichero índice de la colección en memoria. A la inversa, al liberar una colección, Milvus descarga el fichero índice de la memoria. Antes de realizar búsquedas en una colección, asegúrese de que la colección está cargada.</p>
<h3 id="Load-a-collection" class="common-anchor-header">Cargar una colección</h3><div class="language-python">
<p>Para cargar una colección, utilice el método <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Management/load_collection.md"><code translate="no">load_collection()</code></a> especificando el nombre de la colección. También puede configurar <code translate="no">replica_number</code> para determinar cuántas réplicas en memoria de segmentos de datos se crearán en los nodos de consulta cuando se cargue la colección.</p>
<ul>
<li>Milvus Standalone: El valor máximo permitido para <code translate="no">replica_number</code> es 1.</li>
<li>Milvus Cluster: El valor máximo no debe superar el <code translate="no">queryNode.replicas</code> establecido en sus configuraciones de Milvus. Para más detalles, consulte <a href="https://milvus.io/docs/configure_querynode.md#Query-Node-related-Configurations">Configuraciones relacionadas con los nodos de consulta</a>.</li>
</ul>
</div>
<div class="language-java">
<p>Para cargar una colección, utilice el método <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Management/loadCollection.md"><code translate="no">loadCollection()</code></a> especificando el nombre de la colección.</p>
</div>
<div class="language-javascript">
<p>Para cargar una colección, utilice el método <a href="https://milvus.io/api-reference/node/v2.4.x/Management/loadCollection.md"><code translate="no">loadCollection()</code></a> especificando el nombre de la colección.</p>
</div>
<div class="language-shell">
<p>Para cargar una colección, puede utilizar el método <a href="https://milvus.io/api-reference/restful/v2.4.x/v2/Collection%20(v2)/Load.md"><code translate="no">POST /v2/vectordb/collections/load</code></a> y el <a href="https://milvus.io/api-reference/restful/v2.4.x/v2/Collection%20(v2)/GetLoadState.md"><code translate="no">POST /v2/vectordb/collections/get_load_state</code></a> puntos finales de la API.</p>
</div>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a> <a href="#shell">cURL</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># 7. Load the collection</span>
client.load_collection(
    collection_name=<span class="hljs-string">&quot;customized_setup_2&quot;</span>,
    replica_number=<span class="hljs-number">1</span> <span class="hljs-comment"># Number of replicas to create on query nodes. Max value is 1 for Milvus Standalone, and no greater than `queryNode.replicas` for Milvus Cluster.</span>
)

res = client.get_load_state(
    collection_name=<span class="hljs-string">&quot;customized_setup_2&quot;</span>
)

<span class="hljs-built_in">print</span>(res)

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;state&quot;: &quot;&lt;LoadState: Loaded&gt;&quot;</span>
<span class="hljs-comment"># }</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.milvus.v2.service.collection.request.LoadCollectionReq;

<span class="hljs-comment">// 6. Load the collection</span>
<span class="hljs-type">LoadCollectionReq</span> <span class="hljs-variable">loadCollectionReq</span> <span class="hljs-operator">=</span> LoadCollectionReq.builder()
    .collectionName(<span class="hljs-string">&quot;customized_setup_2&quot;</span>)
    .build();

client.loadCollection(loadCollectionReq);

<span class="hljs-comment">// Thread.sleep(5000);</span>

<span class="hljs-comment">// 7. Get load state of the collection</span>
<span class="hljs-type">GetLoadStateReq</span> <span class="hljs-variable">loadStateReq</span> <span class="hljs-operator">=</span> GetLoadStateReq.builder()
    .collectionName(<span class="hljs-string">&quot;customized_setup_2&quot;</span>)
    .build();

res = client.getLoadState(loadStateReq);

System.out.println(res);

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// true</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-comment">// 7. Load the collection</span>
res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">loadCollection</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;customized_setup_2&quot;</span>
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">error_code</span>)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// Success</span>
<span class="hljs-comment">// </span>

<span class="hljs-keyword">await</span> <span class="hljs-title function_">sleep</span>(<span class="hljs-number">3000</span>)

res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">getLoadState</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;customized_setup_2&quot;</span>
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">state</span>)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// LoadStateLoaded</span>
<span class="hljs-comment">// </span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-shell">$ curl -X POST <span class="hljs-string">&quot;http://<span class="hljs-variable">${MILVUS_URI}</span>/v2/vectordb/collections/load&quot;</span> \
-H <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \
-d <span class="hljs-string">&#x27;{
    &quot;collectionName&quot;: &quot;customized_setup_2&quot;
}&#x27;</span>

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;code&quot;: 0,</span>
<span class="hljs-comment">#     &quot;data&quot;: {},</span>
<span class="hljs-comment"># }</span>

$ curl -X POST <span class="hljs-string">&quot;http://<span class="hljs-variable">${MILVUS_URI}</span>/v2/vectordb/collections/get_load_state&quot;</span> \
-H <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \
-d <span class="hljs-string">&#x27;{
  &quot;collectionName&quot;: &quot;customized_setup_2&quot;
}&#x27;</span>

<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;code&quot;: 0,</span>
<span class="hljs-comment">#     &quot;data&quot;: {</span>
<span class="hljs-comment">#         &quot;loadProgress&quot;: 100,</span>
<span class="hljs-comment">#         &quot;loadState&quot;: &quot;LoadStateLoaded&quot;</span>
<span class="hljs-comment">#     }</span>
<span class="hljs-comment"># }</span>
<button class="copy-code-btn"></button></code></pre>
<h3 id="Release-a-collection" class="common-anchor-header">Liberar una colección</h3><div class="language-python">
<p>Para liberar una colección, utilice el método <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Management/release_collection.md"><code translate="no">release_collection()</code></a> especificando el nombre de la colección.</p>
</div>
<div class="language-java">
<p>Para liberar una colección, utilice el método <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Management/releaseCollection.md"><code translate="no">releaseCollection()</code></a> especificando el nombre de la colección.</p>
</div>
<div class="language-javascript">
<p>Para liberar una colección, utilice el método <a href="https://milvus.io/api-reference/node/v2.4.x/Management/releaseCollection.md"><code translate="no">releaseCollection()</code></a> especificando el nombre de la colección.</p>
</div>
<div class="language-shell">
<p>Para liberar una colección, puede utilizar el método <a href="https://milvus.io/api-reference/restful/v2.4.x/v2/Collection%20(v2)/Release.md"><code translate="no">POST /v2/vectordb/collections/release</code></a> y el <a href="https://milvus.io/api-reference/restful/v2.4.x/v2/Collection%20(v2)/GetLoadState.md"><code translate="no">POST /v2/vectordb/collections/get_load_state</code></a> puntos finales de la API.</p>
</div>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a> <a href="#shell">cURL</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># 8. Release the collection</span>
client.release_collection(
    collection_name=<span class="hljs-string">&quot;customized_setup_2&quot;</span>
)

res = client.get_load_state(
    collection_name=<span class="hljs-string">&quot;customized_setup_2&quot;</span>
)

<span class="hljs-built_in">print</span>(res)

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;state&quot;: &quot;&lt;LoadState: NotLoad&gt;&quot;</span>
<span class="hljs-comment"># }</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.milvus.v2.service.collection.request.ReleaseCollectionReq;

<span class="hljs-comment">// 8. Release the collection</span>
<span class="hljs-type">ReleaseCollectionReq</span> <span class="hljs-variable">releaseCollectionReq</span> <span class="hljs-operator">=</span> ReleaseCollectionReq.builder()
    .collectionName(<span class="hljs-string">&quot;customized_setup_2&quot;</span>)
    .build();

client.releaseCollection(releaseCollectionReq);

<span class="hljs-comment">// Thread.sleep(1000);</span>

res = client.getLoadState(loadStateReq);

System.out.println(res);

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// false</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-comment">// 8. Release the collection</span>
res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">releaseCollection</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;customized_setup_2&quot;</span>
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">error_code</span>)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// Success</span>
<span class="hljs-comment">// </span>

res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">getLoadState</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;customized_setup_2&quot;</span>
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">state</span>)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// LoadStateNotLoad</span>
<span class="hljs-comment">// </span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-shell">$ curl -X POST <span class="hljs-string">&quot;http://<span class="hljs-variable">${MILVUS_URI}</span>/v2/vectordb/collections/release&quot;</span> \
-H <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \
-d <span class="hljs-string">&#x27;{
    &quot;collectionName&quot;: &quot;customized_setup_2&quot;
}&#x27;</span>

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;code&quot;: 0,</span>
<span class="hljs-comment">#     &quot;data&quot;: {},</span>
<span class="hljs-comment"># }</span>


$ curl -X POST <span class="hljs-string">&quot;http://<span class="hljs-variable">${MILVUS_URI}</span>/v2/vectordb/collections/get_load_state&quot;</span> \
-H <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \
-d <span class="hljs-string">&#x27;{
  &quot;collectionName&quot;: &quot;customized_setup_2&quot;
}&#x27;</span>


<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;code&quot;: 0,</span>
<span class="hljs-comment">#     &quot;data&quot;: {</span>
<span class="hljs-comment">#         &quot;loadState&quot;: &quot;LoadStateNotLoad&quot;</span>
<span class="hljs-comment">#     }</span>
<span class="hljs-comment"># }</span>
<button class="copy-code-btn"></button></code></pre>
<h2 id="Set-up-aliases" class="common-anchor-header">Establecer alias<button data-href="#Set-up-aliases" class="anchor-icon" translate="no">
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
    </button></h2><p>Puede asignar alias a las colecciones para que tengan más sentido en un contexto específico. Puede asignar varios alias a una colección, pero varias colecciones no pueden compartir un alias.</p>
<h3 id="Create-aliases" class="common-anchor-header">Crear alias</h3><div class="language-python">
<p>Para crear alias, utilice el método <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Collections/create_alias.md"><code translate="no">create_alias()</code></a> especificando el nombre de la colección y el alias.</p>
</div>
<div class="language-java">
<p>Para crear alias, utilice el método <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Collections/createAlias.md"><code translate="no">createAlias()</code></a> especificando el nombre de la colección y el alias.</p>
</div>
<div class="language-javascript">
<p>Para crear alias, utilice el método <a href="https://milvus.io/api-reference/node/v2.4.x/Collections/createAlias.md"><code translate="no">createAlias()</code></a> especificando el nombre de la colección y el alias.</p>
</div>
<div class="language-shell">
<p>Para crear alias de una colección, puede utilizar el punto final de la API <a href="https://milvus.io/api-reference/restful/v2.4.x/v2/Alias%20(v2)/Create.md"><code translate="no">POST /v2/vectordb/aliases/create</code></a> punto final de la API.</p>
</div>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a> <a href="#shell">cURL</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># 9.1. Create aliases</span>
client.create_alias(
    collection_name=<span class="hljs-string">&quot;customized_setup_2&quot;</span>,
    <span class="hljs-built_in">alias</span>=<span class="hljs-string">&quot;bob&quot;</span>
)

client.create_alias(
    collection_name=<span class="hljs-string">&quot;customized_setup_2&quot;</span>,
    <span class="hljs-built_in">alias</span>=<span class="hljs-string">&quot;alice&quot;</span>
)
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.milvus.v2.service.utility.request.CreateAliasReq;

<span class="hljs-comment">// 9. Manage aliases</span>

<span class="hljs-comment">// 9.1 Create alias</span>
<span class="hljs-type">CreateAliasReq</span> <span class="hljs-variable">createAliasReq</span> <span class="hljs-operator">=</span> CreateAliasReq.builder()
    .collectionName(<span class="hljs-string">&quot;customized_setup_2&quot;</span>)
    .alias(<span class="hljs-string">&quot;bob&quot;</span>)
    .build();

client.createAlias(createAliasReq);

createAliasReq = CreateAliasReq.builder()
    .collectionName(<span class="hljs-string">&quot;customized_setup_2&quot;</span>)
    .alias(<span class="hljs-string">&quot;alice&quot;</span>)
    .build();

client.createAlias(createAliasReq);
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-comment">// 9. Manage aliases</span>
<span class="hljs-comment">// 9.1 Create aliases</span>
res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">createAlias</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;customized_setup_2&quot;</span>,
    <span class="hljs-attr">alias</span>: <span class="hljs-string">&quot;bob&quot;</span>
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">error_code</span>)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// Success</span>
<span class="hljs-comment">// </span>

res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">createAlias</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;customized_setup_2&quot;</span>,
    <span class="hljs-attr">alias</span>: <span class="hljs-string">&quot;alice&quot;</span>
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">error_code</span>)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// Success</span>
<span class="hljs-comment">// </span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-shell">$ curl -X POST <span class="hljs-string">&quot;http://<span class="hljs-variable">${MILVUS_URI}</span>/v2/vectordb/aliases/create&quot;</span> \
-H <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \
-d <span class="hljs-string">&#x27;{
    &quot;collectionName&quot;: &quot;customized_setup_2&quot;,
    &quot;aliasName&quot;: &quot;bob&quot;
}&#x27;</span>

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;code&quot;: 0,</span>
<span class="hljs-comment">#     &quot;data&quot;: {}</span>
<span class="hljs-comment"># }</span>

$ curl -X POST <span class="hljs-string">&quot;http://<span class="hljs-variable">${MILVUS_URI}</span>/v2/vectordb/aliases/create&quot;</span> \
-H <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \
-d <span class="hljs-string">&#x27;{
    &quot;collectionName&quot;: &quot;customized_setup_2&quot;,
    &quot;aliasName&quot;: &quot;alice&quot;
}&#x27;</span>

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;code&quot;: 0,</span>
<span class="hljs-comment">#     &quot;data&quot;: {}</span>
<span class="hljs-comment"># }</span>
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
      <td><code translate="no">collection_name</code></td>
      <td>El nombre de la colección para la que se va a crear un alias.</td>
    </tr>
    <tr>
      <td><code translate="no">alias</code></td>
      <td>El alias de la colección. Antes de realizar esta operación, asegúrese de que el alias no existe ya. En caso contrario, se producirán excepciones.</td>
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
      <td><code translate="no">collectionName</code></td>
      <td>El nombre de la colección para la que se va a crear un alias.</td>
    </tr>
    <tr>
      <td><code translate="no">alias</code></td>
      <td>El alias de la colección. Antes de realizar esta operación, asegúrese de que el alias no existe ya. En caso contrario, se producirán excepciones.</td>
    </tr>
  </tbody>
</table>
<table class="language-javascript">
  <thead>
    <tr>
      <th>Parámetro</th>
      <th>Descripción</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code translate="no">collection_name</code></td>
      <td>El nombre de la colección para la que se va a crear un alias.</td>
    </tr>
    <tr>
      <td><code translate="no">alias</code></td>
      <td>El alias de la colección. Antes de realizar esta operación, asegúrese de que el alias no existe ya. En caso contrario, se producirán excepciones.</td>
    </tr>
  </tbody>
</table>
<table class="language-shell">
  <thead>
    <tr>
      <th>Parámetro</th>
      <th>Descripción</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code translate="no">collectionName</code></td>
      <td>El nombre de la colección para la que se va a crear un alias.</td>
    </tr>
    <tr>
      <td><code translate="no">aliasName</code></td>
      <td>El alias de la colección. Antes de realizar esta operación, asegúrese de que el alias no existe ya. En caso contrario, se producirán excepciones.</td>
    </tr>
  </tbody>
</table>
<h3 id="List-aliases" class="common-anchor-header">Lista de alias</h3><div class="language-python">
<p>Para listar alias, utilice el método <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Collections/list_aliases.md"><code translate="no">list_aliases()</code></a> especificando el nombre de la colección.</p>
</div>
<div class="language-java">
<p>Para listar alias, utilice el método <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Collections/listAliases.md"><code translate="no">listAliases()</code></a> especificando el nombre de la colección.</p>
</div>
<div class="language-javascript">
<p>Para enumerar los alias, utilice el método <a href="https://milvus.io/api-reference/node/v2.4.x/Collections/listAliases.md"><code translate="no">listAliases()</code></a> especificando el nombre de la colección.</p>
</div>
<div class="language-shell">
<p>Para enumerar los alias de una colección, puede utilizar el punto final de la API <a href="https://milvus.io/api-reference/restful/v2.4.x/v2/Alias%20(v2)/List.md"><code translate="no">POST /v2/vectordb/aliases/list</code></a> punto final de la API.</p>
</div>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a> <a href="#shell">cURL</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># 9.2. List aliases</span>
res = client.list_aliases(
    collection_name=<span class="hljs-string">&quot;customized_setup_2&quot;</span>
)

<span class="hljs-built_in">print</span>(res)

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;aliases&quot;: [</span>
<span class="hljs-comment">#         &quot;bob&quot;,</span>
<span class="hljs-comment">#         &quot;alice&quot;</span>
<span class="hljs-comment">#     ],</span>
<span class="hljs-comment">#     &quot;collection_name&quot;: &quot;customized_setup_2&quot;,</span>
<span class="hljs-comment">#     &quot;db_name&quot;: &quot;default&quot;</span>
<span class="hljs-comment"># }</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.milvus.v2.service.utility.request.ListAliasesReq;
<span class="hljs-keyword">import</span> io.milvus.v2.service.utility.response.ListAliasResp;

<span class="hljs-comment">// 9.2 List alises</span>
<span class="hljs-type">ListAliasesReq</span> <span class="hljs-variable">listAliasesReq</span> <span class="hljs-operator">=</span> ListAliasesReq.builder()
    .collectionName(<span class="hljs-string">&quot;customized_setup_2&quot;</span>)
    .build();

<span class="hljs-type">ListAliasResp</span> <span class="hljs-variable">listAliasRes</span> <span class="hljs-operator">=</span> client.listAliases(listAliasesReq);

System.out.println(listAliasRes.getAlias());

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// [</span>
<span class="hljs-comment">//     &quot;bob&quot;,</span>
<span class="hljs-comment">//     &quot;alice&quot;</span>
<span class="hljs-comment">// ]</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-comment">// 9.2 List aliases</span>
res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">listAliases</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;customized_setup_2&quot;</span>
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">aliases</span>)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// [ &#x27;bob&#x27;, &#x27;alice&#x27; ]</span>
<span class="hljs-comment">// </span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-shell">$ curl -X POST <span class="hljs-string">&quot;http://<span class="hljs-variable">${MILVUS_URI}</span>/v2/vectordb/aliases/list&quot;</span> \
-H <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \
-d <span class="hljs-string">&#x27;{
    &quot;collectionName&quot;: &quot;customized_setup_2&quot;
}&#x27;</span>

<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;code&quot;: 0,</span>
<span class="hljs-comment">#     &quot;data&quot;: [</span>
<span class="hljs-comment">#         &quot;bob&quot;,</span>
<span class="hljs-comment">#         &quot;alice&quot;</span>
<span class="hljs-comment">#     ]</span>
<span class="hljs-comment"># }</span>
<button class="copy-code-btn"></button></code></pre>
<h3 id="Describe-aliases" class="common-anchor-header">Describir alias</h3><div class="language-python">
<p>Para describir alias, utilice el método <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Collections/describe_alias.md"><code translate="no">describe_alias()</code></a> especificando el alias.</p>
</div>
<div class="language-java">
<p>Para describir alias, utilice el método <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Collections/describeAlias.md"><code translate="no">describeAlias()</code></a> especificando el alias.</p>
</div>
<div class="language-javascript">
<p>Para describir alias, utilice el método <a href="https://milvus.io/api-reference/node/v2.4.x/Collections/describeAlias.md"><code translate="no">describeAlias()</code></a> especificando el alias.</p>
</div>
<div class="language-shell">
<p>Para describir alias de una colección, puede utilizar el punto final de la API <a href="https://milvus.io/api-reference/restful/v2.4.x/v2/Alias%20(v2)/Describe.md"><code translate="no">POST /v2/vectordb/aliases/describe</code></a> punto final de la API.</p>
</div>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a> <a href="#shell">cURL</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># 9.3. Describe aliases</span>
res = client.describe_alias(
    <span class="hljs-built_in">alias</span>=<span class="hljs-string">&quot;bob&quot;</span>
)

<span class="hljs-built_in">print</span>(res)

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;alias&quot;: &quot;bob&quot;,</span>
<span class="hljs-comment">#     &quot;collection_name&quot;: &quot;customized_setup_2&quot;,</span>
<span class="hljs-comment">#     &quot;db_name&quot;: &quot;default&quot;</span>
<span class="hljs-comment"># }</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.<span class="hljs-property">milvus</span>.<span class="hljs-property">v2</span>.<span class="hljs-property">service</span>.<span class="hljs-property">utility</span>.<span class="hljs-property">request</span>.<span class="hljs-property">DescribeAliasReq</span>;
<span class="hljs-keyword">import</span> io.<span class="hljs-property">milvus</span>.<span class="hljs-property">v2</span>.<span class="hljs-property">service</span>.<span class="hljs-property">utility</span>.<span class="hljs-property">response</span>.<span class="hljs-property">DescribeAliasResp</span>;

<span class="hljs-comment">// 9.3 Describe alias</span>
<span class="hljs-title class_">DescribeAliasReq</span> describeAliasReq = <span class="hljs-title class_">DescribeAliasReq</span>.<span class="hljs-title function_">builder</span>()
    .<span class="hljs-title function_">alias</span>(<span class="hljs-string">&quot;bob&quot;</span>)
    .<span class="hljs-title function_">build</span>();

<span class="hljs-title class_">DescribeAliasResp</span> describeAliasRes = client.<span class="hljs-title function_">describeAlias</span>(describeAliasReq);

<span class="hljs-title class_">System</span>.<span class="hljs-property">out</span>.<span class="hljs-title function_">println</span>(<span class="hljs-title class_">JSON</span><span class="hljs-built_in">Object</span>.<span class="hljs-title function_">toJSON</span>(describeAliasRes));

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// {</span>
<span class="hljs-comment">//     &quot;alias&quot;: &quot;bob&quot;,</span>
<span class="hljs-comment">//     &quot;collectionName&quot;: &quot;customized_setup_2&quot;</span>
<span class="hljs-comment">// }</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-comment">// 9.3 Describe aliases</span>
res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">describeAlias</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;customized_setup_2&quot;</span>,
    <span class="hljs-attr">alias</span>: <span class="hljs-string">&quot;bob&quot;</span>
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// {</span>
<span class="hljs-comment">//   status: {</span>
<span class="hljs-comment">//     extra_info: {},</span>
<span class="hljs-comment">//     error_code: &#x27;Success&#x27;,</span>
<span class="hljs-comment">//     reason: &#x27;&#x27;,</span>
<span class="hljs-comment">//     code: 0,</span>
<span class="hljs-comment">//     retriable: false,</span>
<span class="hljs-comment">//     detail: &#x27;&#x27;</span>
<span class="hljs-comment">//   },</span>
<span class="hljs-comment">//   db_name: &#x27;default&#x27;,</span>
<span class="hljs-comment">//   alias: &#x27;bob&#x27;,</span>
<span class="hljs-comment">//   collection: &#x27;customized_setup_2&#x27;</span>
<span class="hljs-comment">// }</span>
<span class="hljs-comment">// </span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-shell">$ curl -X POST <span class="hljs-string">&quot;http://<span class="hljs-variable">${MILVUS_URI}</span>/v2/vectordb/aliases/describe&quot;</span> \
-H <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \
-d <span class="hljs-string">&#x27;{
    &quot;aliasName&quot;: &quot;bob&quot;
}&#x27;</span>

<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;code&quot;: 0,</span>
<span class="hljs-comment">#     &quot;data&quot;: {</span>
<span class="hljs-comment">#         &quot;aliasName&quot;: &quot;bob&quot;,</span>
<span class="hljs-comment">#         &quot;collectionName&quot;: &quot;quick_setup&quot;,</span>
<span class="hljs-comment">#         &quot;dbName&quot;: &quot;default&quot;</span>
<span class="hljs-comment">#     }</span>
<span class="hljs-comment"># }</span>
<button class="copy-code-btn"></button></code></pre>
<h3 id="Reassign-aliases" class="common-anchor-header">Reasignar alias</h3><div class="language-python">
<p>Para reasignar alias a otras colecciones, utilice el método <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Collections/alter_alias.md"><code translate="no">alter_alias()</code></a> especificando el nombre de la colección y el alias.</p>
</div>
<div class="language-java">
<p>Para reasignar alias a otras colecciones, utilice el método <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Collections/alterAlias.md"><code translate="no">alterAlias()</code></a> especificando el nombre de la colección y el alias.</p>
</div>
<div class="language-javascript">
<p>Para reasignar alias a otras colecciones, utilice el método <a href="https://milvus.io/api-reference/node/v2.4.x/Collections/alterAlias.md"><code translate="no">alterAlias()</code></a> especificando el nombre de la colección y el alias.</p>
</div>
<div class="language-shell">
<p>Para reasignar alias a otras colecciones, puede utilizar el punto final de la API <a href="https://milvus.io/api-reference/restful/v2.4.x/v2/Alias%20(v2)/Alter.md"><code translate="no">POST /v2/vectordb/aliases/alter</code></a> punto final de la API.</p>
</div>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a> <a href="#shell">cURL</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># 9.4 Reassign aliases to other collections</span>
client.alter_alias(
    collection_name=<span class="hljs-string">&quot;customized_setup_1&quot;</span>,
    alias=<span class="hljs-string">&quot;alice&quot;</span>
)

res = client.list_aliases(
    collection_name=<span class="hljs-string">&quot;customized_setup_1&quot;</span>
)

<span class="hljs-built_in">print</span>(res)

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;aliases&quot;: [</span>
<span class="hljs-comment">#         &quot;alice&quot;</span>
<span class="hljs-comment">#     ],</span>
<span class="hljs-comment">#     &quot;collection_name&quot;: &quot;customized_setup_1&quot;,</span>
<span class="hljs-comment">#     &quot;db_name&quot;: &quot;default&quot;</span>
<span class="hljs-comment"># }</span>

res = client.list_aliases(
    collection_name=<span class="hljs-string">&quot;customized_setup_2&quot;</span>
)

<span class="hljs-built_in">print</span>(res)

<span class="hljs-comment"># Output</span>
<span class="hljs-comment">#</span>
<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;aliases&quot;: [</span>
<span class="hljs-comment">#         &quot;bob&quot;</span>
<span class="hljs-comment">#     ],</span>
<span class="hljs-comment">#     &quot;collection_name&quot;: &quot;customized_setup_2&quot;,</span>
<span class="hljs-comment">#     &quot;db_name&quot;: &quot;default&quot;</span>
<span class="hljs-comment"># }</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.milvus.v2.service.utility.request.AlterAliasReq;

<span class="hljs-comment">// 9.4 Reassign alias to other collections</span>
AlterAliasReq alterAliasReq = AlterAliasReq.builder()
    .collectionName(<span class="hljs-string">&quot;customized_setup_1&quot;</span>)
    .alias(<span class="hljs-string">&quot;alice&quot;</span>)
    .build();

client.alterAlias(alterAliasReq);

listAliasesReq = ListAliasesReq.builder()
    .collectionName(<span class="hljs-string">&quot;customized_setup_1&quot;</span>)
    .build();

listAliasRes = client.listAliases(listAliasesReq);

System.out.<span class="hljs-built_in">println</span>(listAliasRes.getAlias());

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// [&quot;alice&quot;]</span>

listAliasesReq = ListAliasesReq.builder()
    .collectionName(<span class="hljs-string">&quot;customized_setup_2&quot;</span>)
    .build();

listAliasRes = client.listAliases(listAliasesReq);

System.out.<span class="hljs-built_in">println</span>(listAliasRes.getAlias());

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// [&quot;bob&quot;]</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-comment">// 9.4 Reassign aliases to other collections</span>
res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">alterAlias</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;customized_setup_1&quot;</span>,
    <span class="hljs-attr">alias</span>: <span class="hljs-string">&quot;alice&quot;</span>
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">error_code</span>)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// Success</span>
<span class="hljs-comment">// </span>

res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">listAliases</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;customized_setup_1&quot;</span>
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">aliases</span>)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// [ &#x27;alice&#x27; ]</span>
<span class="hljs-comment">// </span>

res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">listAliases</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;customized_setup_2&quot;</span>
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">aliases</span>)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// [ &#x27;bob&#x27; ]</span>
<span class="hljs-comment">// </span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-shell">$ curl -X POST <span class="hljs-string">&quot;http://<span class="hljs-variable">${MILVUS_URI}</span>/v2/vectordb/aliases/alter&quot;</span> \
-H <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \
-d <span class="hljs-string">&#x27;{
     &quot;collectionName&quot;: &quot;customized_setup_1&quot;,
     &quot;aliasName&quot;: &quot;alice&quot;
}&#x27;</span>

<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;code&quot;: 0,</span>
<span class="hljs-comment">#     &quot;data&quot;: {}</span>
<span class="hljs-comment"># }</span>


$ curl -X POST <span class="hljs-string">&quot;http://<span class="hljs-variable">${MILVUS_URI}</span>/v2/vectordb/aliases/list&quot;</span> \
-H <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \
-d <span class="hljs-string">&#x27;{
    &quot;collectionName&quot;: &quot;customized_setup_1&quot;
}&#x27;</span>


<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;code&quot;: 0,</span>
<span class="hljs-comment">#     &quot;data&quot;: [</span>
<span class="hljs-comment">#         &quot;alice&quot;</span>
<span class="hljs-comment">#     ]</span>
<span class="hljs-comment"># }</span>


$ curl -X POST <span class="hljs-string">&quot;http://<span class="hljs-variable">${MILVUS_URI}</span>/v2/vectordb/aliases/list&quot;</span> \
-H <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \
-d <span class="hljs-string">&#x27;{
    &quot;collectionName&quot;: &quot;customized_setup_2&quot;
}&#x27;</span>


<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;code&quot;: 0,</span>
<span class="hljs-comment">#     &quot;data&quot;: [</span>
<span class="hljs-comment">#         &quot;bob&quot;</span>
<span class="hljs-comment">#     ]</span>
<span class="hljs-comment"># }</span>
<button class="copy-code-btn"></button></code></pre>
<h3 id="Drop-aliases" class="common-anchor-header">Eliminar alias</h3><div class="language-python">
<p>Para eliminar alias, utilice el método <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Collections/drop_alias.md"><code translate="no">drop_alias()</code></a> especificando el alias.</p>
</div>
<div class="language-java">
<p>Para eliminar alias, utilice el método <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Collections/dropAlias.md"><code translate="no">dropAlias()</code></a> especificando el alias.</p>
</div>
<div class="language-javascript">
<p>Para eliminar alias, utilice el método <a href="https://milvus.io/api-reference/node/v2.4.x/Collections/dropAlias.md"><code translate="no">dropAlias()</code></a> especificando el alias.</p>
</div>
<div class="language-shell">
<p>Para eliminar alias de una colección, puede utilizar el punto final de la API <a href="https://milvus.io/api-reference/restful/v2.4.x/v2/Alias%20(v2)/Drop.md"><code translate="no">POST /v2/vectordb/aliases/drop</code></a> punto final de la API.</p>
</div>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># 9.5 Drop aliases</span>
client.drop_alias(
    <span class="hljs-built_in">alias</span>=<span class="hljs-string">&quot;bob&quot;</span>
)

client.drop_alias(
    <span class="hljs-built_in">alias</span>=<span class="hljs-string">&quot;alice&quot;</span>
)
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.milvus.v2.service.utility.request.DropAliasReq;

<span class="hljs-comment">// 9.5 Drop alias</span>
<span class="hljs-type">DropAliasReq</span> <span class="hljs-variable">dropAliasReq</span> <span class="hljs-operator">=</span> DropAliasReq.builder()
    .alias(<span class="hljs-string">&quot;bob&quot;</span>)
    .build();

client.dropAlias(dropAliasReq);

dropAliasReq = DropAliasReq.builder()
    .alias(<span class="hljs-string">&quot;alice&quot;</span>)
    .build();

client.dropAlias(dropAliasReq);
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-comment">// 9.5 Drop aliases</span>
res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">dropAlias</span>({
    <span class="hljs-attr">alias</span>: <span class="hljs-string">&quot;bob&quot;</span>
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">error_code</span>)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// Success</span>
<span class="hljs-comment">// </span>

res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">dropAlias</span>({
    <span class="hljs-attr">alias</span>: <span class="hljs-string">&quot;alice&quot;</span>
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">error_code</span>)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// Success</span>
<span class="hljs-comment">// </span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-shell">$ curl -X POST <span class="hljs-string">&quot;http://<span class="hljs-variable">${MILVUS_URI}</span>/v2/vectordb/aliases/drop&quot;</span> \
-H <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \
-d <span class="hljs-string">&#x27;{
    &quot;aliasName&quot;: &quot;bob&quot;
}&#x27;</span>

<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;code&quot;: 0,</span>
<span class="hljs-comment">#     &quot;data&quot;: {}</span>
<span class="hljs-comment"># }</span>


$ curl -X POST <span class="hljs-string">&quot;http://<span class="hljs-variable">${MILVUS_URI}</span>/v2/vectordb/aliases/drop&quot;</span> \
-H <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \
-d <span class="hljs-string">&#x27;{
    &quot;aliasName&quot;: &quot;alice&quot;
}&#x27;</span>


<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;code&quot;: 0,</span>
<span class="hljs-comment">#     &quot;data&quot;: {}</span>
<span class="hljs-comment"># }</span>
<button class="copy-code-btn"></button></code></pre>
<h2 id="Set-Properties" class="common-anchor-header">Establecer propiedades<button data-href="#Set-Properties" class="anchor-icon" translate="no">
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
    </button></h2><p>Puede establecer propiedades para una colección, como <code translate="no">ttl.seconds</code> y <code translate="no">mmap.enabled</code>. Para más información, consulte <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/ORM/Collection/set_properties.md">set_properties()</a>.</p>
<div class="alert note">
<p>Los fragmentos de código de esta sección utilizan el <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/ORM/Connections/connect.md">módulo PyMilvus ORM</a> para interactuar con Milvus. Los fragmentos de código con el nuevo <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/About.md">SDK MilvusClient</a> estarán disponibles en breve.</p>
</div>
<h3 id="Set-TTL" class="common-anchor-header">Establecer TTL</h3><p>Establece el tiempo de vida (TTL) para los datos de la colección, que especifica cuánto tiempo deben conservarse los datos antes de que se eliminen automáticamente.</p>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> Collection, connections

<span class="hljs-comment"># Connect to Milvus server</span>
connections.connect(host=<span class="hljs-string">&quot;localhost&quot;</span>, port=<span class="hljs-string">&quot;19530&quot;</span>) <span class="hljs-comment"># Change to your Milvus server IP and port</span>

<span class="hljs-comment"># Get existing collection</span>
collection = Collection(<span class="hljs-string">&quot;quick_setup&quot;</span>)

<span class="hljs-comment"># Set the TTL for the data in the collection</span>
collection.set_properties(
    properties={
        <span class="hljs-string">&quot;collection.ttl.seconds&quot;</span>: <span class="hljs-number">60</span>
    }
)
<button class="copy-code-btn"></button></code></pre>
<h3 id="Set-MMAP" class="common-anchor-header">Establecer MMAP</h3><p>Configure la propiedad de asignación de memoria (MMAP) para la colección, que determina si los datos se asignan a la memoria para mejorar el rendimiento de la consulta. Para obtener más información, consulte <a href="https://milvus.io/docs/mmap.md#Configure-memory-mapping">Configurar la asignación de memoria .</a></p>
<div class="alert note">
<p>Antes de configurar la propiedad MMAP, libere primero la colección. De lo contrario, se producirá un error.</p>
</div>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> Collection, connections

<span class="hljs-comment"># Connect to Milvus server</span>
connections.connect(host=<span class="hljs-string">&quot;localhost&quot;</span>, port=<span class="hljs-string">&quot;19530&quot;</span>) <span class="hljs-comment"># Change to your Milvus server IP and port</span>

<span class="hljs-comment"># Get existing collection</span>
collection = Collection(<span class="hljs-string">&quot;quick_setup&quot;</span>)

<span class="hljs-comment"># Before setting memory mapping property, we need to release the collection first.</span>
collection.release()

<span class="hljs-comment"># Set memory mapping property to True or Flase</span>
collection.set_properties(
    properties={
        <span class="hljs-string">&quot;mmap.enabled&quot;</span>: <span class="hljs-literal">True</span>
    }
)
<button class="copy-code-btn"></button></code></pre>
<h2 id="Drop-a-Collection" class="common-anchor-header">Abandonar una colecta<button data-href="#Drop-a-Collection" class="anchor-icon" translate="no">
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
    </button></h2><p>Si una colección ya no es necesaria, puede eliminarla.</p>
<div class="language-python">
<p>Para eliminar una colección, utilice el método <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Collections/drop_collection.md"><code translate="no">drop_collection()</code></a> especificando el nombre de la colección.</p>
</div>
<div class="language-java">
<p>Para eliminar una colección, utilice el método <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Collections/dropCollection.md"><code translate="no">dropCollection()</code></a> especificando el nombre de la colección.</p>
</div>
<div class="language-javascript">
<p>Para eliminar una colección, utilice el método <a href="https://milvus.io/api-reference/node/v2.4.x/Collections/dropCollection.md"><code translate="no">dropCollection()</code></a> especificando el nombre de la colección.</p>
</div>
<div class="language-shell">
<p>Para eliminar una colección, puede utilizar el punto final de la API <a href="https://milvus.io/api-reference/restful/v2.4.x/v2/Collection%20(v2)/Drop.md"><code translate="no">POST /v2/vectordb/collections/drop</code></a> punto final de la API.</p>
</div>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a> <a href="#shell">cURL</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># 10. Drop the collections</span>
client.drop_collection(
    collection_name=<span class="hljs-string">&quot;quick_setup&quot;</span>
)

client.drop_collection(
    collection_name=<span class="hljs-string">&quot;customized_setup_1&quot;</span>
)

client.drop_collection(
    collection_name=<span class="hljs-string">&quot;customized_setup_2&quot;</span>
)
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.milvus.v2.service.collection.request.DropCollectionReq;

<span class="hljs-comment">// 10. Drop collections</span>

<span class="hljs-type">DropCollectionReq</span> <span class="hljs-variable">dropQuickSetupParam</span> <span class="hljs-operator">=</span> DropCollectionReq.builder()
    .collectionName(<span class="hljs-string">&quot;quick_setup&quot;</span>)
    .build();

client.dropCollection(dropQuickSetupParam);

<span class="hljs-type">DropCollectionReq</span> <span class="hljs-variable">dropCustomizedSetupParam</span> <span class="hljs-operator">=</span> DropCollectionReq.builder()
    .collectionName(<span class="hljs-string">&quot;customized_setup_1&quot;</span>)
    .build();

client.dropCollection(dropCustomizedSetupParam);

dropCustomizedSetupParam = DropCollectionReq.builder()
    .collectionName(<span class="hljs-string">&quot;customized_setup_2&quot;</span>)
    .build();

client.dropCollection(dropCustomizedSetupParam);
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-comment">// 10. Drop the collection</span>
res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">dropCollection</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;customized_setup_2&quot;</span>
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">error_code</span>)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// Success</span>
<span class="hljs-comment">// </span>

res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">dropCollection</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;customized_setup_1&quot;</span>
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">error_code</span>)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// Success</span>
<span class="hljs-comment">// </span>

res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">dropCollection</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;quick_setup&quot;</span>
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">error_code</span>)

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// Success</span>
<span class="hljs-comment">// </span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-shell">$ curl -X POST <span class="hljs-string">&quot;http://<span class="hljs-variable">${MILVUS_URI}</span>/v2/vectordb/collections/drop&quot;</span> \
-H <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \
-d <span class="hljs-string">&#x27;{
    &quot;collectionName&quot;: &quot;quick_setup&quot;
}&#x27;</span>

<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;code&quot;: 0,</span>
<span class="hljs-comment">#     &quot;data&quot;: {}</span>
<span class="hljs-comment"># }</span>


$ curl -X POST <span class="hljs-string">&quot;http://<span class="hljs-variable">${MILVUS_URI}</span>/v2/vectordb/collections/drop&quot;</span> \
-H <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \
-d <span class="hljs-string">&#x27;{
    &quot;collectionName&quot;: &quot;customized_setup_1&quot;
}&#x27;</span>


<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;code&quot;: 0,</span>
<span class="hljs-comment">#     &quot;data&quot;: {}</span>
<span class="hljs-comment"># }</span>


$ curl -X POST <span class="hljs-string">&quot;http://<span class="hljs-variable">${MILVUS_URI}</span>/v2/vectordb/collections/drop&quot;</span> \
-H <span class="hljs-string">&quot;Content-Type: application/json&quot;</span> \
-d <span class="hljs-string">&#x27;{
    &quot;collectionName&quot;: &quot;customized_setup_2&quot;
}&#x27;</span>


<span class="hljs-comment"># {</span>
<span class="hljs-comment">#     &quot;code&quot;: 0,</span>
<span class="hljs-comment">#     &quot;data&quot;: {}</span>
<span class="hljs-comment"># }</span>
<button class="copy-code-btn"></button></code></pre>