## Структура кода
### Точка с запятой
Можно не ставить, но лучше ставить.
Так ошибка:
```
alert("Сейчас будет ошибка")
[1, 2].forEach(alert)
```
А так нет:
```
alert("Теперь всё в порядке");
[1, 2].forEach(alert)
```
JavaScript не вставляет точку с запятой перед квадратными скобками [...]
### Комментарии
// - одна строка
/* ... */ - много строк
Вкладывать многострочные нельзя:
```
/*
  /* ERROR */
*/
```
## Use strict
Используется для режима совместимости (изменяя поведение некоторых встроенных функци). Ставится в начале сценария. Отменить его нельзя.
Можно ставить в начале тела функци. Тогда аботает толкьо внутри функции.
> Некоторые функции языка, такие как «классы» и «модули», автоматически включают строгий режим.
##  Переменные
Вот так:
```sh
let message;
```
И так:
```sh
let user = 'John', age = 25, message = 'Hello';
```
И так:
```sh
let user = 'John',
  age = 25,
  message = 'Hello';
```
## Имена переменных
Используем lowerCamelCase:
```sh
myVeryLongName
```
> Имя переменной должно содержать только буквы, цифры или символы ```$``` и ```_```.
> Первый символ не должен быть цифрой.
> Регистр имеет значение.
> Нельзя использовать ``` let, class, return``` и ```function```
> Без ```use strict``` можно и не использовать ``` let```, но так лучше не делать
## Константы
Объявили при помощи ```const``` и если попробуем изменить, то получим ошибку.
> Ошибка будет если мы меняем только само значение. Изменив атрибут объекта (который хранится в константе) ошибку мы не получим.
## Имена констант
Если значение известно, до момента выполнения скрипта - используем CAPS:
```
const COLOR_RED = "#F00";
```
Если значение константы вычисляется, то нет:
```
const pageLoadTime = /* время, потраченное на загрузку веб-страницы */;
```
> var – это устаревший способ объявления. Его вообще не используем его
## Типы данных
> Встроенна функция ```typeof``` возвращает строку с описанием типа данных.
### Примитивные типы
> Примитивные типы сохраняются как значения, в отличие от объектов, хранящихся в качестве ссылки. Можно переназначить примитивный тип переменной, но это будет новое значение, старое не будет и не может быть изменено.
#### Число
```
let n = 123;
n = 12.345;
```
Есть еще бесконечность:
```
alert( 1 / 0 ); // Infinity
alert( Infinity ); // Infinity
alert( -Infinity ); // Infinity
```
Также есть ```NaN``` (результат неправильной или неопределённой математической операции):
```
alert( "строка" / 2 + 5 ); // NaN
```
> Если где-то в математическом выражении есть NaN, то результатом вычислений с его участием будет NaN.
В JavaScript тип ```number```  может содержать числа от 2^-53^ до 2^53^. Для еще больших чисел есть еще ```BigInt```:
```
const bigInt = 1234567890123456789012345678901234567890n;
```
#### Строка
```
let str = "Привет";
let str2 = 'Одинарные кавычки тоже подойдут';
let phrase = `Обратные кавычки позволяют встраивать переменные ${str}`;
```
#### Булево
Ну булево и булево. Вот так с ними можно:
```
let isGreater = 4 > 1;
alert( isGreater ); 
```
#### NULL
Ничего, пустота, отсутствие всякого значения
#### Undefined
Ничего назначено не было
> NULL - чтобы присвоить пустое значение, Undefined - для проверки присваивалось ли какое-либо значение 
#### Symbol
Используется для уникальных идентификаторов.
### Объекты
> Объекты хранятся по ссылке

Все, что не является примитивным типом, является объектом (в том числе и функции). Это особенный тип. 
## Преобразование типов
### Преобразования примитивных типов
|Значение|В строку|В число|В булево|
|-|-|-|-|
|""|""|0|false|
|"   "|""|0|true|
|"a"|"a"|NaN|true|
|123|"123"|123|true|
|1.23|"1.23"|1.23|true|
|true|"true"|1|true|
|false|"false"|0|false|
|Infinity|"Infinity"|Infinity|true|
|NaN|"NaN"|NaN|false|
|null|"null"|0|false|
|undefined|"undefined"|NaN|false|

### Преобразование объектов
Все объекты наследуют два метода преобразования: ```toString()``` и ```valueOf()```.
Метод ```toString()``` возвращает строковое представление объекта. Некоторые типы имеют более специализированные версии метода ```toString()```.
Задача метода ```valueOf()``` определена не так чётко: предполагается, что он должен преобразовать объект в представляющее его простое значение, если такое значение существует
В строку:
* Если объект имеет метод ```toString()```, интерпретатор вызывает его. Если он возвращает простое значение, интерпретатор преобразует значение в строку (если оно не является строкой) и возвращает результат преобразования.
* Если объект не имеет метода ```toString()``` или этот метод не возвращает простое значение, то интерпретатор проверяет наличие метода ```valueOf()```. Если этот метод определён, интерпретатор вызывает его. Если он возвращает простое значение, интерпретатор преобразует это значение в строку (если оно не является строкой) и возвращает результат преобразования.
* В противном случае интерпретатор делает вывод, что ни ```toString()``` ни ```valueOf()``` не позволяют получить простое значение и возбуждает ошибку ```TypeError```.

В число:
* Если объект имеет метод valueOf(), возвращающий простое значение, интерпретатор преобразует (при необходимости) это значение в число и возвращает результат.
* Если объект не имеет метода valueOf() или этот метод не возвращает простое значение, то интерпретатор проверяет наличие метода toString(). Если объект имеет метод toString(), возвращающий простое значение, интерпретатор выполняет преобразование и возвращает полученное значение.
* В противном случае интерпретатор делает вывод, что ни toString() ни valueOf() не позволяют получить простое значение и возбуждает ошибку TypeError.
> Методы toString() и valueOf() доступны для чтения и записи, поэтому их можно переопределить и явно указать, что будет возвращаться при преобразовании

## Операторы
```Унарный``` - оператор, который применяется к одному операнду.
```Бинарный``` - оператор, который применяется к двум  операндам.
Приоритеты операторов (список далеко не полный):
|Приоритет|Оператор|
|-|-|
|16|унарный плюс|
|16|унарный минус|
|14|умножение|
|14|деление|	
|13|бинарный плюс|
|13|бинарный минус|
|3|присваивание|


### Унарный +
Ничего не делает с числами. Но если операнд не число, унарный плюс преобразует его в число.
```
let apples = "2";
let oranges = "3";
alert( +apples + +oranges ); // 5
```
### Унарный -
То же самое, что и ```унарный плюс```, только меняет знак.
### Умножение
Ну умножение и умножение. Преобразует операнды в числа.
### Деление
Ну деление и деление. Преобразует операнды в числа.


### Бинарный +
Складывате числа, если ему подсунуть числа.
Сложит как строки, если один из операндов будет строкой.
> Операции выполняются слева направо. Если перед строкой идут два числа, то числа будут сложены перед преобразованием в строку:
```
alert(2 + 2 + '1' ); // будет "41", а не "221"
```
Если операнд не строка и не число - преобразует в строку.
### Присваивание
Оно выполняется справа-налево:
```
a = b = c = 2 + 2;
```
Сначала вычисляется самое правое выражение ```2 + 2```, и затем оно присваивается переменным слева: ```c```, ```b``` и ```a```

### Инкремент\декремент
Префиксная форма возвращает новое значение:
```
let counter = 1;
let a = ++counter; // 2
```
Постфиксная форма возвращает старое
```
let counter = 1;
let a = counter++; // 1
```
> Инкремент/декремент можно применить только к переменной. Попытка использовать его на значении, типа ```5++```, приведёт к ошибке.
### Оператор запятая
Выполняет каждый из его операндов (слева направо) и возвращает значение последнего операнда.
```
let x = 1;
x = (x++, x);
console.log(x); //2
```
Jператор ```,``` имеет очень низкий приоритет, ниже ```=```, поэтому 
```
let a = (1 + 2, 3 + 4); // 7
```
```
let a = 1 + 2, 3 + 4; // 3
```

## Операторы сравнения
Возвращают ```Boolean```
```>```, ```<```, ```>=```, ```>=``` - все преобразуют в числа.
### ==
```==``` - нестрогое равенство, выполняет преобразование типов (противоположный ему ```!=```).
Сначала преобразует все к одному типу, а затем выполняет ```===```
**Одинаковые** типы:
* ```Строки``` на идентичность (по-символьно, по кодам Unicode);
* ```Числа``` на одинаковость;
* ```Объекты``` - сравнивает ссылки;
* ```NaN``` и ```NaN```, всегда ```false```;
* Остальное всегда ```true```

**Разные** типы:
* ```Строки``` и ```число```, строку в число;
* Что угодно и ```NaN```, всегда ```false```
* ```Булево``` и ```число```, булево в число
* ```Булево``` и ```строка```, оба в числа
* ```NULL``` и ```число```, всегда ```false```
* ```NULL``` и ```строка```, всегда ```false```
* ```NULL``` и ```undefined```, всегда ```true``` (как бы отсутствие значения и там и там)
* ```Объект``` и другие типы, объект преобразуется в примитив.
### ===
```===``` - строгое равенство, сравнивает конкретные значения (противоположный ему ```!==```).
Не выполняет преобразование типов
### Выдержка из спецификации ECMA:
> Абстрактный алгоритм сравнения для отношений
> Сравнение x < y, где x и y являются значениями, возвращает true, false или undefined (последнее означает, что хотя бы один из операндов равен NaN). Такое сравнение производится следующим образом:
1. Вызвать ToPrimitive(x, подсказка Number).
2. Вызвать ToPrimitive(y, подсказка Number).
3. Если Тип(Результата(1)) равен String и Тип(Результата(2)) равен String - переход на шаг 16. (Заметим, что этот шаг отличается от шага 7 в алгоритме для оператора сложения + тем, что в нём используется и вместо или.)
4. Вызвать ToNumber(Результат(1)).
5. Вызвать ToNumber(Результат(2)).
6. Если Результат(4) равен NaN - вернуть undefined.
7. Если Результат(5) равен NaN - вернуть undefined.
8. Если Результат(4) и Результат(5) являются одинаковыми числовыми значениями - вернуть false.
9. Если Результат(4) равен +0 и Результат(5) равен -0 - вернуть false.
10. Если Результат(4) равен -0 и Результат(5) равен +0 - вернуть false.
11. Если Результат(4) равен +∞, вернуть false.
12. Если Результат(5) равен +∞, вернуть true.
13. Если Результат(5) равен -∞, вернуть false.
14. Если Результат(4) равен -∞, вернуть true.
15. Если математическое значение Результата (4) меньше, чем математическое значение Результата(5) (заметим, что эти математические значения оба конечны и не равны нулю) - вернуть true. Иначе вернуть false.
16. Если Результат(2) является префиксом Результата(1), вернуть false. (Строковое значение p является префиксом строкового значения q, если q может быть результатом конкатенации p и некоторой другой строки r. Отметим, что каждая строка является своим префиксом, т.к. r может быть пустой строкой.)
17. Если Результат(1) является префиксом Результата(2), вернуть true.
18. Пусть k - наименьшее неотрицательное число такое, что символ на позиции k Результата(1) отличается от символа на позиции k Результата(2). (Такое k должно существовать, т.к. на данном шаге установлено, что ни одна из строк не является префиксом другой.)
19. Пусть m - целое, равное юникодному коду символа на позиции k строки Результат(1).
20. Пусть n - целое, равное юникодному коду символа на позиции k строки Результат(2).
21. Если m < n, вернуть true. Иначе вернуть false.

> Абстрактный алгоритм сравнения для равенств
Сравнение x == y, где x и y являются значениями, возвращает true или false. Такое сравнение производится следующим образом:
1. Если Тип(x) отличается от Типа(y) - переход на шаг 14.
2. Если Тип(x) равен Undefined - вернуть true.
3. Если Тип(x) равен Null - вернуть true.
4. Если Тип(x) не равен Number - переход на шаг 11.
5. Если x является NaN - вернуть false.
6. Если y является NaN - вернуть false.
7. Если x является таким же числовым значением, что и y, - вернуть true.
8. Если x равен +0, а y равен -0, вернуть true.
9. Если x равен -0, а y равен +0, вернуть true.
10. Вернуть false.
11. Если Тип(x) равен String - вернуть true, если x и y являются в точности одинаковыми последовательностями символов (имеют одинаковую длину и одинаковые символы в соответствующих позициях). Иначе вернуть false.
12. Если Тип(x) равен Boolean, вернуть true, если x и y оба равны true или оба равны false. Иначе вернуть false.
13. Вернуть true, если x и y ссылаются на один и тот же объект или они ссылаются на объекты, которые были объединены вместе (см. раздел 13.1.2). Иначе вернуть false.
14. Если x равно null, а y равно undefined - вернуть true.
15. Если x равно undefined, а y равно null - вернуть true.
16. Если Тип(x) равен Number, а Тип(y) равен String, вернуть результат сравнения x == ToNumber(y).
17. Если Тип(x) равен String, а Тип(y) равен Number, вернуть результат сравнения ToNumber(x)== y.
18. Если Тип(x) равен Boolean, вернуть результат сравнения ToNumber(x)== y.
19. Если Тип(y) равен Boolean, вернуть результат сравнения x == ToNumber(y).
20. Если Тип(x) - String или Number, а Тип(y) - Object, вернуть результат сравнения x == ToPrimitive(y).
21. Если Тип(x) - Object, а Тип(y) - String или Number, вернуть результат сравнения ToPrimitive(x)== y.
22. Вернуть false.

## IF
```
if (year < 2015) {
  alert( 'Это слишком рано...' );
} else if (year > 2015) {
  alert( 'Это поздновато' );
} else {
  alert( 'Верно!' );
}
```
## Тернарный IF
```
let result = условие ? значение1 : значение2;
```
Его можно вкладывать друг в друга
## Логические операторы
```||``` вычисляется до первого истинного значения слева-направо. Приводит все в ```булево```
```&&``` вычисляется до первого ложного значения слева-направо. Приводит все в ```булево```
```!```  приводит все в ```булево```, инвертирует на противоположное.
## WHILE
```
while (condition) {
  // код
}
```
или
```
do {
  // код
} while (condition);
```
## FOR
```
for (начало; условие; шаг) {
  // ... тело цикла ...
}
```
или
```
for (;;) {
  // будет выполняться вечно
}
```
```break``` прерывает цикл.
```continue``` переводит к следующей итерации.
> Нельзя использовать break/continue справа от оператора ```?```

Можно поставить метку и ее прервать:
```
outer: for (let i = 0; i < 3; i++) {
  for (let j = 0; j < 3; j++) {
    break outer; 
  }
}
```
## Switch
Выполняет все ```case``` проходящие по условию, пока не встретит ```break```. Если ни один ```case``` не совпал – выполняется (если есть) вариант ```default```.
```
switch(x) {
  case 'value1':  
    [break]
  case 'value2':  
    [break]
  default:
    [break]
}
```
> Проверка на равенство всегда строгая. Значения должны быть одного типа, чтобы выполнялось равенство.

Можно и так написать (сгруппировать):
```
    case 3: // (*) группируем оба case
    case 5:
    alert('Неправильно!');
    alert("Может вам посетить урок математики?");
    break;
```

## Функции
Движок знает об объявленных функциях с начала выполнения скрипта - поэтому мы можем вызывать их в любом месте кода.
```
function showMessage() {
  // код
}
```
> Объявленную переменную видим только внутри функции. И также видим все внешние переменные. 
Все примитивные типы в качестве параметров передаются по значению.
Если параметр не указан, то его значением становится undefined.

Можно использовать ```return``` 
## Функциональные выражения
Это та же функция, только сохраненная в переменную. Они становятся доступны для вызова только после того, как они инициализированы в в конкретном месте в коде.
```
let sayHi = function() {
  alert( "Привет" );
};
```
> В конце надо ставить ```;``` так как это присваивание
У функций блочная область видимости.
Так будет ошибка:
```
if () {
    function welcome()  {            
} else {
    function welcome() {
}
welcome(); // Ошибка: welcome is not defined
```
А так нет:
```
let welcome;
if () {
    welcome = function() {       
  }                        
} else {
    welcome = function() {   
  }
}
welcome();
```
## Callback
Если мы передаем функцию в качестве параметра в другую функцию, и затем вызываем ее внутри, то эта функция и есть ```Callback```
## Стрелочные функции
```
let func = (arg1, arg2, ...argN) => expression
```
или
```
let sayHi = () => alert("Hello!");
```
>  У стрелочных функций нет this. Если происходит обращение к this, его значение берётся снаружи

