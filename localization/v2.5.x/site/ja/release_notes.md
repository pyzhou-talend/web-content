---
id: release_notes.md
summary: Milvusリリースノート
title: リリースノート
---
<h1 id="Release-Notes" class="common-anchor-header">リリースノート<button data-href="#Release-Notes" class="anchor-icon" translate="no">
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
    </button></h1><p>Milvusの新機能をご確認ください！このページでは、各リリースの新機能、改善点、既知の問題、バグ修正についてまとめています。v2.5.0以降の各バージョンのリリースノートはこのセクションにあります。定期的にこのページをご覧いただき、アップデート情報をご確認ください。</p>
<h2 id="v254" class="common-anchor-header">v2.5.4<button data-href="#v254" class="anchor-icon" translate="no">
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
    </button></h2><p>リリース日: 2025年1月23日</p>
<table>
<thead>
<tr><th>Milvusバージョン</th><th>Python SDKバージョン</th><th>Node.js SDKバージョン</th><th>Java SDKバージョン</th></tr>
</thead>
<tbody>
<tr><td>2.5.4</td><td>2.5.4</td><td>2.5.4</td><td>2.5.4</td></tr>
</tbody>
</table>
<p>Milvus2.5.4のリリースを発表できることを嬉しく思います。このリリースでは、主要なパフォーマンス最適化と、PartitionKeyの分離、DAAT MaxScore付きスパースインデックス、強化されたロックメカニズムなどの新機能が導入されています。このリリースの際立ったハイライトは、10,000コレクションと100万パーティションのサポートであり、マルチテナントのユースケースにとって大きなマイルストーンとなります。このバージョンはまた、全体的な安定性と信頼性を向上させる複数のバグに対処しています。Milvusの継続的な改良のため、皆様からのフィードバックをお待ちしております！</p>
<h3 id="Features" class="common-anchor-header">特徴</h3><ul>
<li>PartitionKeyの分離をサポートし、複数のパーティションキーでのパフォーマンスを改善しました<a href="https://github.com/milvus-io/milvus/pull/39245">(#39245</a>)。詳細については、<a href="/docs/ja/use-partition-key.md">パーティションキーの</a>使用を参照してください。</li>
<li>スパースインデックスがDAAT MaxScore<a href="https://github.com/milvus-io/knowhere/pull/1015">knowhere/#1015に</a>対応しました。詳細は「<a href="/docs/ja/sparse_vector.md">スパース・ベクトル</a>」を参照してください。</li>
<li>式中の<code translate="no">is_null</code> をサポートしました<a href="https://github.com/milvus-io/milvus/pull/38931">(#38931</a>)。</li>
<li>ルート権限をカスタマイズできるように<a href="https://github.com/milvus-io/milvus/pull/39324">なりました(#39324</a>)。</li>
</ul>
<h3 id="Improvements" class="common-anchor-header">改良点</h3><ul>
<li>1クラスタで10Kコレクションと100万パーティションをサポート<a href="https://github.com/milvus-io/milvus/pull/37630">(#37630</a>)。</li>
<li>セグメントの差分情報をキャッシュし、クエリコーディネータを高速化<a href="https://github.com/milvus-io/milvus/pull/39349">(#39349</a>)</li>
<li>メタデータをコレクションレベルで同時に読み込み、障害復旧を高速化<a href="https://github.com/milvus-io/milvus/pull/38900">(#38900</a>)</li>
<li>QueryNodeにおけるロックの粒度を改良<a href="https://github.com/milvus-io/milvus/pull/39282">(#39282</a>)、<a href="https://github.com/milvus-io/milvus/pull/38907">(#38907</a>)</li>
<li>NewCollection CGO呼び出しの処理にCStatusを使用することでスタイルを統一した<a href="https://github.com/milvus-io/milvus/pull/39303">(#39303</a>)。</li>
<li>パーティションが設定されていない場合、パーティションリミッターの生成をスキップするようにした(<a href="https://github.com/milvus-io/milvus/pull/38911">#38911</a>)</li>
<li>RESTful APIのサポートを追加した<a href="https://github.com/milvus-io/milvus/pull/38875">(#38875</a>)<a href="https://github.com/milvus-io/milvus/pull/39425">(#39425</a>)</li>
<li>メモリ使用量を減らすために、QueryNodeとDataNodeの不要なブルームフィルタを削除しました<a href="https://github.com/milvus-io/milvus/pull/38913">(#38913</a>)</li>
<li>QueryCoordにおいて、タスク生成、スケジューリング、実行を高速化し、データロードを高速化しました<a href="https://github.com/milvus-io/milvus/pull/38905">(#38905</a>)</li>
<li>DataCoordにおけるロックを削減し、ロードおよびインサート操作を高速化した<a href="https://github.com/milvus-io/milvus/pull/38904">(#38904</a>)</li>
<li><code translate="no">SearchResult</code> および<code translate="no">QueryResults</code> に主フィールド名を追加した<a href="https://github.com/milvus-io/milvus/pull/39222">(#39222</a>)。</li>
<li>ディスククォータ調整基準として、ビンログサイズとインデックスサイズの両方を使用するようにした(<a href="https://github.com/milvus-io/milvus/pull/38844">#38844</a>)</li>
<li>全文検索のメモリ使用量を最適化した knowhere/#1011</li>
<li>スカラインデックスのバージョン管理を追加した<a href="https://github.com/milvus-io/milvus/pull/39236">(#39236</a>)</li>
<li>不要なコピーを回避することにより、RootCoordからのコレクション情報の取得速度を改善した<a href="https://github.com/milvus-io/milvus/pull/38902">(#38902</a>)</li>
</ul>
<h3 id="Critial-Bug-fixs" class="common-anchor-header">重大なバグ修正</h3><ul>
<li>インデックスを持つ主キーの検索失敗を修正した<a href="https://github.com/milvus-io/milvus/pull/39390">(#39390</a>)。</li>
<li>MixCoordの再起動とフラッシュを同時に実行した場合に発生する可能性のあるデータ損失の問題を修正<a href="https://github.com/milvus-io/milvus/pull/39422">(#39422</a>)</li>
<li>MixCoordの再起動後に、統計タスクとL0コンパクション間の不適切な同時実行が原因で発生する削除の失敗を修正しました<a href="https://github.com/milvus-io/milvus/pull/39460">(#39460</a>)</li>
<li>2.4から2.5へのアップグレードにおいて、スカラー逆インデックスの非互換性を修正しました<a href="https://github.com/milvus-io/milvus/pull/39272">(#39272</a>)。</li>
</ul>
<h3 id="Bug-fixes" class="common-anchor-header">バグ修正</h3><ul>
<li>複数列のロード時に粗いロック粒度に起因する遅いクエリの問題を修正しました<a href="https://github.com/milvus-io/milvus/pull/39255">(#39255</a>)。</li>
<li>エイリアスを使用するとイテレータが間違ったデータベースを巡回する問題を修正した<a href="https://github.com/milvus-io/milvus/pull/39248">(#39248</a>)</li>
<li>データベースを変更した場合にリソースグループの更新に失敗する問題を修正した<a href="https://github.com/milvus-io/milvus/pull/39356">(#39356</a>)</li>
<li>tantivyインデックスがリリース中にインデックスファイルを削除できない問題を修正しました<a href="https://github.com/milvus-io/milvus/pull/39434">(#39434</a>)。</li>
<li>スレッド数が多すぎるとインデックス作成が遅くなる問題を修正しました<a href="https://github.com/milvus-io/milvus/pull/39341">(#39341</a>)。</li>
<li>バルクインポート時にディスククォータチェックがスキップされる問題を修正<a href="https://github.com/milvus-io/milvus/pull/39319">(#39319</a>)</li>
<li>同時実行を制限することにより、メッセージキューのコンシューマが多すぎる場合に 発生するフリーズの問題を解決しました<a href="https://github.com/milvus-io/milvus/pull/38915">(#38915</a>)。</li>
<li>大規模なコンパクション中のMixCoordの再起動によるクエリのタイムアウトを修正しました<a href="https://github.com/milvus-io/milvus/pull/38926">(#38926</a>)。</li>
<li>ノードのダウンタイムに起因するチャネルの不均衡問題を修正しました<a href="https://github.com/milvus-io/milvus/pull/39200">(#39200</a>)。</li>
<li>チャネルバランスがスタックする問題を修正。<a href="https://github.com/milvus-io/milvus/pull/39160">(#39160</a>)</li>
<li>RBACカスタムグループの権限レベルチェックが効かなくなる問題を修正しました<a href="https://github.com/milvus-io/milvus/pull/39224">(#39224</a>)。</li>
<li>空のインデックスの行数の取得に失敗する問題を修正した<a href="https://github.com/milvus-io/milvus/pull/39210">(#39210</a>)。</li>
<li>小さいセグメントのメモリ推定が間違っていた問題を修正した<a href="https://github.com/milvus-io/milvus/pull/38909">(#38909</a>)</li>
</ul>
<h2 id="v253" class="common-anchor-header">v2.5.3<button data-href="#v253" class="anchor-icon" translate="no">
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
    </button></h2><p>リリース日: 2025年1月13日</p>
<table>
<thead>
<tr><th>Milvusバージョン</th><th>Python SDKバージョン</th><th>Node.js SDKバージョン</th><th>Java SDKバージョン</th></tr>
</thead>
<tbody>
<tr><td>2.5.3</td><td>2.5.3</td><td>2.5.3</td><td>2.5.4</td></tr>
</tbody>
</table>
<p>Milvus 2.5.3では、全体的な安定性、信頼性、および使いやすさを向上させるために、重要なバグ修正とパフォーマンスの強化が行われました。このバージョンでは、並行処理の改善、データのインデックス作成と検索機能の強化、いくつかの主要コンポーネントの更新を行い、より堅牢なユーザーエクスペリエンスを実現しています。</p>
<h3 id="Bug-fixes" class="common-anchor-header">バグ修正</h3><ul>
<li><code translate="no">VARCHAR</code> の主キーに対して<code translate="no">IN</code> フィルタを使用すると、空の結果が返される問題を修正した。<a href="https://github.com/milvus-io/milvus/pull/39108">(#39108</a>)</li>
<li>クエリ操作と削除操作の並行処理で、不正な結果が返される問題を修正しました。<a href="https://github.com/milvus-io/milvus/pull/39054">(#39054</a>)</li>
<li>クエリリクエストで<code translate="no">expr</code> が空の場合に反復フィルタリングで発生する不具合を修正しました。<a href="https://github.com/milvus-io/milvus/pull/39034">(#39034</a>)</li>
<li>設定更新中のディスクエラーにより、デフォルトの設定値が使用される問題を修正した。<a href="https://github.com/milvus-io/milvus/pull/39072">(#39072</a>)</li>
<li>クラスタリングコンパクションによって削除されたデータが失われる可能性があった問題を修正した。<a href="https://github.com/milvus-io/milvus/pull/39133">(#39133</a>)</li>
<li>成長中のデータセグメントで、テキストマッチクエリが壊れていた問題を修正した。<a href="https://github.com/milvus-io/milvus/pull/39113">(#39113</a>)</li>
<li>スパースベクトルでインデックスに元データが含まれていない場合に発生する検索失敗を修正した。<a href="https://github.com/milvus-io/milvus/pull/39146">(#39146</a>)</li>
<li>クエリとデータロードの同時実行によって発生する可能性のあるカラムフィールドの競合状態を修正しました。<a href="https://github.com/milvus-io/milvus/pull/39152">(#39152</a>)</li>
<li>nullableまたはdefault_valueフィールドがデータに含まれていない場合に、一括挿入に失敗する問題を修正しました。<a href="https://github.com/milvus-io/milvus/pull/39111">(#39111</a>)</li>
</ul>
<h3 id="Improvements" class="common-anchor-header">改良点</h3><ul>
<li>RESTfulインターフェイスにリソースグループAPIを追加した。<a href="https://github.com/milvus-io/milvus/pull/39092">(#39092</a>)</li>
<li>ビットセット SIMD メソッドを活用することで、検索パフォーマンスを最適化した。<a href="https://github.com/milvus-io/milvus/pull/39041">(#39041</a>)</li>
<li>MVCCタイムスタンプが指定された場合、保証タイムスタンプとして使用するようにした。<a href="https://github.com/milvus-io/milvus/pull/39019">(#39019</a>)</li>
<li>不足していた削除メトリクスを追加した。<a href="https://github.com/milvus-io/milvus/pull/38747">(#38747</a>)</li>
<li>Etcdをv3.5.16に更新。<a href="https://github.com/milvus-io/milvus/pull/38969">(#38969</a>)</li>
<li>プロトを管理するための新しいGoパッケージを作成した<a href="https://github.com/milvus-io/milvus/pull/39128">(#39128</a>)。</li>
</ul>
<h2 id="v252" class="common-anchor-header">v2.5.2<button data-href="#v252" class="anchor-icon" translate="no">
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
    </button></h2><p>リリース日: 2025年1月3日</p>
<table>
<thead>
<tr><th>milvusバージョン</th><th>Python SDKバージョン</th><th>Node.js SDKバージョン</th><th>Java SDKバージョン</th></tr>
</thead>
<tbody>
<tr><td>2.5.2</td><td>2.5.3</td><td>2.5.3</td><td>2.5.3</td></tr>
</tbody>
</table>
<p>Milvus 2.5.2では、VARCHARカラムの最大長の変更がサポートされ、インポート時の同時実行、パーティションドロップ、BM25統計処理に関するいくつかの重大な問題が解決されました。安定性とパフォーマンスの向上のため、このバージョンへのアップグレードを強く推奨します。</p>
<h3 id="Improvements" class="common-anchor-header">改良点</h3><ul>
<li>指定されたパスが存在しない場合にのみディスク使用ログを生成するようになりました。<a href="https://github.com/milvus-io/milvus/pull/38822">(#38822</a>)</li>
<li>VARCHARの最大長を調整するパラメータを追加し、上限を65,535に戻した。<a href="https://github.com/milvus-io/milvus/pull/38883">(#38883</a>)</li>
<li>式のパラメータ型変換をサポートした。<a href="https://github.com/milvus-io/milvus/pull/38782">(#38782</a>)</li>
</ul>
<h3 id="Bug-fixes" class="common-anchor-header">バグ修正</h3><ul>
<li>同時実行シナリオにおけるデッドロックの可能性を修正した。<a href="https://github.com/milvus-io/milvus/pull/38863">(#38863</a>)</li>
<li>NULL値をサポートするフィールドに対してのみindex_null_offsetファイルを生成するようにした。<a href="https://github.com/milvus-io/milvus/pull/38834">(#38834</a>)</li>
<li>reduceフェーズでfree後のretrieveプランの使用を修正しました。<a href="https://github.com/milvus-io/milvus/pull/38841">(#38841</a>)</li>
<li>大文字のANDとORを含む式を認識するようにした。<a href="https://github.com/milvus-io/milvus/pull/38928">(#38928</a>)</li>
<li>ロードに失敗した場合でもパーティションドロップを許可するようにした。<a href="https://github.com/milvus-io/milvus/pull/38874">(#38874</a>)</li>
<li>インポート時の BM25 統計ファイルの登録に関する問題を修正。<a href="https://github.com/milvus-io/milvus/pull/38881">(#38881</a>)</li>
</ul>
<h2 id="v251" class="common-anchor-header">v2.5.1<button data-href="#v251" class="anchor-icon" translate="no">
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
    </button></h2><p>リリース日：2024年12月26日</p>
<table>
<thead>
<tr><th>Milvusバージョン</th><th>Python SDKバージョン</th><th>Node.js SDKバージョン</th><th>Java SDKバージョン</th></tr>
</thead>
<tbody>
<tr><td>2.5.1</td><td>2.5.2</td><td>2.5.2</td><td>2.5.2</td></tr>
</tbody>
</table>
<p>Milvus 2.5.1では、メモリローディング、RBACリスト、クエリノードバランシング、シールされたセグメントインデックスに対応する一連のバグフィックスに重点を置き、同時にWeb UIとインターセプターを改善しました。安定性と信頼性の向上のため、2.5.1へのアップグレードを強くお勧めします。</p>
<h3 id="Improvement" class="common-anchor-header">改善</h3><ul>
<li>Web UI のコレクションとクエリページを更新しました。<a href="https://github.com/milvus-io/milvus/pull/38701">(#38701</a>)</li>
</ul>
<h3 id="Bug-fixes" class="common-anchor-header">バグ修正</h3><ul>
<li>ロード予測にメモリ係数を追加することにより、OOM問題を修正した。<a href="https://github.com/milvus-io/milvus/pull/38722">(#38722</a>)</li>
<li>RootCoord でポリシーを一覧表示する際の特権グループの拡張を修正。<a href="https://github.com/milvus-io/milvus/pull/38760">(#38760</a>)</li>
<li>特権グループとコレクションのリストに関する問題を修正しました。<a href="https://github.com/milvus-io/milvus/pull/38738">(#38738</a>)</li>
<li>バランサが同じクエリノードに繰り返し負荷をかけないように修正。<a href="https://github.com/milvus-io/milvus/pull/38724">(#38724</a>)</li>
<li>QueryCoordの再起動後に予期しないバランスタスクが発生する問題を修正しました。<a href="https://github.com/milvus-io/milvus/pull/38725">(#38725</a>)</li>
<li>ロード設定の更新がコレクションのロードに適用されない問題を修正しました。<a href="https://github.com/milvus-io/milvus/pull/38737">(#38737</a>)</li>
<li>データインポート時に読み取りカウントがゼロになる問題を修正。<a href="https://github.com/milvus-io/milvus/pull/38695">(#38695</a>)</li>
<li>式の JSON キーの Unicode デコードを修正した。<a href="https://github.com/milvus-io/milvus/pull/38653">(#38653</a>)</li>
<li>2.5 の alterCollectionField のインターセプター DB 名を修正。 <a href="https://github.com/milvus-io/milvus/pull/38663">(#38663</a>)</li>
<li>BM25 ブルートフォースサーチを使用した場合に、封印されたセグメントのインデックスパラメータが空だったのを修正した。<a href="https://github.com/milvus-io/milvus/pull/38752">(#38752</a>)</li>
</ul>
<h2 id="v250" class="common-anchor-header">v2.5.0<button data-href="#v250" class="anchor-icon" translate="no">
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
    </button></h2><p>リリース日: 2024年12月23日</p>
<table>
<thead>
<tr><th>Milvusバージョン</th><th>Python SDKバージョン</th><th>Node.js SDKバージョン</th><th>Java SDKバージョン</th></tr>
</thead>
<tbody>
<tr><td>2.5.0</td><td>2.5.1</td><td>2.5.2</td><td>2.5.2</td></tr>
</tbody>
</table>
<p>Milvus 2.5.0は、ベクトル検索や大規模データ管理を扱うユーザーにとって、ユーザビリティ、スケーラビリティ、パフォーマンスを向上させるための大きな進歩をもたらします。本リリースにより、Milvusはタームベース検索、クエリを最適化するクラスタリングコンパクション、スパースおよびデンスベクトル検索メソッドの多用途サポートといった強力な新機能を統合しました。クラスタ管理、インデックス作成、データ処理の強化により、Milvusは新たなレベルの柔軟性と使いやすさを導入し、より堅牢で使いやすいベクトルデータベースとなりました。</p>
<h3 id="Key-Features" class="common-anchor-header">主な機能</h3><h4 id="Full-Text-Search" class="common-anchor-header">全文検索</h4><p>Milvus2.5はSparse-BM25で実装された全文検索に対応しています！この機能は、Milvusの強力なセマンティック検索機能を補完する重要な機能であり、特に希少語や専門用語が含まれるシナリオで威力を発揮します。以前のバージョンでは、Milvusはキーワード検索シナリオを支援するためにスパースベクトルをサポートしていました。これらのスパースベクトルはSPLADEv2/BGE-M3のようなニューラルモデルやBM25アルゴリズムのような統計モデルによってMilvusの外部で生成されていました。</p>
<p><a href="https://github.com/quickwit-oss/tantivy">Tantivyを</a>搭載したMilvus 2.5は、アナライザとスパースベクトル抽出を内蔵しており、APIは入力としてベクトルを受け取るだけでなく、テキストを直接受け取れるように拡張されています。BM25の統計情報は、データが挿入されるとリアルタイムで更新され、使いやすさと精度が向上します。さらに、近似最近傍（ANN）アルゴリズムに基づくスパース・ベクトルは、標準的なキーワード検索システムよりも強力なパフォーマンスを提供します。</p>
<p>詳細については、<a href="/docs/ja/analyzer-overview.md">Analyzer Overview</a>および<a href="/docs/ja/full-text-search.md">Full Text Searchを</a>ご参照ください。</p>
<h4 id="Cluster-Management-WebUI-Beta" class="common-anchor-header">クラスタ管理WebUI（ベータ版）</h4><p>膨大なデータと豊富な機能をより良くサポートするために、Milvusの洗練された設計には様々な依存関係、多数のノードの役割、複雑なデータ構造などが含まれています。このような側面は、使用やメンテナンスに困難をもたらす可能性があります。</p>
<p>Milvus 2.5では、組み込みのクラスタ管理WebUIを導入し、Milvusの複雑な実行環境情報を可視化することで、システムメンテナンスの難易度を下げています。これにはデータベースやコレクション、セグメント、チャネル、依存関係、ノードのヘルスステータス、タスク情報、スロークエリなどの詳細が含まれます。</p>
<p>詳細は<a href="/docs/ja/milvus-webui.md">Milvus WebUIを</a>ご参照ください。</p>
<h4 id="Text-Match" class="common-anchor-header">テキストマッチ</h4><p>Milvus 2.5では、<a href="https://github.com/quickwit-oss/tantivy">Tantivyの</a>アナライザとインデックスを活用してテキストの前処理とインデックスを作成し、特定の用語に基づいたテキストデータの正確な自然言語マッチングをサポートしています。この機能は主に特定の条件を満たすフィルタリング検索に使用され、クエリー結果を絞り込むためにスカラーフィルタリングを組み込むことができ、スカラー条件を満たすベクトル内の類似検索を可能にします。</p>
<p>詳細は<a href="/docs/ja/analyzer-overview.md">アナライザーの概要と</a> <a href="/docs/ja/keyword-match.md">テキストマッチを</a>参照。</p>
<h4 id="Bitmap-Index" class="common-anchor-header">ビットマップインデックス</h4><p>Milvusファミリーに新しいスカラーデータインデックスが追加されました。BitMap インデックスは行数と同じ長さのビットの配列を使用して値の存在を表し、検索を高速化します。</p>
<p>ビットマップインデックスは伝統的に、値の数が少ない、つまり、性別情報を含むカラムの値が男性と女性の2つしかないような、カーディナリティの低いフィールドに有効であった。</p>
<p>詳細は<a href="/docs/ja/bitmap.md">ビットマップインデックスを</a>参照してください。</p>
<h4 id="Nullable--Default-Value" class="common-anchor-header">Nullableとデフォルト値</h4><p>Milvusでは、主キーフィールド以外のスカラーフィールドに対して、Null可能なプロパティとデフォルト値を設定できるようになりました。<code translate="no">nullable=True</code> とマークされたスカラーフィールドについては、ユーザはデータ挿入時にフィールドを省略することができます。システムはエラーをスローすることなく、そのフィールドをヌル値またはデフォルト値（設定されている場合）として扱います。</p>
<p>デフォルト値とNULL可能なプロパティはMilvusに大きな柔軟性を与えます。ユーザは、コレクションを作成する際に、不確かな値を持つフィールドに対してこの機能を利用することができます。また、他のデータベースシステムからMilvusへのデータ移行を簡素化し、元のデフォルト値設定を保持したままNULL値を含むデータセットを扱うことができます。</p>
<p>詳細は<a href="/docs/ja/nullable-and-default.md">Nullable &amp; Default Value</a> を参照してください。</p>
<h4 id="Faiss-based-HNSW-SQPQPRQ" class="common-anchor-header">FaissベースのHNSW SQ/PQ/PRQ</h4><p>Faissコミュニティとの緊密な連携により、FaissのHNSWアルゴリズムは、機能と性能の両面で大幅に改善されました。安定性と保守性を考慮し、Milvus 2.5はHNSWのサポートをhnswlibからFaissに正式に移行しました。</p>
<p>Faissに基づき、Milvus 2.5はHNSWの複数の量子化方式をサポートし、様々なシナリオのニーズに応えます：SQ (Scalar Quantizers)、PQ (Product Quantizer)、PRQ (Product Residual Quantizer)です。SQとPQはより一般的で、SQは優れたクエリ性能と構築速度を提供し、PQは同じ圧縮率でより優れたリコールを提供する。多くのベクトルデータベースでは、SQ量子化の単純な形式であるバイナリ量子化が一般的に使用されている。</p>
<p>PRQはPQとAQ（Additive Quantizer）の融合である。PQと比較すると、特にバイナリ圧縮と言って、高い圧縮率でより良いリコールを実現するために、より長い構築時間を必要とする。</p>
<h4 id="Clustering-Compaction-Beta" class="common-anchor-header">クラスタリング圧縮（ベータ）</h4><p>Milvus2.5では、大規模なコレクションの検索を高速化し、コストを削減するために、クラスタリングコンパクションが導入された。クラスタリングキーとしてスカラーフィールドを指定することで、データを範囲ごとに再分散し、保存と検索を最適化します。グローバルインデックスのように動作するこの機能により、Milvusはクラスタリングメタデータに基づいたクエリ時に効率的にデータを刈り込み、スカラーフィルタが適用された際の検索パフォーマンスを向上させることができます。</p>
<p>詳細は<a href="/docs/ja/clustering-compaction.md">クラスタリング・コンパクションを</a>ご参照ください。</p>
<h3 id="Other-Features" class="common-anchor-header">その他の機能</h3><h4 id="Streaming-Node-Beta" class="common-anchor-header">ストリーミングノード（ベータ版）</h4><p>Milvus 2.5では、Write-Ahead Logging (WAL)サービスを提供するストリーミングノードという新しいコンポーネントが導入されました。これにより、Milvusはチャネルの読み書きの前後でコンセンサスを得ることができるようになり、新たな機能、特徴、最適化を実現します。この機能はMilvus 2.5ではデフォルトで無効になっており、バージョン3.0で正式に利用可能になる。</p>
<h4 id="IPv6-Support" class="common-anchor-header">IPv6サポート</h4><p>MilvusはIPv6をサポートし、ネットワーク接続と互換性の拡張を可能にしました。</p>
<h4 id="CSV-Bulk-Import" class="common-anchor-header">CSV一括インポート</h4><p>JSON、Parquet形式に加え、MilvusはCSV形式のデータの直接一括インポートをサポートするようになりました。</p>
<h4 id="Expression-Templates-for-Query-Acceleration" class="common-anchor-header">クエリ高速化のための式テンプレート</h4><p>Milvusは式テンプレートをサポートし、特に複雑な式のシナリオにおいて式の解析効率を向上させます。</p>
<p>詳細については、「<a href="/docs/ja/filtering-templating.md">フィルタテンプレート</a>」をご参照ください。</p>
<h4 id="GroupBy-Enhancements" class="common-anchor-header">GroupByの強化</h4><ul>
<li><strong>グループサイズのカスタマイズ</strong>：グループごとに返されるエントリの数を指定できるようになりました。</li>
<li><strong>ハイブリッド GroupBy 検索</strong>：複数のベクトル列に基づくハイブリッド GroupBy 検索をサポートしました。</li>
</ul>
<h4 id="Iterator-Enhancements" class="common-anchor-header">イテレーターの機能強化</h4><ul>
<li><strong>MVCCのサポート</strong>：MVCC（Multi-Version Concurrency Control）により、挿入や削除などのデータ変更に影響されずにイテレータを使用できるようになりました。</li>
<li><strong>永続カーソル</strong>：MilvusはQueryIteratorの持続的カーソルをサポートし、Milvusの再起動後、反復処理全体を再起動することなく、最後の位置から反復処理を再開できるようになりました。</li>
</ul>
<h3 id="Improvements" class="common-anchor-header">改良点</h3><h4 id="Deletion-Optimization" class="common-anchor-header">削除の最適化</h4><p>ロックの使用とメモリ管理を最適化することにより、大規模な削除の速度の向上とメモリ使用量の削減を実現しました。</p>
<h4 id="Dependencies-Upgrade" class="common-anchor-header">依存関係のアップグレード</h4><p>ETCD 3.5.16およびPulsar 3.0.7 LTSにアップグレードし、既存のCVEを修正し、セキュリティを強化しました。注意：Pulsar 3.xへのアップグレードは、以前の2.xバージョンとは互換性がありません。</p>
<p>既にMilvusを導入しているユーザは、新機能を使用する前にETCDおよびPulsarコンポーネントをアップグレードする必要があります。詳細については、<a href="/docs/ja/upgrade-pulsar-v3.md">Pulsarを2.xから3.xへアップグレードするを</a>ご参照ください。</p>
<h4 id="Local-Storage-V2" class="common-anchor-header">ローカル・ストレージV2</h4><p>Milvus 2.5で新しいローカル・ファイル・フォーマットを導入し、スカラー・データの読み込みとクエリの効率を高め、メモリ・オーバーヘッドを削減し、将来の最適化の基礎を築きました。</p>
<h4 id="Expression-Parsing-Optimization" class="common-anchor-header">式解析の最適化</h4><p>繰り返し式のキャッシュの実装、ANTLRのアップグレード、<code translate="no">NOT IN</code> 節のパフォーマンスの最適化により、式の解析を改善。</p>
<h4 id="Improved-DDL-Concurrency-Performance" class="common-anchor-header">DDL 同時実行性能の向上</h4><p>データ定義言語（DDL）操作の同時実行パフォーマンスを最適化しました。</p>
<h4 id="RESTful-API-Feature-Alignment" class="common-anchor-header">RESTful API 機能の調整</h4><p>RESTful API の機能を他の SDK と整合させました。</p>
<h4 id="Security--Configuration-Updates" class="common-anchor-header">セキュリティと設定の更新</h4><p>より複雑な環境またはエンタープライズ環境でノード間通信を保護するためにTLSをサポートしました。詳細については、<a href="/docs/ja/tls.md">セキュリティ設定を</a>参照してください。</p>
<h4 id="Compaction-Performance-Enhancements" class="common-anchor-header">コンパクション・パフォーマンスの向上</h4><p>混合コンパクションにおける最大セグメント数の制限を撤廃し、より小さなセグメントを優先的に処理することで、効率が向上し、大規模または断片化されたデータセットに対するクエリが高速化されました。</p>
<h4 id="Score-Based-Channel-Balancing" class="common-anchor-header">スコアベースのチャネル・バランシング</h4><p>チャネル間の負荷を動的に分散するポリシーを導入し、大規模な展開におけるリソースの使用率と全体的な安定性を向上。</p>
