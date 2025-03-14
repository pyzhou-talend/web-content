---
id: lowercase-filter.md
title: 小寫篩選器
summary: 小寫篩選器會將 tokenizer 產生的詞彙轉換為小寫，使搜尋不區分大小寫。
---
<h1 id="Lowercase​" class="common-anchor-header">小寫<button data-href="#Lowercase​" class="anchor-icon" translate="no">
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
    </button></h1><p><code translate="no">lowercase</code> 過濾器可將 tokenizer 產生的詞彙轉換為小寫，使搜尋不區分大小寫。例如，它可以將<code translate="no">[&quot;High&quot;, &quot;Performance&quot;, &quot;Vector&quot;, &quot;Database&quot;]</code> 轉換為<code translate="no">[&quot;high&quot;, &quot;performance&quot;, &quot;vector&quot;, &quot;database&quot;]</code> 。</p>
<h2 id="Configuration​" class="common-anchor-header">配置<button data-href="#Configuration​" class="anchor-icon" translate="no">
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
    </button></h2><p><code translate="no">lowercase</code> 篩選器內建在 Milvus 中。要使用它，只需在<code translate="no">analyzer_params</code> 中的<code translate="no">filter</code> 部分指定其名稱。</p>
<pre><code translate="no" class="language-python">analyzer_params = {​
    <span class="hljs-string">&quot;tokenizer&quot;</span>: <span class="hljs-string">&quot;standard&quot;</span>,​
    <span class="hljs-string">&quot;filter&quot;</span>: [<span class="hljs-string">&quot;lowercase&quot;</span>],​
}​
<button class="copy-code-btn"></button></code></pre>
<p><code translate="no">lowercase</code> 過濾器是在 tokenizer 產生的詞彙上運作，所以它必須與 tokenizer 結合使用。</p>
<p>定義<code translate="no">analyzer_params</code> 之後，您可以在定義集合模式時，將它們套用到<code translate="no">VARCHAR</code> 欄位。這可讓 Milvus 使用指定的分析器來處理該欄位中的文字，以進行有效率的標記化和過濾。詳情請參閱<a href="/docs/zh-hant/analyzer-overview.md#Example-use">範例使用</a>。</p>
<h2 id="Example-output​" class="common-anchor-header">輸出範例<button data-href="#Example-output​" class="anchor-icon" translate="no">
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
    </button></h2><p>以下是<code translate="no">lowercase</code> 過濾器如何處理文字的範例。</p>
<p><strong>原始文字</strong>。</p>
<pre><code translate="no" class="language-python"><span class="hljs-string">&quot;The Lowercase Filter Ensures Uniformity In Text Processing.&quot;</span>​
<button class="copy-code-btn"></button></code></pre>
<p><strong>預期輸出</strong>。</p>
<pre><code translate="no" class="language-python">[<span class="hljs-string">&quot;the&quot;</span>, <span class="hljs-string">&quot;lowercase&quot;</span>, <span class="hljs-string">&quot;filter&quot;</span>, <span class="hljs-string">&quot;ensures&quot;</span>, <span class="hljs-string">&quot;uniformity&quot;</span>, <span class="hljs-string">&quot;in&quot;</span>, <span class="hljs-string">&quot;text&quot;</span>, <span class="hljs-string">&quot;processing&quot;</span>]​
<button class="copy-code-btn"></button></code></pre>
