Что такое Дек (Deque)?
Дек (Deque, двусторонняя очередь) — это абстрактный тип данных, представляющий собой обобщение очереди. В отличие от обычной очереди (FIFO — «первым пришёл — первым ушёл») и стека (LIFO — «последним пришёл — первым ушёл»), дек позволяет добавлять и удалять элементы с обоих концов: с начала (front) и с конца (back). Это делает дек более гибкой структурой данных, подходящей для различных задач.

Иллюстрация Deque
Основные характеристики Дека (Deque, Double-Ended Queue):
Двусторонность (Double-Ended): это ключевая характеристика. Дек позволяет добавлять и удалять элементы с обоих концов — с начала (front) и с конца (back). Это отличает его от очереди (добавление только в конец и удаление из начала) и стека (добавление и удаление только с одного конца).
Упорядоченность (Ordered): элементы в деке хранятся в определенном порядке, в котором они были добавлены. Это означает, что существует четко определенная последовательность элементов от начала до конца.
Динамический размер (Dynamic Size): дек может динамически увеличивать или уменьшать свой размер по мере добавления или удаления элементов. В отличие от массивов фиксированного размера, дек не имеет жёсткого ограничения на количество элементов, которые он может хранить (хотя реализация может иметь максимальный предел, определяемый доступной памятью).
Различные реализации (Multiple Implementations): Декартово произведение — это абстрактный тип данных, а не конкретная реализация. Он может быть реализован с использованием различных базовых структур данных, таких как двусвязный список, динамический массив (с хитрой логикой управления памятью), массив блоков. Выбор реализации влияет на производительность различных операций.
Доступ к элементам (Element Access): хотя дек оптимизирован для добавления и удаления элементов с обоих концов, он также может предоставлять доступ к элементам по индексу (аналогично массиву или std::vector). Однако такой доступ может быть медленнее, чем в std::vector, особенно если дек реализован как связный список.
Непрерывность памяти (Memory Continuity): в отличие от std::vector, элементы дека не обязательно хранятся в непрерывном блоке памяти. Это связано с тем, что дек обычно реализуется как массив блоков, что позволяет ему эффективно расширяться и сжиматься. std::vector гарантирует непрерывность памяти.


Где используется Deque?
Двусторонние очереди (деки) используются во многих ситуациях, когда требуется добавлять и удалять элементы с обоих концов последовательности. Вот несколько распространённых примеров:

1. Реализация других структур данных:

Стек (Stack): дек может быть использован для реализации стека. Операции push_back и pop_back дека соответствуют операциям push и pop стека.
Очередь (Queue): Дек также может быть использован для реализации очереди. Операции push_back и pop_front дека соответствуют операциям enqueue и dequeue очереди.
2. Алгоритмы:

Задача о максимальном/минимальном элементе в скользящем окне (Sliding Window Maximum/Minimum): дек может быть эффективно использован для поиска максимального или минимального элемента в каждом подмассиве фиксированной длины (скользящем окне) данного массива. Дек хранит индексы элементов, которые являются кандидатами на максимум/минимум в текущем окне.
Реализация алгоритма A поиска пути (A Pathfinding):** В некоторых реализациях A* дек может использоваться для хранения узлов, которые необходимо посетить, в порядке их оценочной стоимости (часто с небольшими оптимизациями для повышения производительности). Хотя чаще используется priority_queue, дек может быть полезен для специализированных эвристик.
Задача проверки, является ли строка палиндромом (Palindrome Check): дек можно использовать для эффективной проверки, является ли строка палиндромом (читается одинаково в обоих направлениях). Символы строки добавляются в дек, а затем сравниваются символы в начале и в конце дека до тех пор, пока дек не станет пустым или не будет обнаружено несоответствие.
Обработка отложенных задач: в некоторых алгоритмах (например, в алгоритмах обхода деревьев или графов) необходимо откладывать обработку определенных узлов или задач. Дек может служить для хранения этих отложенных задач и предоставления возможности обрабатывать их как в порядке поступления, так и в обратном порядке.
3. Приложения:

Веб-браузеры (Web Browsers): для хранения истории посещённых страниц (возможность «назад» и «вперёд»). При переходе назад страница добавляется в другой конец списка для «возврата вперёд».
Текстовые редакторы (Text Editors): для реализации функции отмены/возврата (undo/redo). Каждое изменение добавляется в дек, и операции отмены и возврата извлекают изменения с соответствующего конца дека.
Управление задачами (Task Management): в операционных системах или приложениях дек может использоваться для планирования выполнения процессов или задач, особенно когда некоторые задачи могут выполняться с более высоким приоритетом или должны быть выполнены немедленно.
Многопоточное программирование (Multithreaded Programming): в некоторых случаях дек может использоваться в качестве рабочей очереди (work stealing queue), где потоки могут добавлять и удалять задачи с обоих концов, чтобы более эффективно распределять нагрузку.


Как реализуется Deque?
Динамический массив (Dynamic Array) с линейным сдвигом:
Описание: Используется обычный динамический массив (std::vector в C++). При добавлении/удалении в начале все элементы сдвигаются, что делает операции push_front и pop_front неэффективными (O(n)).

Преимущества: Простота реализации.

Недостатки: низкая производительность push_front и pop_front. Обычно не используется для эффективной реализации дека.

2. Циклический буфер (Circular Buffer):

Описание: Используется массив фиксированного размера, где начало и конец считаются соединёнными. Используются указатели front и rear (или head и tail) для отслеживания начала и конца дека.

Преимущества: эффективные операции push_front, push_back, pop_front, pop_back (O(1)).

Недостатки: фиксированный размер. Необходимо динамически изменять размер массива при заполнении, что может быть дорогостоящим.

3. Двусвязный список (Doubly Linked List):

Описание: Каждый элемент хранит указатели на предыдущий и следующий элементы. Добавление и удаление элементов с обоих концов выполняется путем изменения указателей.

Преимущества: эффективные операции push_front, push_back, pop_front, pop_back (O(1)). Динамический размер.

Недостатки: требует больше памяти для хранения указателей. Доступ к произвольным элементам по индексу неэффективен (O(n)).

4. Массив блоков (Array of Arrays) или Map of Chunks:

Описание: std::deque в C++ обычно реализуется следующим образом. Данные хранятся в нескольких блоках памяти (фрагментах), а «карта» (map) или «индекс» (index) хранит указатели на эти блоки. Это позволяет эффективно добавлять и удалять элементы с обоих концов без необходимости перемещения больших объёмов данных.

Преимущества: Быстрые операции добавления и удаления с обоих концов (в среднем O(1)). Динамическое изменение размера. Более эффективное использование памяти, чем связный список, за счёт хранения элементов в блоках.

Недостатки: доступ к произвольным элементам может быть немного медленнее, чем в std::vector, так как требуется два уровня доступа к памяти (сначала к карте, затем к блоку). Более сложная реализация.

В своем коде дек реализовывал с помощью циклического буфера, поэтому разберем что это такое


Циклический Буфер
Циклический буфер (или кольцевой буфер) — это структура данных, использующая массив фиксированного размера, как если бы его начало и конец были соединены, образуя круг. Это позволяет эффективно использовать память для хранения данных, которые должны быть доступны в определённом порядке, без необходимости перемещать элементы при добавлении или удалении.

В нашей реализации дека циклический буфер реализован с помощью массива arr и указателей front и back, которые перемещаются по массиву с помощью операции взятия по модулю (% capacity). Это позволяет добавлять элементы в начало или конец дека, даже если front или back находятся в конце массива, как будто массив «сворачивается».



Объяснение формул циклического сдвига

1. front = (front - 1 + capacity) % capacity;

Эта формула используется в push_front() для перемещения указателя front к предыдущей позиции в массиве.

front - 1 Сначала мы пытаемся сдвинуть front на одну позицию влево. Если front уже равен 0 (начало массива), то получится -1, что является недопустимым индексом.

+ capacity Чтобы избежать отрицательного индекса, мы добавляем capacity к результату. Если front было равно 0, то результат будет capacity - 1.

% capacity: Операция % capacity гарантирует, что индекс всегда будет находиться в диапазоне от 0 до capacity - 1. Если front не равно 0, то результатом будет front - 1, так как front - 1 будет меньше capacity. Если front равно 0, то результатом будет capacity - 1, обеспечивая циклический переход в конец массива.

В итоге: формула позволяет front корректно перемещаться влево, даже если он находится в начале массива, тем самым позволяя добавлять элементы в начало дека, используя циклический буфер.



2. back = (back - 1 + capacity) % capacity;

Эта формула используется в pop_back() для перемещения указателя back к предыдущей позиции в массиве. Логика абсолютно аналогична формуле для front, только применяется к back:

back - 1: Уменьшаем back на 1.

+ capacity: Добавляем capacity, чтобы избежать отрицательного индекса.

% capacity: Гарантируем, что индекс находится в пределах массива.

В итоге: формула позволяет back корректно перемещаться влево, даже если он находится в начале массива, тем самым позволяя удалять элементы из конца дека, используя циклический буфер.



Основные операции, поддерживаемые деком:
push_front(element): Добавляет элемент в начало дека.
push_back(element): Добавляет элемент в конец дека.
pop_front(): Удаляет элемент из начала дека.
pop_back(): Удаляет элемент из конца дека.
get_front(): Возвращает элемент из начала дека (без удаления).
get_back(): Возвращает элемент из конца дека (без удаления).
isEmpty(): Проверяет, пуст ли дек.
isFull(): Проверяет, заполнен ли дек (в случае реализации с фиксированным размером).


Реализация Дека на C++: 
Данная реализация дека использует следующие подходы:

Массив фиксированного размера: для хранения элементов дека используется массив arr с максимальной вместимостью capacity.
Циклический буфер: для эффективного использования памяти массива используется концепция циклического буфера.
Два указателя: front (индекс первого элемента) и back (индекс последнего элемента).
Переменная size: Хранит текущее количество элементов в деке.
Динамическое изменение размера (resize): если дек заполнен, его размер увеличивается вдвое, чтобы вместить новые элементы.


Структура класса Deque:
Поля класса

int* arr;    // Указатель на динамически выделенный массив
 int front;    // Индекс первого элемента дека
int back;    // Индекс последнего элемента дека
int size;    // Текущий размер дека
int capacity;  // Максимальная вместимость дека


Методы класса

Deque(int capacity) (Конструктор):

Выделяет память под массив arr размером capacity.
Инициализирует front и back значением -1 (дек пуст).
Устанавливает size в 0.


~Deque() (Деструктор):

Освобождает память, выделенную под массив arr.


isEmpty():

Возвращает true, если size == 0, иначе false.


isFull():

Возвращает true, если size == capacity, иначе false.


push_front(int element):

Если size == capacity, вызывается resize() для увеличения размера массива.
Если isEmpty(), устанавливает front = 0 и back = 0.
В противном случае вычисляет новый front с помощью формулы front = (front - 1 + capacity) % capacity; (подробнее об этой формуле ниже).
Добавляет element в arr[front].
Увеличивает size.


push_back(int element):

Если size == capacity, вызывается resize().
Если isEmpty(), устанавливает front = 0 и back = 0.
Иначе, вычисляет новый back с использованием формулы back = (back + 1) % capacity;.
Добавляет element в arr[back].
Добавляет element в arr[back].
Увеличивает size.


pop_front():

Если isEmpty(), выводит сообщение об ошибке и возвращает -1.
Сохраняет значение arr[front] в element.
Уменьшает size.
Если isEmpty(), устанавливает front = -1 и back = -1.
Иначе, вычисляет новый front с использованием формулы front = (front + 1) % capacity;.
Возвращает element.


pop_back():

Если isEmpty(), выводит сообщение об ошибке и возвращает -1.
Сохраняет значение arr[back] в element.
Уменьшает size.
Если isEmpty(), устанавливает front = -1 и back = -1.
Иначе, вычисляет новый back с использованием формулы back = (back - 1 + capacity) % capacity;.
Возвращает element.


get_front():

Если isEmpty(), выводит сообщение об ошибке и возвращает -1.
Возвращает arr[front].


get_back():

Если isEmpty(), выводит сообщение об ошибке и возвращает -1.
Возвращает arr[back].


resize():

Увеличивает capacity вдвое.
Создает новый массив newArr размером newCapacity.
Копирует элементы из старого массива arr в newArr, учитывая циклический порядок.
Освобождает память, выделенную под arr.
Устанавливает arr на newArr.
Устанавливает front = 0 и back = size - 1.


Заключение

Данная реализация дека предоставляет основные функциональные возможности с использованием массива фиксированного размера и динамическим изменением размера. Концепция циклического буфера позволяет эффективно использовать память, а формулы циклического сдвига обеспечивают корректную работу дека при добавлении и удалении элементов с обоих концов. Эта реализация может быть использована в различных приложениях, где требуется гибкая структура данных, позволяющая добавлять и удалять элементы как с начала, так и с конца.



Обработка ошибок

В данной реализации при возникновении ошибок (например, при попытке pop_front или pop_back из пустого дека, или get_front или get_back у пустого дека) выводится сообщение в консоль и возвращается значение -1.



Недостатки текущей обработки ошибок:



Использование -1 в качестве индикатора ошибки может быть проблематичным, так как -1 может быть допустимым значением для дека, хранящего целые числа.

Вывод сообщения в консоль ограничивает гибкость обработки ошибок, поскольку вызывающий код не может отреагировать на ошибку каким-либо другим способом.



Ограничения

Использование int для хранения данных: Дек хранит только целые числа (int).
Массив фиксированного размера: хотя дек динамически изменяет свой размер, начальный размер задается при создании дека. Если ожидается хранение очень большого количества элементов, это может привести к частому изменению размера и снижению производительности.
Отсутствие полноценной обработки ошибок: используется простой вывод сообщения в консоль и возврат -1.
Изменение размера в два раза: увеличение размера массива в два раза может привести к неэффективному использованию памяти, если дек содержит лишь немного больше элементов, чем текущая вместимость.
Нет обработки исключений: исключения не используются для сигнализации об ошибках.


Возможные улучшения

Использование шаблонов (templates): реализовать дек как шаблонный класс, чтобы он мог хранить данные любого типа.
Использование исключений: вместо возврата -1 при ошибках следует генерировать исключения. Это позволит вызывающему коду более гибко обрабатывать ошибки.
Использовать более сложные алгоритмы для определения нового размера массива, чтобы избежать слишком частого изменения размера и неэффективного использования памяти.
Реализация с использованием связного списка: вместо массива использовать связный список. Это позволит избежать ограничений фиксированного размера и динамического изменения размера, но может снизить производительность из-за накладных расходов на хранение указателей.
Добавление итераторов: реализовать итераторы для удобного обхода элементов дека.
Использование std::vector: Вместо ручного управления памятью с помощью new и delete можно использовать std::vector, который автоматически управляет памятью и предоставляет множество удобных методов. Это упростит код и сделает его более надёжным.

Источники:

https://learn.microsoft.com/ru-ru/cpp/standard-library/deque-class?view=msvc-170
https://metanit.com/cpp/tutorial/7.8.php
https://sch9.ru/files/lectures/cpp/stl.pdf
https://chatgptchatapp.com/ <3
