---
id: delete-entities.md
title: Delete Entities
---
<h1 id="Delete-Entities​" class="common-anchor-header">Delete Entities​<button data-href="#Delete-Entities​" class="anchor-icon" translate="no">
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
    </button></h1><p>You can delete the entities that are no longer needed by filtering conditions or their primary keys.​</p>
<h2 id="Delete-Entities-by-Filtering-Conditions​" class="common-anchor-header">Delete Entities by Filtering Conditions​<button data-href="#Delete-Entities-by-Filtering-Conditions​" class="anchor-icon" translate="no">
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
    </button></h2><p>When deleting multiple entities that share some attributes in a batch, you can use filter expressions. The example code below uses the <strong>in</strong> operator to bulk delete all Entities with their <strong>color</strong> field set to the values of <strong>red</strong> and <strong>green</strong>. You can also use other operators to construct filter expressions that meet your requirements. For more information about filter expressions, please refer to <a href="/docs/boolean.md">​Metadata Filtering</a>.​</p>
<div class="multipleCode">
  <a href="#python">Python </a>
  <a href="#java">Java</a>
  <a href="#javascript">Node.js</a>
  <a href="#go">Go</a>
  <a href="#curl">cURL</a>
</div>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> MilvusClient​
​
client = MilvusClient(​
    uri=<span class="hljs-string">&quot;http://localhost:19530&quot;</span>,​
    token=<span class="hljs-string">&quot;root:Milvus&quot;</span>​
)​
​
res = client.delete(​
    collection_name=<span class="hljs-string">&quot;quick_setup&quot;</span>,​
    <span class="hljs-comment"># highlight-next-line​</span>
    <span class="hljs-built_in">filter</span>=<span class="hljs-string">&quot;color in [&#x27;red_3314&#x27;, &#x27;purple_7392&#x27;]&quot;</span>​
)​
​
<span class="hljs-built_in">print</span>(res)​
​
<span class="hljs-comment"># Output​</span>
<span class="hljs-comment"># {&#x27;delete_count&#x27;: 2}​</span>

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.milvus.v2.client.ConnectConfig;​
<span class="hljs-keyword">import</span> io.milvus.v2.client.MilvusClientV2;​
<span class="hljs-keyword">import</span> io.milvus.v2.service.vector.request.DeleteReq;​
<span class="hljs-keyword">import</span> io.milvus.v2.service.vector.response.DeleteResp;​
​
<span class="hljs-type">ilvusClientV2</span> <span class="hljs-variable">client</span> <span class="hljs-operator">=</span> <span class="hljs-keyword">new</span> <span class="hljs-title class_">MilvusClientV2</span>(ConnectConfig.builder()​
        .uri(<span class="hljs-string">&quot;http://localhost:19530&quot;</span>)​
        .token(<span class="hljs-string">&quot;root:Milvus&quot;</span>)​
        .build());​
​
<span class="hljs-type">DeleteResp</span> <span class="hljs-variable">deleteResp</span> <span class="hljs-operator">=</span> client.delete(DeleteReq.builder()​
        .collectionName(<span class="hljs-string">&quot;quick_setup&quot;</span>)​
        .filter(<span class="hljs-string">&quot;color in [&#x27;red_3314&#x27;, &#x27;purple_7392&#x27;]&quot;</span>)​
        .build());​
​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-keyword">const</span> { <span class="hljs-title class_">MilvusClient</span>, <span class="hljs-title class_">DataType</span> } = <span class="hljs-built_in">require</span>(<span class="hljs-string">&quot;@zilliz/milvus2-sdk-node&quot;</span>)​
​
<span class="hljs-keyword">const</span> address = <span class="hljs-string">&quot;http://localhost:19530&quot;</span>;​
<span class="hljs-keyword">const</span> token = <span class="hljs-string">&quot;root:Milvus&quot;</span>;​
<span class="hljs-keyword">const</span> client = <span class="hljs-keyword">new</span> <span class="hljs-title class_">MilvusClient</span>({address, token});​
​
<span class="hljs-comment">// 7. Delete entities​</span>
res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">delete</span>({​
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;quick_setup&quot;</span>,​
    <span class="hljs-comment">// highlight-next-line​</span>
    <span class="hljs-attr">filter</span>: <span class="hljs-string">&quot;color in [&#x27;red&#x27;, &#x27;green&#x27;]&quot;</span>​
})​
​
<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">delete_cnt</span>)​
​
<span class="hljs-comment">// Output​</span>
<span class="hljs-comment">// ​</span>
<span class="hljs-comment">// 3​</span>
<span class="hljs-comment">// ​</span>

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-curl">export CLUSTER_ENDPOINT=&quot;http://localhost:19530&quot;​
export TOKEN=&quot;root:Milvus&quot;​
​
curl --request POST \​
--url &quot;${CLUSTER_ENDPOINT}/v2/vectordb/entities/delete&quot; \​
--header &quot;Authorization: Bearer ${TOKEN}&quot; \​
--header &quot;Content-Type: application/json&quot; \​
-d '{​
    &quot;collectionName&quot;: &quot;quick_setup&quot;,​
    &quot;filter&quot;: &quot;color in [\&quot;red_3314\&quot;, \&quot;purple_7392\&quot;]&quot;​
}'​

</code></pre>
<h2 id="Delete-Entities-by-Primary-Keys​" class="common-anchor-header">Delete Entities by Primary Keys​<button data-href="#Delete-Entities-by-Primary-Keys​" class="anchor-icon" translate="no">
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
    </button></h2><p>In most cases, a primary key uniquely identifies an Entity. You can delete Entities by setting their primary keys in the delete request. The example code below demonstrates how to delete two entities with primary keys <strong>18</strong> and <strong>19</strong>.​</p>
<div class="multipleCode">
  <a href="#python">Python </a>
  <a href="#java">Java</a>
  <a href="#javascript">Node.js</a>
  <a href="#go">Go</a>
  <a href="#curl">cURL</a>
</div>
<pre><code translate="no" class="language-python">res = client.delete(​
    collection_name=<span class="hljs-string">&quot;quick_setup&quot;</span>,​
    <span class="hljs-comment"># highlight-next-line​</span>
    ids=[<span class="hljs-number">18</span>, <span class="hljs-number">19</span>]​
)​
​
<span class="hljs-built_in">print</span>(res)​
​
<span class="hljs-comment"># Output​</span>
<span class="hljs-comment"># {&#x27;delete_count&#x27;: 2}​</span>

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.milvus.v2.service.vector.request.DeleteReq;​
<span class="hljs-keyword">import</span> io.milvus.v2.service.vector.response.DeleteResp;​
​
<span class="hljs-keyword">import</span> java.util.Arrays;​
​
​
<span class="hljs-type">DeleteResp</span> <span class="hljs-variable">deleteResp</span> <span class="hljs-operator">=</span> client.delete(DeleteReq.builder()​
        .collectionName(<span class="hljs-string">&quot;quick_setup&quot;</span>)​
        .ids(Arrays.asList(<span class="hljs-number">18</span>, <span class="hljs-number">19</span>))​
        .build());​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-keyword">const</span> { <span class="hljs-title class_">MilvusClient</span>, <span class="hljs-title class_">DataType</span> } = <span class="hljs-built_in">require</span>(<span class="hljs-string">&quot;@zilliz/milvus2-sdk-node&quot;</span>)​
​
res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">delete</span>({​
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;quick_setup&quot;</span>,​
    <span class="hljs-attr">ids</span>: [<span class="hljs-number">18</span>, <span class="hljs-number">19</span>]​
})​
​
<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">delete_cnt</span>)​
​
<span class="hljs-comment">// Output​</span>
<span class="hljs-comment">// ​</span>
<span class="hljs-comment">// 2​</span>
<span class="hljs-comment">// ​</span>

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-curl">export CLUSTER_ENDPOINT=&quot;http://localhost:19530&quot;​
export TOKEN=&quot;root:Milvus&quot;​
​
curl --request POST \​
--url &quot;${CLUSTER_ENDPOINT}/v2/vectordb/entities/delete&quot; \​
--header &quot;Authorization: Bearer ${TOKEN}&quot; \​
--header &quot;Content-Type: application/json&quot; \​
-d '{​
    &quot;collectionName&quot;: &quot;quick_setup&quot;,​
    &quot;filter&quot;: &quot;id in [18, 19]&quot;​
}'​
## {&quot;code&quot;:0,&quot;cost&quot;:0,&quot;data&quot;:{}}​

</code></pre>
<h2 id="Delete-Entities-from-Partitions​" class="common-anchor-header">Delete Entities from Partitions​<button data-href="#Delete-Entities-from-Partitions​" class="anchor-icon" translate="no">
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
    </button></h2><p>You can also delete entities stored in specific partitions. The following code snippets assume that you have a partition named <strong>PartitionA</strong> in your collection.</p>
<div class="multipleCode">
  <a href="#python">Python </a>
  <a href="#java">Java</a>
  <a href="#javascript">Node.js</a>
  <a href="#go">Go</a>
  <a href="#curl">cURL</a>
</div>
<pre><code translate="no" class="language-python">res = client.delete(​
    collection_name=<span class="hljs-string">&quot;quick_setup&quot;</span>,​
    ids=[<span class="hljs-number">18</span>, <span class="hljs-number">19</span>],​
    partition_name=<span class="hljs-string">&quot;partitionA&quot;</span>​
)​
​
<span class="hljs-built_in">print</span>(res)​
​
<span class="hljs-comment"># Output​</span>
<span class="hljs-comment"># {&#x27;delete_count&#x27;: 2}​</span>

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.milvus.v2.service.vector.request.DeleteReq;​
<span class="hljs-keyword">import</span> io.milvus.v2.service.vector.response.DeleteResp;​
​
<span class="hljs-keyword">import</span> java.util.Arrays;​
​
<span class="hljs-type">DeleteResp</span> <span class="hljs-variable">deleteResp</span> <span class="hljs-operator">=</span> client.delete(DeleteReq.builder()​
        .collectionName(<span class="hljs-string">&quot;quick_setup&quot;</span>)​
        .ids(Arrays.asList(<span class="hljs-number">18</span>, <span class="hljs-number">19</span>))​
        .partitionName(<span class="hljs-string">&quot;partitionA&quot;</span>)​
        .build());​

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-keyword">const</span> { <span class="hljs-title class_">MilvusClient</span>, <span class="hljs-title class_">DataType</span> } = <span class="hljs-built_in">require</span>(<span class="hljs-string">&quot;@zilliz/milvus2-sdk-node&quot;</span>)​
​
res = <span class="hljs-keyword">await</span> client.<span class="hljs-title function_">delete</span>({​
    <span class="hljs-attr">collection_name</span>: <span class="hljs-string">&quot;quick_setup&quot;</span>,​
    <span class="hljs-attr">ids</span>: [<span class="hljs-number">18</span>, <span class="hljs-number">19</span>],​
    <span class="hljs-attr">partition_name</span>: <span class="hljs-string">&quot;partitionA&quot;</span>​
})​
​
<span class="hljs-variable language_">console</span>.<span class="hljs-title function_">log</span>(res.<span class="hljs-property">delete_cnt</span>)​
​
<span class="hljs-comment">// Output​</span>
<span class="hljs-comment">// ​</span>
<span class="hljs-comment">// 2​</span>
<span class="hljs-comment">// ​</span>

<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-curl">export CLUSTER_ENDPOINT=&quot;http://localhost:19530&quot;​
export TOKEN=&quot;root:Milvus&quot;​
​
curl --request POST \​
--url &quot;${CLUSTER_ENDPOINT}/v2/vectordb/entities/delete&quot; \​
--header &quot;Authorization: Bearer ${TOKEN}&quot; \​
--header &quot;Content-Type: application/json&quot; \​
-d '{​
    &quot;collectionName&quot;: &quot;quick_setup&quot;,​
    &quot;partitionName&quot;: &quot;partitionA&quot;,​
    &quot;filter&quot;: &quot;id in [18, 19]&quot;​
}'​
​
# {​
#     &quot;code&quot;: 0,​
#     &quot;cost&quot;: 0,​
#     &quot;data&quot;: {}​
# }​

</code></pre>
