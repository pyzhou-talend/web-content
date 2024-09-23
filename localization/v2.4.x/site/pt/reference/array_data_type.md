---
id: array_data_type.md
title: Utilizar campos de matriz
---
<h1 id="Use-Array-Fields" class="common-anchor-header">Utilizar campos de matriz<button data-href="#Use-Array-Fields" class="anchor-icon" translate="no">
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
    </button></h1><p>Este guia explica como utilizar os campos de matriz, tais como a inserção de valores de matriz, a criação de índices em campos de vetor e matriz, bem como a pesquisa e consulta em campos de matriz com operadores básicos e avançados.</p>
<h2 id="Prerequisites" class="common-anchor-header">Pré-requisitos<button data-href="#Prerequisites" class="anchor-icon" translate="no">
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
    </button></h2><p>Certifique-se de que tem o seguinte:</p>
<ul>
<li>Milvus instalado e em execução. Para obter informações sobre como instalar o Milvus, consulte <a href="/docs/pt/install-overview.md">Instalar o Milvus</a>.</li>
<li>Um dos SDKs do Milvus instalado no seu ambiente. Para obter detalhes, consulte <a href="/docs/pt/install-pymilvus.md">Instalar SDKs</a>.</li>
</ul>
<h2 id="Prepare-data-with-an-array-field" class="common-anchor-header">Preparar dados com um campo de matriz<button data-href="#Prepare-data-with-an-array-field" class="anchor-icon" translate="no">
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
    </button></h2><p>O Milvus suporta arrays como um dos tipos de dados de campo. Uma matriz numa coleção Milvus deve ter sempre elementos do mesmo tipo de dados, e o tipo de dados para os elementos da matriz pode ser qualquer um dos tipos de dados suportados em Milvus. Para obter uma lista dos tipos de dados suportados, consulte <a href="https://milvus.io/docs/schema.md#Supported-data-types">Tipos de dados suportados</a>.</p>
<p>O seguinte trecho de código gera um conjunto de dados aleatório contendo um campo de matriz chamado <code translate="no">color_coord</code>, com todos os elementos do tipo de dados interger.</p>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">import</span> random

colors = [<span class="hljs-string">&quot;green&quot;</span>, <span class="hljs-string">&quot;blue&quot;</span>, <span class="hljs-string">&quot;yellow&quot;</span>, <span class="hljs-string">&quot;red&quot;</span>, <span class="hljs-string">&quot;black&quot;</span>, <span class="hljs-string">&quot;white&quot;</span>, <span class="hljs-string">&quot;purple&quot;</span>, <span class="hljs-string">&quot;pink&quot;</span>, <span class="hljs-string">&quot;orange&quot;</span>, <span class="hljs-string">&quot;brown&quot;</span>, <span class="hljs-string">&quot;grey&quot;</span>]
data = []

<span class="hljs-keyword">for</span> i in <span class="hljs-keyword">range</span>(<span class="hljs-number">1000</span>):
    current_color = random.choice(colors)
    current_tag = random.randint(<span class="hljs-number">1000</span>, <span class="hljs-number">9999</span>)
    current_coord = [ random.randint(<span class="hljs-number">0</span>, <span class="hljs-number">40</span>) <span class="hljs-keyword">for</span> _ in <span class="hljs-keyword">range</span>(random.randint(<span class="hljs-number">3</span>, <span class="hljs-number">5</span>)) ]
    data.<span class="hljs-built_in">append</span>({
        <span class="hljs-string">&quot;id&quot;</span>: i,
        <span class="hljs-string">&quot;vector&quot;</span>: [ random.uniform(<span class="hljs-number">-1</span>, <span class="hljs-number">1</span>) <span class="hljs-keyword">for</span> _ in <span class="hljs-keyword">range</span>(<span class="hljs-number">5</span>) ],
        <span class="hljs-string">&quot;color&quot;</span>: current_color,
        <span class="hljs-string">&quot;color_tag&quot;</span>: current_tag,
        <span class="hljs-string">&quot;color_coord&quot;</span>: current_coord,
    })

<span class="hljs-built_in">print</span>(data[<span class="hljs-number">0</span>])
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-title class_">List</span>&lt;<span class="hljs-title class_">String</span>&gt; colors = <span class="hljs-title class_">Arrays</span>.<span class="hljs-title function_">asList</span>(<span class="hljs-string">&quot;green&quot;</span>, <span class="hljs-string">&quot;blue&quot;</span>, <span class="hljs-string">&quot;yellow&quot;</span>, <span class="hljs-string">&quot;red&quot;</span>, <span class="hljs-string">&quot;black&quot;</span>, <span class="hljs-string">&quot;white&quot;</span>, <span class="hljs-string">&quot;purple&quot;</span>, <span class="hljs-string">&quot;pink&quot;</span>, <span class="hljs-string">&quot;orange&quot;</span>, <span class="hljs-string">&quot;brown&quot;</span>, <span class="hljs-string">&quot;grey&quot;</span>);
<span class="hljs-title class_">List</span>&lt;<span class="hljs-title class_">JSON</span><span class="hljs-built_in">Object</span>&gt; data = <span class="hljs-keyword">new</span> <span class="hljs-title class_">ArrayList</span>&lt;&gt;();

<span class="hljs-keyword">for</span> (int i=<span class="hljs-number">0</span>; i&lt;<span class="hljs-number">1000</span>; i++) {
    <span class="hljs-title class_">Random</span> rand = <span class="hljs-keyword">new</span> <span class="hljs-title class_">Random</span>();
    <span class="hljs-title class_">String</span> current_color = colors.<span class="hljs-title function_">get</span>(rand.<span class="hljs-title function_">nextInt</span>(colors.<span class="hljs-title function_">size</span>()-<span class="hljs-number">1</span>));
    <span class="hljs-title class_">Long</span> current_tag = rand.<span class="hljs-title function_">nextLong</span>(8999L) + 1000L;

    <span class="hljs-comment">// Generate an random-sized array</span>
    <span class="hljs-title class_">Long</span> capacity = rand.<span class="hljs-title function_">nextLong</span>(5L) + 1L;
    <span class="hljs-title class_">List</span>&lt;<span class="hljs-title class_">Long</span>&gt; current_coord = <span class="hljs-keyword">new</span> <span class="hljs-title class_">ArrayList</span>&lt;&gt;();
    current_coord.<span class="hljs-title function_">add</span>(rand.<span class="hljs-title function_">nextLong</span>(40L) + 1L);
    current_coord.<span class="hljs-title function_">add</span>(rand.<span class="hljs-title function_">nextLong</span>(40L) + 1L);
    <span class="hljs-keyword">for</span> (int j=<span class="hljs-number">3</span>; j&lt;capacity; j++) {
        current_coord.<span class="hljs-title function_">add</span>(rand.<span class="hljs-title function_">nextLong</span>(40L) + 1L);
    }

    <span class="hljs-title class_">JSON</span><span class="hljs-built_in">Object</span> row = <span class="hljs-keyword">new</span> <span class="hljs-title class_">JSON</span><span class="hljs-built_in">Object</span>();
    row.<span class="hljs-title function_">put</span>(<span class="hljs-string">&quot;id&quot;</span>, <span class="hljs-title class_">Long</span>.<span class="hljs-title function_">valueOf</span>(i));
    row.<span class="hljs-title function_">put</span>(<span class="hljs-string">&quot;vector&quot;</span>, <span class="hljs-title class_">Arrays</span>.<span class="hljs-title function_">asList</span>(rand.<span class="hljs-title function_">nextFloat</span>(), rand.<span class="hljs-title function_">nextFloat</span>(), rand.<span class="hljs-title function_">nextFloat</span>(), rand.<span class="hljs-title function_">nextFloat</span>(), rand.<span class="hljs-title function_">nextFloat</span>()));
    row.<span class="hljs-title function_">put</span>(<span class="hljs-string">&quot;color&quot;</span>, current_color);
    row.<span class="hljs-title function_">put</span>(<span class="hljs-string">&quot;color_tag&quot;</span>, current_tag);
    row.<span class="hljs-title function_">put</span>(<span class="hljs-string">&quot;color_coord&quot;</span>, current_coord);
    data.<span class="hljs-title function_">add</span>(row);
}

<span class="hljs-title class_">System</span>.<span class="hljs-property">out</span>.<span class="hljs-title function_">println</span>(<span class="hljs-title class_">JSON</span><span class="hljs-built_in">Object</span>.<span class="hljs-title function_">toJSON</span>(data.<span class="hljs-title function_">get</span>(<span class="hljs-number">0</span>)));   
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-keyword">const</span> colors = [<span class="hljs-string">&quot;green&quot;</span>, <span class="hljs-string">&quot;blue&quot;</span>, <span class="hljs-string">&quot;yellow&quot;</span>, <span class="hljs-string">&quot;red&quot;</span>, <span class="hljs-string">&quot;black&quot;</span>, <span class="hljs-string">&quot;white&quot;</span>, <span class="hljs-string">&quot;purple&quot;</span>, <span class="hljs-string">&quot;pink&quot;</span>, <span class="hljs-string">&quot;orange&quot;</span>, <span class="hljs-string">&quot;brown&quot;</span>, <span class="hljs-string">&quot;grey&quot;</span>];
<span class="hljs-keyword">let</span> data = [];

<span class="hljs-keyword">for</span> (<span class="hljs-keyword">let</span> i = <span class="hljs-number">0</span>; i &lt; <span class="hljs-number">1000</span>; i++) {
    <span class="hljs-keyword">const</span> current_color = colors[<span class="hljs-title class_">Math</span>.<span class="hljs-title function_">floor</span>(<span class="hljs-title class_">Math</span>.<span class="hljs-title function_">random</span>() * colors.<span class="hljs-property">length</span>)];
    <span class="hljs-keyword">const</span> current_tag = <span class="hljs-title class_">Math</span>.<span class="hljs-title function_">floor</span>(<span class="hljs-title class_">Math</span>.<span class="hljs-title function_">random</span>() * <span class="hljs-number">8999</span> + <span class="hljs-number">1000</span>);
    <span class="hljs-keyword">const</span> current_coord = <span class="hljs-title class_">Array</span>(<span class="hljs-title class_">Math</span>.<span class="hljs-title function_">floor</span>(<span class="hljs-title class_">Math</span>.<span class="hljs-title function_">random</span>() * <span class="hljs-number">5</span> + <span class="hljs-number">1</span>)).<span class="hljs-title function_">fill</span>(<span class="hljs-number">0</span>).<span class="hljs-title function_">map</span>(<span class="hljs-function">() =&gt;</span> <span class="hljs-title class_">Math</span>.<span class="hljs-title function_">floor</span>(<span class="hljs-title class_">Math</span>.<span class="hljs-title function_">random</span>() * <span class="hljs-number">40</span>));

    data.<span class="hljs-title function_">push</span>({
        <span class="hljs-attr">id</span>: i,
        <span class="hljs-attr">vector</span>: <span class="hljs-title class_">Array</span>(<span class="hljs-number">5</span>).<span class="hljs-title function_">fill</span>(<span class="hljs-number">0</span>).<span class="hljs-title function_">map</span>(<span class="hljs-function">() =&gt;</span> <span class="hljs-title class_">Math</span>.<span class="hljs-title function_">random</span>()),
        <span class="hljs-attr">color</span>: current_color,
        <span class="hljs-attr">color_tag</span>: current_tag,
        <span class="hljs-attr">color_coord</span>: current_coord,
    });
}

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(data[<span class="hljs-number">0</span>]);
<button class="copy-code-btn"></button></code></pre>
<p>Este trecho de código prepara uma lista de cores aleatórias e gera um conjunto de dados contendo 1.000 entidades. Cada entidade tem um ID, um vetor de cinco números de vírgula flutuante, uma cor, uma etiqueta de cor e um campo de matriz <code translate="no">color_coord</code> contendo entre 3 a 5 valores inteiros. Os dados de amostra são impressos para verificar a sua estrutura.</p>
<p>Estrutura de saída:</p>
<pre><code translate="no" class="language-json">{
    <span class="hljs-built_in">id</span>: <span class="hljs-number">0</span>,
    vector: [
        <span class="hljs-number">0.0338537420906162</span>,
        <span class="hljs-number">0.6844108238358322</span>,
        <span class="hljs-number">0.28410588909961754</span>,
        <span class="hljs-number">0.09752595400212116</span>,
        <span class="hljs-number">0.22671013058761114</span>
    ],
    color: <span class="hljs-string">&#x27;orange&#x27;</span>,
    color_tag: <span class="hljs-number">5677</span>,
    color_coord: [ <span class="hljs-number">3</span>, <span class="hljs-number">0</span>, <span class="hljs-number">18</span>, <span class="hljs-number">29</span> ]
}
<button class="copy-code-btn"></button></code></pre>
<h2 id="Set-up-MilvusClient" class="common-anchor-header">Configurar o MilvusClient<button data-href="#Set-up-MilvusClient" class="anchor-icon" translate="no">
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
    </button></h2><p>Para interagir com o Milvus, configure o cliente Milvus especificando o endereço do servidor.</p>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> <span class="hljs-title class_">MilvusClient</span>, <span class="hljs-title class_">DataType</span>

<span class="hljs-variable constant_">SERVER_ADDR</span> = <span class="hljs-string">&quot;http://localhost:19530&quot;</span>

client = <span class="hljs-title class_">MilvusClient</span>(uri=<span class="hljs-variable constant_">SERVER_ADDR</span>)
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.milvus.v2.client.ConnectConfig;
<span class="hljs-keyword">import</span> io.milvus.v2.client.MilvusClientV2;
<span class="hljs-keyword">import</span> io.milvus.v2.common.DataType;

<span class="hljs-type">String</span> <span class="hljs-variable">SERVER_ADDR</span> <span class="hljs-operator">=</span> <span class="hljs-string">&quot;http://localhost:19530&quot;</span>;

<span class="hljs-comment">// 1. Connect to Milvus server</span>
<span class="hljs-type">ConnectConfig</span> <span class="hljs-variable">connectConfig</span> <span class="hljs-operator">=</span> ConnectConfig.builder()
    .uri(SERVER_ADDR)
    .build();

<span class="hljs-type">MilvusClientV2</span> <span class="hljs-variable">client</span> <span class="hljs-operator">=</span> <span class="hljs-keyword">new</span> <span class="hljs-title class_">MilvusClientV2</span>(connectConfig);
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-keyword">import</span> { <span class="hljs-title class_">MilvusClient</span>, <span class="hljs-title class_">DataType</span> } <span class="hljs-keyword">from</span> <span class="hljs-string">&quot;@zilliz/milvus2-sdk-node&quot;</span>;

<span class="hljs-comment">// Connect to Milvus server</span>
<span class="hljs-keyword">const</span> address = <span class="hljs-string">&quot;http://localhost:19530&quot;</span>;

<span class="hljs-keyword">const</span> milvusClient = <span class="hljs-keyword">new</span> <span class="hljs-title class_">MilvusClient</span>({<span class="hljs-attr">address</span>: address});
<button class="copy-code-btn"></button></code></pre>
<h2 id="Create-a-collection-with-an-array-field" class="common-anchor-header">Criar uma coleção com um campo de matriz<button data-href="#Create-a-collection-with-an-array-field" class="anchor-icon" translate="no">
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
    </button></h2><h3 id="Define-collection-schema" class="common-anchor-header">Definir o esquema da coleção</h3><p>Um esquema define a estrutura da coleção, incluindo os campos e os respectivos tipos de dados. O exemplo abaixo define um esquema de coleção que corresponde aos dados de amostra gerados na <a href="#prepare-data-with-an-array-field">secção anterior</a>.</p>
<p>Para configurar um campo de matriz numa coleção:</p>
<div class="language-python">
<ol>
<li>Defina o <code translate="no">datatype</code>: Configure-o como <code translate="no">DataType.ARRAY</code>.</li>
<li>Especifique o <code translate="no">element_type</code>: Escolha o tipo de dados para os elementos da matriz. Os elementos de um campo de matriz devem ter todos o mesmo tipo de dados. Neste exemplo, o <code translate="no">element_type</code> é definido como <code translate="no">DataType.INT64</code>.</li>
<li>Definir o <code translate="no">max_capacity</code>: Defina este parâmetro para especificar o número máximo de elementos que o campo de matriz pode conter.</li>
</ol>
</div>
<div class="language-java">
<ol>
<li>Definir o <code translate="no">dataType</code>: Configure-o como <code translate="no">DataType.Array</code>.</li>
<li>Especificar o <code translate="no">elementType</code>: Escolha o tipo de dados para os elementos da matriz. Os elementos de um campo de matriz devem ter todos o mesmo tipo de dados. Neste exemplo, o <code translate="no">elementType</code> é definido como <code translate="no">DataType.Int64</code>.</li>
<li>Definir o <code translate="no">maxCapacity</code>: Defina este parâmetro para especificar o número máximo de elementos que o campo de matriz pode conter.</li>
</ol>
</div>
<div class="language-javascript">
<ol>
<li>Definir o <code translate="no">data_type</code>: Configure-o como <code translate="no">DataType.Array</code>.</li>
<li>Especificar o <code translate="no">element_type</code>: Escolha o tipo de dados para os elementos da matriz. Os elementos de um campo de matriz devem ter todos o mesmo tipo de dados. Neste exemplo, o <code translate="no">element_type</code> é definido como <code translate="no">DataType.Int64</code>.</li>
<li>Defina o <code translate="no">max_capacity</code>: Defina este parâmetro para especificar o número máximo de elementos que o campo de matriz pode conter.</li>
</ol>
</div>
<p>O código de exemplo abaixo define o esquema de coleção com um campo de matriz <code translate="no">color_coord</code>, com um máximo de 5 elementos e cada elemento do tipo de dados integer.</p>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a></div>
<pre><code translate="no" class="language-python">schema = client.create_schema(auto_id=<span class="hljs-literal">False</span>, enable_dynamic_field=<span class="hljs-literal">False</span>)

schema.add_field(field_name=<span class="hljs-string">&quot;id&quot;</span>, datatype=DataType.INT64, is_primary=<span class="hljs-literal">True</span>)
schema.add_field(field_name=<span class="hljs-string">&quot;vector&quot;</span>, datatype=DataType.FLOAT_VECTOR, dim=<span class="hljs-number">5</span>)
schema.add_field(field_name=<span class="hljs-string">&quot;color&quot;</span>, datatype=DataType.VARCHAR, max_length=<span class="hljs-number">512</span>)
schema.add_field(field_name=<span class="hljs-string">&quot;color_tag&quot;</span>, datatype=DataType.INT64)
schema.add_field(field_name=<span class="hljs-string">&quot;color_coord&quot;</span>, datatype=DataType.ARRAY, element_type=DataType.INT64, max_capacity=<span class="hljs-number">5</span>)
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-comment">// Create schema</span>
CreateCollectionReq.<span class="hljs-type">CollectionSchema</span> <span class="hljs-variable">schema</span> <span class="hljs-operator">=</span> client.createSchema();

<span class="hljs-comment">// Add fields to schema</span>
schema.addField(AddFieldReq.builder()
    .fieldName(<span class="hljs-string">&quot;id&quot;</span>)
    .dataType(DataType.Int64)
    .isPrimaryKey(<span class="hljs-literal">true</span>)
    .autoID(<span class="hljs-literal">false</span>)
    .build());

schema.addField(AddFieldReq.builder()
    .fieldName(<span class="hljs-string">&quot;vector&quot;</span>)
    .dataType(DataType.FloatVector)
    .dimension(<span class="hljs-number">5</span>)
    .build());
    
schema.addField(AddFieldReq.builder()
    .fieldName(<span class="hljs-string">&quot;color&quot;</span>)
    .dataType(DataType.VarChar)
    .maxLength(<span class="hljs-number">512</span>)
    .build());

schema.addField(AddFieldReq.builder()
    .fieldName(<span class="hljs-string">&quot;color_tag&quot;</span>)
    .dataType(DataType.Int64)
    .build());

schema.addField(AddFieldReq.builder()
    .fieldName(<span class="hljs-string">&quot;color_coord&quot;</span>)
    .dataType(DataType.Array)
    .elementType(DataType.Int64)
    .maxCapacity(<span class="hljs-number">5</span>)
    .build());
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-keyword">const</span> fields = [
    {
        <span class="hljs-attr">name</span>: <span class="hljs-string">&quot;id&quot;</span>,
        <span class="hljs-attr">data_type</span>: <span class="hljs-title class_">DataType</span>.<span class="hljs-property">Int64</span>,
        <span class="hljs-attr">is_primary_key</span>: <span class="hljs-literal">true</span>,
        <span class="hljs-attr">auto_id</span>: <span class="hljs-literal">false</span>
    },
    {
        <span class="hljs-attr">name</span>: <span class="hljs-string">&quot;vector&quot;</span>,
        <span class="hljs-attr">data_type</span>: <span class="hljs-title class_">DataType</span>.<span class="hljs-property">FloatVector</span>,
        <span class="hljs-attr">dim</span>: <span class="hljs-number">5</span>
    },
    {
        <span class="hljs-attr">name</span>: <span class="hljs-string">&quot;color&quot;</span>,
        <span class="hljs-attr">data_type</span>: <span class="hljs-title class_">DataType</span>.<span class="hljs-property">VarChar</span>,
        <span class="hljs-attr">max_length</span>: <span class="hljs-number">512</span>
    },
    {
        <span class="hljs-attr">name</span>: <span class="hljs-string">&quot;color_tag&quot;</span>,
        <span class="hljs-attr">data_type</span>: <span class="hljs-title class_">DataType</span>.<span class="hljs-property">Int64</span>,
    },
    {
        <span class="hljs-attr">name</span>: <span class="hljs-string">&quot;color_coord&quot;</span>,
        <span class="hljs-attr">data_type</span>: <span class="hljs-title class_">DataType</span>.<span class="hljs-property">Array</span>,
        <span class="hljs-attr">element_type</span>: <span class="hljs-title class_">DataType</span>.<span class="hljs-property">Int64</span>,
        <span class="hljs-attr">max_capacity</span>: <span class="hljs-number">5</span>
    }
];
<button class="copy-code-btn"></button></code></pre>
<div class="language-python">
<p>Para obter mais informações sobre métodos e parâmetros, consulte <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Collections/create_schema.md">create_schema</a> e <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/CollectionSchema/add_field.md">add_field</a>.</p>
</div>
<div class="language-java">
<p>Para mais informações sobre métodos e parâmetros, consulte <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Collections/createSchema.md">createSchema</a> e <a href="https://milvus.io/api-reference/java/v2.4.x/v2/CollectionSchema/addField.md">addField</a>.</p>
</div>
<div class="language-javascript">
<p>Para mais informações sobre métodos e parâmetros, consulte <a href="https://milvus.io/api-reference/node/v2.4.x/Collections/createCollection.md">createCollection</a>.</p>
</div>
<h3 id="Create-the-collection" class="common-anchor-header">Criar a coleção</h3><p>Em seguida, crie a coleção utilizando o esquema definido.</p>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a></div>
<pre><code translate="no" class="language-python">client.create_collection(collection_name=<span class="hljs-string">&quot;test_collection&quot;</span>, schema=schema)
client.list_collections()

<span class="hljs-comment"># Output:</span>
<span class="hljs-comment"># [&#x27;test_collection&#x27;]</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-type">CreateCollectionReq</span> <span class="hljs-variable">customizedSetupReq</span> <span class="hljs-operator">=</span> CreateCollectionReq.builder()
    .collectionName(<span class="hljs-string">&quot;test_collection&quot;</span>)
    .collectionSchema(schema)
    .build();

client.createCollection(customizedSetupReq);
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-keyword">await</span> client.<span class="hljs-title function_">createCollection</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;test_collection&quot;</span>,
    <span class="hljs-attr">fields</span>: fields
});

<span class="hljs-keyword">const</span> res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">listCollections</span>({<span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;test_collection&quot;</span>});

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(<span class="hljs-string">&quot;Existing collections: &quot;</span> + res.<span class="hljs-property">collection_names</span>);

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// Existing collections: test_collection</span>
<button class="copy-code-btn"></button></code></pre>
<div class="language-python">
<p>Para mais informações sobre os métodos e parâmetros, consultar <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Collections/create_collection.md">create_collection</a> e <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Collections/list_collections.md">list_collections</a>.</p>
</div>
<div class="language-java">
<p>Para mais informações sobre métodos e parâmetros, consultar <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Collections/createCollection.md">createCollection</a>.</p>
</div>
<div class="language-javascript">
<p>Para mais informações sobre métodos e parâmetros, consulte <a href="https://milvus.io/api-reference/node/v2.4.x/Collections/createCollection.md">createCollection</a> e <a href="https://milvus.io/api-reference/node/v2.4.x/Collections/listCollections.md">listCollections</a>.</p>
</div>
<h2 id="Create-indexes" class="common-anchor-header">Criar índices<button data-href="#Create-indexes" class="anchor-icon" translate="no">
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
    </button></h2><p>Os índices melhoram o desempenho das operações de pesquisa e consulta. No Milvus, é possível criar índices em campos vectoriais e em campos escalares. Neste exemplo, vamos criar um índice <code translate="no">IVF_FLAT</code> no campo de vetor <code translate="no">vector</code> e um índice <code translate="no">INVERTED</code> no campo de matriz <code translate="no">color_coord</code>. Para obter mais informações sobre índices, consulte <a href="https://milvus.io/docs/index-vector-fields.md?tab=floating">Indexar campos vectoriais</a> e <a href="https://milvus.io/docs/index-scalar-fields.md">Indexar campos escalares</a>.</p>
<h3 id="Index-vector-field" class="common-anchor-header">Indexar campo vetorial</h3><p>A criação de um índice num campo de vetor pode melhorar o desempenho da pesquisa de semelhança de vectores, que é necessária para cada operação de pesquisa.</p>
<p>O exemplo abaixo cria um índice do tipo <code translate="no">IVF_FLAT</code> no campo de vetor <code translate="no">vector</code>.</p>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a></div>
<pre><code translate="no" class="language-python">index_params = client.prepare_index_params()

index_params.add_index(
    field_name=<span class="hljs-string">&quot;vector&quot;</span>,
    metric_type=<span class="hljs-string">&quot;COSINE&quot;</span>,
    index_type=<span class="hljs-string">&quot;IVF_FLAT&quot;</span>,
    index_name=<span class="hljs-string">&quot;vector_index&quot;</span>,
    params={<span class="hljs-string">&quot;nlist&quot;</span>: <span class="hljs-number">128</span>}
)

client.create_index(collection_name=<span class="hljs-string">&quot;test_collection&quot;</span>, index_params=index_params)
client.describe_index(collection_name=<span class="hljs-string">&quot;test_collection&quot;</span>, index_name=<span class="hljs-string">&quot;vector_index&quot;</span>)

# Output:
# {<span class="hljs-string">&#x27;nlist&#x27;</span>: <span class="hljs-string">&#x27;128&#x27;</span>,
#  <span class="hljs-string">&#x27;index_type&#x27;</span>: <span class="hljs-string">&#x27;IVF_FLAT&#x27;</span>,
#  <span class="hljs-string">&#x27;metric_type&#x27;</span>: <span class="hljs-string">&#x27;COSINE&#x27;</span>,
#  <span class="hljs-string">&#x27;field_name&#x27;</span>: <span class="hljs-string">&#x27;vector&#x27;</span>,
#  <span class="hljs-string">&#x27;index_name&#x27;</span>: <span class="hljs-string">&#x27;vector_index&#x27;</span>}
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-type">IndexParam</span> <span class="hljs-variable">indexParam</span> <span class="hljs-operator">=</span> IndexParam.builder()
        .metricType(IndexParam.MetricType.COSINE)
        .indexType(IndexParam.IndexType.IVF_FLAT)
        .fieldName(<span class="hljs-string">&quot;vector&quot;</span>)
        .indexName(<span class="hljs-string">&quot;vector_index&quot;</span>)
        .build();
<span class="hljs-type">CreateIndexReq</span> <span class="hljs-variable">createIndexReq</span> <span class="hljs-operator">=</span> CreateIndexReq.builder()
        .collectionName(<span class="hljs-string">&quot;test_collection&quot;</span>)
        .indexParams(Collections.singletonList(indexParam))
        .build();
client.createIndex(createIndexReq);
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-keyword">await</span> client.createIndex({
    collection_name: <span class="hljs-string">&quot;test_collection&quot;</span>,
    field_name: <span class="hljs-string">&quot;vector&quot;</span>,
    index_type: <span class="hljs-string">&quot;IVF_FLAT&quot;</span>,
    metric_type: <span class="hljs-string">&quot;COSINE&quot;</span>,   
    index_name: <span class="hljs-string">&quot;vector_index&quot;</span>,
    params: { <span class="hljs-string">&quot;nlist&quot;</span>: <span class="hljs-number">128</span> }
});

res = <span class="hljs-keyword">await</span> client.describeIndex({
    collection_name: <span class="hljs-string">&quot;test_collection&quot;</span>,
    index_name: <span class="hljs-string">&quot;vector_index&quot;</span>
});

console.log(<span class="hljs-string">&quot;Vector index description: &quot;</span> + JSON.stringify(res));

// Output:
// Vector index description: {<span class="hljs-string">&quot;index_descriptions&quot;</span>:[{<span class="hljs-string">&quot;params&quot;</span>:[{<span class="hljs-string">&quot;key&quot;</span>:<span class="hljs-string">&quot;params&quot;</span>,<span class="hljs-string">&quot;value&quot;</span>:<span class="hljs-string">&quot;{\&quot;nlist\&quot;:128}&quot;</span>},{<span class="hljs-string">&quot;key&quot;</span>:<span class="hljs-string">&quot;index_type&quot;</span>,<span class="hljs-string">&quot;value&quot;</span>:<span class="hljs-string">&quot;IVF_FLAT&quot;</span>},{<span class="hljs-string">&quot;key&quot;</span>:<span class="hljs-string">&quot;metric_type&quot;</span>,<span class="hljs-string">&quot;value&quot;</span>:<span class="hljs-string">&quot;COSINE&quot;</span>}],<span class="hljs-string">&quot;index_name&quot;</span>:<span class="hljs-string">&quot;vector_index&quot;</span>,<span class="hljs-string">&quot;indexID&quot;</span>:<span class="hljs-string">&quot;451543183233666062&quot;</span>,<span class="hljs-string">&quot;field_name&quot;</span>:<span class="hljs-string">&quot;vector&quot;</span>,<span class="hljs-string">&quot;indexed_rows&quot;</span>:<span class="hljs-string">&quot;0&quot;</span>,<span class="hljs-string">&quot;total_rows&quot;</span>:<span class="hljs-string">&quot;0&quot;</span>,<span class="hljs-string">&quot;state&quot;</span>:<span class="hljs-string">&quot;Finished&quot;</span>,<span class="hljs-string">&quot;index_state_fail_reason&quot;</span>:<span class="hljs-string">&quot;&quot;</span>,<span class="hljs-string">&quot;pending_index_rows&quot;</span>:<span class="hljs-string">&quot;0&quot;</span>}],<span class="hljs-string">&quot;status&quot;</span>:{<span class="hljs-string">&quot;extra_info&quot;</span>:{},<span class="hljs-string">&quot;error_code&quot;</span>:<span class="hljs-string">&quot;Success&quot;</span>,<span class="hljs-string">&quot;reason&quot;</span>:<span class="hljs-string">&quot;&quot;</span>,<span class="hljs-string">&quot;code&quot;</span>:<span class="hljs-number">0</span>,<span class="hljs-string">&quot;retriable&quot;</span>:false,<span class="hljs-string">&quot;detail&quot;</span>:<span class="hljs-string">&quot;&quot;</span>}}
<button class="copy-code-btn"></button></code></pre>
<div class="language-python">
<p>Para obter mais informações sobre métodos e parâmetros, consulte <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Management/prepare_index_params.md">prepare_index_params</a>, <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Management/create_index.md">create_index</a> e <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Management/describe_index.md">describe_index</a>.</p>
</div>
<div class="language-java">
<p>Para mais informações sobre métodos e parâmetros, consulte <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Management/IndexParam.md">IndexParam</a> e <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Management/createIndex.md">createIndex</a>.</p>
</div>
<div class="language-javascript">
<p>Para mais informações sobre métodos e parâmetros, consulte <a href="https://milvus.io/api-reference/node/v2.4.x/Management/createIndex.md">createIndex</a> e <a href="https://milvus.io/api-reference/node/v2.4.x/Management/describeIndex.md">describeIndex</a>.</p>
</div>
<h3 id="Index-array-field" class="common-anchor-header">Campo de matriz de índices</h3><p>A criação de um índice num campo escalar pode melhorar o desempenho da recuperação de consultas nesse campo, o que é opcional mas recomendado para grandes conjuntos de dados.</p>
<p>Neste exemplo, vamos criar um índice invertido no campo da matriz <code translate="no">color_coord</code>. Isto permitir-nos-á acelerar a filtragem com base neste campo. O índice invertido demonstra um excelente desempenho geral, superando significativamente a filtragem de força bruta utilizando dados brutos quando os dados não são recuperados frequentemente e mantendo um desempenho comparável com operações de recuperação frequentes. Para obter mais informações sobre índices invertidos, consulte <a href="/docs/pt/scalar_index.md#Inverted-indexing">Índice escalar</a>.</p>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a></div>
<pre><code translate="no" class="language-python">index_params = client.prepare_index_params()

index_params.add_index(
    field_name=<span class="hljs-string">&quot;color_coord&quot;</span>,
    index_type=<span class="hljs-string">&quot;INVERTED&quot;</span>,
    index_name=<span class="hljs-string">&quot;inverted_index&quot;</span>
)

client.create_index(collection_name=<span class="hljs-string">&quot;test_collection&quot;</span>, index_params=index_params)
client.describe_index(collection_name=<span class="hljs-string">&quot;test_collection&quot;</span>, index_name=<span class="hljs-string">&quot;inverted_index&quot;</span>)

# Output:
# {<span class="hljs-string">&#x27;index_type&#x27;</span>: <span class="hljs-string">&#x27;INVERTED&#x27;</span>,
#  <span class="hljs-string">&#x27;field_name&#x27;</span>: <span class="hljs-string">&#x27;color_coord&#x27;</span>,
#  <span class="hljs-string">&#x27;index_name&#x27;</span>: <span class="hljs-string">&#x27;inverted_index&#x27;</span>}
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-type">IndexParam</span> <span class="hljs-variable">indexParam</span> <span class="hljs-operator">=</span> IndexParam.builder()
        .indexType(IndexParam.IndexType.INVERTED)
        .fieldName(<span class="hljs-string">&quot;color_coord&quot;</span>)
        .indexName(<span class="hljs-string">&quot;inverted_index&quot;</span>)
        .build();
<span class="hljs-type">CreateIndexReq</span> <span class="hljs-variable">createIndexReq</span> <span class="hljs-operator">=</span> CreateIndexReq.builder()
        .collectionName(<span class="hljs-string">&quot;test_collection&quot;</span>)
        .indexParams(Collections.singletonList(indexParam))
        .build();
client.createIndex(createIndexReq);
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-keyword">await</span> client.createIndex({
    collection_name: <span class="hljs-string">&quot;test_collection&quot;</span>,
    field_name: <span class="hljs-string">&quot;color_coord&quot;</span>,
    index_type: <span class="hljs-string">&quot;INVERTED&quot;</span>,
    index_name: <span class="hljs-string">&quot;inverted_index&quot;</span>
});

res = <span class="hljs-keyword">await</span> client.describeIndex({
    collection_name: <span class="hljs-string">&quot;test_collection&quot;</span>,
    index_name: <span class="hljs-string">&quot;inverted_index&quot;</span>
});

console.log(<span class="hljs-string">&quot;Array index description: &quot;</span> + JSON.stringify(res));

// Output:
// Array index description: {<span class="hljs-string">&quot;index_descriptions&quot;</span>:[{<span class="hljs-string">&quot;params&quot;</span>:[{<span class="hljs-string">&quot;key&quot;</span>:<span class="hljs-string">&quot;index_type&quot;</span>,<span class="hljs-string">&quot;value&quot;</span>:<span class="hljs-string">&quot;INVERTED&quot;</span>}],<span class="hljs-string">&quot;index_name&quot;</span>:<span class="hljs-string">&quot;inverted_index&quot;</span>,<span class="hljs-string">&quot;indexID&quot;</span>:<span class="hljs-string">&quot;451543183233667243&quot;</span>,<span class="hljs-string">&quot;field_name&quot;</span>:<span class="hljs-string">&quot;color_coord&quot;</span>,<span class="hljs-string">&quot;indexed_rows&quot;</span>:<span class="hljs-string">&quot;0&quot;</span>,<span class="hljs-string">&quot;total_rows&quot;</span>:<span class="hljs-string">&quot;0&quot;</span>,<span class="hljs-string">&quot;state&quot;</span>:<span class="hljs-string">&quot;Finished&quot;</span>,<span class="hljs-string">&quot;index_state_fail_reason&quot;</span>:<span class="hljs-string">&quot;&quot;</span>,<span class="hljs-string">&quot;pending_index_rows&quot;</span>:<span class="hljs-string">&quot;0&quot;</span>}],<span class="hljs-string">&quot;status&quot;</span>:{<span class="hljs-string">&quot;extra_info&quot;</span>:{},<span class="hljs-string">&quot;error_code&quot;</span>:<span class="hljs-string">&quot;Success&quot;</span>,<span class="hljs-string">&quot;reason&quot;</span>:<span class="hljs-string">&quot;&quot;</span>,<span class="hljs-string">&quot;code&quot;</span>:<span class="hljs-number">0</span>,<span class="hljs-string">&quot;retriable&quot;</span>:false,<span class="hljs-string">&quot;detail&quot;</span>:<span class="hljs-string">&quot;&quot;</span>}}
<button class="copy-code-btn"></button></code></pre>
<div class="language-python">
<p>Para obter mais informações sobre métodos e parâmetros, consulte <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Management/prepare_index_params.md">prepare_index_params</a>, <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Management/create_index.md">create_index</a> e <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Management/describe_index.md">describe_index</a>.</p>
</div>
<div class="language-java">
<p>Para mais informações sobre métodos e parâmetros, consulte <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Management/IndexParam.md">IndexParam</a> e <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Management/createIndex.md">createIndex</a>.</p>
</div>
<div class="language-javascript">
<p>Para mais informações sobre métodos e parâmetros, consulte <a href="https://milvus.io/api-reference/node/v2.4.x/Management/createIndex.md">createIndex</a> e <a href="https://milvus.io/api-reference/node/v2.4.x/Management/describeIndex.md">describeIndex</a>.</p>
</div>
<h2 id="Insert-data" class="common-anchor-header">Inserir dados<button data-href="#Insert-data" class="anchor-icon" translate="no">
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
    </button></h2><p>Assim que a coleção e os índices forem criados, podemos inserir os dados na coleção. Esta etapa insere 1.000 entidades no site <code translate="no">test_collection</code>.</p>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a></div>
<pre><code translate="no" class="language-python">res = client.insert(collection_name=<span class="hljs-string">&quot;test_collection&quot;</span>, data=data)
<span class="hljs-built_in">print</span>(res)

# Output:
# {<span class="hljs-string">&#x27;insert_count&#x27;</span>: <span class="hljs-number">1000</span>, <span class="hljs-string">&#x27;ids&#x27;</span>: [<span class="hljs-number">0</span>, <span class="hljs-number">1</span>, <span class="hljs-number">2</span>, <span class="hljs-number">3</span>, <span class="hljs-number">4</span>, <span class="hljs-number">5</span>, <span class="hljs-number">6</span>, <span class="hljs-number">7</span>, <span class="hljs-number">8</span>, <span class="hljs-number">9</span>, <span class="hljs-number">10</span>, <span class="hljs-number">11</span>, <span class="hljs-number">12</span>, <span class="hljs-number">13</span>, <span class="hljs-number">14</span>, <span class="hljs-number">15</span>, <span class="hljs-number">16</span>, <span class="hljs-number">17</span>, <span class="hljs-number">18</span>, <span class="hljs-number">19</span>, <span class="hljs-number">20</span>, <span class="hljs-number">21</span>, <span class="hljs-number">22</span>, <span class="hljs-number">23</span>, <span class="hljs-number">24</span>, <span class="hljs-number">25</span>, <span class="hljs-number">26</span>, <span class="hljs-number">27</span>, <span class="hljs-number">28</span>, <span class="hljs-number">29</span>, <span class="hljs-number">30</span>, <span class="hljs-number">31</span>, <span class="hljs-number">32</span>, <span class="hljs-number">33</span>, <span class="hljs-number">34</span>, <span class="hljs-number">35</span>, <span class="hljs-number">36</span>, <span class="hljs-number">37</span>, <span class="hljs-number">38</span>, <span class="hljs-number">39</span>, <span class="hljs-number">40</span>, <span class="hljs-number">41</span>, <span class="hljs-number">42</span>, <span class="hljs-number">43</span>, <span class="hljs-number">44</span>, <span class="hljs-number">45</span>, <span class="hljs-number">46</span>, <span class="hljs-number">47</span>, <span class="hljs-number">48</span>, <span class="hljs-number">49</span>, <span class="hljs-number">50</span>, <span class="hljs-number">51</span>, <span class="hljs-number">52</span>, <span class="hljs-number">53</span>, <span class="hljs-number">54</span>, <span class="hljs-number">55</span>, <span class="hljs-number">56</span>, <span class="hljs-number">57</span>, <span class="hljs-number">58</span>, <span class="hljs-number">59</span>, <span class="hljs-number">60</span>, <span class="hljs-number">61</span>, <span class="hljs-number">62</span>, <span class="hljs-number">63</span>, <span class="hljs-number">64</span>, <span class="hljs-number">65</span>, <span class="hljs-number">66</span>, <span class="hljs-number">67</span>, <span class="hljs-number">68</span>, <span class="hljs-number">69</span>, <span class="hljs-number">70</span>, <span class="hljs-number">71</span>, <span class="hljs-number">72</span>, <span class="hljs-number">73</span>, <span class="hljs-number">74</span>, <span class="hljs-number">75</span>, <span class="hljs-number">76</span>, <span class="hljs-number">77</span>, <span class="hljs-number">78</span>, <span class="hljs-number">79</span>, <span class="hljs-number">80</span>, <span class="hljs-number">81</span>, <span class="hljs-number">82</span>, <span class="hljs-number">83</span>, <span class="hljs-number">84</span>, <span class="hljs-number">85</span>, <span class="hljs-number">86</span>, <span class="hljs-number">87</span>, <span class="hljs-number">88</span>, <span class="hljs-number">89</span>, <span class="hljs-number">90</span>, <span class="hljs-number">91</span>, <span class="hljs-number">92</span>, <span class="hljs-number">93</span>, <span class="hljs-number">94</span>, <span class="hljs-number">95</span>, <span class="hljs-number">96</span>, <span class="hljs-number">97</span>, <span class="hljs-number">98</span>, <span class="hljs-number">99</span>, <span class="hljs-number">100</span>, <span class="hljs-number">101</span>, <span class="hljs-number">102</span>, <span class="hljs-number">103</span>, <span class="hljs-number">104</span>, <span class="hljs-number">105</span>, <span class="hljs-number">106</span>, <span class="hljs-number">107</span>, <span class="hljs-number">108</span>, <span class="hljs-number">109</span>, <span class="hljs-number">110</span>, <span class="hljs-number">111</span>, <span class="hljs-number">112</span>, <span class="hljs-number">113</span>, <span class="hljs-number">114</span>, <span class="hljs-number">115</span>, <span class="hljs-number">116</span>, <span class="hljs-number">117</span>, <span class="hljs-number">118</span>, <span class="hljs-number">119</span>, <span class="hljs-number">120</span>, <span class="hljs-number">121</span>, <span class="hljs-number">122</span>, <span class="hljs-number">123</span>, <span class="hljs-number">124</span>, <span class="hljs-number">125</span>, <span class="hljs-number">126</span>, <span class="hljs-number">127</span>, <span class="hljs-number">128</span>, <span class="hljs-number">129</span>, <span class="hljs-number">130</span>, <span class="hljs-number">131</span>, <span class="hljs-number">132</span>, <span class="hljs-number">133</span>, <span class="hljs-number">134</span>, <span class="hljs-number">135</span>, <span class="hljs-number">136</span>, <span class="hljs-number">137</span>, <span class="hljs-number">138</span>, <span class="hljs-number">139</span>, <span class="hljs-number">140</span>, <span class="hljs-number">141</span>, <span class="hljs-number">142</span>, <span class="hljs-number">143</span>, <span class="hljs-number">144</span>, <span class="hljs-number">145</span>, <span class="hljs-number">146</span>, <span class="hljs-number">147</span>, <span class="hljs-number">148</span>, <span class="hljs-number">149</span>, <span class="hljs-number">150</span>, <span class="hljs-number">151</span>, <span class="hljs-number">152</span>, <span class="hljs-number">153</span>, <span class="hljs-number">154</span>, <span class="hljs-number">155</span>, <span class="hljs-number">156</span>, <span class="hljs-number">157</span>, <span class="hljs-number">158</span>, <span class="hljs-number">159</span>, <span class="hljs-number">160</span>, <span class="hljs-number">161</span>, <span class="hljs-number">162</span>, <span class="hljs-number">163</span>, <span class="hljs-number">164</span>, <span class="hljs-number">165</span>, <span class="hljs-number">166</span>, <span class="hljs-number">167</span>, <span class="hljs-number">168</span>, <span class="hljs-number">169</span>, <span class="hljs-number">170</span>, <span class="hljs-number">171</span>, <span class="hljs-number">172</span>, <span class="hljs-number">173</span>, <span class="hljs-number">174</span>, <span class="hljs-number">175</span>, <span class="hljs-number">176</span>, <span class="hljs-number">177</span>, <span class="hljs-number">178</span>, <span class="hljs-number">179</span>, <span class="hljs-number">180</span>, <span class="hljs-number">181</span>, <span class="hljs-number">182</span>, <span class="hljs-number">183</span>, <span class="hljs-number">184</span>, <span class="hljs-number">185</span>, <span class="hljs-number">186</span>, <span class="hljs-number">187</span>, <span class="hljs-number">188</span>, <span class="hljs-number">189</span>, <span class="hljs-number">190</span>, <span class="hljs-number">191</span>, <span class="hljs-number">192</span>, <span class="hljs-number">193</span>, <span class="hljs-number">194</span>, <span class="hljs-number">195</span>, <span class="hljs-number">196</span>, <span class="hljs-number">197</span>, <span class="hljs-number">198</span>, <span class="hljs-number">199</span>, <span class="hljs-number">200</span>, <span class="hljs-number">201</span>, <span class="hljs-number">202</span>, <span class="hljs-number">203</span>, <span class="hljs-number">204</span>, <span class="hljs-number">205</span>, <span class="hljs-number">206</span>, <span class="hljs-number">207</span>, <span class="hljs-number">208</span>, <span class="hljs-number">209</span>, <span class="hljs-number">210</span>, <span class="hljs-number">211</span>, <span class="hljs-number">212</span>, <span class="hljs-number">213</span>, <span class="hljs-number">214</span>, <span class="hljs-number">215</span>, <span class="hljs-number">216</span>, <span class="hljs-number">217</span>, <span class="hljs-number">218</span>, <span class="hljs-number">219</span>, <span class="hljs-number">220</span>, <span class="hljs-number">221</span>, <span class="hljs-number">222</span>, <span class="hljs-number">223</span>, <span class="hljs-number">224</span>, <span class="hljs-number">225</span>, <span class="hljs-number">226</span>, <span class="hljs-number">227</span>, <span class="hljs-number">228</span>, <span class="hljs-number">229</span>, <span class="hljs-number">230</span>, <span class="hljs-number">231</span>, <span class="hljs-number">232</span>, <span class="hljs-number">233</span>, <span class="hljs-number">234</span>, <span class="hljs-number">235</span>, <span class="hljs-number">236</span>, <span class="hljs-number">237</span>, <span class="hljs-number">238</span>, <span class="hljs-number">239</span>, <span class="hljs-number">240</span>, <span class="hljs-number">241</span>, <span class="hljs-number">242</span>, <span class="hljs-number">243</span>, <span class="hljs-number">244</span>, <span class="hljs-number">245</span>, <span class="hljs-number">246</span>, <span class="hljs-number">247</span>, <span class="hljs-number">248</span>, <span class="hljs-number">249</span>, <span class="hljs-number">250</span>, <span class="hljs-number">251</span>, <span class="hljs-number">252</span>, <span class="hljs-number">253</span>, <span class="hljs-number">254</span>, <span class="hljs-number">255</span>, <span class="hljs-number">256</span>, <span class="hljs-number">257</span>, <span class="hljs-number">258</span>, <span class="hljs-number">259</span>, <span class="hljs-number">260</span>, <span class="hljs-number">261</span>, <span class="hljs-number">262</span>, <span class="hljs-number">263</span>, <span class="hljs-number">264</span>, <span class="hljs-number">265</span>, <span class="hljs-number">266</span>, <span class="hljs-number">267</span>, <span class="hljs-number">268</span>, <span class="hljs-number">269</span>, <span class="hljs-number">270</span>, <span class="hljs-number">271</span>, <span class="hljs-number">272</span>, <span class="hljs-number">273</span>, <span class="hljs-number">274</span>, <span class="hljs-number">275</span>, <span class="hljs-number">276</span>, <span class="hljs-number">277</span>, <span class="hljs-number">278</span>, <span class="hljs-number">279</span>, <span class="hljs-number">280</span>, <span class="hljs-number">281</span>, <span class="hljs-number">282</span>, <span class="hljs-number">283</span>, <span class="hljs-number">284</span>, <span class="hljs-number">285</span>, <span class="hljs-number">286</span>, <span class="hljs-number">287</span>, <span class="hljs-number">288</span>, <span class="hljs-number">289</span>, <span class="hljs-number">290</span>, <span class="hljs-number">291</span>, <span class="hljs-number">292</span>, <span class="hljs-number">293</span>, <span class="hljs-number">294</span>, <span class="hljs-number">295</span>, <span class="hljs-number">296</span>, <span class="hljs-number">297</span>, <span class="hljs-number">298</span>, <span class="hljs-number">299</span>, <span class="hljs-number">300</span>, <span class="hljs-number">301</span>, <span class="hljs-number">302</span>, <span class="hljs-number">303</span>, <span class="hljs-number">304</span>, <span class="hljs-number">305</span>, <span class="hljs-number">306</span>, <span class="hljs-number">307</span>, <span class="hljs-number">308</span>, <span class="hljs-number">309</span>, <span class="hljs-number">310</span>, <span class="hljs-number">311</span>, <span class="hljs-number">312</span>, <span class="hljs-number">313</span>, <span class="hljs-number">314</span>, <span class="hljs-number">315</span>, <span class="hljs-number">316</span>, <span class="hljs-number">317</span>, <span class="hljs-number">318</span>, <span class="hljs-number">319</span>, <span class="hljs-number">320</span>, <span class="hljs-number">321</span>, <span class="hljs-number">322</span>, <span class="hljs-number">323</span>, <span class="hljs-number">324</span>, <span class="hljs-number">325</span>, <span class="hljs-number">326</span>, <span class="hljs-number">327</span>, <span class="hljs-number">328</span>, <span class="hljs-number">329</span>, <span class="hljs-number">330</span>, <span class="hljs-number">331</span>, <span class="hljs-number">332</span>, <span class="hljs-number">333</span>, <span class="hljs-number">334</span>, <span class="hljs-number">335</span>, <span class="hljs-number">336</span>, <span class="hljs-number">337</span>, <span class="hljs-number">338</span>, <span class="hljs-number">339</span>, <span class="hljs-number">340</span>, <span class="hljs-number">341</span>, <span class="hljs-number">342</span>, <span class="hljs-number">343</span>, <span class="hljs-number">344</span>, <span class="hljs-number">345</span>, <span class="hljs-number">346</span>, <span class="hljs-number">347</span>, <span class="hljs-number">348</span>, <span class="hljs-number">349</span>, <span class="hljs-number">350</span>, <span class="hljs-number">351</span>, <span class="hljs-number">352</span>, <span class="hljs-number">353</span>, <span class="hljs-number">354</span>, <span class="hljs-number">355</span>, <span class="hljs-number">356</span>, <span class="hljs-number">357</span>, <span class="hljs-number">358</span>, <span class="hljs-number">359</span>, <span class="hljs-number">360</span>, <span class="hljs-number">361</span>, <span class="hljs-number">362</span>, <span class="hljs-number">363</span>, <span class="hljs-number">364</span>, <span class="hljs-number">365</span>, <span class="hljs-number">366</span>, <span class="hljs-number">367</span>, <span class="hljs-number">368</span>, <span class="hljs-number">369</span>, <span class="hljs-number">370</span>, <span class="hljs-number">371</span>, <span class="hljs-number">372</span>, <span class="hljs-number">373</span>, <span class="hljs-number">374</span>, <span class="hljs-number">375</span>, <span class="hljs-number">376</span>, <span class="hljs-number">377</span>, <span class="hljs-number">378</span>, <span class="hljs-number">379</span>, <span class="hljs-number">380</span>, <span class="hljs-number">381</span>, <span class="hljs-number">382</span>, <span class="hljs-number">383</span>, <span class="hljs-number">384</span>, <span class="hljs-number">385</span>, <span class="hljs-number">386</span>, <span class="hljs-number">387</span>, <span class="hljs-number">388</span>, <span class="hljs-number">389</span>, <span class="hljs-number">390</span>, <span class="hljs-number">391</span>, <span class="hljs-number">392</span>, <span class="hljs-number">393</span>, <span class="hljs-number">394</span>, <span class="hljs-number">395</span>, <span class="hljs-number">396</span>, <span class="hljs-number">397</span>, <span class="hljs-number">398</span>, <span class="hljs-number">399</span>, <span class="hljs-number">400</span>, <span class="hljs-number">401</span>, <span class="hljs-number">402</span>, <span class="hljs-number">403</span>, <span class="hljs-number">404</span>, <span class="hljs-number">405</span>, <span class="hljs-number">406</span>, <span class="hljs-number">407</span>, <span class="hljs-number">408</span>, <span class="hljs-number">409</span>, <span class="hljs-number">410</span>, <span class="hljs-number">411</span>, <span class="hljs-number">412</span>, <span class="hljs-number">413</span>, <span class="hljs-number">414</span>, <span class="hljs-number">415</span>, <span class="hljs-number">416</span>, <span class="hljs-number">417</span>, <span class="hljs-number">418</span>, <span class="hljs-number">419</span>, <span class="hljs-number">420</span>, <span class="hljs-number">421</span>, <span class="hljs-number">422</span>, <span class="hljs-number">423</span>, <span class="hljs-number">424</span>, <span class="hljs-number">425</span>, <span class="hljs-number">426</span>, <span class="hljs-number">427</span>, <span class="hljs-number">428</span>, <span class="hljs-number">429</span>, <span class="hljs-number">430</span>, <span class="hljs-number">431</span>, <span class="hljs-number">432</span>, <span class="hljs-number">433</span>, <span class="hljs-number">434</span>, <span class="hljs-number">435</span>, <span class="hljs-number">436</span>, <span class="hljs-number">437</span>, <span class="hljs-number">438</span>, <span class="hljs-number">439</span>, <span class="hljs-number">440</span>, <span class="hljs-number">441</span>, <span class="hljs-number">442</span>, <span class="hljs-number">443</span>, <span class="hljs-number">444</span>, <span class="hljs-number">445</span>, <span class="hljs-number">446</span>, <span class="hljs-number">447</span>, <span class="hljs-number">448</span>, <span class="hljs-number">449</span>, <span class="hljs-number">450</span>, <span class="hljs-number">451</span>, <span class="hljs-number">452</span>, <span class="hljs-number">453</span>, <span class="hljs-number">454</span>, <span class="hljs-number">455</span>, <span class="hljs-number">456</span>, <span class="hljs-number">457</span>, <span class="hljs-number">458</span>, <span class="hljs-number">459</span>, <span class="hljs-number">460</span>, <span class="hljs-number">461</span>, <span class="hljs-number">462</span>, <span class="hljs-number">463</span>, <span class="hljs-number">464</span>, <span class="hljs-number">465</span>, <span class="hljs-number">466</span>, <span class="hljs-number">467</span>, <span class="hljs-number">468</span>, <span class="hljs-number">469</span>, <span class="hljs-number">470</span>, <span class="hljs-number">471</span>, <span class="hljs-number">472</span>, <span class="hljs-number">473</span>, <span class="hljs-number">474</span>, <span class="hljs-number">475</span>, <span class="hljs-number">476</span>, <span class="hljs-number">477</span>, <span class="hljs-number">478</span>, <span class="hljs-number">479</span>, <span class="hljs-number">480</span>, <span class="hljs-number">481</span>, <span class="hljs-number">482</span>, <span class="hljs-number">483</span>, <span class="hljs-number">484</span>, <span class="hljs-number">485</span>, <span class="hljs-number">486</span>, <span class="hljs-number">487</span>, <span class="hljs-number">488</span>, <span class="hljs-number">489</span>, <span class="hljs-number">490</span>, <span class="hljs-number">491</span>, <span class="hljs-number">492</span>, <span class="hljs-number">493</span>, <span class="hljs-number">494</span>, <span class="hljs-number">495</span>, <span class="hljs-number">496</span>, <span class="hljs-number">497</span>, <span class="hljs-number">498</span>, <span class="hljs-number">499</span>, <span class="hljs-number">500</span>, <span class="hljs-number">501</span>, <span class="hljs-number">502</span>, <span class="hljs-number">503</span>, <span class="hljs-number">504</span>, <span class="hljs-number">505</span>, <span class="hljs-number">506</span>, <span class="hljs-number">507</span>, <span class="hljs-number">508</span>, <span class="hljs-number">509</span>, <span class="hljs-number">510</span>, <span class="hljs-number">511</span>, <span class="hljs-number">512</span>, <span class="hljs-number">513</span>, <span class="hljs-number">514</span>, <span class="hljs-number">515</span>, <span class="hljs-number">516</span>, <span class="hljs-number">517</span>, <span class="hljs-number">518</span>, <span class="hljs-number">519</span>, <span class="hljs-number">520</span>, <span class="hljs-number">521</span>, <span class="hljs-number">522</span>, <span class="hljs-number">523</span>, <span class="hljs-number">524</span>, <span class="hljs-number">525</span>, <span class="hljs-number">526</span>, <span class="hljs-number">527</span>, <span class="hljs-number">528</span>, <span class="hljs-number">529</span>, <span class="hljs-number">530</span>, <span class="hljs-number">531</span>, <span class="hljs-number">532</span>, <span class="hljs-number">533</span>, <span class="hljs-number">534</span>, <span class="hljs-number">535</span>, <span class="hljs-number">536</span>, <span class="hljs-number">537</span>, <span class="hljs-number">538</span>, <span class="hljs-number">539</span>, <span class="hljs-number">540</span>, <span class="hljs-number">541</span>, <span class="hljs-number">542</span>, <span class="hljs-number">543</span>, <span class="hljs-number">544</span>, <span class="hljs-number">545</span>, <span class="hljs-number">546</span>, <span class="hljs-number">547</span>, <span class="hljs-number">548</span>, <span class="hljs-number">549</span>, <span class="hljs-number">550</span>, <span class="hljs-number">551</span>, <span class="hljs-number">552</span>, <span class="hljs-number">553</span>, <span class="hljs-number">554</span>, <span class="hljs-number">555</span>, <span class="hljs-number">556</span>, <span class="hljs-number">557</span>, <span class="hljs-number">558</span>, <span class="hljs-number">559</span>, <span class="hljs-number">560</span>, <span class="hljs-number">561</span>, <span class="hljs-number">562</span>, <span class="hljs-number">563</span>, <span class="hljs-number">564</span>, <span class="hljs-number">565</span>, <span class="hljs-number">566</span>, <span class="hljs-number">567</span>, <span class="hljs-number">568</span>, <span class="hljs-number">569</span>, <span class="hljs-number">570</span>, <span class="hljs-number">571</span>, <span class="hljs-number">572</span>, <span class="hljs-number">573</span>, <span class="hljs-number">574</span>, <span class="hljs-number">575</span>, <span class="hljs-number">576</span>, <span class="hljs-number">577</span>, <span class="hljs-number">578</span>, <span class="hljs-number">579</span>, <span class="hljs-number">580</span>, <span class="hljs-number">581</span>, <span class="hljs-number">582</span>, <span class="hljs-number">583</span>, <span class="hljs-number">584</span>, <span class="hljs-number">585</span>, <span class="hljs-number">586</span>, <span class="hljs-number">587</span>, <span class="hljs-number">588</span>, <span class="hljs-number">589</span>, <span class="hljs-number">590</span>, <span class="hljs-number">591</span>, <span class="hljs-number">592</span>, <span class="hljs-number">593</span>, <span class="hljs-number">594</span>, <span class="hljs-number">595</span>, <span class="hljs-number">596</span>, <span class="hljs-number">597</span>, <span class="hljs-number">598</span>, <span class="hljs-number">599</span>, <span class="hljs-number">600</span>, <span class="hljs-number">601</span>, <span class="hljs-number">602</span>, <span class="hljs-number">603</span>, <span class="hljs-number">604</span>, <span class="hljs-number">605</span>, <span class="hljs-number">606</span>, <span class="hljs-number">607</span>, <span class="hljs-number">608</span>, <span class="hljs-number">609</span>, <span class="hljs-number">610</span>, <span class="hljs-number">611</span>, <span class="hljs-number">612</span>, <span class="hljs-number">613</span>, <span class="hljs-number">614</span>, <span class="hljs-number">615</span>, <span class="hljs-number">616</span>, <span class="hljs-number">617</span>, <span class="hljs-number">618</span>, <span class="hljs-number">619</span>, <span class="hljs-number">620</span>, <span class="hljs-number">621</span>, <span class="hljs-number">622</span>, <span class="hljs-number">623</span>, <span class="hljs-number">624</span>, <span class="hljs-number">625</span>, <span class="hljs-number">626</span>, <span class="hljs-number">627</span>, <span class="hljs-number">628</span>, <span class="hljs-number">629</span>, <span class="hljs-number">630</span>, <span class="hljs-number">631</span>, <span class="hljs-number">632</span>, <span class="hljs-number">633</span>, <span class="hljs-number">634</span>, <span class="hljs-number">635</span>, <span class="hljs-number">636</span>, <span class="hljs-number">637</span>, <span class="hljs-number">638</span>, <span class="hljs-number">639</span>, <span class="hljs-number">640</span>, <span class="hljs-number">641</span>, <span class="hljs-number">642</span>, <span class="hljs-number">643</span>, <span class="hljs-number">644</span>, <span class="hljs-number">645</span>, <span class="hljs-number">646</span>, <span class="hljs-number">647</span>, <span class="hljs-number">648</span>, <span class="hljs-number">649</span>, <span class="hljs-number">650</span>, <span class="hljs-number">651</span>, <span class="hljs-number">652</span>, <span class="hljs-number">653</span>, <span class="hljs-number">654</span>, <span class="hljs-number">655</span>, <span class="hljs-number">656</span>, <span class="hljs-number">657</span>, <span class="hljs-number">658</span>, <span class="hljs-number">659</span>, <span class="hljs-number">660</span>, <span class="hljs-number">661</span>, <span class="hljs-number">662</span>, <span class="hljs-number">663</span>, <span class="hljs-number">664</span>, <span class="hljs-number">665</span>, <span class="hljs-number">666</span>, <span class="hljs-number">667</span>, <span class="hljs-number">668</span>, <span class="hljs-number">669</span>, <span class="hljs-number">670</span>, <span class="hljs-number">671</span>, <span class="hljs-number">672</span>, <span class="hljs-number">673</span>, <span class="hljs-number">674</span>, <span class="hljs-number">675</span>, <span class="hljs-number">676</span>, <span class="hljs-number">677</span>, <span class="hljs-number">678</span>, <span class="hljs-number">679</span>, <span class="hljs-number">680</span>, <span class="hljs-number">681</span>, <span class="hljs-number">682</span>, <span class="hljs-number">683</span>, <span class="hljs-number">684</span>, <span class="hljs-number">685</span>, <span class="hljs-number">686</span>, <span class="hljs-number">687</span>, <span class="hljs-number">688</span>, <span class="hljs-number">689</span>, <span class="hljs-number">690</span>, <span class="hljs-number">691</span>, <span class="hljs-number">692</span>, <span class="hljs-number">693</span>, <span class="hljs-number">694</span>, <span class="hljs-number">695</span>, <span class="hljs-number">696</span>, <span class="hljs-number">697</span>, <span class="hljs-number">698</span>, <span class="hljs-number">699</span>, <span class="hljs-number">700</span>, <span class="hljs-number">701</span>, <span class="hljs-number">702</span>, <span class="hljs-number">703</span>, <span class="hljs-number">704</span>, <span class="hljs-number">705</span>, <span class="hljs-number">706</span>, <span class="hljs-number">707</span>, <span class="hljs-number">708</span>, <span class="hljs-number">709</span>, <span class="hljs-number">710</span>, <span class="hljs-number">711</span>, <span class="hljs-number">712</span>, <span class="hljs-number">713</span>, <span class="hljs-number">714</span>, <span class="hljs-number">715</span>, <span class="hljs-number">716</span>, <span class="hljs-number">717</span>, <span class="hljs-number">718</span>, <span class="hljs-number">719</span>, <span class="hljs-number">720</span>, <span class="hljs-number">721</span>, <span class="hljs-number">722</span>, <span class="hljs-number">723</span>, <span class="hljs-number">724</span>, <span class="hljs-number">725</span>, <span class="hljs-number">726</span>, <span class="hljs-number">727</span>, <span class="hljs-number">728</span>, <span class="hljs-number">729</span>, <span class="hljs-number">730</span>, <span class="hljs-number">731</span>, <span class="hljs-number">732</span>, <span class="hljs-number">733</span>, <span class="hljs-number">734</span>, <span class="hljs-number">735</span>, <span class="hljs-number">736</span>, <span class="hljs-number">737</span>, <span class="hljs-number">738</span>, <span class="hljs-number">739</span>, <span class="hljs-number">740</span>, <span class="hljs-number">741</span>, <span class="hljs-number">742</span>, <span class="hljs-number">743</span>, <span class="hljs-number">744</span>, <span class="hljs-number">745</span>, <span class="hljs-number">746</span>, <span class="hljs-number">747</span>, <span class="hljs-number">748</span>, <span class="hljs-number">749</span>, <span class="hljs-number">750</span>, <span class="hljs-number">751</span>, <span class="hljs-number">752</span>, <span class="hljs-number">753</span>, <span class="hljs-number">754</span>, <span class="hljs-number">755</span>, <span class="hljs-number">756</span>, <span class="hljs-number">757</span>, <span class="hljs-number">758</span>, <span class="hljs-number">759</span>, <span class="hljs-number">760</span>, <span class="hljs-number">761</span>, <span class="hljs-number">762</span>, <span class="hljs-number">763</span>, <span class="hljs-number">764</span>, <span class="hljs-number">765</span>, <span class="hljs-number">766</span>, <span class="hljs-number">767</span>, <span class="hljs-number">768</span>, <span class="hljs-number">769</span>, <span class="hljs-number">770</span>, <span class="hljs-number">771</span>, <span class="hljs-number">772</span>, <span class="hljs-number">773</span>, <span class="hljs-number">774</span>, <span class="hljs-number">775</span>, <span class="hljs-number">776</span>, <span class="hljs-number">777</span>, <span class="hljs-number">778</span>, <span class="hljs-number">779</span>, <span class="hljs-number">780</span>, <span class="hljs-number">781</span>, <span class="hljs-number">782</span>, <span class="hljs-number">783</span>, <span class="hljs-number">784</span>, <span class="hljs-number">785</span>, <span class="hljs-number">786</span>, <span class="hljs-number">787</span>, <span class="hljs-number">788</span>, <span class="hljs-number">789</span>, <span class="hljs-number">790</span>, <span class="hljs-number">791</span>, <span class="hljs-number">792</span>, <span class="hljs-number">793</span>, <span class="hljs-number">794</span>, <span class="hljs-number">795</span>, <span class="hljs-number">796</span>, <span class="hljs-number">797</span>, <span class="hljs-number">798</span>, <span class="hljs-number">799</span>, <span class="hljs-number">800</span>, <span class="hljs-number">801</span>, <span class="hljs-number">802</span>, <span class="hljs-number">803</span>, <span class="hljs-number">804</span>, <span class="hljs-number">805</span>, <span class="hljs-number">806</span>, <span class="hljs-number">807</span>, <span class="hljs-number">808</span>, <span class="hljs-number">809</span>, <span class="hljs-number">810</span>, <span class="hljs-number">811</span>, <span class="hljs-number">812</span>, <span class="hljs-number">813</span>, <span class="hljs-number">814</span>, <span class="hljs-number">815</span>, <span class="hljs-number">816</span>, <span class="hljs-number">817</span>, <span class="hljs-number">818</span>, <span class="hljs-number">819</span>, <span class="hljs-number">820</span>, <span class="hljs-number">821</span>, <span class="hljs-number">822</span>, <span class="hljs-number">823</span>, <span class="hljs-number">824</span>, <span class="hljs-number">825</span>, <span class="hljs-number">826</span>, <span class="hljs-number">827</span>, <span class="hljs-number">828</span>, <span class="hljs-number">829</span>, <span class="hljs-number">830</span>, <span class="hljs-number">831</span>, <span class="hljs-number">832</span>, <span class="hljs-number">833</span>, <span class="hljs-number">834</span>, <span class="hljs-number">835</span>, <span class="hljs-number">836</span>, <span class="hljs-number">837</span>, <span class="hljs-number">838</span>, <span class="hljs-number">839</span>, <span class="hljs-number">840</span>, <span class="hljs-number">841</span>, <span class="hljs-number">842</span>, <span class="hljs-number">843</span>, <span class="hljs-number">844</span>, <span class="hljs-number">845</span>, <span class="hljs-number">846</span>, <span class="hljs-number">847</span>, <span class="hljs-number">848</span>, <span class="hljs-number">849</span>, <span class="hljs-number">850</span>, <span class="hljs-number">851</span>, <span class="hljs-number">852</span>, <span class="hljs-number">853</span>, <span class="hljs-number">854</span>, <span class="hljs-number">855</span>, <span class="hljs-number">856</span>, <span class="hljs-number">857</span>, <span class="hljs-number">858</span>, <span class="hljs-number">859</span>, <span class="hljs-number">860</span>, <span class="hljs-number">861</span>, <span class="hljs-number">862</span>, <span class="hljs-number">863</span>, <span class="hljs-number">864</span>, <span class="hljs-number">865</span>, <span class="hljs-number">866</span>, <span class="hljs-number">867</span>, <span class="hljs-number">868</span>, <span class="hljs-number">869</span>, <span class="hljs-number">870</span>, <span class="hljs-number">871</span>, <span class="hljs-number">872</span>, <span class="hljs-number">873</span>, <span class="hljs-number">874</span>, <span class="hljs-number">875</span>, <span class="hljs-number">876</span>, <span class="hljs-number">877</span>, <span class="hljs-number">878</span>, <span class="hljs-number">879</span>, <span class="hljs-number">880</span>, <span class="hljs-number">881</span>, <span class="hljs-number">882</span>, <span class="hljs-number">883</span>, <span class="hljs-number">884</span>, <span class="hljs-number">885</span>, <span class="hljs-number">886</span>, <span class="hljs-number">887</span>, <span class="hljs-number">888</span>, <span class="hljs-number">889</span>, <span class="hljs-number">890</span>, <span class="hljs-number">891</span>, <span class="hljs-number">892</span>, <span class="hljs-number">893</span>, <span class="hljs-number">894</span>, <span class="hljs-number">895</span>, <span class="hljs-number">896</span>, <span class="hljs-number">897</span>, <span class="hljs-number">898</span>, <span class="hljs-number">899</span>, <span class="hljs-number">900</span>, <span class="hljs-number">901</span>, <span class="hljs-number">902</span>, <span class="hljs-number">903</span>, <span class="hljs-number">904</span>, <span class="hljs-number">905</span>, <span class="hljs-number">906</span>, <span class="hljs-number">907</span>, <span class="hljs-number">908</span>, <span class="hljs-number">909</span>, <span class="hljs-number">910</span>, <span class="hljs-number">911</span>, <span class="hljs-number">912</span>, <span class="hljs-number">913</span>, <span class="hljs-number">914</span>, <span class="hljs-number">915</span>, <span class="hljs-number">916</span>, <span class="hljs-number">917</span>, <span class="hljs-number">918</span>, <span class="hljs-number">919</span>, <span class="hljs-number">920</span>, <span class="hljs-number">921</span>, <span class="hljs-number">922</span>, <span class="hljs-number">923</span>, <span class="hljs-number">924</span>, <span class="hljs-number">925</span>, <span class="hljs-number">926</span>, <span class="hljs-number">927</span>, <span class="hljs-number">928</span>, <span class="hljs-number">929</span>, <span class="hljs-number">930</span>, <span class="hljs-number">931</span>, <span class="hljs-number">932</span>, <span class="hljs-number">933</span>, <span class="hljs-number">934</span>, <span class="hljs-number">935</span>, <span class="hljs-number">936</span>, <span class="hljs-number">937</span>, <span class="hljs-number">938</span>, <span class="hljs-number">939</span>, <span class="hljs-number">940</span>, <span class="hljs-number">941</span>, <span class="hljs-number">942</span>, <span class="hljs-number">943</span>, <span class="hljs-number">944</span>, <span class="hljs-number">945</span>, <span class="hljs-number">946</span>, <span class="hljs-number">947</span>, <span class="hljs-number">948</span>, <span class="hljs-number">949</span>, <span class="hljs-number">950</span>, <span class="hljs-number">951</span>, <span class="hljs-number">952</span>, <span class="hljs-number">953</span>, <span class="hljs-number">954</span>, <span class="hljs-number">955</span>, <span class="hljs-number">956</span>, <span class="hljs-number">957</span>, <span class="hljs-number">958</span>, <span class="hljs-number">959</span>, <span class="hljs-number">960</span>, <span class="hljs-number">961</span>, <span class="hljs-number">962</span>, <span class="hljs-number">963</span>, <span class="hljs-number">964</span>, <span class="hljs-number">965</span>, <span class="hljs-number">966</span>, <span class="hljs-number">967</span>, <span class="hljs-number">968</span>, <span class="hljs-number">969</span>, <span class="hljs-number">970</span>, <span class="hljs-number">971</span>, <span class="hljs-number">972</span>, <span class="hljs-number">973</span>, <span class="hljs-number">974</span>, <span class="hljs-number">975</span>, <span class="hljs-number">976</span>, <span class="hljs-number">977</span>, <span class="hljs-number">978</span>, <span class="hljs-number">979</span>, <span class="hljs-number">980</span>, <span class="hljs-number">981</span>, <span class="hljs-number">982</span>, <span class="hljs-number">983</span>, <span class="hljs-number">984</span>, <span class="hljs-number">985</span>, <span class="hljs-number">986</span>, <span class="hljs-number">987</span>, <span class="hljs-number">988</span>, <span class="hljs-number">989</span>, <span class="hljs-number">990</span>, <span class="hljs-number">991</span>, <span class="hljs-number">992</span>, <span class="hljs-number">993</span>, <span class="hljs-number">994</span>, <span class="hljs-number">995</span>, <span class="hljs-number">996</span>, <span class="hljs-number">997</span>, <span class="hljs-number">998</span>, <span class="hljs-number">999</span>], <span class="hljs-string">&#x27;cost&#x27;</span>: <span class="hljs-number">0</span>}
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-type">InsertReq</span> <span class="hljs-variable">insertReq</span> <span class="hljs-operator">=</span> InsertReq.builder()
    .collectionName(<span class="hljs-string">&quot;test_collection&quot;</span>)
    .data(data)
    .build();

<span class="hljs-type">InsertResp</span> <span class="hljs-variable">insertResp</span> <span class="hljs-operator">=</span> client.insert(insertReq);
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript">res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">insert</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;test_collection&quot;</span>,
    <span class="hljs-attr">data</span>: data
});

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(<span class="hljs-string">`Inserted <span class="hljs-subst">${res.insert_cnt}</span> entities`</span>);

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// Inserted 1000 entities</span>
<button class="copy-code-btn"></button></code></pre>
<h2 id="Load-the-collection" class="common-anchor-header">Carregar a coleção<button data-href="#Load-the-collection" class="anchor-icon" translate="no">
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
    </button></h2><p>Depois de inserir os dados, precisamos de carregar a coleção para a tornar disponível para operações de pesquisa e consulta.</p>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a></div>
<pre><code translate="no" class="language-python">client.<span class="hljs-title function_">load_collection</span>(<span class="hljs-string">&#x27;test_collection&#x27;</span>)
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-type">LoadCollectionReq</span> <span class="hljs-variable">loadCollectionReq</span> <span class="hljs-operator">=</span> LoadCollectionReq.builder()
        .collectionName(<span class="hljs-string">&quot;test_collection&quot;</span>)
        .build();
client.loadCollection(loadCollectionReq);
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-keyword">await</span> client.<span class="hljs-title function_">loadCollection</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;test_collection&quot;</span>
});

res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">getLoadState</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;test_collection&quot;</span>
});

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(<span class="hljs-string">&quot;Collection load state: &quot;</span> + res.<span class="hljs-property">state</span>);

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// Collection load state: LoadStateLoaded</span>
<button class="copy-code-btn"></button></code></pre>
<h2 id="Basic-scalar-filtering" class="common-anchor-header">Filtragem escalar básica<button data-href="#Basic-scalar-filtering" class="anchor-icon" translate="no">
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
    </button></h2><p>Depois de todos os dados terem sido adicionados, pode efetuar pesquisas e consultas utilizando os elementos do campo de matriz da mesma forma que faria com um campo escalar padrão.</p>
<div class="language-python">
<p>Para mais informações sobre parâmetros, consulte <a href="https://milvus.io/api-reference/pymilvus/v2.4.x/MilvusClient/Vector/search.md"><code translate="no">search()</code></a> na referência do SDK.</p>
</div>
<div class="language-java">
<p>Para obter mais informações sobre parâmetros, consulte <a href="https://milvus.io/api-reference/java/v2.4.x/v2/Vector/search.md"><code translate="no">search()</code></a> na referência do SDK.</p>
</div>
<div class="language-javascript">
<p>Para obter mais informações sobre parâmetros, consulte <a href="https://milvus.io/api-reference/node/v2.4.x/Vector/search.md"><code translate="no">search()</code></a> na referência do SDK.</p>
</div>
<div class="multipleCode">
   <a href="#python">Python </a> <a href="#java">Java</a> <a href="#javascript">Node.js</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># 4. Basic search with the array field</span>
query_vectors = [ [ random.uniform(-<span class="hljs-number">1</span>, <span class="hljs-number">1</span>) <span class="hljs-keyword">for</span> _ <span class="hljs-keyword">in</span> <span class="hljs-built_in">range</span>(<span class="hljs-number">5</span>) ]]

res = client.search(
    collection_name=<span class="hljs-string">&quot;test_collection&quot;</span>,
    data=query_vectors,
    <span class="hljs-built_in">filter</span>=<span class="hljs-string">&quot;color_coord[0] &lt; 10&quot;</span>,
    search_params={
        <span class="hljs-string">&quot;metric_type&quot;</span>: <span class="hljs-string">&quot;COSINE&quot;</span>,
        <span class="hljs-string">&quot;params&quot;</span>: {<span class="hljs-string">&quot;nprobe&quot;</span>: <span class="hljs-number">16</span>}
    },
    output_fields=[<span class="hljs-string">&quot;id&quot;</span>, <span class="hljs-string">&quot;color&quot;</span>, <span class="hljs-string">&quot;color_tag&quot;</span>, <span class="hljs-string">&quot;color_coord&quot;</span>],
    limit=<span class="hljs-number">3</span>
)

<span class="hljs-built_in">print</span>(res)

<span class="hljs-comment"># Output:</span>
<span class="hljs-comment"># data: [&quot;[{&#x27;id&#x27;: 918, &#x27;distance&#x27;: 0.974249541759491, &#x27;entity&#x27;: {&#x27;color_coord&#x27;: [4, 34, 9, 18, 29], &#x27;id&#x27;: 918, &#x27;color&#x27;: &#x27;purple&#x27;, &#x27;color_tag&#x27;: 2940}}, {&#x27;id&#x27;: 822, &#x27;distance&#x27;: 0.9177230000495911, &#x27;entity&#x27;: {&#x27;color_coord&#x27;: [7, 36, 32], &#x27;id&#x27;: 822, &#x27;color&#x27;: &#x27;red&#x27;, &#x27;color_tag&#x27;: 8519}}, {&#x27;id&#x27;: 981, &#x27;distance&#x27;: 0.9116519689559937, &#x27;entity&#x27;: {&#x27;color_coord&#x27;: [7, 16, 40, 32, 32], &#x27;id&#x27;: 981, &#x27;color&#x27;: &#x27;pink&#x27;, &#x27;color_tag&#x27;: 2992}}]&quot;] , extra_info: {&#x27;cost&#x27;: 0}</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-comment">// 4. Basic search with an Array field</span>

<span class="hljs-title class_">QueryReq</span> queryReq = <span class="hljs-title class_">QueryReq</span>.<span class="hljs-title function_">builder</span>()
    .<span class="hljs-title function_">collectionName</span>(<span class="hljs-string">&quot;test_collection&quot;</span>)
    .<span class="hljs-title function_">filter</span>(<span class="hljs-string">&quot;color_coord[0] in [7, 8, 9]&quot;</span>)
    .<span class="hljs-title function_">outputFields</span>(<span class="hljs-title class_">Arrays</span>.<span class="hljs-title function_">asList</span>(<span class="hljs-string">&quot;id&quot;</span>, <span class="hljs-string">&quot;color&quot;</span>, <span class="hljs-string">&quot;color_tag&quot;</span>, <span class="hljs-string">&quot;color_coord&quot;</span>))
    .<span class="hljs-title function_">limit</span>(3L)
    .<span class="hljs-title function_">build</span>();

<span class="hljs-title class_">QueryResp</span> queryResp = client.<span class="hljs-title function_">query</span>(queryReq);

<span class="hljs-title class_">System</span>.<span class="hljs-property">out</span>.<span class="hljs-title function_">println</span>(<span class="hljs-title class_">JSON</span><span class="hljs-built_in">Object</span>.<span class="hljs-title function_">toJSON</span>(queryResp));

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// {&quot;queryResults&quot;: [</span>
<span class="hljs-comment">//     {&quot;entity&quot;: {</span>
<span class="hljs-comment">//         &quot;color&quot;: &quot;orange&quot;,</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: 2464,</span>
<span class="hljs-comment">//         &quot;id&quot;: 18,</span>
<span class="hljs-comment">//         &quot;color_coord&quot;: [</span>
<span class="hljs-comment">//             9,</span>
<span class="hljs-comment">//             30</span>
<span class="hljs-comment">//         ]</span>
<span class="hljs-comment">//     }},</span>
<span class="hljs-comment">//     {&quot;entity&quot;: {</span>
<span class="hljs-comment">//         &quot;color&quot;: &quot;pink&quot;,</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: 2602,</span>
<span class="hljs-comment">//         &quot;id&quot;: 22,</span>
<span class="hljs-comment">//         &quot;color_coord&quot;: [</span>
<span class="hljs-comment">//             8,</span>
<span class="hljs-comment">//             34,</span>
<span class="hljs-comment">//             16</span>
<span class="hljs-comment">//         ]</span>
<span class="hljs-comment">//     }},</span>
<span class="hljs-comment">//     {&quot;entity&quot;: {</span>
<span class="hljs-comment">//         &quot;color&quot;: &quot;pink&quot;,</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: 1243,</span>
<span class="hljs-comment">//         &quot;id&quot;: 42,</span>
<span class="hljs-comment">//         &quot;color_coord&quot;: [</span>
<span class="hljs-comment">//             9,</span>
<span class="hljs-comment">//             20</span>
<span class="hljs-comment">//         ]</span>
<span class="hljs-comment">//     }}</span>
<span class="hljs-comment">// ]}</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-keyword">const</span> query_vectors = [<span class="hljs-title class_">Array</span>(<span class="hljs-number">5</span>).<span class="hljs-title function_">fill</span>(<span class="hljs-number">0</span>).<span class="hljs-title function_">map</span>(<span class="hljs-function">() =&gt;</span> <span class="hljs-title class_">Math</span>.<span class="hljs-title function_">random</span>())];

res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">search</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;test_collection&quot;</span>,
    <span class="hljs-attr">data</span>: query_vectors,
    <span class="hljs-attr">filter</span>: <span class="hljs-string">&quot;color_coord[0] &lt; 10&quot;</span>,
    <span class="hljs-attr">output_fields</span>: [<span class="hljs-string">&quot;id&quot;</span>, <span class="hljs-string">&quot;color&quot;</span>, <span class="hljs-string">&quot;color_tag&quot;</span>, <span class="hljs-string">&quot;color_coord&quot;</span>],
    <span class="hljs-attr">limit</span>: <span class="hljs-number">3</span>,
    <span class="hljs-attr">metric_type</span>: <span class="hljs-string">&quot;COSINE&quot;</span>
});

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(<span class="hljs-string">&quot;Search result: &quot;</span> + <span class="hljs-title class_">JSON</span>.<span class="hljs-title function_">stringify</span>(res));

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// Search result: [</span>
<span class="hljs-comment">//     {</span>
<span class="hljs-comment">//         &quot;score&quot;: 0.9969238042831421,</span>
<span class="hljs-comment">//         &quot;id&quot;: &quot;212&quot;,</span>
<span class="hljs-comment">//         &quot;color&quot;: &quot;green&quot;,</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: &quot;5603&quot;,</span>
<span class="hljs-comment">//         &quot;color_coord&quot;: [</span>
<span class="hljs-comment">//             &quot;9&quot;,</span>
<span class="hljs-comment">//             &quot;14&quot;,</span>
<span class="hljs-comment">//             &quot;22&quot;,</span>
<span class="hljs-comment">//             &quot;4&quot;,</span>
<span class="hljs-comment">//             &quot;35&quot;</span>
<span class="hljs-comment">//         ]</span>
<span class="hljs-comment">//     },</span>
<span class="hljs-comment">//     {</span>
<span class="hljs-comment">//         &quot;score&quot;: 0.9952742457389832,</span>
<span class="hljs-comment">//         &quot;id&quot;: &quot;339&quot;,</span>
<span class="hljs-comment">//         &quot;color&quot;: &quot;yellow&quot;,</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: &quot;8867&quot;,</span>
<span class="hljs-comment">//         &quot;color_coord&quot;: [</span>
<span class="hljs-comment">//             &quot;8&quot;,</span>
<span class="hljs-comment">//             &quot;0&quot;,</span>
<span class="hljs-comment">//             &quot;6&quot;,</span>
<span class="hljs-comment">//             &quot;19&quot;,</span>
<span class="hljs-comment">//             &quot;23&quot;</span>
<span class="hljs-comment">//         ]</span>
<span class="hljs-comment">//     },</span>
<span class="hljs-comment">//     {</span>
<span class="hljs-comment">//         &quot;score&quot;: 0.9944050312042236,</span>
<span class="hljs-comment">//         &quot;id&quot;: &quot;24&quot;,</span>
<span class="hljs-comment">//         &quot;color&quot;: &quot;red&quot;,</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: &quot;7686&quot;,</span>
<span class="hljs-comment">//         &quot;color_coord&quot;: [</span>
<span class="hljs-comment">//             &quot;6&quot;,</span>
<span class="hljs-comment">//             &quot;17&quot;,</span>
<span class="hljs-comment">//             &quot;6&quot;,</span>
<span class="hljs-comment">//             &quot;32&quot;</span>
<span class="hljs-comment">//         ]</span>
<span class="hljs-comment">//     }</span>
<span class="hljs-comment">// ]</span>
<button class="copy-code-btn"></button></code></pre>
<h2 id="Advanced-filtering" class="common-anchor-header">Filtragem avançada<button data-href="#Advanced-filtering" class="anchor-icon" translate="no">
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
    </button></h2><p>À semelhança do que acontece com um campo JSON, o Milvus também fornece operadores de filtragem avançados para arrays, nomeadamente <code translate="no">ARRAY_CONTAINS</code>, <code translate="no">ARRAY_CONTAINS_ALL</code>, <code translate="no">ARRAY_CONTAINS_ANY</code> e <code translate="no">ARRAY_LENGTH</code>. Para mais informações sobre os operadores, consulte a <a href="#reference-on-array-filters">Referência sobre filtros de matrizes</a>.</p>
<ul>
<li><p>Filtra todas as entidades com um <code translate="no">10</code> nos seus valores <code translate="no">color_coord</code>.</p>
<p><div class="multipleCode">
<a href="#python">Python </a><a href="#java">Java</a><a href="#javascript">Node.js</a></div></p>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># 5. Advanced query within the array field</span>

res = client.query(
    collection_name=<span class="hljs-string">&quot;test_collection&quot;</span>,
    <span class="hljs-built_in">filter</span>=<span class="hljs-string">&quot;ARRAY_CONTAINS(color_coord, 10)&quot;</span>,
    output_fields=[<span class="hljs-string">&quot;id&quot;</span>, <span class="hljs-string">&quot;color&quot;</span>, <span class="hljs-string">&quot;color_tag&quot;</span>, <span class="hljs-string">&quot;color_coord&quot;</span>],
    limit=<span class="hljs-number">3</span>
)

<span class="hljs-built_in">print</span>(res)

<span class="hljs-comment"># Output:</span>
<span class="hljs-comment"># data: [&quot;{&#x27;id&#x27;: 2, &#x27;color&#x27;: &#x27;green&#x27;, &#x27;color_tag&#x27;: 3676, &#x27;color_coord&#x27;: [26, 37, 30, 10]}&quot;, &quot;{&#x27;id&#x27;: 28, &#x27;color&#x27;: &#x27;red&#x27;, &#x27;color_tag&#x27;: 4735, &#x27;color_coord&#x27;: [30, 10, 40, 34]}&quot;, &quot;{&#x27;id&#x27;: 32, &#x27;color&#x27;: &#x27;green&#x27;, &#x27;color_tag&#x27;: 8816, &#x27;color_coord&#x27;: [10, 9, 24, 39]}&quot;] , extra_info: {&#x27;cost&#x27;: 0}</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-comment">// 5. Advanced query within an Array field</span>
queryReq = <span class="hljs-title class_">QueryReq</span>.<span class="hljs-title function_">builder</span>()
    .<span class="hljs-title function_">collectionName</span>(<span class="hljs-string">&quot;test_collection&quot;</span>)
    .<span class="hljs-title function_">filter</span>(<span class="hljs-string">&quot;ARRAY_CONTAINS(color_coord, 10)&quot;</span>)
    .<span class="hljs-title function_">outputFields</span>(<span class="hljs-title class_">Arrays</span>.<span class="hljs-title function_">asList</span>(<span class="hljs-string">&quot;id&quot;</span>, <span class="hljs-string">&quot;color&quot;</span>, <span class="hljs-string">&quot;color_tag&quot;</span>, <span class="hljs-string">&quot;color_coord&quot;</span>))
    .<span class="hljs-title function_">limit</span>(<span class="hljs-number">3</span>)
    .<span class="hljs-title function_">build</span>();

queryResp = client.<span class="hljs-title function_">query</span>(queryReq);

<span class="hljs-title class_">System</span>.<span class="hljs-property">out</span>.<span class="hljs-title function_">println</span>(<span class="hljs-title class_">JSON</span><span class="hljs-built_in">Object</span>.<span class="hljs-title function_">toJSON</span>(queryResp));

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// {&quot;queryResults&quot;: [</span>
<span class="hljs-comment">//     {&quot;entity&quot;: {</span>
<span class="hljs-comment">//         &quot;color&quot;: &quot;blue&quot;,</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: 4337,</span>
<span class="hljs-comment">//         &quot;id&quot;: 17,</span>
<span class="hljs-comment">//         &quot;color_coord&quot;: [</span>
<span class="hljs-comment">//             11,</span>
<span class="hljs-comment">//             33,</span>
<span class="hljs-comment">//             10,</span>
<span class="hljs-comment">//             20</span>
<span class="hljs-comment">//         ]</span>
<span class="hljs-comment">//     }},</span>
<span class="hljs-comment">//     {&quot;entity&quot;: {</span>
<span class="hljs-comment">//         &quot;color&quot;: &quot;white&quot;,</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: 5219,</span>
<span class="hljs-comment">//         &quot;id&quot;: 25,</span>
<span class="hljs-comment">//         &quot;color_coord&quot;: [</span>
<span class="hljs-comment">//             10,</span>
<span class="hljs-comment">//             15</span>
<span class="hljs-comment">//         ]</span>
<span class="hljs-comment">//     }},</span>
<span class="hljs-comment">//     {&quot;entity&quot;: {</span>
<span class="hljs-comment">//         &quot;color&quot;: &quot;red&quot;,</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: 7120,</span>
<span class="hljs-comment">//         &quot;id&quot;: 35,</span>
<span class="hljs-comment">//         &quot;color_coord&quot;: [</span>
<span class="hljs-comment">//             19,</span>
<span class="hljs-comment">//             10,</span>
<span class="hljs-comment">//             10,</span>
<span class="hljs-comment">//             14</span>
<span class="hljs-comment">//         ]</span>
<span class="hljs-comment">//     }}</span>
<span class="hljs-comment">// ]}</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-comment">// 5. Advanced search within the array field</span>
res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">search</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;test_collection&quot;</span>,
    <span class="hljs-attr">data</span>: query_vectors,
    <span class="hljs-attr">filter</span>: <span class="hljs-string">&quot;ARRAY_CONTAINS(color_coord, 10)&quot;</span>,
    <span class="hljs-attr">output_fields</span>: [<span class="hljs-string">&quot;id&quot;</span>, <span class="hljs-string">&quot;color&quot;</span>, <span class="hljs-string">&quot;color_tag&quot;</span>, <span class="hljs-string">&quot;color_coord&quot;</span>],
    <span class="hljs-attr">limit</span>: <span class="hljs-number">3</span>
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(<span class="hljs-title class_">JSON</span>.<span class="hljs-title function_">stringify</span>(res.<span class="hljs-property">results</span>, <span class="hljs-literal">null</span>, <span class="hljs-number">4</span>))

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// [</span>
<span class="hljs-comment">//     {</span>
<span class="hljs-comment">//         &quot;score&quot;: 1.7962548732757568,</span>
<span class="hljs-comment">//         &quot;id&quot;: &quot;696&quot;,</span>
<span class="hljs-comment">//         &quot;color&quot;: &quot;red&quot;,</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: &quot;1798&quot;,</span>
<span class="hljs-comment">//         &quot;color_coord&quot;: [</span>
<span class="hljs-comment">//             &quot;33&quot;,</span>
<span class="hljs-comment">//             &quot;10&quot;,</span>
<span class="hljs-comment">//             &quot;37&quot;</span>
<span class="hljs-comment">//         ]</span>
<span class="hljs-comment">//     },</span>
<span class="hljs-comment">//     {</span>
<span class="hljs-comment">//         &quot;score&quot;: 1.7126177549362183,</span>
<span class="hljs-comment">//         &quot;id&quot;: &quot;770&quot;,</span>
<span class="hljs-comment">//         &quot;color&quot;: &quot;red&quot;,</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: &quot;1962&quot;,</span>
<span class="hljs-comment">//         &quot;color_coord&quot;: [</span>
<span class="hljs-comment">//             &quot;21&quot;,</span>
<span class="hljs-comment">//             &quot;23&quot;,</span>
<span class="hljs-comment">//             &quot;10&quot;</span>
<span class="hljs-comment">//         ]</span>
<span class="hljs-comment">//     },</span>
<span class="hljs-comment">//     {</span>
<span class="hljs-comment">//         &quot;score&quot;: 1.6707111597061157,</span>
<span class="hljs-comment">//         &quot;id&quot;: &quot;981&quot;,</span>
<span class="hljs-comment">//         &quot;color&quot;: &quot;yellow&quot;,</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: &quot;3100&quot;,</span>
<span class="hljs-comment">//         &quot;color_coord&quot;: [</span>
<span class="hljs-comment">//             &quot;28&quot;,</span>
<span class="hljs-comment">//             &quot;39&quot;,</span>
<span class="hljs-comment">//             &quot;10&quot;,</span>
<span class="hljs-comment">//             &quot;6&quot;</span>
<span class="hljs-comment">//         ]</span>
<span class="hljs-comment">//     }</span>
<span class="hljs-comment">// ]</span>
<span class="hljs-comment">// </span>
<button class="copy-code-btn"></button></code></pre></li>
<li><p>Filtra todas as entidades com um <code translate="no">7</code> e um <code translate="no">8</code> nos seus valores <code translate="no">color_coord</code>.</p>
<p><div class="multipleCode">
<a href="#python">Python </a><a href="#java">Java</a><a href="#javascript">Node.js</a></div></p>
<pre><code translate="no" class="language-python">res = client.query(
    collection_name=<span class="hljs-string">&quot;test_collection&quot;</span>,
    filter=<span class="hljs-string">&quot;ARRAY_CONTAINS_ALL(color_coord, [7, 8])&quot;</span>,
    output_fields=[<span class="hljs-string">&quot;id&quot;</span>, <span class="hljs-string">&quot;color&quot;</span>, <span class="hljs-string">&quot;color_tag&quot;</span>, <span class="hljs-string">&quot;color_coord&quot;</span>],
    limit=<span class="hljs-number">3</span>
)

<span class="hljs-built_in">print</span>(res)

# Output:
# data: [<span class="hljs-string">&quot;{&#x27;id&#x27;: 147, &#x27;color&#x27;: &#x27;brown&#x27;, &#x27;color_tag&#x27;: 1287, &#x27;color_coord&#x27;: [7, 8, 11, 0]}&quot;</span>, <span class="hljs-string">&quot;{&#x27;id&#x27;: 257, &#x27;color&#x27;: &#x27;white&#x27;, &#x27;color_tag&#x27;: 3641, &#x27;color_coord&#x27;: [2, 8, 31, 7]}&quot;</span>, <span class="hljs-string">&quot;{&#x27;id&#x27;: 280, &#x27;color&#x27;: &#x27;orange&#x27;, &#x27;color_tag&#x27;: 1072, &#x27;color_coord&#x27;: [22, 7, 8]}&quot;</span>] , extra_info: {<span class="hljs-string">&#x27;cost&#x27;</span>: <span class="hljs-number">0</span>}
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java">queryReq = <span class="hljs-title class_">QueryReq</span>.<span class="hljs-title function_">builder</span>()
    .<span class="hljs-title function_">collectionName</span>(<span class="hljs-string">&quot;test_collection&quot;</span>)
    .<span class="hljs-title function_">filter</span>(<span class="hljs-string">&quot;ARRAY_CONTAINS_ALL(color_coord, [7, 8, 9])&quot;</span>)
    .<span class="hljs-title function_">outputFields</span>(<span class="hljs-title class_">Arrays</span>.<span class="hljs-title function_">asList</span>(<span class="hljs-string">&quot;id&quot;</span>, <span class="hljs-string">&quot;color&quot;</span>, <span class="hljs-string">&quot;color_tag&quot;</span>, <span class="hljs-string">&quot;color_coord&quot;</span>))
    .<span class="hljs-title function_">limit</span>(<span class="hljs-number">3</span>)
    .<span class="hljs-title function_">build</span>();

queryResp = client.<span class="hljs-title function_">query</span>(queryReq);

<span class="hljs-title class_">System</span>.<span class="hljs-property">out</span>.<span class="hljs-title function_">println</span>(<span class="hljs-title class_">JSON</span><span class="hljs-built_in">Object</span>.<span class="hljs-title function_">toJSON</span>(queryResp));     

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// {&quot;queryResults&quot;: [{&quot;entity&quot;: {</span>
<span class="hljs-comment">//     &quot;color&quot;: &quot;red&quot;,</span>
<span class="hljs-comment">//     &quot;color_tag&quot;: 6986,</span>
<span class="hljs-comment">//     &quot;id&quot;: 423,</span>
<span class="hljs-comment">//     &quot;color_coord&quot;: [</span>
<span class="hljs-comment">//         26,</span>
<span class="hljs-comment">//         7,</span>
<span class="hljs-comment">//         8,</span>
<span class="hljs-comment">//         9</span>
<span class="hljs-comment">//     ]</span>
<span class="hljs-comment">// }}]}</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript">res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">search</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;test_collection&quot;</span>,
    <span class="hljs-attr">data</span>: query_vectors,
    <span class="hljs-attr">filter</span>: <span class="hljs-string">&quot;ARRAY_CONTAINS_ALL(color_coord, [7, 8])&quot;</span>,
    <span class="hljs-attr">output_fields</span>: [<span class="hljs-string">&quot;id&quot;</span>, <span class="hljs-string">&quot;color&quot;</span>, <span class="hljs-string">&quot;color_tag&quot;</span>, <span class="hljs-string">&quot;color_coord&quot;</span>],
    <span class="hljs-attr">limit</span>: <span class="hljs-number">3</span>
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(<span class="hljs-title class_">JSON</span>.<span class="hljs-title function_">stringify</span>(res.<span class="hljs-property">results</span>, <span class="hljs-literal">null</span>, <span class="hljs-number">4</span>))

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// [</span>
<span class="hljs-comment">//     {</span>
<span class="hljs-comment">//         &quot;score&quot;: 0.8267516493797302,</span>
<span class="hljs-comment">//         &quot;id&quot;: &quot;913&quot;,</span>
<span class="hljs-comment">//         &quot;color&quot;: &quot;brown&quot;,</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: &quot;8897&quot;,</span>
<span class="hljs-comment">//         &quot;color_coord&quot;: [</span>
<span class="hljs-comment">//             &quot;39&quot;,</span>
<span class="hljs-comment">//             &quot;31&quot;,</span>
<span class="hljs-comment">//             &quot;8&quot;,</span>
<span class="hljs-comment">//             &quot;29&quot;,</span>
<span class="hljs-comment">//             &quot;7&quot;</span>
<span class="hljs-comment">//         ]</span>
<span class="hljs-comment">//     },</span>
<span class="hljs-comment">//     {</span>
<span class="hljs-comment">//         &quot;score&quot;: 0.6889009475708008,</span>
<span class="hljs-comment">//         &quot;id&quot;: &quot;826&quot;,</span>
<span class="hljs-comment">//         &quot;color&quot;: &quot;blue&quot;,</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: &quot;4903&quot;,</span>
<span class="hljs-comment">//         &quot;color_coord&quot;: [</span>
<span class="hljs-comment">//             &quot;7&quot;,</span>
<span class="hljs-comment">//             &quot;25&quot;,</span>
<span class="hljs-comment">//             &quot;5&quot;,</span>
<span class="hljs-comment">//             &quot;12&quot;,</span>
<span class="hljs-comment">//             &quot;8&quot;</span>
<span class="hljs-comment">//         ]</span>
<span class="hljs-comment">//     },</span>
<span class="hljs-comment">//     {</span>
<span class="hljs-comment">//         &quot;score&quot;: 0.5851659774780273,</span>
<span class="hljs-comment">//         &quot;id&quot;: &quot;167&quot;,</span>
<span class="hljs-comment">//         &quot;color&quot;: &quot;blue&quot;,</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: &quot;1550&quot;,</span>
<span class="hljs-comment">//         &quot;color_coord&quot;: [</span>
<span class="hljs-comment">//             &quot;8&quot;,</span>
<span class="hljs-comment">//             &quot;27&quot;,</span>
<span class="hljs-comment">//             &quot;7&quot;</span>
<span class="hljs-comment">//         ]</span>
<span class="hljs-comment">//     }</span>
<span class="hljs-comment">// ]</span>
<span class="hljs-comment">// </span>
<button class="copy-code-btn"></button></code></pre></li>
<li><p>Filtra todas as entidades com 7, 8 ou 9 nos seus valores <code translate="no">color_coord</code>.</p>
<p><div class="multipleCode">
<a href="#python">Python </a><a href="#java">Java</a><a href="#javascript">Node.js</a></div></p>
<pre><code translate="no" class="language-python">res = client.query(
    collection_name=<span class="hljs-string">&quot;test_collection&quot;</span>,
    filter=<span class="hljs-string">&quot;ARRAY_CONTAINS_ANY(color_coord, [7, 8, 9])&quot;</span>,
    output_fields=[<span class="hljs-string">&quot;id&quot;</span>, <span class="hljs-string">&quot;color&quot;</span>, <span class="hljs-string">&quot;color_tag&quot;</span>, <span class="hljs-string">&quot;color_coord&quot;</span>],
    limit=<span class="hljs-number">3</span>
)

<span class="hljs-built_in">print</span>(res)

# Output:
# data: [<span class="hljs-string">&quot;{&#x27;id&#x27;: 0, &#x27;color&#x27;: &#x27;white&#x27;, &#x27;color_tag&#x27;: 2081, &#x27;color_coord&#x27;: [16, 7, 35, 5, 25]}&quot;</span>, <span class="hljs-string">&quot;{&#x27;id&#x27;: 1, &#x27;color&#x27;: &#x27;purple&#x27;, &#x27;color_tag&#x27;: 4669, &#x27;color_coord&#x27;: [11, 9, 15, 38, 21]}&quot;</span>, <span class="hljs-string">&quot;{&#x27;id&#x27;: 3, &#x27;color&#x27;: &#x27;yellow&#x27;, &#x27;color_tag&#x27;: 2612, &#x27;color_coord&#x27;: [0, 12, 22, 7]}&quot;</span>] , extra_info: {<span class="hljs-string">&#x27;cost&#x27;</span>: <span class="hljs-number">0</span>}
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java">queryReq = <span class="hljs-title class_">QueryReq</span>.<span class="hljs-title function_">builder</span>()
    .<span class="hljs-title function_">collectionName</span>(<span class="hljs-string">&quot;test_collection&quot;</span>)
    .<span class="hljs-title function_">filter</span>(<span class="hljs-string">&quot;ARRAY_CONTAINS_ANY(color_coord, [7, 8, 9])&quot;</span>)
    .<span class="hljs-title function_">outputFields</span>(<span class="hljs-title class_">Arrays</span>.<span class="hljs-title function_">asList</span>(<span class="hljs-string">&quot;id&quot;</span>, <span class="hljs-string">&quot;color&quot;</span>, <span class="hljs-string">&quot;color_tag&quot;</span>, <span class="hljs-string">&quot;color_coord&quot;</span>))
    .<span class="hljs-title function_">limit</span>(<span class="hljs-number">3</span>)
    .<span class="hljs-title function_">build</span>();

queryResp = client.<span class="hljs-title function_">query</span>(queryReq);

<span class="hljs-title class_">System</span>.<span class="hljs-property">out</span>.<span class="hljs-title function_">println</span>(<span class="hljs-title class_">JSON</span><span class="hljs-built_in">Object</span>.<span class="hljs-title function_">toJSON</span>(queryResp));   

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// {&quot;queryResults&quot;: [</span>
<span class="hljs-comment">//     {&quot;entity&quot;: {</span>
<span class="hljs-comment">//         &quot;color&quot;: &quot;orange&quot;,</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: 2464,</span>
<span class="hljs-comment">//         &quot;id&quot;: 18,</span>
<span class="hljs-comment">//         &quot;color_coord&quot;: [</span>
<span class="hljs-comment">//             9,</span>
<span class="hljs-comment">//             30</span>
<span class="hljs-comment">//         ]</span>
<span class="hljs-comment">//     }},</span>
<span class="hljs-comment">//     {&quot;entity&quot;: {</span>
<span class="hljs-comment">//         &quot;color&quot;: &quot;pink&quot;,</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: 2602,</span>
<span class="hljs-comment">//         &quot;id&quot;: 22,</span>
<span class="hljs-comment">//         &quot;color_coord&quot;: [</span>
<span class="hljs-comment">//             8,</span>
<span class="hljs-comment">//             34,</span>
<span class="hljs-comment">//             16</span>
<span class="hljs-comment">//         ]</span>
<span class="hljs-comment">//     }},</span>
<span class="hljs-comment">//     {&quot;entity&quot;: {</span>
<span class="hljs-comment">//         &quot;color&quot;: &quot;pink&quot;,</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: 1243,</span>
<span class="hljs-comment">//         &quot;id&quot;: 42,</span>
<span class="hljs-comment">//         &quot;color_coord&quot;: [</span>
<span class="hljs-comment">//             9,</span>
<span class="hljs-comment">//             20</span>
<span class="hljs-comment">//         ]</span>
<span class="hljs-comment">//     }}</span>
<span class="hljs-comment">// ]}</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript">res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">search</span>({
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;test_collection&quot;</span>,
    <span class="hljs-attr">data</span>: query_vectors,
    <span class="hljs-attr">filter</span>: <span class="hljs-string">&quot;ARRAY_CONTAINS_ANY(color_coord, [7, 8, 9])&quot;</span>,
    <span class="hljs-attr">output_fields</span>: [<span class="hljs-string">&quot;id&quot;</span>, <span class="hljs-string">&quot;color&quot;</span>, <span class="hljs-string">&quot;color_tag&quot;</span>, <span class="hljs-string">&quot;color_coord&quot;</span>],
    <span class="hljs-attr">limit</span>: <span class="hljs-number">3</span>
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(<span class="hljs-title class_">JSON</span>.<span class="hljs-title function_">stringify</span>(res.<span class="hljs-property">results</span>, <span class="hljs-literal">null</span>, <span class="hljs-number">4</span>))

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// [</span>
<span class="hljs-comment">//     {</span>
<span class="hljs-comment">//         &quot;score&quot;: 2.015894889831543,</span>
<span class="hljs-comment">//         &quot;id&quot;: &quot;260&quot;,</span>
<span class="hljs-comment">//         &quot;color&quot;: &quot;green&quot;,</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: &quot;5320&quot;,</span>
<span class="hljs-comment">//         &quot;color_coord&quot;: [</span>
<span class="hljs-comment">//             &quot;1&quot;,</span>
<span class="hljs-comment">//             &quot;7&quot;,</span>
<span class="hljs-comment">//             &quot;33&quot;,</span>
<span class="hljs-comment">//             &quot;13&quot;,</span>
<span class="hljs-comment">//             &quot;23&quot;</span>
<span class="hljs-comment">//         ]</span>
<span class="hljs-comment">//     },</span>
<span class="hljs-comment">//     {</span>
<span class="hljs-comment">//         &quot;score&quot;: 1.783075213432312,</span>
<span class="hljs-comment">//         &quot;id&quot;: &quot;593&quot;,</span>
<span class="hljs-comment">//         &quot;color&quot;: &quot;orange&quot;,</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: &quot;4079&quot;,</span>
<span class="hljs-comment">//         &quot;color_coord&quot;: [</span>
<span class="hljs-comment">//             &quot;8&quot;,</span>
<span class="hljs-comment">//             &quot;19&quot;</span>
<span class="hljs-comment">//         ]</span>
<span class="hljs-comment">//     },</span>
<span class="hljs-comment">//     {</span>
<span class="hljs-comment">//         &quot;score&quot;: 1.7713876962661743,</span>
<span class="hljs-comment">//         &quot;id&quot;: &quot;874&quot;,</span>
<span class="hljs-comment">//         &quot;color&quot;: &quot;blue&quot;,</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: &quot;7029&quot;,</span>
<span class="hljs-comment">//         &quot;color_coord&quot;: [</span>
<span class="hljs-comment">//             &quot;14&quot;,</span>
<span class="hljs-comment">//             &quot;8&quot;,</span>
<span class="hljs-comment">//             &quot;15&quot;</span>
<span class="hljs-comment">//         ]</span>
<span class="hljs-comment">//     }</span>
<span class="hljs-comment">// ]</span>
<span class="hljs-comment">// </span>
<button class="copy-code-btn"></button></code></pre></li>
<li><p>Filtra entidades que têm exatamente quatro elementos.</p>
<p><div class="multipleCode">
<a href="#python">Python </a><a href="#java">Java</a><a href="#javascript">Node.js</a></div></p>
<pre><code translate="no" class="language-python">res = client.query(
    collection_name=<span class="hljs-string">&quot;test_collection&quot;</span>,
    filter=<span class="hljs-string">&quot;ARRAY_LENGTH(color_coord) == 4&quot;</span>,
    output_fields=[<span class="hljs-string">&quot;id&quot;</span>, <span class="hljs-string">&quot;color&quot;</span>, <span class="hljs-string">&quot;color_tag&quot;</span>, <span class="hljs-string">&quot;color_coord&quot;</span>],
    limit=<span class="hljs-number">3</span>
)

<span class="hljs-built_in">print</span>(res)

# Output:
# data: [<span class="hljs-string">&quot;{&#x27;id&#x27;: 2, &#x27;color&#x27;: &#x27;green&#x27;, &#x27;color_tag&#x27;: 3676, &#x27;color_coord&#x27;: [26, 37, 30, 10]}&quot;</span>, <span class="hljs-string">&quot;{&#x27;id&#x27;: 3, &#x27;color&#x27;: &#x27;yellow&#x27;, &#x27;color_tag&#x27;: 2612, &#x27;color_coord&#x27;: [0, 12, 22, 7]}&quot;</span>, <span class="hljs-string">&quot;{&#x27;id&#x27;: 4, &#x27;color&#x27;: &#x27;green&#x27;, &#x27;color_tag&#x27;: 6912, &#x27;color_coord&#x27;: [4, 5, 19, 28]}&quot;</span>] , extra_info: {<span class="hljs-string">&#x27;cost&#x27;</span>: <span class="hljs-number">0</span>}
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java">queryReq = <span class="hljs-title class_">QueryReq</span>.<span class="hljs-title function_">builder</span>()
    .<span class="hljs-title function_">collectionName</span>(<span class="hljs-string">&quot;test_collection&quot;</span>)
    .<span class="hljs-title function_">filter</span>(<span class="hljs-string">&quot;ARRAY_LENGTH(color_coord) == 4&quot;</span>)
    .<span class="hljs-title function_">outputFields</span>(<span class="hljs-title class_">Arrays</span>.<span class="hljs-title function_">asList</span>(<span class="hljs-string">&quot;id&quot;</span>, <span class="hljs-string">&quot;color&quot;</span>, <span class="hljs-string">&quot;color_tag&quot;</span>, <span class="hljs-string">&quot;color_coord&quot;</span>))
    .<span class="hljs-title function_">limit</span>(<span class="hljs-number">3</span>)
    .<span class="hljs-title function_">build</span>();

queryResp = client.<span class="hljs-title function_">query</span>(queryReq);

<span class="hljs-title class_">System</span>.<span class="hljs-property">out</span>.<span class="hljs-title function_">println</span>(<span class="hljs-title class_">JSON</span><span class="hljs-built_in">Object</span>.<span class="hljs-title function_">toJSON</span>(queryResp));   

<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// {&quot;queryResults&quot;: [</span>
<span class="hljs-comment">//     {&quot;entity&quot;: {</span>
<span class="hljs-comment">//         &quot;color&quot;: &quot;green&quot;,</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: 2984,</span>
<span class="hljs-comment">//         &quot;id&quot;: 2,</span>
<span class="hljs-comment">//         &quot;color_coord&quot;: [</span>
<span class="hljs-comment">//             27,</span>
<span class="hljs-comment">//             31,</span>
<span class="hljs-comment">//             23,</span>
<span class="hljs-comment">//             29</span>
<span class="hljs-comment">//         ]</span>
<span class="hljs-comment">//     }},</span>
<span class="hljs-comment">//     {&quot;entity&quot;: {</span>
<span class="hljs-comment">//         &quot;color&quot;: &quot;black&quot;,</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: 6867,</span>
<span class="hljs-comment">//         &quot;id&quot;: 4,</span>
<span class="hljs-comment">//         &quot;color_coord&quot;: [</span>
<span class="hljs-comment">//             37,</span>
<span class="hljs-comment">//             3,</span>
<span class="hljs-comment">//             30,</span>
<span class="hljs-comment">//             33</span>
<span class="hljs-comment">//         ]</span>
<span class="hljs-comment">//     }},</span>
<span class="hljs-comment">//     {&quot;entity&quot;: {</span>
<span class="hljs-comment">//         &quot;color&quot;: &quot;brown&quot;,</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: 3464,</span>
<span class="hljs-comment">//         &quot;id&quot;: 10,</span>
<span class="hljs-comment">//         &quot;color_coord&quot;: [</span>
<span class="hljs-comment">//             31,</span>
<span class="hljs-comment">//             38,</span>
<span class="hljs-comment">//             21,</span>
<span class="hljs-comment">//             28</span>
<span class="hljs-comment">//         ]</span>
<span class="hljs-comment">//     }}</span>
<span class="hljs-comment">// ]}</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript">res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">search</span>({
<span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;test_collection&quot;</span>,
<span class="hljs-attr">data</span>: query_vectors,
<span class="hljs-attr">filter</span>: <span class="hljs-string">&quot;ARRAY_LENGTH(color_coord) == 4&quot;</span>,
<span class="hljs-attr">output_fields</span>: [<span class="hljs-string">&quot;id&quot;</span>, <span class="hljs-string">&quot;color&quot;</span>, <span class="hljs-string">&quot;color_tag&quot;</span>, <span class="hljs-string">&quot;color_coord&quot;</span>],
<span class="hljs-attr">limit</span>: <span class="hljs-number">3</span>
})

<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(<span class="hljs-title class_">JSON</span>.<span class="hljs-title function_">stringify</span>(res.<span class="hljs-property">results</span>, <span class="hljs-literal">null</span>, <span class="hljs-number">4</span>))

<span class="hljs-comment">// Output</span>
<span class="hljs-comment">// </span>
<span class="hljs-comment">// [</span>
<span class="hljs-comment">//     {</span>
<span class="hljs-comment">//         &quot;score&quot;: 2.0404388904571533,</span>
<span class="hljs-comment">//         &quot;id&quot;: &quot;439&quot;,</span>
<span class="hljs-comment">//         &quot;color&quot;: &quot;orange&quot;,</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: &quot;7096&quot;,</span>
<span class="hljs-comment">//         &quot;color_coord&quot;: [</span>
<span class="hljs-comment">//             &quot;27&quot;,</span>
<span class="hljs-comment">//             &quot;34&quot;,</span>
<span class="hljs-comment">//             &quot;26&quot;,</span>
<span class="hljs-comment">//             &quot;39&quot;</span>
<span class="hljs-comment">//         ]</span>
<span class="hljs-comment">//     },</span>
<span class="hljs-comment">//     {</span>
<span class="hljs-comment">//         &quot;score&quot;: 1.9059759378433228,</span>
<span class="hljs-comment">//         &quot;id&quot;: &quot;918&quot;,</span>
<span class="hljs-comment">//         &quot;color&quot;: &quot;purple&quot;,</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: &quot;2903&quot;,</span>
<span class="hljs-comment">//         &quot;color_coord&quot;: [</span>
<span class="hljs-comment">//             &quot;28&quot;,</span>
<span class="hljs-comment">//             &quot;19&quot;,</span>
<span class="hljs-comment">//             &quot;36&quot;,</span>
<span class="hljs-comment">//             &quot;35&quot;</span>
<span class="hljs-comment">//         ]</span>
<span class="hljs-comment">//     },</span>
<span class="hljs-comment">//     {</span>
<span class="hljs-comment">//         &quot;score&quot;: 1.8385567665100098,</span>
<span class="hljs-comment">//         &quot;id&quot;: &quot;92&quot;,</span>
<span class="hljs-comment">//         &quot;color&quot;: &quot;yellow&quot;,</span>
<span class="hljs-comment">//         &quot;color_tag&quot;: &quot;4693&quot;,</span>
<span class="hljs-comment">//         &quot;color_coord&quot;: [</span>
<span class="hljs-comment">//             &quot;1&quot;,</span>
<span class="hljs-comment">//             &quot;23&quot;,</span>
<span class="hljs-comment">//             &quot;2&quot;,</span>
<span class="hljs-comment">//             &quot;3&quot;</span>
<span class="hljs-comment">//         ]</span>
<span class="hljs-comment">//     }</span>
<span class="hljs-comment">// ]</span>
<span class="hljs-comment">// </span>
<button class="copy-code-btn"></button></code></pre></li>
</ul>
<h2 id="Limits" class="common-anchor-header">Limites<button data-href="#Limits" class="anchor-icon" translate="no">
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
<li><p>Os elementos de um campo ARRAY devem ter o mesmo tipo de dados, especificado por <code translate="no">element_type</code>. Qualquer tipo de dados válido disponível para campos escalares em Milvus pode ser utilizado como <code translate="no">element_type</code>. Para obter uma lista dos tipos de dados suportados, consulte <a href="https://milvus.io/docs/schema.md#Supported-data-types">Tipos de dados suportados</a>.</p></li>
<li><p>O número de elementos num campo ARRAY deve ser inferior ou igual à capacidade máxima do campo array, especificada em <code translate="no">max_capacity</code>.</p></li>
</ul>
<h2 id="Reference-on-array-filters" class="common-anchor-header">Referência sobre filtros de matriz<button data-href="#Reference-on-array-filters" class="anchor-icon" translate="no">
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
    </button></h2><p>Ao trabalhar com campos de matriz, pode colocar um valor de cadeia de caracteres entre aspas duplas ("") ou aspas simples (''). É importante notar que o Milvus armazena os valores das cadeias de caracteres no campo da matriz tal como estão, sem efetuar a fuga semântica ou a conversão. Por exemplo, <strong>'a &quot;b',</strong> <strong>&quot;a'b&quot;,</strong> <strong>'a'b'</strong> e <strong>&quot;a &quot;b&quot;</strong> serão guardados tal como estão, enquanto que <strong>'a'b'</strong> e <strong>&quot;a &quot;b&quot;</strong> serão tratados como valores inválidos.</p>
<p>Suponha que foram definidos dois campos de matriz <code translate="no">int_array</code> e <code translate="no">var_array</code>. A tabela seguinte descreve as expressões booleanas suportadas que pode utilizar em <code translate="no">expr</code> ao pesquisar com campos de matriz.</p>
<table>
<thead>
<tr><th>Operador</th><th>Exemplos</th><th>Observações</th></tr>
</thead>
<tbody>
<tr><td>&lt;</td><td><code translate="no">‘int_array[0] &lt; 3’</code></td><td>Esta expressão é avaliada como verdadeira se o valor de <code translate="no">int_array[0]</code> for inferior a 3.</td></tr>
<tr><td>&gt;</td><td><code translate="no">‘int_array[0] &gt; 5’</code></td><td>Essa expressão será avaliada como verdadeira se o valor de <code translate="no">int_array[0]</code> for maior que 5.</td></tr>
<tr><td>==</td><td><code translate="no">‘int_array[0] == 0’</code></td><td>Esta expressão é avaliada como verdadeira se o valor de <code translate="no">int_array[0]</code> for igual a 0.</td></tr>
<tr><td>!=</td><td><code translate="no">‘var_array[0] != &quot;a&quot;’</code></td><td>Esta expressão é avaliada como verdadeira se o valor de <code translate="no">var_array[0]</code> não for igual a <code translate="no">“a”</code>.</td></tr>
<tr><td>&lt;=</td><td><code translate="no">‘int_array[0] &lt;= 3’</code></td><td>Esta expressão é avaliada como verdadeira se o valor de <code translate="no">int_array[0]</code> for menor ou igual a 3.</td></tr>
<tr><td>&gt;=</td><td><code translate="no">‘int_array[0] &gt;= 10’</code></td><td>Esta expressão é avaliada como verdadeira se o valor de <code translate="no">int_array[0]</code> for maior ou igual a 10.</td></tr>
<tr><td>em</td><td><code translate="no">'var_array[0] in [&quot;str1&quot;, “str2”]'</code></td><td>Esta expressão é avaliada como verdadeira se o valor de <code translate="no">var_array[0]</code> for <code translate="no">“str1”</code> ou <code translate="no">“str2”</code>.</td></tr>
<tr><td>not in</td><td><code translate="no">'int_array[0] not in [1, 2, 3]'</code></td><td>Esta expressão é avaliada como verdadeira se o valor de <code translate="no">int_array[0]</code> não for 1, 2 ou 3.</td></tr>
<tr><td>+, -, *, /, %, **</td><td><code translate="no">‘int_array[0] + 100 &gt; 200’</code></td><td>Esta expressão é avaliada como verdadeira se o valor de <code translate="no">int_array[0] + 100</code> for superior a 200.</td></tr>
<tr><td>like (LIKE)</td><td><code translate="no">‘var_array[0] like &quot;prefix%&quot;’</code></td><td>Esta expressão é avaliada como verdadeira se o valor de <code translate="no">var_array[0]</code> for prefixado com <code translate="no">“prefix”</code>.</td></tr>
<tr><td>and (&amp;&amp;)</td><td><code translate="no">‘var_array[0] like “prefix%” &amp;&amp; int_array[0] &lt;= 100’</code></td><td>Esta expressão é avaliada como verdadeira se o valor de <code translate="no">var_array[0]</code> for prefixado com <code translate="no">“prefix”</code>, e o valor de <code translate="no">int_array[0]</code> for menor ou igual a 100.</td></tr>
<tr><td>or (||)</td><td><code translate="no">‘var_array[0] like “prefix%” || int_array[0] &lt;= 100’</code></td><td>Esta expressão é avaliada como verdadeira se o valor de <code translate="no">var_array[0]</code> for prefixado com <code translate="no">“prefix”</code>, ou se o valor de <code translate="no">int_array[0]</code> for menor ou igual a 100.</td></tr>
<tr><td>array_contains (ARRAY_CONTAINS)</td><td><code translate="no">'array_contains(int_array, 100)'</code></td><td>Esta expressão é avaliada como verdadeira se <code translate="no">int_array</code> contiver o elemento <code translate="no">100</code>.</td></tr>
<tr><td>array_contains_all (ARRAY_CONTAINS_ALL)</td><td><code translate="no">'array_contains_all(int_array, [1, 2, 3])'</code></td><td>Esta expressão é avaliada como verdadeira se <code translate="no">int_array</code> contiver todos os elementos <code translate="no">1</code>, <code translate="no">2</code>, e <code translate="no">3</code>.</td></tr>
<tr><td>array_contains_any (ARRAY_CONTAINS_ANY)</td><td><code translate="no">'array_contains_any(var_array, [&quot;a&quot;, &quot;b&quot;, “c”])'</code></td><td>Esta expressão é avaliada como verdadeira se <code translate="no">var_array</code> contiver qualquer elemento de <code translate="no">“a”</code>, <code translate="no">“b”</code>, e <code translate="no">“c”</code>.</td></tr>
<tr><td>array_length</td><td><code translate="no">‘array_length(int_array) == 10’</code></td><td>Esta expressão é avaliada como verdadeira se <code translate="no">int_array</code> contiver exatamente 10 elementos.</td></tr>
</tbody>
</table>