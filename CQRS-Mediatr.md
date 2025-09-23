# CQRS Ve Mediatr

## CQRS Nedir?
CQRS(Command Query Responsibility Segregation), write (yazma) ve read (okuma) sorumluluklarının ayrıştırılmasına dayanan bir mimari tasarım modelidir. 

<img width="788" height="522" alt="image" src="https://github.com/user-attachments/assets/d1aa7828-3c28-4f7e-a28f-3b0d5f8edcd5" />








Resim kaynakçası ->  https://sefikcankanber.medium.com/cqrs-command-query-responsibility-segregation-nedir-16b196376389





- Geleneksel bir mimaride, hem okuma hem de yazma işlemleri için genellikle tek bir veri modeli kullanılır. Bu yaklaşım basittir ve temel oluşturma, okuma, güncelleme ve silme (CRUD) işlemleri için uygundur. Uygulamalar büyüdükçe, tek bir veri modeli üzerinde okuma ve yazma işlemlerini optimize etmek giderek zorlaşabilir. Okuma ve yazma işlemleri genellikle farklı performans ve ölçekleme gereksinimlerine sahiptir. Geleneksel bir CRUD mimarisi bu asimetriyi hesaba katmaz ve bu da veri uyumsuzluğu, kilit çekişmesi, performans ve güvenlik ile ilgili sorunlara yol açmaktadır.
- Çözüm ise: CQRS. Yazma işlemlerini veya komutları okuma işlemlerinden veya sorgulardan ayırmak için CQRS modelini kullanılır . Komutlar verileri günceller. Sorgular verileri alır. CQRS modeli, komutlar ve okumalar arasında net bir ayrım gerektiren senaryolarda kullanışlıdır.
- CQRS mimarisi, CQS ilkesi baz alınarak kurulmuştur. CQS’in ana fikrinden bahsetmek gerekirse; bir metot objenin durumunu değiştirmelidir ya da geriye bir sonuç dönmelidir, ancak 2 işlemi birden yapmamalıdır. Metotlar yalnızca yan etki yaratmıyorsa bir değer döndürmelidir. Basitçe söylemek gerekirse: bir sorgu asla state değerini değiştirmemeli , bir komut ise state değerini değiştirebilir ancak asla bir dönüş değerine sahip olmamalıdır . Uygulamalarınızda CQRS mimari modeline göre oluşturursanız; uygulamanızın performansını, ölçeklenebilirliğini ve güvenliğini en üst düzeye çıkarabilirsiniz.
- Bu yaklaşımda metotlar 2 farklı modele ayrılmalıdır: **Commands**, Objenin veya sistemin durumunu değiştirir. **Queries**, Sadece sonucu geriye döner herhangi bir objenin veya sistemin durumunu değiştirmez.


### Commands
Yeni bir veri eklemek ya da var olan veri üzerinde güncelleme yapmak için kullanılır. Örnek vermek gerekirse; Insert, Update, Delete. Geriye veri döndürmez. Örnek olarak;

```charp
public class AddBlacklistCustomerCommand : ICommand
{
    public readonly int Id
    public redonly string BlacklistNote;
    public AddBlacklistCustomerCommand(int id, string blacklistNote)
    {
        Id = id;
        BlacklistNote = blacklistNote;
    }
}
```

### Queries
Veritabanından veri almak için kullanılır. Geriye sadece belirtilen modeli döner ve veri üzerinde herhangi bir değişiklik yapmaz. Oluşturacağımız Query’lerimiz genellikle ‘Get’ ön eki ile isimlendirilir. Örnek olarak;

```charp
public class GetCustomerByIdQuery() : IQuery
{
    public int Id { get; set; }
    public GetCustomerByIdQuery(int id)
    {
        Id = id;
    }
}
```

### CQRS Ne Zaman Kullanılmalı ?
- Birbirinden ayrı sistemlerde olası bir servisin hata vermesi durumunda bu hatanın sistemin akışına olumsuz yönde etkisi olmuyorsa kullanılabilir.
- Kompleks iş kurallarının olabileceği veya iş kurallarının sık sık değiştiği yapılarda kullanılabilir.
- Yüksek veri trafiğinin olduğu sistemlerde kullanılabilir.
### CQRS’i Ne Zaman Kullanmamalıyız ?
- İş kurallarının basit ve çok değişmediği sistemlerde,
- Basit CRUD işlemlerinin yapıldığı sistemlerde

---

### CQRS’in Avantajları
- Read ve write operasyonlarının ayrılması performansı, ölçeklenebilirliği ve güvenliği artırmaya yardımcı olabilir.
- Read ve write işlemleriniz için farklı veritabanları kullanabilirsiniz.(Örneğin, yazma işlemleri için MySQL kullanırken okuma işlemleri için Couchbase kullanabilirsiniz).
- Read ve write işlemleri ayrıldığı için, herhangi yapılacak bir read işleminde write işlemini beklemek zorunda kalmayız.
- Her ekibin farklı Domain Logic’i üzerinde çalışabileceği bir yapı kurulmasına yardımcı olabilir.

### CQRS’in Dezavantajları
- Kod karmaşıklığını arttırır.
- Event bazlı bir yapıya sahipseniz, uygulamanızın queue’da yer alan hataları ve tekrarlanan işlemleri yönetebilmesi gerekmektedir. Olası failover senaryolarını düşünmediğinizde veri kaybı veya daha büyük sorunlarla karşılaşabilirsiniz.

---

## Mediator Design Pattern

- **Mediator Pattern**: Aynı interface üzerinden türeyen nesneler arasındaki iletişimi, tek bir nokta üzerinden sağlar. Örnek vermek gerekirse; uçakların hepsi kule ile iletişime geçer, birbirleriyle doğrudan iletişime geçmezler. Bu örnekte, Mediator nesnesi kule, uçaklar da türeyen sınıflar diyebiliriz.

- **MediatR**: Mediator Pattern’inin kullanılmasını sağlayan bir kütüphanedir. (.NET)

<img width="831" height="498" alt="image" src="https://github.com/user-attachments/assets/3e3b6e1d-ba62-4f15-8030-8928719d6cf6" />

- .Net Core projesi oluşturup MediatR kütüphanesini ve bağımlılıklarını yükleme:

```csharp
dotnet add package MediatR
dotnet add package MediatR.Extensions.Microsoft.DependencyInjection
```

### Model

```charp
public class Customer
{
    public int Id { get; set; }
    public string Name { get; set; } = "";
    public string Email { get; set; } = "";
}
```

### Repository

```charp
public interface ICustomerRepository
{
    Task<Customer?> GetByIdAsync(int id);
    Task<IEnumerable<Customer>> GetAllAsync();
    Task AddAsync(Customer customer);
    Task DeleteAsync(int id);
}
```


### Queries

Tek müşteri getir

```charp
using MediatR;

public record GetCustomerByIdQuery(int Id) : IRequest<Customer?>;
```

Tüm müşterileri getir

```charp
using MediatR;

public record GetAllCustomersQuery() : IRequest<IEnumerable<Customer>>;
```

### Commands

Yeni müşteri oluştur

```charp
using MediatR;

public record CreateCustomerCommand(string Name, string Email) : IRequest<int>;
```


Müşteri sil

```charp
using MediatR;

public record DeleteCustomerCommand(int Id) : IRequest;
```


### Handlers

Query Handler

```charp
public class GetCustomerByIdQueryHandler 
    : IRequestHandler<GetCustomerByIdQuery, Customer?>
{
    private readonly ICustomerRepository _repository;

    public GetCustomerByIdQueryHandler(ICustomerRepository repository)
    {
        _repository = repository;
    }

    public async Task<Customer?> Handle(GetCustomerByIdQuery request, CancellationToken cancellationToken)
    {
        return await _repository.GetByIdAsync(request.Id);
    }
}
```



Command Handler

```charp
public class CreateCustomerCommandHandler 
    : IRequestHandler<CreateCustomerCommand, int>
{
    private readonly ICustomerRepository _repository;

    public CreateCustomerCommandHandler(ICustomerRepository repository)
    {
        _repository = repository;
    }

    public async Task<int> Handle(CreateCustomerCommand request, CancellationToken cancellationToken)
    {
        var customer = new Customer
        {
            Name = request.Name,
            Email = request.Email
        };

        await _repository.AddAsync(customer);

        return customer.Id; // kaydedilen müşteri Id’si döner
    }
}
```

### Program.cs içinde MeditR kaydı

```charp
builder.Services.AddMediatR(cfg => 
    cfg.RegisterServicesFromAssembly(typeof(Program).Assembly));
```

### Örnek bir mediator kullanımı

```charp
[ApiController]
[Route("api/[controller]")]
public class CustomersController : ControllerBase
{
    private readonly IMediator _mediator;

    public CustomersController(IMediator mediator)
    {
        _mediator = mediator;
    }

    [HttpGet("{id}")]
    public async Task<IActionResult> GetById(int id)
    {
        var result = await _mediator.Send(new GetCustomerByIdQuery(id));
        return result is null ? NotFound() : Ok(result);
    }

    [HttpGet]
    public async Task<IActionResult> GetAll()
    {
        var result = await _mediator.Send(new GetAllCustomersQuery());
        return Ok(result);
    }

    [HttpPost]
    public async Task<IActionResult> Create([FromBody] CreateCustomerCommand command)
    {
        var newId = await _mediator.Send(command);
        return CreatedAtAction(nameof(GetById), new { id = newId }, null);
    }

    [HttpDelete("{id}")]
    public async Task<IActionResult> Delete(int id)
    {
        await _mediator.Send(new DeleteCustomerCommand(id));
        return NoContent();
    }
}
```
---

### Bu yapının sonucunda:

- Controller → sadece API giriş noktası olur.

- Command & Query → veriyi işlemek için ayrı nesneler kullanılır.

- Handler → iş mantığını içerir.

- MediatR → istekleri ilgili handler’a yönlendirir.

**Sonuçta**: Daha okunabilir, bakımı kolay, test edilebilir ve genişlemeye açık bir mimari elde edilir.

### Sonuç
Event üzerinden işlemlerin yürütüldüğü sistemlerde transactional bağımlılık olmadığı için okuma ve yazma eylemleri birbirlerini beklemezler. Bu sebeple de CQRS altyapısı performansın önemli olduğu yerlerde kullanılmaktadır.
CQRS ile yazılım geliştirme maliyetli bir yöntemdir. Doğru yerde kullanılması halinde, geliştirilen sistemin bakımının yapılması ve sürdürülebilir şekilde olması daha kolay olacaktır. Bu sebeple, her yazılım geliştirme deseninde olduğu gibi gerektiği yerde kullanılması gerekmektedir.




Sonuç olarak CQRS ve MediatR birlikte kullanıldığında, sorumlulukların ayrımı (Separation of Concerns) sağlanarak kod daha modüler ve test edilebilir hale gelir. Bu yaklaşım, genişlemeye uygun bir altyapı oluştururken aynı zamanda validasyon, logging, caching gibi ortak davranışların pipeline behavior’lar aracılığıyla merkezi bir şekilde yönetilmesine imkân tanır. Böylece özellikle orta ve büyük ölçekli projelerde sürdürülebilir, temiz ve profesyonel bir mimari elde etmek mümkün olur.


# KAYNAKÇA
- https://sefikcankanber.medium.com/cqrs-command-query-responsibility-segregation-nedir-16b196376389 
- https://www.dotnetcurry.com/patterns-practices/1461/command-query-separation-cqs  -> CQS için detaylı bilgi
- https://learn.microsoft.com/en-us/azure/architecture/patterns/cqrs
- https://medium.com/@berkaybasoz/cqrs-command-query-responsibility-segregation-nedir-fd94882f195e
- https://www.geeksforgeeks.org/system-design/cqrs-command-query-responsibility-segregation/
- https://eryilmaz0.medium.com/mediatr-nedir-4913b99784dd
- https://medium.com/@mugrcn/asp-net-core-mediatr-ile-cqrs-pattern-uygulamas%C4%B1-c0dd8217ac89
- https://medium.com/@darshana-edirisinghe/cqrs-and-mediator-design-patterns-f11d2e9e9c2e
- https://www.gencayyildiz.com/blog/cqrs-pattern-nedir-mediatr-kutuphanesi-ile-nasil-uygulanir/#google_vignette
- https://www.milanjovanovic.tech/blog/cqrs-pattern-with-mediatr
- https://codewithmukesh.com/blog/cqrs-and-mediatr-in-aspnet-core/
- https://www.c-sharpcorner.com/article/cqrs-pattern-using-mediatr-in-net-5/
- https://code-maze.com/cqrs-mediatr-in-aspnet-core/
