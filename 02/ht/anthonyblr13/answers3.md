#Что нового появилось в ES6 по сравнению с ES5?
Добавлена возможность объявления переменых через `let` и `const`
Основные отличия `let`: видны только после объявления и их областью видимости является блок `{ …}`, эти переменные нельзя переобъявлять в рамках блока `{ …}`, при объявлении внутри цикла `for(let = …)` переменная видна только в цикле, и каждая новая итерация цикла имеет свою `let`.
Основные отличия `const`: эту переменную нельзя менять, это константа, но если константе присвоен объект, то свойства внутри объекта могут меняться, то же и для массива.
Добавлена возможность объявлять функции через запись `=>` (arrow function)
Новая конструкция `class` –  для задания конструктора вместе с прототипом.
```javascript
'use strict';

class User {

  constructor(name) {
    this.name = name;
  }

  sayHi() {
    alert(this.name);
  }

}

let user = new User("Вася");
user.sayHi(); // Вася
```
Добавлен новый примитивный тип данных `Symbol` служит для создания уникальных идентификаторов.
```javascript
let sym = Symbol(); // без new, т.к. примитив
```
Добавлена новая концепция «итерируемых» (iterable) объектов.
Итерируемые  объекты – это те, содержимое которых можно перебрать в цикле.
Например, перебираемым объектом является массив. Но не только он. В браузере существует множество объектов, которые не являются массивами, но содержимое которых можно перебрать.
Для перебора таких объектов добавлен новый синтаксис цикла: `for..of`.
```javascript
'use strict';

for (let char of "Привет") {
  alert(char); //  П, р, и, в, е, т
}
```
Добавлены новые типы коллекций : `Set`, `Map`, `WeakSet` и `WeakMap`.
В отличие от объектов, в которых ключами могут быть только строки, в Map ключом может быть произвольное значение.
```javascript
'use strict';

let map = new Map();

map.set('1', 'str1');   // ключ-строка
map.set(1, 'num1');     // число
map.set(true, 'bool1'); // булевое значение

// в обычном объекте это было бы одно и то же,
// map сохраняет тип ключа
alert( map.get(1)   ); // 'num1'
alert( map.get('1') ); // 'str1'

alert( map.size ); // 3
```
Добавлен Set – коллекция для хранения множества значений, причём каждое значение может встречаться лишь один раз.
```javascript
'use strict';

let set = new Set();

let vasya = {name: "Вася"};
let petya = {name: "Петя"};
let dasha = {name: "Даша"};

// посещения, некоторые пользователи заходят много раз
set.add(vasya);
set.add(petya);
set.add(dasha);
set.add(vasya);
set.add(petya);

// set сохраняет только уникальные значения
alert( set.size ); // 3

set.forEach( user => alert(user.name ) ); // Вася, Петя, Даша
```
Добавлены `Promise` (промисы)
Promise – это специальный объект, который содержит своё состояние. Вначале `pending` («ожидание»), затем – одно из: `fulfilled` («выполнено успешно») или `rejected` («выполнено с ошибкой»).
Синтаксис:
```javascript
var promise = new Promise(function(resolve, reject) {
  // Эта функция будет вызвана автоматически

  // В ней можно делать любые асинхронные операции,
  // А когда они завершатся — нужно вызвать одно из:
  // resolve(результат) при успешном выполнении
  // reject(ошибка) при ошибке
})
```
#Что такое "стрелочная" ("arrow function") функция? Чем она отличается от обычной?
Новый синтаксис для задания функций через `=>`
```javascript
let inc = x => x+1; // запись через 'arrow function'

let inc = function(x) { return x + 1; }; // запись идентичная той что вверху 
```
слева от фунуции находится аргумент, справа выражение, которое нужно вернуть, если аргументов несколько
используют (a, b), либо если нет аргументов (). Когда тело функции достаточно большое, то можно его обернуть в фигурные скобки {…},
в данном случае надо явно прописывать `return` если надо что-то вернуть.
Значения специальных переменных `this`, `super` и `arguments` определяются не тем, как стрелочные функции были вызваны, а тем, как они были созданы.
Неизменяемые `this`, `super` и `arguments`. Значения этих переменных внутри стрелочных функций остаются неизменными на протяжении всего жизненного цикла функции.
Стрелочные функции не могут быть использованы как конструктор и возвращают ошибку при использовании с оператором `new`.
Недоступность «собственного» значения переменной `arguments`.
#Что такое Promise? Какой стандарт отписывает поведение Promise? Основные пункты стандарта?
Promise – это специальный объект, который содержит своё состояние. Вначале `pending` («ожидание»), затем – одно из: `fulfilled` («выполнено успешно») или `rejected` («выполнено с ошибкой»).
Синтаксис:
```javascript
var promise = new Promise(function(resolve, reject) {
  // Эта функция будет вызвана автоматически

  // В ней можно делать любые асинхронные операции,
  // А когда они завершатся — нужно вызвать одно из:
  // resolve(результат) при успешном выполнении
  // reject(ошибка) при ошибке
})
```
#Чем куки (cookie) отличаются от localStorage ?
#     	                            Cookie 	                                      localStorage и sessionStorage
Где хранятся?	            На компьютере пользователя	                          На компьютере пользователя
Доступность данных	        Данные доступны как со стороны сервера,               Данные доступны только со стороны браузера посредством JavaScript API
                            так и со стороны клиента	
Максимальный размер данных	4 Кбайт	                                              5 или 10 Мбайт в зависимости от браузера
Удобство методов для работы
с данными	                  Неудобные методы для работы с cookie на               Простые и удобные методы для работы с данными
                            стороне клиента (браузера)	
Время хранения данных     	ограниченное время                                    неограниченное время
                            (в конце сеанса или по истечении указанной даты)	    (localStorage) или после завершения сеанса (sessionStorage)
Передаётся ли информация
на веб-сервер?	            Информация всегда передаётся веб-серверу              Информация никогда не передаётся на сервер
                            в составе HTTP-заголовка	
#Что такое CORS?
Правило одного источника является важным принципом обеспечения безопасности, реализованное web браузерами для предотвращения выполнения JavaScript кодом запросов к другим источникам (т.е. к другим доменам), а не к тому, с которого он передан. Несмотря на эффективность такого правила, оно также ограничивает в законных взаимодействиях между сервером и клиентами из надежных источников.
Cross-Origin Resource Sharing (CORS) является техникой для ослабления правила одного источника, позволяя JavaScript на web странице обрабатывать ответ от REST API от другого источника.
#Что такое и какие есть коды ответов HTTP?
Код состояния HTTP (англ. HTTP status code) — код состояния является частью первой строки ответа сервера. Он представляет из себя целое число из 3 арабских цифр. Первая цифра указывает на класс состояния. За кодом ответа обычно следует отделённая пробелом поясняющая фраза на английском языке, которая разъясняет человеку причину именно такого ответа. Пример:

403 Access allowed only for registered users

Клиент узнаёт по коду ответа о результатах его запроса и определяет, какие действия ему предпринимать дальше. Набор кодов состояния является стандартом, и все они описаны в соответствующих документах RFC. Введение новых кодов должно производится только после согласования с IETF. Клиент может не знать все коды состояния, но он обязан отреагировать в соответствии с классом кода.

В настоящее время выделено пять классов кодов состояния:

1xx: Informational (Информационный) — запрос получен и понят, а обработка продолжается.
2xx: Success (Успешно) — запрос был успешно получен, понят и обработан.
3xx: Redirection (Перенаправление) — для выполнения запроса должны быть предприняты дальнейшие действия.
4xx: Client Error (Ошибка клиента) — запрос имеет плохой синтаксис или не может быть выполнен.
5xx: Server Error (Ошибка сервера) — сервер не в состоянии выполнить допустимый запрос.  
#Что такое jsonp-запрос?
JSONP или «JSON with padding» — это дополнение к базовому формату JSON. Он предоставляет способ запросить данные с сервера, находящегося в другом домене — операцию, запрещённую в типичных веб-браузерах из-за политики ограничения домена.
По правилу ограничения домена веб-страница, доставляемая с сервера server1.example.com, не может нормально связаться с сервером, отличным от server1.example.com. Исключением является HTML-элемент <script> находящийся на данной странице. Используя открытую политику для элементов <script>, некоторые страницы используют их, чтобы загружать JavaScript-код, оперирующий динамически создаваемыми JSON-данными из других источников. Этот шаблон поведения известен как JSONP.
#Как код, написанный на ES6 (ES2015-2017) превратить в код, который поддерживается IE10?
C помощью транспайлеров (например Babel.JS), которые переписывают код нового формата в старый, понятный IE10.
#Что такое полифилл?
«Полифилл» (англ. polyfill) – это библиотека, которая добавляет в старые браузеры поддержку возможностей, которые в современных браузерах являются встроенными.
#Как реализовать простейший модуль на js?
Когда приложение сложное и кода много – правильно разбить его на файлы. В каждом файле описываем какую-то часть. Эти файлы и есть модули.
Функции – единственная вещь в JavaScript, создающая новую область видимости. Если нам нужно, чтобы у модулей была своя область видимости, придётся основывать их на функциях.
Простейший модуль:
```javascript
var dayName = function() {
  var names = ["Понедельник", "Вторник", "Среда", "Четверг", "Пятница", "Суббота", "Воскресенье"];
  return function(number) {
    return names[number];
  };
}();

console.log(dayName(3));
```
#Что такое и зачем нужен паттерн модуль? Какие модули существуют в JS?
«Модуль» — это популярный паттерн проектирования, задача которого заключается в изоляции части логики приложения от глобального контекста для избегания конфликтов и ошибок. Модуль представляет собой в идеале независимый компонент, решающий одну небольшую задачу. Внутри модуля может быть сложная логика, но его цель — скрыть её от нас и предоставить нам простой и понятный API.

В языке JavaScript нет разделения на публичные, защищённые и приватные переменные. Но можно добиться псевдоприватности с помощью замыканий. Распространённая реализация «модуля» использует немедленно вызываемую функцию (IIFE) для скрытия внутренних переменных и функций.
```javascript
var tagList = (function() {
  // Приватная переменная, к
  // которой получить доступ можно
  // только внутри этой функции
  var tags = [];

  // «модуль» — это объект.
  // Возвращаемый объект публичен.
  // Снаружи можно получить доступ ко всем данным из этого объекта
  return {
    // публичные методы
    getItemsCount: function() {
      return tags.length;
    },

    addItem: function(tag) {
      tags.push(tag);
    }
  }
})();
```
#Как реализовать подписку на клик по кнопке, которая отработает только один раз? ( с примером кода )
#Какие события не "всплывают" ?
#Какие вспомогательные методы есть для работы с промисами?


#Календарь
http://jsbin.com/cuboyotufe/1/edit?html,css,js,output
