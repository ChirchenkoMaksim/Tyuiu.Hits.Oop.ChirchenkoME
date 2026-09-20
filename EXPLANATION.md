# Шпаргалка по коду Sprint0 и Sprint1

Это разбор именно тех code-ячеек, которые были добавлены в проект. Читать лучше сверху вниз. Если преподаватель показывает строку, сначала объясни, **что хранится**, потом **что делает строка**, потом **зачем это нужно**.

## Самые важные слова C#

| Запись | Совсем простое значение |
|---|---|
| `class` | Описание будущего объекта. Например, класс `Review` описывает, из чего состоит отзыв. |
| `new` | Создать настоящий объект по описанию класса. |
| `public` | Доступно из других классов. |
| `private` | Доступно только внутри своего класса. |
| `string` | Текст. |
| `int` | Целое число. |
| `double` | Число с дробной частью. |
| `bool` | Да/нет: `true` или `false`. |
| `void` | Метод ничего не возвращает. |
| `return` | Вернуть результат из метода. |
| `get` | Как прочитать свойство. |
| `set` | Как изменить свойство. |
| `:` после имени класса | Наследование: класс справа получает возможности класса после двоеточия. |
| `virtual` | Метод можно заменить в дочернем классе. |
| `override` | Дочерний класс действительно заменяет родительский метод. |
| `abstract` | Заготовка, которую нельзя использовать напрямую; дочерний класс обязан дописать её часть. |
| `interface` | Договор: какие методы класс обязан иметь. |
| `readonly` | Поле можно задать один раз и потом не заменить. |
| `static` | Общее значение для всех объектов класса, а не отдельное значение каждого объекта. |
| `=>` | Короткая запись метода или свойства. |
| `$"...{переменная}..."` | Текст с подстановкой значения переменной. |

---

# Sprint0

## Task0 — массив чисел

Файл: [Sprint0/Task0.ipynb](Sprint0/Task0.ipynb)

```csharp
int[] numbers = { 5, 8, 1, 3, 9, 6, 7, 2 };
int min = numbers.Min();
int max = numbers.Max();
int sum = numbers.Sum();
double average = numbers.Average();
int[] sorted = numbers.OrderBy(number => number).ToArray();
bool containsSeven = numbers.Contains(7);
Console.WriteLine($"Минимум: {min}; максимум: {max}; сумма: {sum}; среднее: {average:F2}");
Console.WriteLine($"По возрастанию: {string.Join(", ", sorted)}");
Console.WriteLine($"Массив содержит 7: {containsSeven}");
```

Разбор:

1. `int[] numbers` — создаём массив целых чисел. Внутри восемь значений.
2. `Min()` ищет самое маленькое число. Ответ `1`.
3. `Max()` ищет самое большое число. Ответ `9`.
4. `Sum()` складывает все числа. Ответ `41`.
5. `Average()` считает среднее. `41 / 8 = 5,125`, поэтому выводится `5,13`.
6. `OrderBy(number => number)` сортирует числа по возрастанию. `number => number` означает «для каждого числа взять само это число как ключ сортировки».
7. `ToArray()` превращает результат сортировки обратно в массив.
8. `Contains(7)` проверяет, есть ли число 7. Результат — `true`.
9. `Console.WriteLine` печатает строку.
10. `:F2` просит показать дробное число с двумя знаками после запятой.
11. `string.Join(", ", sorted)` соединяет элементы массива через запятую.

Что сказать преподавателю: «Это массив `int`. Методы `Min`, `Max`, `Sum`, `Average`, `OrderBy` и `Contains` выполняют стандартные операции над коллекцией. `OrderBy` возвращает отсортированную последовательность, а `ToArray` сохраняет её как массив».

## Task1 — основы ООП на животных

Файл: [Sprint0/Task1.ipynb](Sprint0/Task1.ipynb)

### Ячейка 1: класс и объект

```csharp
class AnimalClassesDemo
{
    public string Name { get; } = "Барсик";
    public void Speak() => Console.WriteLine($"{Name} издает звук");
}
new AnimalClassesDemo().Speak();
```

`AnimalClassesDemo` — класс. `Name` — свойство только для чтения: есть `get`, но нет `set`. Метод `Speak` печатает имя и сообщение. `new AnimalClassesDemo()` создаёт объект. Последний `.Speak()` сразу вызывает его метод.

### Ячейка 2: инкапсуляция

```csharp
class EncapsulatedAnimal
{
    private int age;
    public int Age
    {
        get => age;
        private set => age = Math.Max(0, value);
    }
    public EncapsulatedAnimal(int age) => Age = age;
}
var cat = new EncapsulatedAnimal(3);
Console.WriteLine($"Возраст животного: {cat.Age}");
```

`age` — настоящее внутреннее поле. Оно `private`, поэтому снаружи напрямую изменить его нельзя. `Age` — безопасное свойство. При записи используется `Math.Max(0, value)`, поэтому возраст не станет отрицательным. `private set` означает: читать возраст можно снаружи, менять — только внутри класса. Конструктор получает возраст и записывает его через свойство.

### Ячейка 3: наследование

```csharp
class InheritedAnimal
{
    public virtual void Move() => Console.WriteLine("Животное движется");
}
class InheritedDog : InheritedAnimal
{
    public override void Move() => Console.WriteLine("Собака бежит");
}
new InheritedDog().Move();
```

`InheritedDog : InheritedAnimal` означает: собака является животным и получает его методы. `virtual` разрешает изменить метод. `override` меняет поведение для собаки. Поэтому при вызове выводится «Собака бежит».

### Ячейка 4: полиморфизм

```csharp
class PolymorphicAnimal { public virtual string Sound() => "звук"; }
class PolymorphicCat : PolymorphicAnimal { public override string Sound() => "мяу"; }
class PolymorphicDog : PolymorphicAnimal { public override string Sound() => "гав"; }
foreach (PolymorphicAnimal animal in new PolymorphicAnimal[] { new PolymorphicCat(), new PolymorphicDog() })
    Console.WriteLine(animal.Sound());
```

Массив имеет тип `PolymorphicAnimal`, но внутри лежат кошка и собака. Переменная `animal` каждый раз имеет общий тип животного. Благодаря `virtual/override` C# смотрит на настоящий тип объекта и вызывает нужную версию `Sound`: сначала «мяу», потом «гав». Это и есть полиморфизм.

### Ячейка 5: абстракция

```csharp
abstract class AbstractAnimal
{
    public abstract string Habitat { get; }
    public void Show() => Console.WriteLine($"Среда обитания: {Habitat}");
}
class AbstractFish : AbstractAnimal
{
    public override string Habitat => "вода";
}
new AbstractFish().Show();
```

`abstract class` нельзя создать напрямую. Он задаёт общую идею животного. Свойство `Habitat` объявлено без готового значения, поэтому дочерний класс обязан его переопределить. `AbstractFish` говорит, что среда обитания — вода. Метод `Show` общий для всех наследников.

### Ячейка 6: композиция

```csharp
class AnimalFood
{
    public string Name { get; }
    public AnimalFood(string name) => Name = name;
}
class ComposedAnimal
{
    private readonly AnimalFood food = new("корм");
    public void Eat() => Console.WriteLine($"Животное ест: {food.Name}");
}
new ComposedAnimal().Eat();
```

`ComposedAnimal` сам создаёт внутри себя `AnimalFood`. Это композиция: часть создаётся и принадлежит целому. Поле `food` хранит корм, а `Eat` использует его имя. `readonly` запрещает заменить ссылку на другой объект после создания.

### Ячейка 7: агрегация

```csharp
class AnimalOwner
{
    public string Name { get; }
    public AnimalOwner(string name) => Name = name;
}
class AggregatedAnimal
{
    public AnimalOwner Owner { get; }
    public AggregatedAnimal(AnimalOwner owner) => Owner = owner;
}
var owner = new AnimalOwner("Максим");
Console.WriteLine($"Владелец животного: {new AggregatedAnimal(owner).Owner.Name}");
```

Сначала отдельно создаётся `owner`. Потом этот уже готовый объект передаётся животному. Это агрегация: животное использует владельца, но владелец может существовать отдельно от животного.

Остальные ячейки Task1 повторяют те же идеи с другими именами: `AnimalPolymorphismTask` — полиморфизм, `AbstractTaskAnimal` — абстрактный класс, `TaskCompositionAnimal` — композиция, `TaskAggregationAnimal` — агрегация, `FinalAnimal` и `FinalDog` — переопределение метода. Если попросят любую из них, объяснение такое же: родитель задаёт общую возможность, дочерний класс уточняет её.

## Task2 — SOLID

Файл: [Sprint0/Task2.ipynb](Sprint0/Task2.ipynb)

### Single Responsibility — одна ответственность

```csharp
class SolidAnimal
{
    public string Name { get; }
    public SolidAnimal(string name) => Name = name;
}
class AnimalPrinter
{
    public void Print(SolidAnimal animal) => Console.WriteLine($"Животное: {animal.Name}");
}
new AnimalPrinter().Print(new SolidAnimal("Барсик"));
```

`SolidAnimal` хранит данные животного. `AnimalPrinter` занимается выводом. Класс животного не смешан с печатью. Это принцип единственной ответственности.

### Open/Closed — открыт для расширения, закрыт для изменения

```csharp
interface IAnimalSound { string MakeSound(); }
class SolidDog : IAnimalSound { public string MakeSound() => "гав"; }
class SolidCat : IAnimalSound { public string MakeSound() => "мяу"; }
foreach (IAnimalSound animal in new IAnimalSound[] { new SolidDog(), new SolidCat() })
    Console.WriteLine(animal.MakeSound());
```

Есть общий договор `IAnimalSound`. Чтобы добавить новое животное, достаточно создать новый класс с `MakeSound`. Старые классы менять не нужно. Поэтому код расширяется добавлением новых классов.

### Liskov Substitution — дочерний класс заменяет родительский

```csharp
abstract class SolidBird { public abstract void Move(); }
class SolidFlyingBird : SolidBird { public override void Move() => Console.WriteLine("Птица летит"); }
new SolidFlyingBird().Move();
```

`SolidFlyingBird` можно использовать там, где ожидается `SolidBird`. Он выполняет обещанный метод `Move`, поэтому не ломает ожидания родительского типа.

### Interface Segregation — маленькие интерфейсы

```csharp
interface IWalkable { void Walk(); }
interface IFeedable { void Feed(); }
class SolidAnimalCapabilities : IWalkable, IFeedable
{
    public void Walk() => Console.WriteLine("Животное идет");
    public void Feed() => Console.WriteLine("Животное ест");
}
var capabilities = new SolidAnimalCapabilities();
capabilities.Walk();
capabilities.Feed();
```

Вместо одного огромного интерфейса сделаны два маленьких: ходьба и кормление. Класс явно реализует оба. Маленькие договоры проще понимать и использовать.

### Dependency Inversion — зависимость от договора

```csharp
interface IAnimalRepository { string GetName(); }
class MemoryAnimalRepository : IAnimalRepository
{
    public string GetName() => "Барсик";
}
class AnimalService
{
    private readonly IAnimalRepository repository;
    public AnimalService(IAnimalRepository repository) => this.repository = repository;
    public void Show() => Console.WriteLine($"Имя из хранилища: {repository.GetName()}");
}
new AnimalService(new MemoryAnimalRepository()).Show();
```

`AnimalService` не зависит напрямую от конкретного `MemoryAnimalRepository`. Он зависит от интерфейса `IAnimalRepository`. Поэтому позже можно заменить память на базу данных, не переписывая `AnimalService`. Объект хранилища передаётся в конструктор — это внедрение зависимости.

## Task3 — главный проект варианта №18

Файл: [Sprint0/Task3.ipynb](Sprint0/Task3.ipynb)

### Базовый класс Review

```csharp
public class Review
{
    public int ReviewId { get; }
    public string Text { get; }
    public int Rating { get; private set; }
```

`Review` — общий класс для любого отзыва. `ReviewId` — номер отзыва. `Text` — текст. `Rating` — оценка. У номера и текста есть только `get`, значит после создания их нельзя заменить. У рейтинга есть `private set`: снаружи рейтинг нельзя менять напрямую, только через метод класса.

```csharp
public Review(int reviewId, string text, int rating)
{
    ReviewId = reviewId;
    Text = text;
    Rating = Math.Clamp(rating, 1, 5);
}
```

Это конструктор. Он запускается при `new Review(...)`. `Math.Clamp(rating, 1, 5)` ограничивает оценку диапазоном от 1 до 5: если передать 8, сохранится 5; если передать 0, сохранится 1.

```csharp
public virtual void DisplayReview() =>
    Console.WriteLine($"Отзыв #{ReviewId}: {Text} ({Rating}/5)");
```

Метод печатает отзыв. `virtual` означает, что производный класс может печатать его по-своему.

```csharp
public virtual void RateProduct(int rating)
{
    Rating = Math.Clamp(rating, 1, 5);
}
```

Метод меняет рейтинг безопасным способом. Это лучше, чем делать `Rating` полностью открытым для записи.

```csharp
public virtual string GetReviewDetails() =>
    $"#{ReviewId}, рейтинг {Rating}/5: {Text}";
```

Метод возвращает подробности как строку. Он тоже `virtual`, потому что дочерние классы добавляют свои поля.

### ServiceReview — отзыв об услуге

```csharp
public class ServiceReview : Review
{
    public DateTime VisitDate { get; }
    public ServiceReview(int id, string text, int rating, DateTime visitDate)
        : base(id, text, rating) => VisitDate = visitDate;
```

`ServiceReview : Review` означает, что сервисный отзыв является обычным отзывом плюс дата посещения. `base(...)` вызывает конструктор родительского `Review`, чтобы тот заполнил номер, текст и рейтинг. `DateTime` хранит дату и время.

```csharp
public override void DisplayReview() =>
    Console.WriteLine($"Сервисный отзыв #{ReviewId} от {VisitDate:dd.MM.yyyy}: {Text} ({Rating}/5)");

public override string GetReviewDetails() =>
    $"{base.GetReviewDetails()}, дата посещения: {VisitDate:dd.MM.yyyy}";
```

`override` заменяет родительское поведение. `base.GetReviewDetails()` сначала получает обычные сведения отзыва, затем к ним добавляется дата.

### ProductReview — отзыв о товаре

```csharp
public class ProductReview : Review
{
    public string ProductId { get; }
    public ProductReview(int id, string text, int rating, string productId)
        : base(id, text, rating) => ProductId = productId;
```

Это дочерний класс с дополнительным идентификатором товара. Он повторно использует конструктор базового класса.

```csharp
public override void RateProduct(int rating)
{
    base.RateProduct(rating);
    Console.WriteLine($"Товар {ProductId} получил рейтинг {Rating}/5");
}
```

Сначала вызывается обычное изменение рейтинга через `base.RateProduct`. Потом добавляется специальный вывод для товара. Это хороший пример переопределения с расширением поведения.

### ServiceTimeReview — услуга с временем начала

```csharp
public class ServiceTimeReview : ServiceReview
{
    public TimeSpan StartTime { get; }
    public ServiceTimeReview(..., DateTime date, TimeSpan startTime)
        : base(id, text, rating, date) => StartTime = startTime;
```

Этот класс наследуется от `ServiceReview`, поэтому у него уже есть дата посещения. Он добавляет время начала услуги. `TimeSpan` хранит промежуток времени или время суток.

```csharp
public override string GetReviewDetails() =>
    $"{base.GetReviewDetails()}, начало услуги: {StartTime:hh\\:mm}";
```

Берём готовое описание сервиса и дописываем время. Обратный слэш перед двоеточием нужен для правильного форматирования `TimeSpan`.

### Создание объектов и полиморфизм

```csharp
Review[] reviews =
{
    new ServiceReview(...),
    new ProductReview(...),
    new ServiceTimeReview(...)
};
```

Массив имеет общий тип `Review`, но внутри лежат три разных дочерних объекта. Это главный пример полиморфизма.

```csharp
foreach (Review review in reviews)
{
    review.DisplayReview();
    Console.WriteLine(review.GetReviewDetails());
}
```

`foreach` по очереди берёт каждый отзыв. Несмотря на общий тип `Review`, C# вызывает правильный переопределённый метод настоящего объекта: для сервиса — сервисный вывод, для времени — расширенное описание.

```csharp
((ProductReview)reviews[1]).RateProduct(5);
```

`reviews[1]` — второй элемент массива. Для компилятора он имеет общий тип `Review`, поэтому мы явно говорим: «считай его `ProductReview`». Это называется приведение типа. После этого можно вызвать специальный метод товара.

Что сказать преподавателю: «Базовый класс хранит общие данные и методы. Производные классы добавляют свои поля и переопределяют виртуальные методы. Массив базового типа хранит объекты разных дочерних типов, а `foreach` вызывает нужную реализацию во время выполнения — это полиморфизм».

---

# Sprint1

## Task0 — структура класса

Файл: [Sprint1/Task0.ipynb](Sprint1/Task0.ipynb)

```csharp
class ReviewStructure
{
    public int Id { get; }
    public string Text { get; set; }
    public ReviewStructure(int id, string text) { Id = id; Text = text; }
    public void Show() => Console.WriteLine($"#{Id}: {Text}");
}
new ReviewStructure(1, "Структура класса отзыва").Show();
```

Класс хранит номер и текст. `Id` нельзя изменить после создания, а `Text` можно читать и менять. Конструктор заполняет свойства. `Show` выводит объект на экран.

```csharp
interface IReviewDisplay { void Display(); }
class ReviewClass : IReviewDisplay
{
    public static int Count;
    public string Text { get; set; }
    public ReviewClass(string text) { Text = text; Count++; }
    public void Display() => Console.WriteLine($"Отзыв: {Text}");
}
```

`IReviewDisplay` требует метод `Display`. `ReviewClass` выполняет этот договор. `static Count` один на весь класс: каждый созданный отзыв увеличивает общий счётчик.

## Task1 — свойства, геттеры и сеттеры

Файл: [Sprint1/Task1.ipynb](Sprint1/Task1.ipynb)

```csharp
class ReviewWithProperties
{
    private int rating;
    public int Rating
    {
        get => rating;
        set => rating = Math.Clamp(value, 1, 5);
    }
    public string Text { get; set; } = "";
    public void Show() => Console.WriteLine($"{Text} — {Rating}/5");
}
```

`rating` — закрытое поле. Свойство `Rating` не позволяет записать число меньше 1 или больше 5. `Text` имеет обычные `get` и `set`, поэтому его можно менять. `= ""` задаёт пустое начальное значение и не оставляет текст незаполненным.

```csharp
class ReviewBaseS1 { ... }
class ProductReviewS1 : ReviewBaseS1 { ... }
class ServiceReviewS1 : ReviewBaseS1 { ... }
```

Здесь один базовый отзыв расширяется двумя видами: товарным с `ProductId` и сервисным с `VisitDate`. `: base(text)` передаёт текст родительскому конструктору. `override Display` печатает каждый тип по-разному.

## Task2 — взаимодействие объектов

Файл: [Sprint1/Task2.ipynb](Sprint1/Task2.ipynb)

```csharp
class ReviewInteraction
{
    public string Text { get; set; }
    public ReviewInteraction(string text) => Text = text;
    public virtual void Display() => Console.WriteLine(Text);
}
class ProductInteraction : ReviewInteraction
{
    public ProductInteraction(string text) : base(text) { }
    public override void Display() => Console.WriteLine($"Товар получил отзыв: {Text}");
}
```

`ProductInteraction` получает текст через конструктор родителя. Его `Display` заменяет обычный вывод специальным сообщением про товар.

```csharp
class ReviewBoard
{
    private readonly List<ReviewInteraction> reviews = new();
    public void Add(ReviewInteraction review) => reviews.Add(review);
    public void ShowAll()
    {
        foreach (var review in reviews) review.Display();
    }
}
```

`ReviewBoard` — доска отзывов. `List` — изменяемый список. `Add` добавляет отзыв. `ShowAll` проходит по списку и вызывает метод каждого объекта. Здесь снова работает полиморфизм.

```csharp
var board = new ReviewBoard();
board.Add(new ProductInteraction("Качество отличное"));
board.Add(new ProductInteraction("Доставка быстрая"));
board.ShowAll();
```

Создаём доску, добавляем два объекта и просим доску показать все отзывы.

Вторая ячейка Task2 использует `ReviewAuthor` и `ReviewWithAuthor`. Автор создаётся отдельно и передаётся отзыву в конструкторе. Это агрегация: отзыв знает автора, но автор может существовать самостоятельно.

## Task3 — итоговый вариант Sprint1

Файл: [Sprint1/Task3.ipynb](Sprint1/Task3.ipynb)

Классы `Review`, `ServiceReview`, `ProductReview` и `ServiceTimeReview` работают так же, как в Sprint0. Главное отличие Sprint1 — свойства `Text`, `VisitDate`, `ProductId` и `StartTime` имеют `set`, поэтому состояние объекта можно изменить после создания.

```csharp
var reviewList = new List<Review>
{
    new ServiceReview(...),
    new ProductReview(...),
    new ServiceTimeReview(...)
};
foreach (Review review in reviewList)
{
    review.DisplayReview();
    Console.WriteLine(review.GetReviewDetails());
}
```

Вместо массива используется `List<Review>`. Список удобнее, если количество отзывов меняется. Тип списка общий `Review`, поэтому разные виды отзывов снова обрабатываются одним циклом и демонстрируют полиморфизм.

---

# Короткие ответы на частые вопросы

**Почему `Review` базовый?** Потому что у всех отзывов есть общие данные: номер, текст и рейтинг.

**Почему нужны дочерние классы?** У сервиса есть дата посещения, у товара — идентификатор товара, у услуги — время начала. Эти поля не нужны каждому отзыву.

**Что такое полиморфизм в проекте?** Массив или список имеет тип `Review`, но хранит разные дочерние объекты. Вызов одного метода приводит к разному результату в зависимости от настоящего типа объекта.

**Зачем `virtual` и `override`?** `virtual` разрешает изменить метод, `override` сообщает, что дочерний класс его изменил.

**Зачем `base`?** Чтобы вызвать конструктор или метод родительского класса и не дублировать его код.

**Чем `private set` отличается от `set`?** При `private set` менять свойство можно только внутри класса. При обычном `set` менять его можно снаружи.

**Чем композиция отличается от агрегации?** При композиции объект создаёт свою часть сам и владеет ею. При агрегации готовый объект передают внутрь, и он может жить отдельно.

**Зачем `Math.Clamp`?** Чтобы рейтинг всегда оставался от 1 до 5.

**Что делает конструктор?** Настраивает новый объект сразу при создании.

**Что делает `foreach`?** По очереди берёт каждый элемент массива или списка.

**Почему `ProductReview` можно привести из `Review`?** Потому что `ProductReview` наследуется от `Review`. Любой объект товара одновременно является отзывом, но не каждый отзыв является товарным.

**Что такое интерфейс?** Набор обязательных методов без конкретного хранения данных. Класс, который его реализует, обязан написать эти методы.

**Что такое SOLID в этой работе?** Пять правил, которые помогают разделять обязанности, расширять код без переписывания, правильно использовать наследников, делать маленькие интерфейсы и передавать зависимости через абстракции.

Если забыл точное слово, безопасная схема ответа такая: «Это объявление класса/свойства/метода. Здесь хранится ..., этот метод делает ..., а нужно это для ...». Главное — не молчать и объяснять назначение строки простыми словами.
