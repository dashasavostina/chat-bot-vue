## Project setup
npm install
## Compiles and hot-reloads for development
npm run serve
## Compiles and minifies for production
npm run build
## Lints and fixes files
npm run lint

## как встроить на сторонние сайты
Пример для Vue.js: HTML (внешняя страница):

html Copy code

// родительский блок
JS (внешняя страница):

html Copy code

<script src="https://cdn.jsdelivr.net/npm/vue@2"></script> <script src="path/to/your/vue-app.js"></script>
Vue.js (внешняя страница):

javascript Copy code // Ваш Vue.js код в файле vue-app.js new Vue({ el: '#external-chat-widget', template: '', // Используйте компонент Vue.js для виджета components: { 'external-chat-widget': httpVueLoader('path/to/your/external-chat-widget.vue'), // Подключение компонента Vue.js }, });