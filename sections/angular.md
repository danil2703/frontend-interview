# Angular:

<details>
<summary>Что такое DI? Как работает</summary>

Это важный паттерн шаблон проектирования приложений. В Angular внедрение зависимостей реализовано из-под капота.
Зависимости - это сервисы или объекты, которые нужны классу для выполнения своих функций. DI -позволяет запрашивать зависимости от внешних источников.

Есть 3 способа зарегестрировать сервис у провайдера:

* На уровне компонента (массив providers у компонента)

* На уровне модуля (массив providers у модуля)

* На корневом уровне (providedIn: 'root')

</details>

<details>
<summary>В чем отличие ngOnInit от constructor</summary>

Конструктор сам по себе является фичей самого класса, а не Angular. Основная разница в том, что Angular запустит ngOnInit, после того, как закончит настройку компонента, то есть, это сигнал, благодаря которому свойства @Input() и другие байндинги, и декорируемые свойства доступны в ngOnInit, но не определены внутри конструктора, по дизайну.
Старайтесь писать как можно меньше логики в конструкторе.

</details>

<details>
<summary>Что такое JIT и AOT, в чем их отличия и каковы сферы применения?</summary>

Angular приложение можно скомпилировать с помощью команд `ng serve` и `ng build`. При этом, можно работать с разными видами компиляции:

* <b>JIT</b> - (Just-In-Time compilation) - компиляция "на лету", динамическая компиляция. В Angular используется по умолчанию.
* <b>AOT</b> - (Ahead-Of-Time compilation) - компиляции перед исполнением.

<table>
    <thead>
      <tr><td>Параметры</td><td>JIT</td><td>AOT</td></tr>
    </thead>
    <tbody>
      <tr>
        <td>Когда компилируется</td>
        <td>в момент запуска приложения в браузере</td>
        <td>в момент сборки приложения</td>
      </tr>
      <tr>
        <td>Рекомендуется использовать для</td>
        <td>локальной разработки</td>
        <td>создания продуктовой сборки</td>
      </tr>
      <tr>
        <td>Как включить</td>
        <td>Не нужно выставлять дополнительных флагов</td>
        <td>Нужно добавить флаг --aot или --prod</td>
      </tr>
      <tr>
        <td>Скорость</td>
        <td>Скорость компиляции быстрее, загрузка в браузере дольше</td>
        <td>Скорость компиляции дольше, загрузка в браузере быстрее</td>
      </tr>
      <tr>
        <td>Размер бандла</td>
        <td>Бандл имеет большой размер из-за включенного в бандл компилятора.</td>
        <td>Бандл имеет небольшой размер, тк содержит полностью скомпилированный и оптимизированный код.</td>
      </tr>
      <tr>
        <td>Выявление ошибок</td>
        <td>Ошибки отобразятся во время запуска приложения в браузере</td>
        <td>Выявление ошибок во время компиляции</td>
      </tr>
      <tr>
        <td>Работа с файлами</td>
        <td>Может компилировать только измененные файлы отдельно</td>
        <td>Компилирует сразу все файлы приложения</td>
      </tr>
    </tbody>
  </table>
</details>

<details>
<summary>Для чего нужны директивы ng-template, ng-container, ng-content?</summary>
<div>
  <h4>1. ng-template</h4>
  
  `<template>` — это механизм для отложенного рендера клиентского контента, который не отображается во время загрузки, но может быть инициализирован при помощи JavaScript. <br><br>
  Template можно представить себе как фрагмент контента, сохранённый для последующего использования в документе. Хотя парсер и обрабатывает содержимое элемента `template` во время загрузки страницы, он делает это только чтобы убедиться в валидности содержимого; само содержимое при этом не отображается. <br><br>
  
  `<ng-template>` - является имплементацией стандартного элемента template, данный элемент появился с четвертой версии Angular, это было сделано с точки зрения совместимости со встраиваемыми на страницу template элементами, которые могли попасть в шаблон ваших компонентов по тем или иным причинам. <br><br>

Пример:

```html
<div class="lessons-list" *ngIf="lessons else loading">...</div>

<ng-template #loading>
  <div>Loading...</div>
</ng-template>
```

  <h4>2. ng-container</h4>
  
  `<ng-container>` - это логический контейнер, который может использоваться для группировки узлов, но не отображается в дереве DOM как узел (node).

На самом деле структурные директивы (*ngIf, *ngFor, …) являются синтаксическим сахаром для наших шаблонов. В реальности, данные шаблоны трансформируются в такие конструкции:

```html
<ng-template [ngIf]="lessons" [ngIfElse]="loading">
   <div class="lessons-list">
     ...
   </div>
</div>

<ng-template #loading>
    <div>Loading...</div>
</ng-template>
```

Но что делать, если я хочу применить несколько структурных директив?
(спойлер: к сожалению, так нельзя сделать)

```html
<div class="lesson" *ngIf="lessons" *ngFor="let lesson of lessons">
  <div class="lesson-detail">{{lesson | json}}</div>
</div>
```

```
Uncaught Error: Template parse errors:
Can't have multiple template bindings on one element. Use only one attribute
named 'template' or prefixed with *
```

Но можно сделать так:

```html
<div *ngIf="lessons">
  <div class="lesson" *ngFor="let lesson of lessons">
    <div class="lesson-detail">{{lesson | json}}</div>
  </div>
</div>
```

Однако, чтобы избежать необходимости создавать дополнительный div, мы можем вместо этого использовать директиву ng-container:

```html
<ng-container *ngIf="lessons">
  <div class="lesson" *ngFor="let lesson of lessons">
    <div class="lesson-detail">{{lesson | json}}</div>
  </div>
</ng-container>
```

Как мы видим, директива ng-container предоставляет нам элемент, в котором мы можем использовать структурную директиву, без необходимости создавать дополнительный элемент.

Еще пара примечательных примеров, если все же вы хотите использовать ng-template вместо ng-container, по определенным правилам вы не сможете использовать полную конструкцию структурных директив.

Вы можете писать либо так:

```html
<div class="mainWrap">
  <ng-container *ngIf="true">
    <h2>Title</h2>
    <div>Content</div>
  </ng-container>
</div>
```

Либо так:

```html
<div class="mainWrap">
  <ng-template [ngIf]="true">
    <h2>Title</h2>
    <div>Content</div>
  </ng-template>
</div>
```

На выходе, при рендеринге будет одно и тоже:

```html
<div class="mainWrap">
  <h2>Title</h2>
  <div>Content</div>
</div>
```

 <h4>3. ng-content</h4>
 
`<ng-content>` - позволяет внедрять родительским компонентам html-код в дочерние компоненты.
 
Здесь на самом деле, немного сложнее уже чем с ng-template, ng-container. Так как ng-content решает задачу проецирования контента в ваши веб-компоненты. Веб-компоненты состоят из нескольких отдельных технологий. Вы можете думать о Веб-компонентах как о переиспользуемых виджетах пользовательского интерфейса, которые создаются с помощью открытых веб-технологий. Они являются частью браузера и поэтому не нуждаются во внешних библиотеках, таких как jQuery или Dojo. Существующий Веб-компонент может быть использован без написания кода, просто путем импорта выражения на HTML-страницу. Веб-компоненты используют новые или разрабатываемые стандартные возможности браузера.

Давайте представим ситуацию от обратного, нам нужно параметризовать наш компонент. Мы хотим сделать так, чтобы на вход в компонент мы могли передать какие-либо статичные данные. Это можно сделать несколькими способами.

comment.component.ts:

```ts
@Component({
  selector: "comment",
  template: `
    <h1>Комментарий:</h1>
    <p>{{ data }}</p>
  `,
})
export class CommentComponent {
  @Input() data: string = null;
}
```

app.component.html

```html
<div *ngFor="let message of comments">
  <comment [data]="message"></comment>
</div>
```

Но можно поступить и другим путем. <br>
comment.component.ts:

```ts
@Component({
  selector: "comment",
  template: `
    <h1>Комментарий:</h1>
    <ng-content></ng-content>
  `,
})
export class CommentComponent {}
```

app.component.html

```html
<div *ngFor="let message of comments">
  <comment>
    <p>{{message}}</p>
  </comment>
</div>
```

Конечно, эти примеры плохо демонстрируют подводные камни, свои плюсы и минусы. Но второй способ демонстрирует подход при работе, когда мы оперируем независимыми абстракциями и можем проецировать контент внутрь наших компонентов (подход веб-компонентов).

</div>
</details>

## RXJS:

<details>
<summary>Что такое Subject? Виды Subject, их отличия</summary>

Тип `Subject` — разновидность `RxJS Observable`, который может доставлять данные сразу нескольким подписчикам.

```ts
let subject = new Subject();

subject.subscribe((v) => {
    console.log('Observer 1: ' + v);
});
subject.subscribe((v) => {
    console.log('Observer 2: ' + v);
});

subject.next(9);
```

Виды Subject:

* `Subject` - все значения которые были переданы без подписчиков - игнорируются.

* `BehaviorSubject` - передает новому подписчику последнее значение, в качестве аргумента принимает начальное значение.

```ts
let behaviorSubject = new BehaviorSubject<Number>(3);

behaviorSubject.subscribe((v) => {
    console.log('Observer with value of 3: ' + v);
});

behaviorSubject.next(9);

behaviorSubject.subscribe((v) => {
    console.log('Observer with value of 9: ' + v);
});
```

* `ReplaySubject` - передает новому подписчику все предыдущие значения, принимаемый параметр — количество предыдущих значений (размер буфера).

```ts
let replaySubject = new ReplaySubject<Number>(2);

replaySubject.next(3);
replaySubject.next(6);
replaySubject.next(9);
replaySubject.next(12);

replaySubject.subscribe((value) => {
    console.log('ReplaySubject: ' + value);
});
```
В примере выше в консоль выведутся значения 9 и 12, т.к. размер буфера предыдущих значений 2.

* `AsyncSubject` - передает новому подписчику последнее значение, но только после того, как будет вызван метод complete().

```ts
let asyncSubject = new AsyncSubject<Number>(3);

asyncSubject.subscribe((value) => {
    console.log('AsyncSubject: ' + value);
});

asyncSubject.next(3);
asyncSubject.next(6);
asyncSubject.next(9);

asyncSubject.complete();
```
</details>

