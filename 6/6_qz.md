## Принципы построения приложений. "Чистая архитектура".
### DCI BCE Гексагональная архитектура

Data Context Interaction(DCI)	подход в создании систем. Отделяет контект использования(опер. деят-ность, текучка) от модели домена(данные, ядро основной деятельности, миссия), вместо того чтобы объединять их в одном интерфейсе класса.

DСI на уровне объектов	предполагает объекты на уровне ментальных моделей, а не абстрактный объектно-ориентированый подход на основе классов, помогает разработчикам рассуждать на уровне состояния и поведения всей системы, а не только состоянии и поведении объектов.

Особенность DCI по срезам 	один сценарий( срез) - один файл.



Сущности Boundary-Control-Entity(BCE)	Actor( внешний вызов),Boundary - пограничный класс, Control - класс бизнес-логики,  Entity - долгосрочный класс, как правило часть домена -ядра бизнеса.

Boundary-Control-Entity(BCE)	Модель структуры классов, командующая луковичное взаимодействие интерфейсов. Внешний элемент(actor) может взаимодействовать(<=>) c actor,boundary.  Boundary <=>boundary,actor, control; сontrol <=> control, boundary, entity; entity <=> entity, control.

Что из себя представляет отдельный boundary	Use-case, полный этаж вертикального среза

Миссия BCE 	разделение задач и жесткий контроль зон ответсвенности.

Уточнение Boundary	интерфейс к внешнему миру. Содержит конфигурацию и и установление внешних соединений.

Уточнение Control	Логика не входящая в boundary; алгоритмы и sql-запросы.

Уточнение Entity	структуры данных, которым разрешено базовое поведение.

Hexagonal Architecture 	архитектура портов и адаптеров. Шестиугольник - абстрактен, указывает что приложение многогранно. Каждая грань - порт, интерфейс для определённой цели. Акторы подключаются через реализации портов - адаптеры.
Каждая грань - срез? 

Абстракция окружения и ядра Гексагональной структуры 	Среда(окружение) в которую направлены адаптеры может быть как внешней, для акторов, так и внутренней, для взаимодействия с структурой данных. Внутренняя часть- условные фреймворки,  операционная логика приложения, и домен - ядро бизнеса.

## ## Принципы построения приложений. "Чистая архитектура".
### Чистая архитектура

Чистая архитектура 	способ разделения ответственностей и частей функционала, по степени их близости к предметной области(домену) приложения

Первое правило проектирования	не зависеть ни от чего что может часто меняться

Политика системы 	все бизнес-правила и процедуры, основная ценность системы.

Детали системы 	детали реализации, по определению изменяемые.устройства ввода-вывода, базы данных, веб-системы, серверы, фреймворки, протоколы обмена данных и пр.

Принципы чистоты архитектуры 	..независимость от фреймворков
..независимость от базы данных
..независимость от интерфейса пользователя
..независимость от любых внешних агентов
..простота тестирования

Независимость от фреймворков 	фреймворки - детали системы, Архитектура не должна зависеть ни от какого из них.

Независимость от базы данных 	Схема, база данных, язык запросов - детали системы, и не достаточно масштабны чтобы стать именованным элементом архитектуры. Абстракция БД, же - поддерживает любую реализацию.

Независимость от пользовательского интерфейса 	интерфейс пользователя может меняться как в своих деталях, так и по своему типу( консольный, десктопный, веб-интерфейс). Так, архитектор регламентирует лишь контракт между логикой и интерфейсом пользователя, создавая свободу реализации UI

Независимость от любых внешних агентов	мы не можем и не должны знать что происходит снаружи; задача бизнес-логики - внутреннее поведение.

Простота тестирования 	тесты - независимая, внешняя часть любого компонента и архитектуры в общем. Ничто в системе не зависит от тестов, но тесты прямо зависят от реализаций. Тесты связанные с системой, изменятся вместе с системой; 

Слои чистой архитектуры и критерий объединения	отсортировано по вероятности изменений
..внешние зависимости
..адаптеры интерфейсов
..прикладные бизнес-правила
..сущность домена

Правило зависимостей чистой архитектуры 	зависимости в исходном коде должны быть направлены внутрь, в сторону политик, и от деталей. Ничто во внутреннем круге не знает о внешних кругах, взаимодействуют интерфейсы. Внешние круги не должны влиять на внутренние( иначе чем передачей регламентированного возврата)

Принципы чистой архитектуры 	..приложение строится вокруг независимых от других слоёв объектной модели
..внутреннии слои определяют интерфейсы, внешние - содержат реализации интерфейсов
.. направление зависимостей - от внешних к внутренним
.. при пересечении границ слоя данные должны преобразовываться

Сушность	объект, воплощающий небольшой набор критических бизнес-правил, оперирующий критическими бизнес-данными. Либо содержит к.б.д, либо имеет простой доступ к ним. Программное выражение идеи, имеющей решающее значение для бизнеса.

Варианты использования	Отображают только конкретные правила работы приложения, порядок взаимодействия между пользователями и сущностями. Содержит интерфейс входных данных, интерфейс выходных данных, регламент действий, ссылки на сущности с которыми взаимодействуют.

Отображение вариантов использования на uml	овалы сплошные - варианты уникальные для акторов; овалы пунктирные - варианты совпадающие для двух и более акторов.

Адаптеры интерфейсов	преобразуют удобный для варианта использования вариант в удобрый для внешнего агента.

Фреймворки и драйверы	детали реализации, которые дополняют или реализуют уже готовые сущности и юз-кейсы.

Пересечение границ между кругами архитектуры	при вызовах внутренний круг пользуется только интерфейсов, без хардовых ссылок на внешний круг, а внешний круг так же реализует этот интерфейс. При передаче данных через границу, они форматируются в формат более удобный для внутреннего круга.

Принцип построения ядра приложения для ч.а.	включает сущности, службы, и интерфейсы.

SMTP 	simple mail transfer protocol; простой протокол пересылки писем; односторонний, от отправителя - получателю.

Роль инфраструктуры	приложения для ч.а.	 включает реализацию доступа к данным и реализацию служб с инфраструктурными задачами, типа логгера или SMTP- уведомителя.