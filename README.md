1. Избегайте глобальных переменных

a) В большом проекте при обилии глобальных переменных возникает путаница в именах.

b) Глобальные переменные видны для любой функции, поэтому их легко можно изменить.

let a;

function doThis(){
    a = 4;
}

function doThat(){
    a = 5;
    doThis(); 
    console.log(a);
}

doThat(); // ответ a = 4, хотя мы ожидаем, что a = 5


2. Всегда объявлять локальные переменные

a) Локальные переменные не изменяет глобальную переменную
b) В противном случае переменная будет объявлена как глобальная и как свойство объекта window

Хорошо:

let name = "John";

function showName() {
let name = "Jack"; // локальная переменная, доступна только внутри функции
  console.log(name); // Jack
}
console.log(name); // John. Это глобальная переменная

Плохо:

let name = "Michael Jackson";

function showCelebrityName() {
    console.log(name);
}

function showOrdinaryPersonName() {
    name = "Johnny Evers";
    console.log(name);
}
showCelebrityName(); // Michael Jackson

// переменная name не была объявлена в функции, поэтому она изменяет глобальную
showOrdinaryPersonName(); // Johnny Evers
showCelebrityName(); // Johnny Evers

3. Объявления сверху

a) Делает ваш код немного чище.
b) Предотвращение нежелательных (подразумеваемых) глобальных переменных
с) Уменьшение нежелательных повторных деклараций
Хорошо:

let  someItem = 'some string',
     anotherItem = 'another string',
     oneMoreItem = 'one more string';

Плохо:

let someItem = 'some string';
alert('Hello World!');
let anotherItem = 'another string';
console.log(anotherItem);
let oneMoreItem = 'one more string';

4. Инициализация переменных

a) Делает ваш код немного чище.
b) Предотвращение неопределенного значения (undefined)

Хорошо:

let x = 1,
  y = 1;

Плохо:

let x;
let y;
x = 1;
y = 1;

5. Никогда не объявляйте числа, строки или логические объекты

let x = "Привет"  // строка         
new String("Привет"); // обьект


Хорошо:

var x = "John";  ;

Плохо:

var y = new String("John");

var x = "John";             
var y = new String("John");
(x === y) //  При сравнении будет false потому что обьект и строка не равны

6. Не использовать новый объект ()

Объявления через new Number(),new String() создаст обьект;
A String () возвращает строковый примитив
При строгом сравнении : 
var x = 5;             
var y = new Number(5);
будет false потому что обьект и строка не равны


Плохо:

var o = new Object();
 o.name = 'Jeffrey';
 o.lastName = 'Way';
 o.someFunction = function() {
    console.log(this.name);
 }

 Хорошо:

 var o = {
    name: 'Jeffrey',
    lastName = 'Way',
    someFunction : function() {
       console.log(this.name);
    }
 };

7. Остерегайтесь автоматического преобразования типов

Числа могут быть случайно преобразованы в строки или NaN (не число).
Вычитание строки из строки не приводит к ошибке, но возвращает NaN (не число)

Хорошо:

var x = 5 + 7;

Плохо:

var x = 5 + "7";

8. Используйте === вместо ==

Рекомендуется всегда использовать  === при сравнении т.к. он предотвращает ошибки приведения типов. 

Оператор = = сравнения всегда преобразует (в совпадающие типы) перед сравнением.

Оператор = = = заставляет сравнивать значения и тип:

0 === "";       // false
1 === "1";      // false
1 === true;     // false

Плохо:

0 == "";        // true
1 == "1";       // true
1 == true;      // true

9. Использовать параметры по умолчанию

Если функция вызывается с отсутствующими аргументами, отсутствующие значения устанавливаются в: undefined.

Хорошо:

function foo(bar = 10) {
   console.log(bar);
}

  foo(); // 10
  foo(undefined); // 10
  foo(20); //20

Плохо:

function foo(bar) {
   console.log(bar);
  }

foo(); // undefined

10. Завершение переключателей по умолчанию
Если вы не использовали инструкцию break, то будут выполнены инструкции следующего случая. И проверка на соответствие выражению не будет выполняться.
Если ни один case не совпал – выполняется вариант default.

Пример:
 
let arg = prompt("Введите число?");

switch (arg) {
  case '0':
  case '1':
    alert( 'Один или ноль' );
    break;

  case '2':
    alert( 'Два' );
    break;

  default:
    alert( 'Неизвестное значение' );
}

