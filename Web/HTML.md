# HTML
## Содержание
## Тэг <script>
### Внешние скрипты
Если js-кода много, то его можно вынести в отельный файл и подключить на страницу с помощью:
`<script src="path/to/script.js"></script>`

Особенности тэга:
- Браузер старается **кэшировать** скрипты, то есть при правильной настройке сервера он скачает их в первый раз, а потом будет брать из кэша.
- Если указать *src*, то содержимое тега будет игнорироваться.

### Async/defer
Поскольку браузер **загружает страницу постепенно**, то он обязан сначала выполнить js-код, а потом продолжить загрузку страницы. То есть браузер, доходя до тега `<script>`, выполняет его содержимое и идёт дальше. **Именно поэтому** рекомендуется помещать тэги `<script>` в конец `<body>` при синхронном (последовательном) выполнении.

Однако есть способ избежать выполнения js-кода сразу и продолжить загрузку. Для этого у тега <script> есть атрибут **async** (не поддерживается в IE9-):
```
<script async src="..."></script>
```
Так браузер начнёт загружать скрипт и продолжить отрисовку страницы, а когда скрипт загрузится, то браузер выполнит его. Однако, есть один нюанс: если мы загружаем несколько скриптов асинхнонно, то первым выполнится тот скрипт, который раньше загрузится. Что делать, если мы хотим сохранить последовательность выполнения асинхронных скриптов? Для этого есть атрибут **defer**:
```
<script defer src=".../1.js"></script>
<script defer src=".../2.js"></script>
```
В данном примере *2.js* выполнится после *1.js*, даже если загрузится раньше.

**ВАЖНО:**
- скрипты с атрибутом **defer** будут ждать загрузки страницы целиком. То есть если скрипт с атрибутом async может выполниться до полной загрузки страницы, то скрипт с тэгом defer не может.
- при одновременном указании атрибутов, современные браузеры будут выполнять сценарий async.
- эти атрибуты применяются только для внешних скриптов
- скрипты, добавляемые через js, по умолчанию async. Чтобы сохранить порядок выполнения, нужно написать `script.async = false;`
