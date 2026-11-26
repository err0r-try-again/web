# lab1
тема: 16 онлайн издание (журнал, газета)

### Как устроена сетка

#### 1. Общая архитектура
* **CSS Flexbox** используется для **одномерных потоков** (выстраивание элементов в одну строку или колонку): вертикальный каркас страницы `body` для прижатия подвала, верхняя панель шапки `.header-top`, навигация `.nav-list` и внутреннее содержимое карточек `.news-card`.
* **CSS Grid** используется для **двумерных раскладок** (строки и колонки одновременно): главный блок с боковой колонкой `.lead-section`, асимметричная газетная сетка карточек `.cards-wrapper`, сетка формы `.form-layout` и 4-колоночный подвал `.footer-grid`.

---

#### 2. Flexbox: родитель (контейнер) и дочерние элементы

* **Каркас страницы (`body` → `.site-main`, `.site-footer`):**
  * **Родитель (`body`):** `display: flex; flex-direction: column; min-height: 100vh;` — задаёт вертикальную ось сверху вниз.
  * **Дочерние элементы:** `.site-main` имеет `flex: 1 0 auto;` (`flex-grow: 1`, `flex-shrink: 0`, `flex-basis: auto`), за счёт чего растягивается на всё свободное место, а `.site-footer` с `margin-top: auto;` всегда прижат к низу экрана.

* **Верхняя панель шапки (`.header-top` → `.header-date`, `.header-brand`, `.header-actions`):**
  * **Родитель (`.header-top`):** `display: flex; flex-direction: row; flex-wrap: wrap; justify-content: space-between; align-items: center; align-content: center; gap: 16px;`.
  * **Дочерние элементы:**
    * `.header-date` и `.header-actions` имеют `flex-basis: 180px;` (симметричная ширина по бокам), причём у `.header-actions` задано `align-self: center;`.
    * `.header-brand` имеет `flex-grow: 1;` (занимает центр), а в `@media (max-width: 640px)` получает `order: -1;`, чтобы на телефоне логотип вставал самым первым.

* **Навигация (`.nav-list`) и внутренняя сетка карточек (`.news-card`):**
  * `.nav-list`: `display: flex; flex-direction: row; flex-wrap: nowrap; justify-content: flex-start; align-items: center; gap: 24px;`.
  * Внутри `.card-content` (внутри flex-колонки) тег `.card-inline-tag` выровнен по левому краю через `align-self: flex-start;`.

---

#### 3. CSS Grid: родитель (контейнер) и дочерние элементы

* **Главная секция с сайдбаром (`.lead-section` → `.lead-article`, `.sidebar-news`):**
  * **Родитель (`.lead-section`):** `display: grid; grid-template-columns: 2fr 1fr; grid-template-rows: auto; grid-template-areas: "lead sidebar"; gap: 40px; align-items: start;`.
  * **Дочерние элементы:**
    * `.lead-article`: `grid-area: lead;`
    * `.sidebar-news`: `grid-area: sidebar; align-self: start;`
  * На экранах `<= 992px` сетка перестраивается в одну колонку (`grid-template-columns: 1fr;` и `grid-template-areas: "lead" "sidebar";`).

* **Газетная сетка карточек (`.cards-wrapper` → `.news-card`, `.news-card--featured`, `.news-card--wide`):**
  * **Родитель (`.cards-wrapper`):** `display: grid; grid-template-columns: repeat(3, 1fr); grid-auto-rows: minmax(220px, auto); gap: 28px; justify-items: stretch; align-items: stretch;`.
  * **Дочерние элементы (позиционирование по линиям сетки):**
    * `.news-card--featured` («Экономика»): `grid-column: 1 / 3; grid-row: 1 / 2;` — растянута на 2 первые колонки в 1-м ряду.
    * Карточка «Культура» автоматически занимает 3-ю колонку 1-го ряда.
    * Карточка-цитата `.quote-card` занимает 1-ю колонку 2-го ряда.
    * `.news-card--wide` («Общество»): `grid-column: 2 / 4;` — растянута на 2-ю и 3-ю колонки во 2-м ряду.
  * На планшетах (`<= 992px`) задаётся `grid-template-columns: repeat(2, 1fr);` и сбрасывается явное растяжение (`grid-column: auto; grid-row: auto;`), а на смартфонах (`<= 640px`) — `grid-template-columns: 1fr;`.

* **Подвал (`.footer-grid`) и форма (`.form-layout`):**
  * `.footer-grid`: `display: grid; grid-template-columns: 2fr 1fr 1fr 1.5fr; gap: 36px;`.
  * `.form-layout`: `display: grid; grid-template-columns: 2fr 1fr; grid-template-areas: "lead sidebar"; gap: 40px; align-items: start;`.

---

