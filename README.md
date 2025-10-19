# Builder
```cs
class Product { List<string> parts = new(); public void Add(string p)=>parts.Add(p); public void Show()=>Console.WriteLine(string.Join(", ", parts)); }

interface IBuilder { void BuildPartA(); void BuildPartB(); Product GetResult(); }

class ConcreteBuilder : IBuilder {
    Product product = new();
    public void BuildPartA()=>product.Add("PartA");
    public void BuildPartB()=>product.Add("PartB");
    public Product GetResult()=>product;
}

class Director {
    public void Construct(IBuilder b){ b.BuildPartA(); b.BuildPartB(); }
}

class Program {
    static void Main() {
        var builder=new ConcreteBuilder(); var director=new Director();
        director.Construct(builder); builder.GetResult().Show();
    }
}
