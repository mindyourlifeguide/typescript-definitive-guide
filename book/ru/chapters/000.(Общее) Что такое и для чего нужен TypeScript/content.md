# Что такое и для чего нужен TypeScript
Поскольку постижение всего нового занимает много драгоценного времени и сил, то человек прежде чем сделать выбор должен взвесить все "за" и "против". Чем больше у него сопряженного опыта тем легче будет принять решение. Это означает, что недавно присоединившимся к _JavaScript_ сообществу будет наиболее полезно начать свое погружение в _TypeScript_ с подтверждения правильности своего выбора. Кроме того, данная глава сможет ответить на многие вопросы опытных разработчиков которые обдумывают использование данного языка при создании очередного проекта. Поэтому обойдемся без затягивания и начнем по порядку разбирать самые часто возникающие вопросы связанные с _TypeScript_.

## Что такое TypeScript

_TypeScript_ — это язык программирования со статической типизацией, позиционирующий себя как язык расширяющий возможности _JavaScript_.
  
_Typescript_ код компилируется в _JavaScript_ код, который можно запускать как на клиентской стороне (браузер), так и на стороне сервера (_nodejs_). Качество сгенерированного кода сопоставимо с кодом, написанным профессиональным разработчиком с большим стажем. Мультиплатформенный компилятор _TypeScript_ отличается высокой скоростью компиляции и распространяется по лицензии _Apache_, а в его создании принимают участие разработчики со всего мира, что привело к традиции выпускать новую версию каждые два месяца. Несмотря на такую периодичность версии долгое время сохраняют совместимость, а по истечению долгого времени устаревшее поведение остается доступным при активизации специальных флагов компилятора. Поэтому не стоит опасаться, что проект будет лишен новых возможностей языка из-за версионных различий _TypeScript_. Ну а большое количество разработчиков компилятора означает, что с каждой новой версией компилятор получает обновления касающиеся всех направлений, будь, то синтаксические конструкции или оптимизации скорости компиляции и сборки проекта.


## История TypeScript

Разработчиком языка _TypeScript_ является _Андерс Хейлсберг_, также известный как создатель языков _Turbo Pascal_, _Delphi_ и _C#_. С момента своего анонсирования компанией _MicroSoft*_ в 2012 году, _TypeScript_ не перестает развиваться и склоняет все больше профессиональных разработчиков писать свои программы на нем. На текущий момент трудно представить крупную компанию не использующую его в своих проектах. Поэтому знание _TypeScript_ будет весомым критерием при устройстве на работу своей мечты.


## Для чего нужен TypeScript

Поскольку сложность современных вэб приложений сопоставима с настольными, то прежде всего _TypeScript_ предназначен для выявления ошибок на этапе компиляции, а не на этапе выполнения. Кроме того, за счет системы типов разработчики получают такие возможности, как подсказки и переходы по коду, которые значительно ускоряют процесс разработки. Помимо этого, система типов в значительной степени избавляет разработчиков от комментирования кода, которое отнимает значительное время. Также система типов помогает раньше выявлять проблемы архитектуры, исправление которых обходятся дешевле на ранних этапах.

Хотя на текущий момент практически невозможно найти библиотеку, которая бы не была портирована на _TypeScript_. _JavaScript_ код, оставшийся от предыдущих проектов, не стоит списывать со счетов, поскольку его совместное использование не вызовет никакой проблемы. Компилятор _TypeScript_ отлично справляется с динамическим _JavaScript_ кодом, включенным в свою типизированную среду, и даже выявляет в нем ошибки. Кроме того, при компиляции _.ts_ файлов в _.js_ дополнительно генерируются файлы декларации _.d.ts_, с помощью которых разработчики создающие свои программы исключительно на _JavaScript_ получат все прелести типизированного автодополнения в любой современной среде разработки.


## Зачем разработчику TypeScript

_TypeScript_ значительно сокращает время на устранение ошибок и выявление багов, которые порой не так просто отыскать в динамической среде _JavaScript_.

В случае, если для разработчика _TypeScript_ является первым типизированным языком, следует знать, что его изучение значительно ускорит процесс профессионального роста поскольку типизированный мир открывает аспекты программирования неочевидные в динамических языках.

Помимо этого, _TypeScript_ позволяет писать более понятный и читаемый код максимально описывающий предметную область, за счет чего архитектура приложения становится более выраженной, а разработка неявно увеличивает профессиональный уровень программиста.

Всё это, в своей совокупности, сокращает время разработки программы, снижая её стоимость и предоставляя разработчикам возможность поскорее приступить к реализации нового и ещё более интересного проекта.
