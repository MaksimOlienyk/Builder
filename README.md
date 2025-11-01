# Builder - Патерн Проєктування

Цей приклад демонструє шаблон **Builder** у мові C#.

**Builder** використовується для **покрокового конструювання складних об’єктів**, приховуючи деталі створення та дозволяючи варіювати представлення об’єкта.

---

## Ідея патерна

> Розділити процес створення об’єкта на кроки.  
> Один і той самий процес побудови може створювати різні варіанти об’єкта.

Патерн дозволяє:
- будувати об’єкти поступово, по частинах;
- контролювати порядок складання;
- використовувати різні будівничі (`Builder`) для створення різних представлень продукту.

---

## Структура

| Роль | Опис |
|------|------|
| `Product` | Об’єкт, який будується з частин |
| `IBuilder` | Інтерфейс, що визначає кроки побудови |
| `ConcreteBuilder` | Реалізує побудову конкретного продукту |
| `Director` | Керує послідовністю побудови (опціонально) |

---

## Код

```csharp
class Product {
    List<string> parts = new();
    public void Add(string p) => parts.Add(p);
    public void Show() => Console.WriteLine(string.Join(", ", parts));
}

interface IBuilder {
    void BuildPartA();
    void BuildPartB();
    Product GetResult();
}

class ConcreteBuilder : IBuilder {
    Product product = new();
    public void BuildPartA() => product.Add("PartA");
    public void BuildPartB() => product.Add("PartB");
    public Product GetResult() => product;
}

class Director {
    public void Construct(IBuilder b) {
        b.BuildPartA();
        b.BuildPartB();
    }
}

class Program {
    static void Main() {
        var builder = new ConcreteBuilder();
        var director = new Director();

        director.Construct(builder);
        builder.GetResult().Show();
    }
}
## ConcrateBuilder - вирішує як саме створювати частини продукта
## Director - визначає частини і в якому порядку потрібно створювати
## Program - лише виконує цей процес

