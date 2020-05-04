# Короткий довідник Java Script

[Посібник JavaScript MDN](https://developer.mozilla.org/uk/docs/Web/JavaScript/Guide), [яваскрипт.укр](http://яваскрипт.укр), [Современный учебник JavaScript](https://learn.javascript.ru/)

## Структура коду

Інструкції пишуться через крапку з комою. 

Синтаксис коментарів такий самий, як в C++ та багатьох інших мовах програмування:

```js
// коментар для одного рядка 
/* довгий коментар
   на кілька рядків
 */
/* Однак, не можна /* змішувати коментарі */ SyntaxError */
```

## Робота з даними

### Змінні та константи <a name="vars"></a>

#### Оголошення (var,let,const)

Для створення змінної в JavaScript використовується ключове слово [`let`](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Statements/let). Оператор **`let`** оголошує локальну змінну блочної області видимості, з необов'язковим присвоєнням їй початкового значення.

Даний приклад створює (іншими словами: *об'являє* або *означує*) змінну з іменем «message», і поміщає в неї дані використовуючи оператор присвоювання `=` . Рядок збережеться в області пам'яті, зв'язаною зі змінною. Ми можемо отримати до неї доступ, використовуючи ім'я змінної. 

```javascript
let message1;
message1 = 'Hello'; // записати рядок в змінну
console.log(message1); // пише в консоль значення змінної
let message2 = 'Hello';//Можна суміщати об'явлення змінної і запис даних в один рядок.   
let user = 'John', age = 25, message3 = 'Hello';//можна кілька змінних об'являти в одному рядку
//або навіть так
let user1 = 'John',
  age1 = 25,
  message4 = 'Hello';
```

Областю видимості змінних, оголошених через **`let`**, є блок, у якому вони визначені, а також будь-які вкладені в нього блоки. У цьому сенсі **`let`** дуже схожий на **`var`**. Головна відмінність полягає в тому, що областю видимості змінної **`var`** є уся замикаюча функція.

На верхньому рівні програм та функцій **`let`**, на відміну від **`var`**, не створює властивості глобального об'єкта. 

Можна також використовувати інше ключове слово  [`var`](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Statements/var) замість `let`. Оголошення змінних через `var` обробляються до виконання будь-якого коду. Область видимості змінної, що її оголошено оператором `var`, залежить від *контексту виконання*, це або замикаюча функція, або — якщо змінну оголошено поза межами всіх функцій — глобальний контекст. Повторне оголошення змінної у JavaScript не скидає її значення. 

```javascript
var message = 'Hello';
```

**Оголошення `const`**  створює посилання на значення, доступне лише для читання. Що **не** гарантує незмінність значення, на котре вказує посилання, а лише той факт, що не можна повторно присвоїти будь-яке значення змінній з відповідним ім'ям.

#### Області видимості

Коли ви оголошуєте змінну за  межами будь-якої функції, вона називається глобальною змінною, оскільки  вона доступна для будь-якого іншого коду в поточному документі. Коли ви оголошуєте змінну в межах функції, вона називається локальною змінною, оскільки вона доступна лише в межах цієї функції. 

JavaScript версій, що передують ECMAScript 6, не має області [блокових операторів](https://developer.mozilla.org/uk/docs/Web/JavaScript/Guide/Control_flow_and_error_handling#Block_statement); вірніше, змінна, оголошена у блокові, є локальною для *функції,* у якій знаходиться цей блок *(або глобальною змінною, якщо блок поза функціями у скрипті)*. Для прикладу розглянемо код, який буде записувати `5`, тому, що область видимості змінної `x` - функція (або глобальинй контекст), у якій оголошена функція `x`, а не блок оператора `if`.

```js
if (true) {
  var x = 5;
}
console.log(x);  // 5
```

Ця поведінка змінюється при використанні ключового слова `let`, введенного в ECMAScript 6.

```js
if (true) {
  let y = 5;
}
console.log(y);  // ReferenceError: y is not defined
```

Глобальні змінні фактично є властивостями глобальних об'єктів. На веб-сторінках глобальним об'єктом є [`window`](https://developer.mozilla.org/uk/docs/Web/API/Window), тому ви можете встановлювати та отримувати доступ до глобальних змінних за допомогою синтаксису `window.*variable*`.

Отже, ви можете отримати доступ до глобальних змінних оголошених в  одному вікні або фреймі з іншого вікна або фрейму, вказавши при цьому  ім'я цього вікна або фрейму. Наприклад, якщо в документі оголошена  змінна під назвою `phoneNumber`, ви можете звернутися до неї з фрейму `parent.phoneNumber`.

### Типи даних та літерали <a name="types"></a>

Змінна в JavaScript може містити будь-які дані. У один момент там може бути рядок, а в інший – число. Коли змінна не прив'язується до конкретного типу, але при цьому типи даних існують, це називається "динамічною типізацією". 

```javascript
// не буде помилкою
let message = "hello";
message = 123456;
```

В JS існує вісім типів даних: `number`, `BigInt`, `string`, `boolean`, `null`, `undefined`, `object`, `symbol` 

#### number

Числовий тип даних (`number`) представляють собою як цілочисельні значення, так і числа з  плаваючою комою. Крім звичайних чисел (`15` чи  `36.6`) існують спеціальні числові значення: `Infinity` (нескінченність), `-Infinity` і `NaN` (не число).

```js
console.log(1+2);//видасть 3
console.log(1.1+2.1);//видасть 3.2
console.log("2"+3);//видасть "23"
console.log("два"+3);//видасть "два3"
console.log(2/"0.5");//видасть 4
console.log("два"/3);//видасть NaN
console.log(1/0);//видасть Infinity
```

Цілочисельні літерали типів [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) та [`BigInt`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt) можна виразити у різних формах, в залежності від першої літери: 10-ковій (без літери), всімковій (`0o`), 16-ковій (`0x`), 2-вій (`0b`), наприклад: 

```js
console.log(-345);		//-345
console.log(-0o77);		//-63
console.log(-0xF1A7);	//-61863
console.log(-0b11);		//-3
```

Літерали з плаваючою комою можуть задаватися у різному форматі:

```js
console.log(3.1415926);	//3.1415926
console.log(-.123456789);//-0.123456789
console.log(-3.1E+12);	//-3100000000000
console.log(.1e-3);		//0.0001
```

#### BigInt

У JavaScript тип `number` не може містити більше, ніж `2`[^53] (два в степені 53), або менше, ніж `-2`[^53] для від'ємних. Це технічне обмеження викликає їх внутрішнє представлення. `2`[^53] - це досить велике число. Але іноді нам потрібні дійсно гігантські числа, наприклад в криптографії або при використанні мітки часу («timestamp») з мікросекундами. Тип `BigInt` був доданий в JavaScript, щоб дати можливість працювати з цілими числами довільної довжини. Щоб створити значення типу `BigInt`, необхідно додати `n` в кінець числового літералу:

```javascript
// символ "n" в кінці значить, що це BigInt
const bigInt = 1234567890123456789012345678901234567890n;
console.log(-345n);//-345n
console.log(-0o77n);//-63n
console.log(-0xF1A7n);//-61863n
console.log(-0b11n);//-3n
```

#### string <a name="string"></a>

Стрічка (`string`) в JavaScript повинна бути взята в лапки.

```javascript
let str = "Рядок в двойнищ лапках";
let str2 = 'Можна використовувати одинарні лапки';
let phrase = `Зворотні лапки (зліва від '1') дозволяють вставляти значення змінних ${str}, інші лапки таке не дозвоялють робити`;
```

Крім звичайних символів, ви можете також включати до рядків спеціальні символи, як показано в наступному прикладі.

```js
"one line \n another line"
```

У наступній таблиці перераховані спеціальні символи, які можна використовувати в рядках JavaScript.

| Character     | Meaning                                                      |
| ------------- | ------------------------------------------------------------ |
| `\0`          | Null Byte                                                    |
| `\b`          | Backspace                                                    |
| `\f`          | Form feed                                                    |
| `\n`          | New line                                                     |
| `\r`          | Carriage return                                              |
| `\t`          | Tab                                                          |
| `\v`          | Vertical tab                                                 |
| `\'`          | Apostrophe or single quote                                   |
| `\"`          | Double quote                                                 |
| `\\`          | Backslash character                                          |
| `\*XXX*`      | The character with the Latin-1 encoding specified by up to three octal digits *XXX* between 0 and 377. For example, \251 is the octal sequence for the copyright symbol. |
| `\x*XX*`      | The character with the Latin-1 encoding specified by the two hexadecimal digits *XX* between 00 and FF. For example, \xA9 is the hexadecimal sequence for the copyright symbol. |
| `\u*XXXX*`    | The Unicode character specified by the four hexadecimal digits *XXXX*. For example, \u00A9 is the Unicode sequence for the copyright symbol. See [Unicode escape sequences](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Lexical_grammar#String_literals). |
| `\u*{XXXXX}*` | Unicode code point escapes. For example, \u{2F804} is the same as the simple Unicode escapes \uD87E\uDC04. |

Наприклад

```js
var quote = "He read \"The Cremation of Sam McGee\" by R.W. Service.";
console.log(quote);// He read "The Cremation of Sam McGee" by R.W. Service.
var home = "c:\\temp";
console.log(home);// c:\temp
```

Ви також можете уникнути розривів ліній, передуючи їм зворотньою  косою. Зворотня коса та розрив рядків видаляються зі значення рядка.

```js
var str = "цей текст\
розірваний \
між кількома \
рядками."
console.log(str);   // цей текст розірваний між кількома рядками.
```

```js
var poem = 
"Roses are red,\n\
Violets are blue.\n\
I'm schizophrenic,\n\
And so am I."
```

#### boolean

Булевий тип (`boolean`) може приймати значення: `true` (істина) і `false` (хибність). Можуть бути результатом порівняння 

```javascript
let isGreater = 4 > 1;
console.log(isGreater); // буде true 
let a = true; // булевий літерал
```

#### null 

Це тип і значення `null`, що значить `нічого`

```javascript
let age = null;
```

#### undefined

Значення `undefined` - значить, що змінній не було присвоєне значення                       

```javascript
let x;
console.log(x); // виведе "undefined"
```

#### function

Типу змінної `function` не існує. Тим не менше, функції інколи проявляють властивості змінних. Робота з функціями описана у розділі [Функції](#functions)

#### object

Детальніше про роботу з обєктами можна почитати [тут](jsobjects.md).

`object` - у JavaScript є колекції **властивостей** і **методів**. Методом  називається функція, яка є членом об'єкта. Властивість є значення або  набір значень (у вигляді масиву або об'єкта), який є членом об'єкта і  може містити будь який тип даних.

Конструктор `Object` створює об'єкт-обгортку для переданого значення.  Якщо значенням є `null` або `undefined`, створює і повертає порожній об'єкт, в іншому випадку повертає об'єкт такого типу, який відповідає  переданому значенню.

 JavaScript підтримує 4 типи об'єктів:

- внутрішні об'єкти, такі як [Array](http://xn--80adth0aefm3i.xn--j1amh/Array) і [String](http://xn--80adth0aefm3i.xn--j1amh/String);
- створені об'єкти за допомогою конструктора або [функції-конструктор](http://xn--80adth0aefm3i.xn--j1amh/функція-конструктор);
- об'єкти базового середовища, такі як [window](http://xn--80adth0aefm3i.xn--j1amh/window) і [document](http://xn--80adth0aefm3i.xn--j1amh/document);
- об'єкти ActiveX.

Обєкт можна створити через конструктор, або через літерал

```javascript
let user = new Object(); // синтаксис "конструктор об'єкта"
let user = {};  // синтаксис "літерал об'єкта"
```

Об'єктні літерали - це список з нуля або більше пар імен властивостей та асоційованих значень об'єкту, взятих у фігурні дужки (`{}`). **Не використовуйте об'єктні літерали на початку інструкції!** Це призведе до помилки (або не поводитиметься так, як ви очікували), оскільки `{` буде інтерпретуватися як початок блоку.

Властивості, які також називають **полями**,  мають ключ, який також називають **ім'ям** або **ідентифікатором**.  Використовуючи літеральний синатксис об'явлення ми можемо одразу в об'єкт помістити кілька властивостей через пару "ключ : значення".  Значення може бути будь якого типу, в тому числі об'єктом. Доступ до властивостей може проводитися через крапку. Наприклад: 

```js
var sales = 'Toyota';
function carTypes(name) {
  if (name === 'Honda') {
    return name;
  } else {
    return "Sorry, we don't sell " + name + ".";
  }
}
var car = { myCar: 'Saturn', getCar: carTypes('Honda'), special: sales };
console.log(car.myCar);   // Saturn
console.log(car.getCar);  // Honda
console.log(car.special); // Toyota 
```

Видалення властивостей проводитсья через `delete`

```javascript
delete user.age;
```

Крім того, ви можете використовувати числовий або  рядковий літерал для назви властивості або вкладати об'єкт всередину  іншого. У наступному прикладі використовуються ці можливості.

```js
var car = { manyCars: {a: 'Saab', b: 'Jeep'}, 7: 'Mazda' };
console.log(car.manyCars.b); // Jeep
console.log(car[7]); // Mazda
```

Імена властивостей об'єкта можуть бути будь-якими  рядками, включаючи порожні. Якщо ім'я властивості не є дійсним ідентифікатором (не за правилами найменування змінних, наприклад включає пробіли) чи числом JavaScript, воно повинно бути вставлено в  лапки. До імен властивостей, які не є дійсними ідентифікаторами, не можна отримати доступ до властивості через крапку (`.`), але *можна* можна це зробити через квадартін лапки ("`[]`").

```js
var unusualPropertyNames = {
  '': 'An empty string',
  '!': 'Bang!'
}
console.log(unusualPropertyNames.'');   // SyntaxError: Unexpected string
console.log(unusualPropertyNames['']);  // An empty string
console.log(unusualPropertyNames.!);    // SyntaxError: Unexpected token !
console.log(unusualPropertyNames['!']); // Bang!
```

Доступ через квадратні лапки також дає можливість доступатися до властивостей об'єкту через змінну або вираз. 

```javascript
let key = "likes birds";
user[key] = true; // те саме, що і user["likes birds"] = true;

let fruit = prompt("Який фрукт купити?", "apple");
let bag = {
  [fruit]: 5, // ім'я властивості буде взято зі змінної fruit 
};
```

 Якщо необхідно властивості надавати значення з тим самим іменем, його можна не вказувати:

```javascript
function makeUser(name, age) {
  return {
    name, // те саме, що і name: name
    age   // те саме, що і age: age
    // ...
  };
}
```

Перевірка властивостей продиться через оператор [`in`](#in)

Перебір усіх властивостей проводитьс через [`for..in`](#forin)

Присвоєння для обєктів працює як копіювання за посиланням на той же об`єкт.

Порівняння обєктних змінних `==` або `===` показує, що ці змінні посилаються на той же обєкт.

#### array (масив) <a name="array"></a>

*Масив* - це упорядкований набір значень, на який ви посилаєтесь з ім'ям та індексом.

У JavaScript немає явного типу даних масиву. Однак ви можете використовувати заздалегідь заданий об’єкт `Array` та його методи для роботи з масивами у ваших програмах. Об'єкт `Array` має методи маніпулювання масивами різними способами, такими як  з'єднання(joining), реверсування(reversing) та сортування. Він має  властивість визначати довжину масиву та інші властивості для  використання з регулярними виразами.

Наступні операції створюють еквівалентні масиви:

```js
let arr1 = new Array(element0, element1, ..., elementN)
let arr2 = Array(element0, element1, ..., elementN)
let arr3 = [element0, element1, ..., elementN]
```

Для створення масиву з ненульовою довжиною, але без будь-яких елементів, може бути використане будь-яке з наведеного нижче:

```js
let arr1 = new Array(arrayLength) 
let arr2 = Array(arrayLength)
// Це має точно такий же ефект 
let arr3 = []: arr3.length = arrayLength
```

На рівні реалізації масиви JavaScript фактично зберігають свої елементи як стандартні властивості об'єкта, використовуючи індекс масиву як ім'я властивості.

Властивість `length` особлива. Вона завжди повертає індекс останнього елемента плюс один. (У наведеному нижче прикладі `'Dusty' `індексується на рівні 30, тому `cats.length` повертає `30 + 1`). Ви також можете записати значення у властивість `length`. Введення значення, коротшого за кількість збережених елементів, скорочує масив. Написання `0` спустошує масив повністю:

Наступний код створює багатовимірний масив.

```js
let a = new Array(4)
for (let i = 0; i < 4; i++) {
  a[i] = new Array(4)
  for (let j = 0; j < 4; j++) {
    a[i][j] = '[' + i + ', ' + j + ']'
  }
}
```

```js
let ar1 = [[1,2,3],[4,5,6]];//двовимірний масив 2 на 3
console.log (ar1.length);   //2
console.log (ar1[0].length);//3
console.log (ar1[1]);       //Array(3) [4, 5, 6]
console.log (ar1[1][1]);    //5
```

Для перебору елементів масиву використовують операції [ітерацій](#loops)

У таблиці нижче наведений перелік методів та властивостей масивів:

| Метод                                                        | Призначення                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [concat](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/concat) | поєднання масивів                                            |
| [copyWithin](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/copyWithin) | додає дрібну копію частини масиву в іншу позицію в тому ж масиві |
| [entries](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/entries) | повертає новий об'єкт ітератора масиву (**Array Iterator**), який містить пари ключ-значення для кожного індексу в масиві. |
| [every](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/every) | перевіряє, чи всі елементи масиву відповідають умові, що задана функцією, яка передається як аргумент |
| [fill](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/fill) | заповнює (змінює) всі елементи масиву з початкового індексу до кінцевого  статичним значенням |
| [filter](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) | створює новий масив з усіма елементами, що пройшли перевірку вказаною функцією |
| [find](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/find) | повертає значення першого елемента в масиві, що задовільняє передану функцію тестування |
| [findIndex](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex) | повертає індекс першого елемента у масиві, який задовольняє надану перевірочну функцію |
| [flat](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/flat) | створює новий масив який містить всі елементи вкладених масивів до вказаної глибини |
| [flatMap](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/flatMap) | аналогічно послідовному виклику [`map()`](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/map) та [`flat()`](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/flat) з глибиною 1 |
| [forEach](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach) | виконує надану функцію один раз для кожного елемента масиву  |
| [from](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/from) | створює новий екземпляр `Array` з подібного до масиву або ітерабельного об'єкта |
| [includes](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/includes) | з'ясовує, чи масив містить елемент із вказаним значенням     |
| [indexOf](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf) | повертає перший індекс, за яким даний елемент був знайдений в масиві |
| [isArray](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/isArray) | з'ясовує, чи є передане значення є масивом                   |
| [join](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/join) | створює та повертає рядок, що об'єднує всі елементи масиву   |
| [keys](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/keys) | вертає новий об'єкт перебирача ключів (індексів) масиву      |
| [lastIndexOf](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/lastIndexOf) | повертає останній індекс, за яким заданий елемент було знайдено у масиві |
| [length](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/length) | встановлює або повертає кількість елементів у цьому масиві   |
| [map](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/map) | створює новий масив з результатами виклику наданої функції на кожному елементі масиву |
| [of](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/of) | створює новий екземпляр `Array` з заданої кількості аргументів |
| [pop](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/pop) | видаляє останній елемент масиву та повертає цей елемент      |
| [`prototype`](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/prototype) | Дозволяє додавати властивості до масивів.                    |
| [push](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/push) | додає один або більше елементів у кінець масиву та повертає нову довжину масиву |
| [reduce](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce) | виконує вказану функцію для кожного елемента масиву та повертає єдине значення |
| [reduceRight](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/reduceRight) | застосовує функцію до акумулятора та кожного елемента масиву (справа наліво), зменшуючи його до єдиного значення |
| [reverse](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse) | транспонує масив , змінюючи послідовність елементів на протилежну |
| [shift](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/shift) | видаляє перший елемент з масиву і повертає цей елемент       |
| [slice](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/slice) | повертає дрібну копію частини масиву у новий масив           |
| [some](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/some) | з'ясовує, чи містить масив хоч один елемент, для якого зазначена функція |
| [sort](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) | відсортовує елементи масиву                                  |
| [splice](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/splice) | змінює вміст масиву, видаляючи існуючі та/або додаючи нові елементи |
| [toLocaleString](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/toLocaleString) | повертає рядок, що відображає елементи масиву                |
| [toSource](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/toSource) | повертає рядкове представлення першокоду масиву              |
| [toString](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/toString) | повертає рядкове представлення заданого масиву та його елементів |
| [unshift](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/unshift) | додає один або декілька елементів на початок масиву          |
| [values](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array/values) | повертає новий об'єкт ітератора масиву (Array Iterator), який містить значення кожного елемента масиву |

Див також [MSDN](https://wiki.developer.mozilla.org/uk/docs/Web/JavaScript/Guide/Indexed_collections)

#### symbol

Тип `symbol` (символ) наряду з типом `string` використовується для створення ідентифікаторів властивостей об'єктів. Однак символи є унікальними ідентифікаторами.  

```javascript
// Створюємо новий символ id
let id = Symbol();
let user = {
  name: "Вася",
  age: 30,
  [id]: 123
};
console.log (user[id]);
```

Є також глобальні символи, системні символи доступні через глобальний об'єкт `Symbol`. 

#### Оператор typeof <a name="typeof"></a>

Оператор `typeof` повертає тип аргумента. Він працює однаково з довма синтаксисами

```js
typeof операнд
typeof (операнд)
```

```javascript
console.log (typeof undefined);// "undefined"
console.log (typeof 0) ;// "number"
console.log (typeof 1n); // "bigint"
console.log (typeof true); // "boolean"
console.log (typeof "foo"); // "string"
console.log (typeof Symbol("id")); // "symbol"
conso;e.log (typeof (['Я','М']));//"object", бо масиви це об'єкти
console.log (typeof Math); // "object" - так як Math вбудований в JS обєкт для роботи з мат.операціями
console.log (typeof null); // "object" - хоч це не так
console.log (typeof console.log); // "function" - хоч формально такого типу немає, для методів і функцій поертається "function"
```







### Перетворення типів <a name="typeconv"></a>

Найчастіше оператори і функції автоматично перетворюють передані їм значення (примітвиного типу) до потрібного типу. Наприклад, `console.log` автоматично перетворює будь-яке значення до рядка. Математичні оператори перетворюють значення до чисел. Але в випадки, коли нам потрібно явно перетворити значення в очікуваний тип.

#### В string

Можна використовувати функцію `String (value)`, щоб явно перетворити значення до рядка:              

```javascript
let value = true;
console.log (typeof value); // boolean
value = String(value); // тепер це рядок "true"
console.log (typeof value); // string
```

#### В Number

Можна використати функцію `Number(value)`, щоб явно перетворити `value` в число. Якщо рядок не може бути перетверений в число, результатом буде `NaN`.

```javascript
let str = "123"; console.log(typeof str); // string
let num = Number(str); console.log(typeof num); // стає числом 123, тому number
let age = Number("Будь який рядок без числа"); console.log(age); // NaN, перетворення не вдалося
console.log(Number("   123   ") ); // 123
console.log(Number("123z") );      // NaN (помилка читання числа в "z")
console.log(Number(true) );        // 1
console.log(Number(false) );       // 0
```

Почти усі математичні оператори иконують чисельне перетворення, за виключенням  `+`. Якщо один із доданків є рядком, тоді всі інші приводться до рядків і робиться конкатинація (зєднання).                     

У випадку, коли значення, що представляє число, знаходиться в пам'яті як рядок, існують методи для перетворення [`parseInt()`](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/parseInt) та [`parseFloat()`](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/parseFloat). 

`parseInt` повертає тільки цілі числа, тому його використання обмежується десятковими знаками. Окрім того, найкращою практикою для `parseInt` завжди є включення параметра radix. Параметр radix використовується для визначення чисельної системи, яка буде використовуватися.

```js
let a='10'; console.log (parseInt(a,10));//10, бо база 10-кова
let b='10'; console.log (parseInt(b,16));//16, бо база 16-кова
let c='10'; console.log (parseInt(c,2));//2, бо база 2-кова
let d='10ttf'; console.log (parseInt(d,16));//16
```

```js
let a='10.1'; console.log (parseFloat(a));//10.1
let b='1e+2'; console.log (parseFloat(b));//100
let c='.456'; console.log (parseFloat(c));//0.456
let d='0,456'; console.log (parseFloat(d,16));//0
let e='4.5ffff.34'; console.log (parseFloat(e,16));//4.5
```

Альтернативним способом отримання числа з рядка є оператор `+` (одинарний плюс):

```js
"1.1" + "1.1" = "1.11.1"
(+"1.1") + (+"1.1") = 2.2   
```

#### В Boolean                    

```javascript
console.log(Boolean(1)); // true
console.log(Boolean(0)); // false
console.log(Boolean("Привіт!")); // true
console.log(Boolean("")); // false
console.log(Boolean("0")); // true
console.log(Boolean(" ")); // пробіл це також true (любий непустий рядок це true)
```

### Оператори <a name="operators"></a>

[developer.mozilla.org](https://developer.mozilla.org/uk/docs/Web/JavaScript/Guide/%D0%92%D0%B8%D1%80%D0%B0%D0%B7%D0%B8_%D1%82%D0%B0_%D0%BE%D0%BF%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%B8)

#### Присвоєння (=)

Лівосторонньому операнду `=` дається значення правостороннього виразу.

```javascript
let x = 2 * 2 + 1;
console.log(x); // 5
let a, b, c;
a = b = c = 2 + 2;//присвоєння ланцюжком, усім змінним буде присвоєно 4
let a1 = 1;//1
let b1 = 2;//2
let c1 = 3 - (a1 = b1 + 1);//0
```

Для об'єктів присвоюється не значення  копіюється посилання. Тобто 

```javascript
let user = { name: "John" };
let admin = user; // це друга змінна, яка посилається на той же об'єкт
```



#### Оператори порівняння

[Оператор порівняння](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Operators/Оператори_порівняння) порівнює свої операнди та повертає логічне значення, базуючись на істинності  порівняння. Операнди можуть бути числовими, рядковими, логічними  значеннями або об'єктами. Рядки порівнюються згідно стандартного  лексикографічного порядку, з використанням значень Unicode. У більшості  випадків, якщо два операнди не належать до одного типу, JavaScript  намагається привести їх до належного для порівняння типу. Зазвичай це  призводить до числового порівняння операндів. Єдиними винятками у  конвертації типів під час порівняння є оператори `===` та `!==`, які виконують перевірку на строгу рівність та строгу нерівність. Ці  оператори не намагаються перед перевіркою на рівність привести операнди  до спільного типу. Наступна таблиця наводить оператори порівняння у  контексті цього фрагменту коду:

```js
var var1 = 3;
var var2 = 4;
```

| Оператор                                                     | Опис                                                         | Приклади, які повертають true              |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------ |
| [Рівність](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Operators/Оператори_порівняння#Рівність) (`==`) | Повертає `true`, якщо оператори рівні.                       | `3 == var1`    `"3" == var1`    `3 == '3'` |
| [Нерівність](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Operators/Оператори_порівняння#Нерівність_!) (`!=`) | Повертає `true`, якщо оператори нерівні.                     | `var1 != 4    var2 != "3"`                 |
| [Строга рівність](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Operators/Оператори_порівняння#Ідентичність_строга_рівність) (`===`) | Повертає `true` якщо оператори рівні та належать до одного типу. Дивіться також [`Object.is`](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Object/is) та [однаковість у JS](https://developer.mozilla.org/uk/docs/Web/JavaScript/Перевірка_на_рівність_та_однаковість). | `3 === var1`                               |
| [Строга нерівність](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Operators/Оператори_порівняння#Неідентичність_строга_нерівність_!) (`!==`) | Повертає `true`, якщо оператори належать до одного типу, але нерівні, або належать до різних типів. | `var1 !== "3"    3 !== '3'`                |
| [Більше ніж](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Operators/Оператори_порівняння#Більше_ніж_>) (`>`) | Повертає `true`, якщо лівий операнд більший за правий.       | `var2 > var1    "12" > 2`                  |
| [Більше чи дорівнює](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Operators/Оператори_порівняння#Більше_чи_дорівнює_>) (`>=`) | Повертає `true`, якщо значення лівого операнда більше або дорівнює значенню правого операнда. | `var2 >= var1    var1 >= 3`                |
| [Менше ніж](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Operators/Оператори_порівняння#Менше_ніж_<) (`<`) | Повертає `true`, якщо лівий операнд менший за правий.        | `var1 < var2    "2" < 12`                  |
| [Менше чи дорівнює](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Operators/Оператори_порівняння#Менше_чи_дорівнює_<) (`<=`) | Повертає `true`, якщо значення лівого операнда менше або дорівнює значенню правого операнда. | `var1 <= var2    var2 <= 5`                |

**Заувага:** (**=>**) не оператор, а позначення для [стрілкових функцій](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Functions/Стрілкові_функції).

#### Арифметичні оператори

[Арифметичний оператор](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Operators/Arithmetic_Operators) приймає числові значення (літерали чи змінні) в якості операндів та повертає єдине числове  значення. Стандартними арифметичними операторами є додавання (`+`), віднімання (`-`), множення (`*`) та ділення (`/`). Ці оператори працюють так само, як і в більшості інших  мов програмування при використанні з числами з рухомою комою (зокрема,  зауважте, що ділення на нуль повертає [`Infinity`](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Infinity)). Додаткові арифметичні оператори:

| Оператор                     | Опис                                                         | Приклад                                                      |
| ---------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Остача(`%`)                  | Бінарний оператор. Повертає цілочисельну остачу від ділення двох операндів. | `12 % 5` повертає 2.                                         |
| Інкремент (`++`)             | Унарний оператор. Додає до операнда одиницю. Якщо використовується як префіксний оператор (`++x`), повертає значення операнда після додавання одиниці; якщо використовується як постфіксний оператор (`x++`), повертає значення операнда перед додаванням одиниці. | Якщо `x` дорівнює 3, тоді `++x` присвоює `x` значення 4 та повертає 4, в той час, як `x++` повертає 3 і лише тоді присвоює `x` значення 4. |
| Декремент (`--`)             | Унарний оператор. Віднімає одиницю від свого операнда. Повернене значення аналогічне поверненому значенню оператора інкременту. | Якщо `x` дорівнює 3, тоді `--x` присвоює `x` значення 2 та повертає 2, в той час, як `x--` повертає 3 і тільки тоді присвоює `x` значення 2. |
| Унарний мінус (`-`)          | Унарний оператор. Повертає операнд з протилежним знаком.     | Якщо `x` дорівнює 3, то `-x` повертає -3.                    |
| Унарний плюс (`+`)           | Унарний оператор. Намагається перетворити операнд на число, якщо він не є числом. | `+"3"` повертає `3`.     `+true` повертає `1.`               |
| Піднесення до степеня (`**`) | Підносить `основу степеня` до `показника` степеня, тобто, `основапоказник` | `2 ** 3` повертає `8`.     `10 ** -1` повертає `0.1`.        |

#### Бітові оператори

[Бітовий оператор](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators) опрацьовує свої операнди як послідовність 32-х бітів (нулів та одиниць), а не як  десяткові, шістнадцяткові або вісімкові числа. Наприклад, десяткове  число дев'ять має бітове представлення 1001. Бітові оператори виконують  операції над цими бітовими представленнями, але повертають стандартні  числові значення JavaScript. Наступна таблиця наводить перелік бітових операторів JavaScript.

| Оператор                          | Застосування | Опис                                                         |
| --------------------------------- | ------------ | ------------------------------------------------------------ |
| Побітове І (AND)                  | `a & b`      | Повертає одиницю на кожній позиції, де відповідні біти обох операндів дорівнюють одиницям. |
| Побітове АБО (OR)                 | `a | b`      | Повертає нуль на кожній позиції, де відповідні біти обох операндів дорівнюють нулям. |
| Виключне побітове АБО (XOR)       | `a ^ b`      | Повертає нуль на кожній позиції, де відповідні біти однакові.     [Повертає один на кожній позиції, де відповідні біти мають різні значення.] |
| Побітове НЕ (NOT)                 | `~ a`        | Виконує інверсію бітів операнду.                             |
| Лівий зсув                        | `a << b`     | Зсуває `a` у двійковому представленні на `b` бітів ліворуч, заповнюючи позиції справа нулями. |
| Правий зсув з розширенням знаку   | `a >> b`     | Зсуває `a` у двійковому представленні на `b` бітів праворуч, відкидаючи зсунуті біти. |
| Правий зсув із заповненням нулями | `a >>> b`    | Зсуває `a` у двійковому представленні на `b` бітів праворуч, відкидаючи зсунуті біти та заповнюючи позиції зліва нулями. |

Концептуально побітові логічні оператори працюють наступним чином:

- Операнди перетворюються на 32-бітні цілі числа та виражаються  послідовністю бітів (нулів та одиниць). Числа, що мають більше 32 бітів, втрачають свої старші біти. Наприклад, наступне ціле число, що має  більше 32 бітів, буде перетворено на 32-бітне ціле число:  

  ```html
  До:     11100110111110100000000000000110000000000001
  Після:              10100000000000000110000000000001
  ```

-  Кожен біт першого операнду ставиться у пару до відповідного біту  другого операнду: перший біт до першого біту, другий біт до другого, і  так далі.
- Оператор застосовується до кожної пари бітів, а результат будується побітово. Наприклад, бінарним представленням числа дев'ять є 1001, а бінарним  представленням п'ятнадцяти є 1111. Отже, коли бітові оператори  застосовуються до цих величин, результати будуть наступні:

| Вираз    | Результат | Двійковий опис                                               |
| -------- | --------- | ------------------------------------------------------------ |
| `15 & 9` | `9`       | `1111 & 1001 = 1001`                                         |
| `15 | 9` | `15`      | `1111 | 1001 = 1111`                                         |
| `15 ^ 9` | `6`       | `1111 ^ 1001 = 0110`                                         |
| `~15`    | `-16`     | `~``00000000...``00001111 = ``1111``1111``...``11110000`     |
| `~9`     | `-10`     | `~``00000000``...``0000``1001 = ``1111``1111``...``1111``0110` |

Зауважте, що усі 32 біти інвертуються побітовим оператором НЕ, і що  значення, в яких найстарший (перший зліва) біт дорівнює 1, відображають  від'ємні числа (формат доповняльного коду).

Оператори бітового зсуву приймають два операнди: перший є величиною, в якій треба виконати зсув, а другий вказує кількість бітових позицій для зсуву. Напрямок операції зсуву контролюється застосованим оператором. Оператори зсуву перетворюють свої операнди на 32-бітні цілі числа та  повертають результат того самого типу, до якого належить лівий операнд.

| Оператор                                 | Опис                                                         | Приклад                                                      |
| ---------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Лівий зсув     (`<<`)                    | Цей оператор виконує зсув першого операнду на вказану кількість  бітів ліворуч. Надлишкові біти, зсунуті ліворуч, відкидаються. Біти,  додані справа, заповнюються нулями. | `9<<2` вертає 36, тому що число 1001, зсунуте на 2 біти ліворуч, стає 100100, тобто, 36. |
| Правий зсув з розширенням знаку (`>>`)   | Цей оператор виконує зсув першого операнду на вказану кількість  бітів праворуч. Надлишкові біти, зсунуті праворуч, відкидаються. Біти,  додані зліва, заповнюються значенням старшого біта. | `9>>2` вертає 2, тому що число 1001, зсунуте на 2 біти праворуч, стає 10, тобто 2. Аналогічно, `-9>>2` вертає -3, тому що знак зберігається. |
| Правий зсув із заповненням нулями(`>>>`) | Цей оператор виконує зсув першого операнду на вказану кількість  бітів праворуч. Надлишкові біти, зсунуті праворуч, відкидаються. Біти,  додані зліва, заповнюються нулями. | `19>>>2` вертає 4, тому що число 10011,  зсунуте на 2 бітів праворуч, стає 100, тобто 4. Для невід'ємних чисел,  правий зсув із заповненням нулями та правий зсув з розширенням знаку  дають однаковий результат. |

#### Логічні оператори

[Логічні оператори](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Operators/Logical_Operators) застосовуються до булевих (логічних) значень; в цьому випадку вони повертають значення типу Boolean. Однак, оператори `&&` та `||` насправді повертають значення одного з заданих операндів, тому, якщо ці оператори використовуються зі значеннями не булевого типу, вони повернуть  значення не булевого типу. Логічні оператори описані у наведеній нижче  таблиці.

| Оператор          | Застосування     | Опис                                                         |
| ----------------- | ---------------- | ------------------------------------------------------------ |
| Логічне І (`&&`)  | `expr1 && expr2` | Вертає вираз `expr1`, якщо він може бути перетворений на `false`; інакше, повертає `expr2`. Таким чином, при використанні з булевими значеннями `&&` вертає `true`, якщо обидва операнди дорівнюють true; інакше, вертає `false`. |
| Логічне АБО(`||`) | `expr1 || expr2` | Вертає вираз `expr1`, якщо він може бути перетворений на `true`; інакше, вертає `expr2`. Таким чином, при використанні з булевими значеннями `||` вертає `true`, якщо будь-який з операндів дорівнює true; якщо обидва дорівнюють false, вертає `false`. |
| Логічне НЕ(`!`)   | `!expr`          | Вертає `false`, якщо його єдиний операнд може бути перетворений на `true`; інакше, вертає `true`. |

Прикладами виразів, які можуть бути перетворені на `false`, є ті, які повертають null, 0, NaN, порожній рядок ("") або undefined. Наступний код демонструє приклади оператора `&&` (логічне І).

Оскільки логічні вирази обчислюються зліва направо, вони  перевіряються на можливе "коротке замикання" обчислення за наступними  правилами:

- `false` && *будь-що* обчислюється як false.
- `true` || *будь-що* обчислюється як true.

Правила логіки гарантують, що ці обчислення завжди будуть правильними. Зауважте, що частина виразу *будь-що* не обчислюється, тому будь-які побічні ефекти від цих обчислень не відбудуться.

```js
var a1 =  true && true;     // t && t вертає true
var a2 =  true && false;    // t && f вертає false
var a3 = false && true;     // f && t вертає false
var a4 = false && (3 == 4); // f && f вертає false
var a5 = 'Кіт' && 'Пес';    // t && t вертає Пес
var a6 = false && 'Кіт';    // f && t вертає false
var a7 = 'Кіт' && false;    // t && f вертає false
```

Наступний код демонструє приклади оператора `||` (логічне АБО).

```js
var o1 =  true || true;     // t || t вертає true
var o2 = false || true;     // f || t вертає true
var o3 =  true || false;    // t || f вертає true
var o4 = false || (3 == 4); // f || f вертає false
var o5 = 'Кіт' || 'Пес';    // t || t вертає Кіт
var o6 = false || 'Кіт';    // f || t вертає Кіт
var o7 = 'Кіт' || false;    // t || f вертає Кіт
```

Наступний код демонструє приклади оператора `!` (логічне НЕ).

```js
var n1 = !true;  // !t вертає false
var n2 = !false; // !f вертає true
var n3 = !'Кіт'; // !t вертає false
```

#### Рядкові оператори

На додачу до операторів порівняння, які можуть застосовуватись до  рядкових значень, оператор конкатенації (+) об'єднує значення двох  рядків, повертаючи інший рядок, який є об'єднанням рядків двох  операндів. Наприклад,

```js
console.log('мій ' + 'рядок'); // консоль виводить рядок "мій рядок".
```

Скорочений оператор присвоєння += також може застосовуватись для конкатенації рядків. Наприклад,

```js
var mystring = 'алфа';
mystring += 'віт'; // повертає "алфавіт" та присвоює це значення mystring.
```

#### Умовний (тернарний) оператор

[Умовний оператор](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Operators/Conditional_Operator) - єдиний оператор у JavaScript, який приймає три операнди. У оператора  може бути одне чи два значення, в залежності від умови. Використовує  наступний синтакс:

```javascript
умова ? значення1 : значення2
```

Якщо `умова` дорівнює true, оператор повертає `значення1`. В іншому випадку - `значення2`. Умовний оператор можна використовувати будь-де, де використовується звичайний оператор. Наприклад:

```js
var status = (age >= 18) ? 'дорослий' : 'неповнолітній';
```

Ця інструкція присвоює значення "дорослий" змінній `status`, якщо значення `age` (вік) більше чи дорівнює 18. Інакше, вона присвоює змінній `status` значення "неповнолітній".

#### Оператор кома

[Оператор кома](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Operators/Comma_Operator) (`,`) просто обчислює обидва свої операнди та повертає значення останнього  операнда. Цей оператор найчастіше використовується всередині циклу `for`, що дозволяє оновлювати більше однієї змінної на кожному проході циклу. Наприклад, якщо `a` є двовимірним масивом з 10 елементами  по кожній стороні, наступний код використовує оператор кома, щоб оновити дві змінні одночасно. Код виводить значення діагональних елементів  масиву:

```js
for (var i = 0, j = 9; i <= j; i++, j--)
  console.log('a[' + i + '][' + j + ']= ' + a[i][j]);
```

#### Унарні оператори

Унарна операція - це операція лише з одним операндом.

##### `delete`

Оператор `delete` видаляє об'єкт, властивість об'єкта або елемент за вказаним індексом у масиві. Синтаксис наступний:

```js
delete objectName;
delete objectName.property;
delete objectName[index];
delete property; // працює лише всередині конструкції with
```

де `objectName` є іменем об'єкта, `property` - існуюча властивість, а `index` - ціле число, що вказує розташування елемента у масиві. Четверта форма працює лише всередині блоку `with` для видалення властивості об'єкта. 

Ви можете використовувати оператор `delete` для видалення змінних, оголошених неявно, але не тих, що були оголошені (оператором `var` ,`let` або `const`.

Якщо оператор `delete` відпрацьовує успішно, значенням властивості чи елемента стає `undefined`. Оператор `delete` повертає `true`, якщо операція можлива; він повертає `false`, якщо операція неможлива.

```js
x = 42;
var y = 43;
myobj = new Number();
myobj.h = 4;    // створює властивість h
delete x;       // вертає true (можна видалити властивість, оголошену неявно)
delete y;       // вертає false (не можна видалити властивість, оголошену через var)
delete Math.PI; // вертає false (не можна видаляти попередньо визначені властивості)
delete myobj.h; // вертає true (можна видалити властивість, визначену користувачем)
delete myobj;   // вертає true (можна видалити, якщо властивість оголошена неявно)
```

Коли ви видаляєте елемент масиву, це не впливає на довжину масиву. Для прикладу, якщо ви видалите `a[3]`, `a[4]` досі є `a[4]`, а `a[3]` дорівнює undefined. Коли оператор `delete` видаляє елемент масиву, цей елемент більше не існує у масиві. У наступному прикладі `trees[3]` видаляється оператором `delete`. Однак, адреса `trees[3]` досі доступна та повертає `undefined`.

```js
var trees = ['секвоя', 'лавр', 'кедр', 'дуб', 'клен'];
delete trees[3];
if (3 in trees) {
  // це не виконається
}
```

Якщо вам потрібно, щоб елемент існував, але мав значення undefined, скористайтесь ключовим словом `undefined` замість оператора `delete`. У наступному прикладі `trees[3]` присвоюється значення `undefined`, але елемент масиву досі існує:

```js
var trees = ['секвоя', 'лавр', 'кедр', 'дуб', 'клен'];
trees[3] = undefined;
if (3 in trees) {
  // це виконається
}
```

##### `typeof`

Опис `typeof` наведений [вище](#typeof)

##### `void`

Оператор [`void`](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Operators/void) використовується наступним чином:

```
void (вираз)
void вираз
```

Оператор `void` вказує, що вираз має бути обчислений без повернення значення. `Вираз` є виразом JavaScript, який треба обчислити. Дужки, що оточують вираз, є необов'язковими, але вживати їх є гарним стилем. Наступний код створює гіпертекстове посилання, яке відправляє форму, коли користувач натискає на нього.

```html
<a href="javascript:void(document.form.submit())">
Натисніть сюди, щоб відправити</a>
```

#### Оператори відношення

Оператор відношення порівнює свої операнди та повертає значення `Boolean`, на підставі того, чи є порівняння істиною.

##### `in` (існування властивості або індекс масиву) <a name="in"></a>

Оператор [`in`](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Operators/in) повертає `true`, якщо вказана властивість існує на вказаному об'єкті. Синтаксис наступний:

```js
propNameOrNumber in objectName
```

де `propNameOrNumber` є рядковим або числовим виразом, який відображає ім'я властивості або індекс у масиві, а `objectName` є ім'ям об'єкта. Наступний приклад демонструє варіанти використання оператора `in`.

```js
// --- Масиви
var trees = ['секвоя', 'лавр', 'кедр', 'дуб', 'клен'];
0 in trees;        // вертає true
3 in trees;        // вертає true
6 in trees;        // вертає false
'лавр' in trees;   // вертає false (ви маєте вказати індекс,а не значення за цим індексом)
'length' in trees; // вертає true (length є властивістю масиву)
// --- вбудовані об'єкти
'PI' in Math;          // вертає true
var myString = new String('корал');
'length' in myString;  // вертає true
// --- Користувацькі об'єкти
var mycar = { make: 'Honda', model: 'Accord', year: 1998 };
'make' in mycar;  // вертає true
'model' in mycar; // вертає true
```

##### `instanceof` (належність об'єкту до типу)

Оператор [`instanceof`](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Operators/instanceof) повертає `true`, якщо вказаний об'єкт належить до вказаного типу. Синтаксис наступний:

```js
objectName instanceof objectType
```

де `objectName` є ім'ям об'єкта, який порівнюється з `objectType`, а `objectType` є типом об'єкта, наприклад, [`Date`](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Date) або [`Array`](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array).

Використовуйте `instanceof`, коли вам необхідно  підтвердити тип об'єкта під час виконання. Наприклад, перехоплюючи  винятки, ви можете зробити відгалуження до іншого коду обробки винятків, в залежності від типу викинутого винятку. Наприклад, наступний код використовує `instanceof` для визначення того, чи `theDay` є об'єктом `Date`. Оскільки `theDay` є об'єктом `Date`, інструкції у блоці `if` будуть виконані.

```js
var theDay = new Date(1995, 12, 17);
if (theDay instanceof Date) {
  // інструкції для виконання
}
```

#### Пріоритет операторів

*Пріоритет* операторів визначає порядок, у якому вони  застосовуються під час обчислення виразу. Ви можете змінити пріоритет  оператора, використавши дужки. Наступна таблиця наводить пріоритети операторів, від найвищого до найнижчого.

| Тип оператора                 | Окремі оператори                         |
| ----------------------------- | ---------------------------------------- |
| властивість                   | `. []`                                   |
| виклик / створення екземпляра | `() new`                                 |
| заперечення / інкремент       | `! ~ - + ++ -- typeof void delete`       |
| множення / ділення            | `* / %`                                  |
| додавання / віднімання        | `+ -`                                    |
| бітовий зсув                  | `<< >> >>>`                              |
| відношення                    | `< <= > >= in instanceof`                |
| рівність                      | `== != === !==`                          |
| побітове-і                    | `&`                                      |
| виключне-побітове-або         | `^`                                      |
| побітове-або                  | `|`                                      |
| логічне-і                     | `&&`                                     |
| логічне-або                   | `||`                                     |
| умовний                       | `?:`                                     |
| присвоєння                    | `= += -= *= /= %= <<= >>= >>>= &= ^= |=` |
| кома                          | `,`                                      |

Більш детальну версію цієї таблиці, доповнену посиланнями на додаткові подробиці щодо кожного оператора, можна знайти у [довіднику з JavaScript](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Operators/Operator_Precedence).

### Вирази <a name="expression"></a>

#### `this`

Використовуйте [ключове слово `this`](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Operators/this) для посилання на поточний об'єкт. Загалом, `this` у методі посилається на об'єкт, що його викликав. Використовуйте `this` або з крапкою, або з дужковою нотацією:

```
this['propertyName']
this.propertyName
```

#### Оператор групування

Оператор групування `( )` керує пріоритетом обчислення у виразах. Наприклад, ви можете змінити обчислення спочатку множення та  ділення, а потім додавання та віднімання, щоб обчислити спочатку  додавання.

#### `new`

Ви можете скористатись [оператором `new`](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Operators/new), щоб створити екземпляр визначеного користувачем типу об'єкта або одного з вбудованих типів. Використовуйте `new` наступним чином:

```js
var objectName = new objectType([param1, param2, ..., paramN]);
```

#### super

[Ключове слово super](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Operators/super) використовується для виклику функцій батьківського об'єкта. Воно корисне для використання з [класами](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Classes), для виклику батьківського конструктора, наприклад.

```
super([arguments]); // викликає батьківський конструктор.
super.functionOnParent([arguments]);
```

#### Оператор розпакування (`...`)

[Оператор розпакування](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Operators/Spread_syntax) дозволяє розкласти вираз там, де очікується більше одного аргументу (для  викликів функцій) або більше одного елемента (для масивних літералів).

**Приклад:** Сьогодні, якщо ви маєте масив та бажаєте  створити новий масив, використавши існуючий масив як його частину,  синтаксису масивного літералу більше недостатньо, і вам доводиться  повертатись до імперативного коду, використовуючи комбінацію з `push`, `splice`, `concat`, і т. д. З оператором розпакування все стає набагато лаконічнішим:

```js
var parts = ['плечі', 'коліна'];
var lyrics = ['голова', ...parts, 'та', 'пальці'];
```

## Основні програмні структури

### Блокова інструкція

Об'єднує декілька інструкцій в одну. Блокова інструкція зазвичай використовується поряд з інструкціями для управління потоком виконання (наприклад, `if`, `for`, `while`). Блок обмежується парою фігурних дужок.

```javascript
{
  інструкція_1;
  .
  інструкція_n;
}
```

Починаючи з ECMAScript2015, декларації змінних `let` і `const` мають блокову область видимості. Докладніше на довідкових сторінках [`let`](https://wiki.developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Statements/let) і [`const`](https://wiki.developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Statements/const).

### Умовні інструкції.

##### `if`

```javascript
if (умова) {
  інструкція_1;
} else {
  інструкція_2;
}
```

```javascript
if (умова_1) {
  інструкція_1;
} else if (умова_n) {
  інструкція_n;
} else {
  інструкція_остання;
} 
```

Наступні значення обчислюються до `false` (також знані як [False](https://wiki.developer.mozilla.org/uk/docs/Glossary/Falsy) значення):

- `false`
- `undefined`
- `null`
- `0`
- `NaN`
- порожня стрічка (`""`)

Всі інші значення (включно з усіма об'єктами), при передачі в умовний вираз обчислюються як `true` .

##### `switch`

Конструкція `switch` замінює собою одразу кілька `if`. Вона має один або кілька блоків `case` і необов'язковий блок `default`.

```javascript
switch(x) {
  case 'value1':  // if (x === 'value1')
    ...
    [break]
  case 'value2':  // if (x === 'value2')
    ...
    [break]
  default:		//якщо не знайдено жодного варіанту
    ...
    [break]
}
```

Пример использования `switch` (сработавший код выделен):

```javascript
let a = 2 + 2;
switch (a) {
  case 3:
    console.log( 'Малувато' );
    break;
  case 4:
    console.log( 'В точку!' ); //виведе цей варіант
    break;					  //після чого перестане перебирати	
  case 5:
    console.log( 'Перебор' );
    break;
  default:
    console.log( "Нема таких значень" );
}
```

**Якщо `break` немає, то виконання піде нижче по наступним`case`, при цьому інші умови ігноруються.**

```javascript
let a = 2 + 2;
switch (a) {
  case 3:
    console.log( 'Малувато' ); 
  case 4:
    console.log( 'В точку!' ); 	//виконається, бо a = 4
  case 5:
    console.log( 'Перебор' );	//виконається, бо немає `break`
  default:
    console.log( "Нема таких значень" );//виконається, бо немає `break`
}
```

Можна групувати кілька варіантів. 

```javascript
let a = 3;
switch (a) {
  case 4:
    console.log('Правильно!');
    break;
  case 3: // (*) групуємо оба case
  case 5:
    console.log('Трохи не попали!');
    break;
}
```

### Цикли <a name="loops"></a>

#### `while`

Код з тіла циклу виконується, поки уомва виконується. Наприклад, цикл нижче выводить `i`, поки `i < 3`       

```javascript
let i = 0;
while (i < 3) { // виводить 0, потім 1, потім 2
  console.log( i );
  i++;
}
```

Одне виконання циклу називається ітерацією. Вище наведено 3 ітерації. 

Якщо тіло циклу має тільки одну інструкцію, оператори блоку `{…}` можна не писати                     

```javascript
let i = 3;
while (i) console.log(i--);
```

Синтаксис **`do..while`** дає можливість виконати тіло циклу принаймні один раз.

```javascript
do {
  // тіло циклу
} while (condition);
```

#### `for`

```javascript
for (начало; условие; шаг) {
  // ... тіло циклу ...
}
```

Цикл нижче выконує `console.log(i)` для `i` від `0` до (але не включаючи) `3`:  

```javascript
for (let i = 0; i < 3; i++) { // выведе 0, потім 1, потім 2
  console.log(i);
}
```

| часть     |                  |                                                              |
| --------- | ---------------- | ------------------------------------------------------------ |
| *початок* | `i = 0`          | Виконується один раз при вході в цикл                        |
| *умова*   | `i < 3`          | Перевіряється *перед* кожною ітерацією циклу. Якщо воно буде `false` - цикл зупиниться. |
| *крок*    | `i++`            | Виконується *після* тіла циклу на кажній ітерації *перед* перевіркою умови. |
| *тіло*    | `console.log(i)` | Виконується знову і знову, поки умова виконується  `true`.   |

Можна використовувати існуючу змінну. Будь яка частина `for` може бути пропущена.                       

#### `break` (вихід з циклу)

Можна вийти з циклу у будь який момент за допомогою директиви `break`. Наприклад:

```javascript
let sum = 0;
while (true) {
  let value = +prompt("Ведіть число", '');
  if (!value) break; // (*)
  sum += value;
}
alert( 'Сумма: ' + sum );
```

#### `continue` (перехід до наступної ітерації)

```javascript
 for (let i = 0; i < 10; i++) {
  // якщо парне, пропустити іншу частину тіла циклу
  if (i % 2 == 0) continue;
  console.log(i); // 1, потім 3, 5, 7, 9
}
```

#### `for..of`(перебір елементів)   

[`For..of`](https://wiki.developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Statements/for...of) Перебирає елементи в ітерабельних (перелічувальних) змінних .  

```javascript
let fruits = ["Яблуко", "Апельсин", "Слива"];
for (let fruit of fruits) {
  console.log (fruit);
}
let iterable = 'ой';
for (let value of iterable) {
  console.log(value);
}

```

#### `for..in`(перебір властивостей)<a name="forin"></a>

Цикл `for...in` перебирає лише перелічувані, не символьні властивості. Об'єкти, створені вбудованими конструкторами

```js
var obj = {a: 1, b: 2, c: 3};   
for (const prop in obj) {
  console.log(`obj.${prop} = ${obj[prop]}`);
}
// Виведе:
// "obj.a = 1"
// "obj.b = 2"
// "obj.c = 3"
```

## Функції <a name="functions"></a>

Окрім вбудованих системних функцій є також можливість писати власні.

### Оголошення функції

**Оголошення функції** (функціональний оператор) означує функцію з вказаними параметрами.

```js
function name([param[, param,[..., param]]]) {
   [statements]
}
```

- `name` - Ім'я функції.
- `param`- Ім'я аргументу, що передається у функцію. Максимальна кількість аргументів відрізняється у різних рушіях.
- `statements`- Інструкції, які складають тіло функції.

### Виклик функції з передачою параметрів

Функції повинні бути в області видимості під час виклику, але оголошення функції може  бути записаним нижче виклику, як у цьому прикладі:

```js
console.log (sum(2)); 	//значення параметра b не задається, результат виведе 5
function sum(a, b=3) {	//b з передачою значення за замовченням
  return (a+b);
}
```
У функцію можуть передаватися параметри за замовченням, як показано вище в прикладі для змінної b. Примітивні параметри (такі, як число) передаються функціям **за** **значенням**; значення передається до функції, але якщо функція змінює значення параметра, **ця зміна не відображається глобально або у функції виклику.**

Якщо ви передаєте об'єкт (тобто, непримітивне значення, наприклад, [`Array`](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Array) або визначений користувачем об'єкт) у якості параметра, і функція змінює властивості об'єкта, ця зміна видима за межами функції, як показано на наступному прикладі:

```js
function myFunc(theObject) {
  theObject.make = 'Toyota';
}
let mycar = {make: 'Honda', model: 'Accord', year: 1998};
let x, y;
x = mycar.make; // x отримує значення "Honda"
myFunc(mycar);
y = mycar.make; // y отримує значення "Toyota"
                // (властивість make була змінена функцією)
```

Після виклику `return`  функція завершує своє виконання. Якщо в `return`  нічого не передається, результатом виклику буде тип `undefined`.

### Функціональні вирази

Функції також можуть бути створені за допомогою функціональних виразів. Така функція може бути **анонімною**; їй не обов'язково мати ім'я. Наприклад, `square` можна визначити як:

```js
let square = function(number) { return number * number; };
let x = square(4); // x gets the value 16
```

Проте, ім'я  може бути надане у функціональному виразі, і може бути  використане всередині функції, щоб звернутися до самої себе, або в  налагоджувач, щоб визначити функцію в трасуванні стеку:

```js
var factorial = function fac(n) { return n < 2 ? 1 : n * fac(n - 1); };
console.log(factorial(3));
```

Підняття функції (використання раніше об'явлення) працює тільки для оголошення функції, а не для функціонального виразу.

Функціональні вирази зручні при передачі функції як аргументу до іншої функції. Наступний приклад показує функцію map, яка повинна отримати функцію як перший аргумент, а масив як другий аргумент.

```jsx
function map(f, a) {
  let result = [], // Створення нового масиву
      i;
  for (i = 0; i != a.length; i++)
    result[i] = f(a[i]);
  return result;
}
```

У наступному коді наша функція приймає функцію, означену функціональним виразом,  та виконує її для кожного елемента масиву, отриманого в якості другого  аргументу.

```js
function map(f, a) {
  let result = []; // Створення нового масиву
  let i; //  Оголошення змінної
  for (i = 0; i != a.length; i++)
    result[i] = f(a[i]);
      return result;
}
let f = function(x) {
   return x * x * x; 
}
let numbers = [0,1, 2, 5,10];
var cube = map(f,numbers);
console.log(cube);//повертає: [0, 1, 8, 125, 1000].
```

У JavaScript функція може бути визначена на основі умови. Наприклад, наступне визначення функції означує `myFunc` тільки якщо `num` дорівнює 0:

```js
let myFunc;
if (num === 0) {
  myFunc = function(theObject) {
    theObject.make = 'Toyota';
  }
}
```

На додаток до означення функцій, як описано тут, ви також можете використовувати конструктор [`Function`](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Function) для створення функцій з текстового рядка під час виконання, як і [`eval()`](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/eval).

**Метод** - це функція, яка є властивістю об'єкта. Докладніше про об'єкти та методи у  [Working with objects](https://developer.mozilla.org/uk/docs/Web/JavaScript/Guide/Working_with_Objects).

### Область видимості функції

Змінні, означені всередині функції, недоступні ззовні цієї функції. Проте,  функція може звертатись до усіх змінних та функцій, означених у області видимості, де вона оголошена. Іншими словами, функція, оголошена у  глобальній області видимості, може звертатись до усіх змінних,  оголошених у глобальній області видимості. Функція, оголошена всередині  іншої функції, має доступ до усіх змінних, оголошених у батьківській  функції, а також до будь-якої змінної, до якої має доступ батьківська  функція.

```js
// Ці змінні визначені у глобальній області видимості
let num1 = 20, num2 = 3, name = 'Chamahk';
// Ця функція означена у глобальній області видимості
function multiply() {
  return num1 * num2;
}
console.log (multiply()); // Повертає 60

// Приклад вкладеної функції
function getScore() {
  let num1 = 2, num2 = 3;
  function add() {
    // використовуються змінні об'явлені в функції getScore   
    return name + ' scored ' + (num1 + num2);
  }
  return add();
}
console.log (getScore()); // Повертає "Chamahk scored 5"
```

### Функції зворотного виклику

Рассмотрим ещё примеры функциональных выражений и передачи функции как значения.

Давайте напишем функцию `ask(question, yes, no)` с тремя параметрами:

- `question`

  Текст вопроса

- `yes`

  Функция, которая будет вызываться, если ответ будет «Yes»

- `no`

  Функция, которая будет вызываться, если ответ будет «No»

Наша функция должна задать вопрос `question` и, в зависимости от того, как ответит пользователь, вызвать `yes()` или `no()`:               

```javascript
function ask(question, yes, no) {
  if (confirm(question)) yes()
  else no();
}

function showOk() {
  alert( "Вы согласны." );
}

function showCancel() {
  alert( "Вы отменили выполнение." );
}

// использование: функции showOk, showCancel передаются в качестве аргументов ask
ask("Вы согласны?", showOk, showCancel);
```

На практике подобные функции очень полезны. Основное отличие «реальной» функции `ask` от примера выше будет в том, что она использует более сложные способы взаимодействия с пользователем, чем простой вызов `confirm`. В браузерах такие функции обычно отображают красивые диалоговые окна. Но это уже другая история.

**Аргументы функции `ask` ещё называют \*функциями-колбэками\* или просто \*колбэками\*.**

Ключевая идея в том, что мы передаём функцию и ожидаем, что она  вызовется обратно (от англ. «call back» – обратный вызов) когда-нибудь  позже, если это будет необходимо. В нашем случае, `showOk` становится *колбэком*’ для ответа «yes», а `showCancel` – для ответа «no».

Мы можем переписать этот пример значительно короче, используя Function Expression:                  

```javascript
function ask(question, yes, no) {
  if (confirm(question)) yes()
  else no();
}

ask(
  "Вы согласны?",
  function() { alert("Вы согласились."); },
  function() { alert("Вы отменили выполнение."); }
);
```

Здесь функции объявляются прямо внутри вызова `ask(...)`. У них нет имён, поэтому они называются *анонимными*. Такие функции недоступны снаружи `ask` (потому что они не присвоены переменным), но это как раз то, что нам нужно.

Подобный код, появившийся в нашем скрипте выглядит очень естественно, в духе JavaScript.

> Функция – это значение, представляющее «действие»
>
> Обычные значения, такие как строки или числа представляют собой *данные*.
>
> Функции, с другой стороны, можно воспринимать как «действия».
>
> Мы можем передавать их из переменной в переменную и запускать, когда захотим.

### Функції як об'єкти

Функція, утворена через оголошення функції, є об'єктом `Function`, і має усі властивості, методи та поведінку об'єктів `Function`. Більш детальну інформацію щодо функцій дивіться у статті [`Function`](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Global_Objects/Function).

Функція також може бути створена через за допомогою виразу (дивіться [`функціональний вираз`](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Operators/function)).

За замовчуванням функції повертають `undefined`. Щоб повернути будь-яке інше значення, функція повинна мати оператор [`return`](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Statements/return), який вказує значення, що буде повернене.



## Обробка помилок

