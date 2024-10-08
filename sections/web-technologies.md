# Web Technologies:

<details>
<summary>Что такое REST API?</summary>
<br />
<b>REST</b> (Representational State Transfer)  - это концепция (архитектура) для организации взаимодействия между независимыми объектами (приложениями) посредством протокола HTTP.
Включает в себя набор принципов (рекомендаций) взаимодействия клиент-серверных приложений. Обычно он представлен в формате JSON.

Основная идея REST API - разделение разных операций (чаще всего CRUD) при обращении к одному и тому же URL с помощью HTTP-методов.

Клиент посещает URL-адрес и отправляет серверу запрос, чтобы получить ответ.

![Test Image 4](https://github.com/danil2703/frontend-interview/blob/main/assets/web-technologies/1.png)
</details>

<details>
<summary>6 принципов архитектуры REST API</summary>
<br />

### 1. Клиент-серверная модель
Этот принцип требует отделять друг от друга два понятия: клиент и сервер.

Сервер — программа, в которой хранятся и обрабатываются ресурсы. Сервер может располагаться на одном или нескольких компьютерах; но даже в одном компьютере может быть несколько виртуальных серверов.

Клиент — программа, которая запрашивает у сервера доступ к ресурсам. Для этого она использует API.

### 2. Отсутствие состояния
Это значит, что на сервере не хранится никаких данных о прошлых взаимодействиях с клиентом — каждый запрос должен содержать всю информацию для его обработки.

Это снижает нагрузку на сервер, что особенно полезно, если к нему подключено одновременно много клиентов. Не нужно хранить дополнительную информацию о прошлых обращениях каждого из них. Достаточно обработать каждый запрос в отдельности.

### 3. Кэшируемость
Это ограничение требует, чтобы для данных в ответе на запрос явно было указано -- можно их кэшировать или нет. Если ответ поддерживает кэширование, то клиент имеет право повторно использовать данные в последующих эквивалентных запросов без обращения на сервер.

### 4. Единообразие интерфейса

Файлы обычно передаются клиенту не в том виде, в котором хранятся на сервере. В вебе их часто преобразуют в JSON или XML и только потом отправляют клиенту. Ответ на запросы к новому ресурсу должен приходить в том же формате, что и к старым, и сразу же содержать дополнительную информацию: что разрешается делать с ресурсом, можно ли его изменять и удалять на сервере и так далее.

REST накладывает на интерфейс четыре ограничения: 1) идентичность ресурсов; 2) манипуляция над ресурсами через представление; 3) исчерпывающие, понятные человеку сообщения; 4) гипермедиа (hypermedia) как движок для состояния приложения (HATEOAS).

### 5. Многоуровневая система

Многоуровневость достигается засчёт ограничения поведения компонентов таким образом, что компоненты "не видят" другие компоненты, кроме расположенных на ближайших уровнях, с которыми они взаимодействуют.

Между сервером и клиентом могут быть несколько промежуточных узлов, выполняющих вспомогательные функции, — прокси-серверы.

Они используются для кэширования, обеспечения безопасности, дополнительной обработки данных. Если основных серверов несколько, то дополнительные серверы-балансировщики могут распределять нагрузку между ними и решать, в какой из них направлять запрос:

Никто из участников цепочки не знает всего пути, который проходит запрос, — только своих «соседей» справа и слева.

![Test Image 4](https://github.com/danil2703/frontend-interview/blob/main/assets/web-technologies/2.png)

### 6. Код по требованию (необязательно)

Является необязательным принципом.

</details>

<details>
<summary>Разница между cookie, sessionStorage и localStorage?</summary>
<br />
<table>
    <thead>
        <tr>
            <th></th>
            <th><code>cookie</code></th>
            <th><code>localStorage</code></th>
            <th><code>sessionStorage</code></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Инициатор</td>
            <td>Клиент или сервер. Сервер может использовать заголовок <code>Set-Cookie</code></td>
            <td>Клиент</td>
            <td>Клиент</td>
        </tr>
        <tr>
            <td>Срок хранения</td>
            <td>Устанавливается вручную</td>
            <td>Всегда</td>
            <td>До закрытия вкладки</td>
        </tr>
        <tr>
            <td>Хранение между сессиями</td>
            <td>Зависит от установки срока хранения</td>
            <td>Да</td>
            <td>Нет</td>
        </tr>
        <tr>
            <td>Отправка на сервер с каждым HTTP-запросом</td>
            <td>автоматически, с помощью заголовка <code>Cookie</code></td>
            <td>Нет</td>
            <td>Нет</td>
        </tr>
        <tr>
            <td>Емкость (на один домен)</td>
            <td>4 КБ</td>
            <td>5 МБ</td>
            <td>5 МБ</td>
        </tr>
        <tr>
            <td>Доступность</td>
            <td>В любом окне</td>
            <td>В любом окне</td>
            <td>В той же вкладке</td>
        </tr>
    </tbody>
</table>
</details>

<details>
<summary>Что такое прогрессивный рендеринг?</summary>
<br />
Чтобы понять что такое progressive rendering, нужно понимать отличие client-side rendering от server-side rendering.

При client-side rendering (CSR) контент отрисовывается на стороне клиента (в браузере). Такой подход используется в React, когда браузеру отсылается практически пустой HTML-документ, а потом запускается скрипт, который генерирует HTML в указанном скрипту теге. Как правило это `<div id="root">`. Пользователь будет видеть пустую страницу, пока JS-файл полностью не загрузится.

При server-side rendering (SSR) HTML-разметка генерируется на сервере, отсылается браузеру и после этого отрисовывается на клиенте. Пользователь увидит контент сразу же, но не сможет взаимодействовать со страницей, пока не загрузится JS-файл.

При использовании прогрессивного рендеринга, кусочки HTML генерируется на сервере и отсылаются браузеру в порядке их приоритетности. То есть, элементы с самым высоким приоритетом (например `<header>`, фон, главная интерактивная часть страницы) генерируются на сервере, отсылаются браузеру и отрисовываются в первую очередь. Это позволяет пользователю увидеть самый важный контент как можно скорее, не дожидаясь полной загрузки всего контента. То есть, progressive rendering что-то среднее между client-side rendering и server-side rendering.

Техники реализации прогрессивного рендеринга:

Ленивая загрузка (Lazy Loading). Загрузка контента по мере необходимости. Например, если страница достаточно большая, не нужно загружать изображения вне вьюпорта. Загрузка изображения стартует за некоторое время до того как она появится во вьюпорте. Эту же технику можно использовать для загрузки контента изначально скрытых элементов. Например, можно загрузить контент закрытого меню когда пользователь наводит курсор на кнопку открытия.
Приоритизация контента. Например, не загружать изначально все CSS-стили. Добавлять в `<head>` загрузку только тех стилей, которые нужны для текущей видимой области HTML-документа. Остальные стили можно добавить в `<body>`.

</details>


<details>
<summary>polling, long polling</summary>

### Polling
1. Отправляем запрос на сервер.
2. Получаем немедленный ответ.
3. Повторяем это действие каждые X секунд/минут/etc., чтобы получать актуальные данные для приложения (setInterval).

Такой подход подразумевает большое количество запросов на сервер. Это создаёт определённую нагрузку на сетевой трафик. Ресурсы сервера нагружаются только во время запроса, но выгружаются как только был отдан ответ.

##### Плюсы:

* Простота реализации. Причём, простота реализации тут достаточно условная. Клиентская часть – довольно проста, а вот сервер получает сразу большой поток запросов. Даже если клиент ушёл пить чай – его браузер каждые 10 секунд будет «долбить» сервер запросами. Готов ли сервер к такому?

##### Минусы:

* Лишний входящий трафик на сервер. При каждом запросе браузер передает множество заголовков и в ответ получает, кроме данных, также заголовки. Для некоторых приложений трафик заголовков может в 10 и более раз превосходить трафик реальных данных.
* Задержки между событием и уведомлением. Сервер отсылает данные не тогда, когда они появились, а когда прилетит новый запрос.
* Серверу приходится хранить события пока клиент не заберет их или пока они не устареют. Это можно перекрыть, добавив кеширующий слой типа Varnish (потребуется больше памяти).

### Long Polling

1. Отправляем запрос на сервер.
2. Соединение не закрывается сервером, пока не появится сообщение.
3. Когда сообщение появилось – сервер отвечает на запрос, пересылая данные.
4. Браузер тут же делает новый запрос.

Улучшенный вариант предыдущего метода. Клиент отправляет запрос на сервер, сервер держит открытое соединение (thread) пока не придут какие-нибудь данные или клиент не отключится самостоятельно. Как только данные пришли — отправляется ответ и соединение закрывается, открывается следующее и так далее.

##### Плюсы:
* Минимальное количество запросов. Не нужно постоянно «долбать» сервер запросами.
* Realtime-отдача данных.
##### Минусы:
* Потребляет больше серверных ресурсов. Нагрузка существенно увеличивается, если входящие данные имеют большой размер.


</details>

<details>
<summary>Что такое RPC?</summary>
<br />
<b>RPC</b> (Remote Procedure Call) — это способ, позволяющий программе на одном компьютере вызвать функцию на другом компьютере так, будто эта функция находится на первом компьютере. Представьте, что вы просите друга сделать что-то за вас — это и есть идея RPC.

RPC работает следующим образом:

Клиент (тот, кто делает запрос) отправляет запрос на сервер, сообщая, какую функцию он хочет выполнить и какие данные нужно использовать (аргументы).
Сервер (тот, кто обрабатывает запрос) получает запрос, выполняет функцию и отправляет результат обратно клиенту.

В RPC клиент вызывает функции напрямую, используя бинарные форматы для передачи данных, тогда как в REST используются стандартные HTTP-запросы и текстовые форматы, такие как JSON или XML.

RPC лучше подходит для внутреннего взаимодействия между микросервисами из-за высокой производительности и низкого оверхеда. Применяется, когда важна скорость и эффективность передачи данных.

### Преимущество RPC:

RPC может быть быстрее и эффективнее за счет использования бинарных форматов данных и прямых вызовов функций, что снижает оверхед по сравнению с REST.
Бинарные форматы (например, Protocol Buffers) более компактны и быстрее обрабатываются.
Вызов функций напрямую упрощает структуру взаимодействия и уменьшает задержки.
В высоконагруженных системах, где важна минимальная задержка и максимальная производительность, использование RPC позволяет ускорить обмен данными между сервисами.

</details>