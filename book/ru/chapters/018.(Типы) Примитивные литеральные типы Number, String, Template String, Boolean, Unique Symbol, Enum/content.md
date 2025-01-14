# Примитивные литеральные типы Number, String, Template String, Boolean, Unique Symbol, Enum

Помимо обычных примитивных типов перешедших их _JavaScript_, в _TypeScript_ существуют так называемые _литеральные типы_, которые, как можно понять из названия, представляют литералы обычных примитивных типов. Число `5`, строка `“apple”`, логическое значение `true` или константа перечисления `Fruits.Apple` может выступать в качестве самостоятельно типа. Не сложно догадаться, что в качестве значений в таком случае могут выступать только литеральные эквиваленты самих типов, а также `null` и `undefined` (при `--strictNullChecks` со значением `false`).

Литеральные типы были созданы для того, что бы на этапе компиляции выявлять ошибки, возникающие из-за несоответствия значений заранее объявленных констант, как, например, номер порта или идентификатор динамического типа. Ранее такие ошибки можно было выявить только на этапе выполнения.


## Литеральный тип Number (Numeric Literal Types)

Литеральный тип `number` должен состоять из литеральных значений, входящих в допустимый диапазон чисел от `Number.MIN_VALUE` (-9007199254740992) до `Number.MAX_VALUE` (9007199254740992), и может записываться в любой системе счисления (двоичной, восьмеричной, десятичной, шестнадцатеричной).

Очень часто в программе фигурируют константные значения, ограничить которые одним типом недостаточно. Здесь на помощь и приходят литеральные типы данных. Сервер, конфигурацией которого разрешено запускаться на `80` или `42` порту, мог бы иметь метод, вызываемый с аргументами, включающими номер порта. Поскольку значение принадлежало бы к типу `number`, то единственный способ его проверки был возможен при помощи условия расположенном в блоке `if`, с последующим выбрасыванием исключения. Но подобное решение выявило бы несоответствие только на этапе выполнения. Помощь статической типизации в данном случае выражалась лишь в ограничении по типу `number`.

`````ts
const port80: number = 80;
const port42: number = 42;

// параметры ограничены лишь типом данных
function start(port: number): void {
    // блок if сообщит об ошибке только во время выполнения
    if (port !== port80 || port !== port42) {
        throw new Error(`port #${port} is not valid.`);
    }
}

start(81); // вызов с неправильным значением
`````

Именно для таких случаев и были введены литеральные типы данных. Благодаря литеральному типу `number` стало возможно выявлять ошибки не дожидаясь выполнения программы. В данном случае значение допустимых портов можно указать в качестве типа параметров функции.

`````ts
const port80: number = 80;
const port42: number = 42;

function start(port: 80 | 42): void {
    // блок if сообщит об ошибке только во время выполнения
    if (port !== port80 || port !== port42) {
        throw new Error(`port #${port} is not valid.`);
    }
}

start(81); // ошибка выявлена на этапе компиляции!
`````

Для повышения семантики кода литеральные типы, представляющие номера порта, можно сокрыть за псевдонимом типа.

`````ts
type ValidPortValue = 80 | 42;

const port80: number = 80;
const port42: number = 42;

function start(port: ValidPortValue): void {
    // блок if сообщит об ошибке только во время выполнения
    if (port !== port80 || port !== port42) {
        throw new Error(`port #${port} is not valid.`);
    }
}

start(81); // ошибка выявлена на этапе компиляции!
`````

Как уже было сказано ранее, литеральный тип `number` можно указывать в любой системе счисления.

`````ts
type NumberLiteralType = 0b101 | 0o5 | 5 | 0x5;
`````

Примитивный литеральный тип `number` является уникальным для _TypeScript_, в _JavaScript_ подобного типа не существует.


## Литеральный тип String (String Literal Types)

Литеральный тип `string` может быть указан только строковыми литералами, заключенными в одинарные (`' '`) или двойные (`" "`) кавычки. Так называемые шаблонные строки, заключенные в обратные кавычки (`` ` ` ``), не могут быть использованы в качестве строкового литерального типа.

В ходе разработки, конвенциями проекта могут быть наложены ограничения на типы используемой анимации. Чтобы не допустить ошибочных идентификационных значений, их тип можно ограничить литеральным строковым типом.

`````ts
function animate(name: "ease-in" | "ease-out"): void {

}

animate('ease-in'); // Ok
animate('ease-in-out'); // Error
`````

Примитивный литеральный тип `string` является уникальным для _TypeScript_, в _JavaScript_ подобного типа не существует.

## Шаблонный литеральный тип String (Template String Literal Types)

_Шаблонный литеральный строковый тип_ — это тип, позволяющий на основе литеральных строковых типах динамически определять новый литеральный строковый тип. Простыми словами, это известный по _JavaScript_ механизм создания шаблонных строк только для типов.

`````ts
type Type = "Type";
type Script = "Script";

/**
 * type Message = "I ❤️ TypeScript"
 */
type Message = `I ❤️ ${Type}${Script}`;
`````

Но вся мощь данного типа раскрывается в момент определение нового типа на основе объединения (`union`). В подобных случаях новый тип будет также представлять объединение, элементы которого представляют все возможные варианты, полученные на основе исходного объединения. 

`````ts
type Sides = "top" | "right" | "bottom" | "left";

/**
 * type PaddingSides = "padding-top" | "padding-right" | "padding-bottom" | "padding-left"
 */
type PaddingSides = `padding-${Sides}`;
`````

Аналогичное поведение будет справедливо и для нескольких типов объединения.

`````ts
type AxisX = "top" | "bottom";
type AxisY = "left" | "right";


/**
 * type Sides = "top-left" | "top-right" | "bottom-left" | "bottom-right"
 */
type Sides = `${AxisX}-${AxisY}`;

/**
 * type BorderRadius = "border-top-left-radius" | "border-top-right-radius" | "border-bottom-left-radius" | "border-bottom-right-radius"
 */
type BorderRadius = `border-${Sides}-radius`;
`````

Поскольку с высокой долей вероятности в подобных операциях потребуется трансформация регистра строк, создателями данного механизма также были добавлены новые утилитарные алиасы типов - `Uppercase`, `Lowercase`, `Capitalize` и `Uncapitalize`.

`````ts
type A = `${Uppercase<"AbCd">}`; // type A = "ABCD"
type B = `${Lowercase<"AbCd">}`; // type B = "abcd"
type C = `${Capitalize<"abcd">}`; // type C = "Abcd"
type D = `${Uncapitalize<"Abcd">}`; // type D = "abcd"
`````

## Литеральный Тип Boolean (Boolean Literal Types)

Литеральный тип `boolean` ограничен всего двумя литеральными значениями `true` и `false`.

Так как литеральный тип `boolean` состоит всего из двух литеральных значений `true` и `false`, то детально разбирать, собственно, и нечего. Зато это прекрасный повод, что бы ещё раз повторить определение. Каждый раз, когда встречается часть кода, работа которой зависит от заранее определенного значения-константы, стоит подумать, можно ли ограничивать тип литеральным типом, сможет ли это повысить типобезопасность и семантику кода.

`````ts
function setFlag(flag: true | "true"): void {

}
`````

Примитивный литеральный тип `boolean` является уникальным для _TypeScript_, в _JavaScript_ подобного типа не существует.


## Литеральный Тип Unique Symbol (unique symbol) уникальный символьный тип

Несмотря на то, что тип данных `symbol` является уникальным для программы, с точки зрения системы типов, он не может гарантировать типобезопасность.

`````ts
function f(key: symbol) {
  // для успешного выполнения программы предполагается, что параметр key будет принадлежать к типу Symbol.for('key')...
}

f(Symbol.for('bad key')); // ... тем не менее функцию f() можно вызвать с любым другим символом
`````

Для того, что бы избежать подобного сценария, _TypeScript_ добавил новый примитивный литеральный тип `unique symbol`. `unique symbol` является подтипом `symbol` и указывается в аннотации с помощью литерального представления `unique symbol`.

Экземпляр `unique symbol` создается теми же способами, что и обычный `symbol` при помощи прямого вызова конструктора `Symbol()` или статического метода `Symbol.for()`. Но, в отличие от обычного `symbol`, `unique symbol` может быть указан только в аннотации константы (`const`) и поля класса (`static`) объявленного с модификатором `readonly`.

`````ts
const v0: unique symbol = Symbol.for('key'); // Ok
let v1: unique symbol = Symbol.for('key'); // Error
var v2: unique symbol = Symbol.for('key'); // Error

class Identifier {
    public static readonly f0: unique symbol = Symbol.for('key'); // Ok
    
    public static f1: unique symbol = Symbol.for('key'); // Error
    public f2: unique symbol = Symbol.for('key'); // Error
}
`````

Кроме того, что бы ограничить значение до значения принадлежащего к типу `unique symbol`, требуется прибегать к механизму запроса типа, который подробно был рассмотрен  в главе [“Типы - Type Queries (запросы типа), Alias (псевдонимы типа)”](../017.(Типы)%20Type%20Queries%20(запросы%20типа),%20Alias%20(псевдонимы%20типа)).

`````ts
const KEY: unique symbol = Symbol.for('key');

// аннотация параметра и возвращаемого из функции типа при помощи механизма запросов типа
function f(key: typeof KEY): typeof KEY {
    return key;
}

f(KEY); // Ok
f(Symbol('key')); // Error
f(Symbol.for('key')); // Error
`````

Поскольку каждый `unique symbol` имеет собственное представление в системе типов, совместимыми могут считаться только символы, имеющие идентичную ссылку на объявление.

`````ts
const KEY: unique symbol = Symbol.for('key');
const OTHER_KEY: unique symbol = Symbol.for('key');

if (KEY === OTHER_KEY) { // Ошибка, unique symbol не равно unique symbol

}

function f(key: typeof KEY): typeof KEY {
    return key;
}

let key = KEY; // let key: symbol; // symbol !== unique symbol

f(key); // Error
`````

Тип `unique symbol` предназначен для аннотирования уникальных символьных литералов. С его помощью реализуется задуманное для _JavaScript_ поведение в типизированной среде _TypeScript_.


## Литеральный тип Enum (Enum Literal Types)

Литеральный тип `enum` ограничивается литеральными значениями его констант. Это утверждение верно с одной оговоркой: правило совместимости типов для перечисления, у которого имеются константы с числовым значением, распространяется и на литеральный тип `enum`.

Напомним, если перечисление составляют только строковые константы, то в качестве значения может быть присвоено только константы перечисления.

`````ts
enum Berries {
    Strawberry = "strawberry",
    Raspberry = "raspberry",
    Blueberry = "blueberry"
}

type RedBerry = Berries.Raspberry | Berries.Strawberry;

var berry: RedBerry = Berries.Strawberry; // Ok
var berry: RedBerry = Berries.Raspberry; // Ok
var berry: RedBerry = Berries.Blueberry; // Error
var berry: RedBerry = 123; // Error
var berry: RedBerry = "strawberry"; // Error
`````

В том же случае, если в перечислении присутствует константа с числовым значением, в качестве значения может быть присвоено любое число.

`````ts
enum Fruits {
    Apple,
    Pear,
    Banana = "banana"
}

type FruitGrowOnTree = Fruits.Apple | Fruits.Pear;

var fruit: FruitGrowOnTree = Fruits.Apple; // Ok
var fruit: FruitGrowOnTree = Fruits.Pear; // Ok
var fruit: FruitGrowOnTree = Fruits.Banana; // Error
var fruit: FruitGrowOnTree = 123; // Ok!
var fruit: FruitGrowOnTree = "apple"; // Error
`````

Правила литеральных типов `enum` распространяются и на перечисления объявленных с помощью ключевого слова `const`.

Примитивный литеральный тип `enum` является уникальным для _TypeScript_, в _JavaScript_ подобного типа не существует.

