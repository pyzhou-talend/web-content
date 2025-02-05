---
id: roadmap.md
title: Дорожная карта Milvus
related_key: Milvus roadmap
summary: >-
  Milvus - это векторная база данных с открытым исходным кодом, созданная для
  работы приложений искусственного интеллекта. Вот наша дорожная карта, по
  которой мы будем развиваться.
---
<h1 id="Milvus-Roadmap" class="common-anchor-header">Дорожная карта Milvus<button data-href="#Milvus-Roadmap" class="anchor-icon" translate="no">
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
    </button></h1><p>Добро пожаловать в дорожную карту Milvus! Присоединяйтесь к нам в нашем непрерывном путешествии по улучшению и развитию Milvus. Мы рады поделиться с вами нашими достижениями, планами на будущее и видением того, что ждет нас впереди. Наша дорожная карта - это не просто список предстоящих функций, она отражает нашу приверженность инновациям и стремление работать с сообществом. Мы приглашаем вас ознакомиться с нашей дорожной картой, оставить свой отзыв и помочь сформировать будущее Milvus!</p>
<h2 id="Roadmap" class="common-anchor-header">Дорожная карта<button data-href="#Roadmap" class="anchor-icon" translate="no">
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
    </button></h2><table>
    <thead>
        <tr>
            <th>Категория</th>
            <th>Milvus 2.5.0 (достигнуто в последних выпусках)</th>
            <th>Следующий релиз (середина CY25)</th>
            <th>Будущая дорожная карта (в течение 1 года)</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><strong>Обработка неструктурированных данных на основе ИИ</strong><br/><i>Расширение возможностей обработки и анализа неструктурированных данных с использованием моделей ИИ и передовых технологий.</i></td>
            <td><strong>Полнотекстовый поиск</strong><br/><i>Поддержка полнотекстового поиска с помощью Sparse-BM25. Новый API принимает текст на вход и автоматически генерирует разреженный вектор внутри Milvus</i><br/><br/><strong>Sparse Vector(GA)</strong><br/><i>Поддержка эффективного метода хранения и индексации разреженного вектора.</i><br/></td>
            <td><strong>Ввод и вывод данных</strong><br/><i>Поддержка основных модельных сервисов для ввода исходных данных</i><br/><br/><strong>Расширенный реранкер</strong><br/><i>Поддержка реранкеров на основе модели и пользовательской функции оценки</i><br/><br/><strong>Улучшение JSON</strong><br/><i>Индексация и парсинг JSON для ускорения обработки.</i></td>
            <td><strong>Ввод и вывод исходных данных</strong><br/><i>Поддержка Blob и url ссылок для обработки исходных данных</i><br/><br/><strong>Поддержка большего количества типов данных</strong><br/><i>например, Datetime, Map, GIS</i><br/><br/><strong>Поддержка тензоров</strong><br/><i>Поддержка списка векторов, типичных для использования, таких как Colbert, Copali и т.д.</i></td>
        </tr>
        <tr>
            <td><strong>Качество и производительность поиска</strong><br/><i>Предоставление точных, релевантных и быстрых результатов за счет оптимизации архитектуры, алгоритмов и API.</i></td>
            <td><strong>Функция сопоставления текста</strong><br/><i>Быстрая фильтрация ключевых слов/токенов в тексте/varchar</i><br/><br/><strong>Улучшение поиска по группам</strong><br/><i>Внедрение group_size и добавление поддержки group by в гибридном поиске</i><br/><br/><strong>Растровый индекс и инвертированный индекс</strong><br/><i>Ускорение фильтрации по тегам</i>.</td>
            <td><strong>Advanced Match</strong><br/> Например<i>, Match Phrase, Fuzzy Match и другие токенизаторы</i><br/><br/><strong>Агрегации</strong><br/><i>Скалярные агрегации полей, например, min, max, count, distinct.</i><br/></td>
            <td><strong>Частичное обновление</strong><br/><i>Поддержка обновления значения конкретного поля</i><br/><br/><strong>Возможность сортировки</strong><br/><i>Сортировка по скалярным полям во время выполнения</i><br/><br/><strong>Поддержка кластеризации данных</strong><br/><i>Совместное расположение данных</i>.</td>
        </tr>
        <tr>
            <td><strong>Богатый функционал и управление</strong><br/><i>Удобные для разработчиков и надежные функции управления данными</i></td>
            <td><strong>Поддержка CSV файлов при импорте данных</strong><br/><i>Bulkinsert поддерживает формат CSV</i><br/><br/><strong>Поддержка Null и Default Value</strong><br/><i>Типы</i> Null<i>и Default упрощают импорт данных из других СУБД</i><br/><br/><strong>Milvus WebUI (Beta)</strong><br/><i>Визуальные инструменты управления для DBA.</i></td>
            <td><strong>Дедупликация первичных ключей</strong><br/><i>С помощью глобального индекса pk</i><br/><br/><strong>Изменение схемы в режиме онлайн</strong><br/> Например<i>, добавление/удаление поля, изменение длины varchar</i><br/><br/><strong>Версионирование и восстановление данных</strong><br/><i>Поддержка версионирования данных по снимкам.</i></td>
            <td><strong>Rust и C++ SDK</strong><br/><i>Поддержка большего числа клиентов</i><br/><br/><strong>Поддержка UDF </strong><br/><i>Определяемая пользователем функция</i></td>
        </tr>
        <tr>
            <td><strong>Экономическая эффективность и ахитектура</strong><br/><i>Современные системы, приоритет стабильности, экономичности и масштабируемости. </i></td>
            <td><strong>Загрузка по полю</strong><br/><i>Выбор части коллекции для загрузки</i><br/><br/><strong>Оптимизация памяти</strong><br/><i>Снижение OOM и повышение нагрузки</i><br/><br/><strong>Потоковый узел (Beta)</strong><br/><i>Обеспечение глобальной согласованности и решение проблемы узкого места в производительности корневого координатора</i><br/><br/><strong>Формат хранения V2 (Beta)</strong><br/><i>Универсальный дизайн форматов и основа для доступа к данным на основе диска</i><br/><br/><strong>Кластеризация уплотнения</strong><br/><i>Перераспределение данных на основе конфигурации для ускорения чтения.</i></td>
            <td><strong>Ленивая загрузка</strong><br/><i>Загрузка может быть инициирована первой операцией чтения без явного вызова load()</i><br/><br/> Многоуровневое<strong>хранение</strong><br/><i>Поддержка горячего и холодного хранения для оптимизации затрат</i><br/><br/><strong>Освобождение по полям</strong><br/><i>Освобождение части коллекции для сокращения использования памяти</i><br/><br/><strong>Потоковый узел (GA)</strong><br/><i>Обработка потоковых данных и упрощение архитектуры.</i></td>
            <td><strong>Устранение зависимостей</strong><br/><i>Уменьшение или устранение зависимостей от внешних компонентов, таких как pulsar, etcd</i><br/><br/><strong>Слияние логики коорд в MixCoord</strong><br/><i>Упрощение архитектуры</i></td>
        </tr>
    </tbody>
</table>
<ul>
<li>Наша дорожная карта обычно состоит из трех частей: самый последний релиз, следующий предстоящий релиз и среднесрочная и долгосрочная перспектива на ближайший год.</li>
<li>По мере продвижения мы постоянно учимся и время от времени корректируем наш фокус, добавляя или убирая элементы по мере необходимости.</li>
<li>Эти планы являются ориентировочными и могут меняться в зависимости от подписки на услуги.</li>
<li>Мы неуклонно придерживаемся нашей дорожной карты, а наши <a href="/docs/ru/release_notes.md">заметки о релизах</a> служат в качестве справочного материала.</li>
</ul>
<h2 id="How-to-contribute" class="common-anchor-header">Как внести свой вклад<button data-href="#How-to-contribute" class="anchor-icon" translate="no">
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
    </button></h2><p>Будучи проектом с открытым исходным кодом, Milvus процветает благодаря вкладу сообщества. Вот как вы можете стать частью нашего пути.</p>
<h3 id="Share-feedback" class="common-anchor-header">Поделиться отзывами</h3><ul>
<li><p>Сообщайте о проблемах: Столкнулись с ошибкой или у вас есть предложение? Откройте проблему на нашей <a href="https://github.com/milvus-io/milvus/issues">странице GitHub</a>.</p></li>
<li><p>Предложения по функциям: У вас есть идеи по поводу новых функций или улучшений? <a href="https://github.com/milvus-io/milvus/discussions">Мы будем рады их услышать!</a></p></li>
</ul>
<h3 id="Code-contributions" class="common-anchor-header">Вклад в код</h3><ul>
<li><p>Pull requests: Вносите свой вклад непосредственно в нашу <a href="https://github.com/milvus-io/milvus/pulls">кодовую базу</a>. Будь то исправление ошибок, добавление функций или улучшение документации - ваш вклад приветствуется.</p></li>
<li><p>Руководство по разработке: Ознакомьтесь с нашим <a href="https://github.com/milvus-io/milvus/blob/82915a9630ab0ff40d7891b97c367ede5726ff7c/CONTRIBUTING.md">руководством для разработчиков</a>, чтобы узнать о правилах внесения вклада в код.</p></li>
</ul>
<h3 id="Spread-the-word" class="common-anchor-header">Распространяйте информацию</h3><ul>
<li><p>Социальный обмен: Любите Milvus? Поделитесь своими примерами использования и опытом в социальных сетях и технических блогах.</p></li>
<li><p>Отметьте нас на GitHub: Выразите свою поддержку, отметив звездой наш <a href="https://github.com/milvus-io/milvus">репозиторий на GitHub</a>.</p></li>
</ul>
