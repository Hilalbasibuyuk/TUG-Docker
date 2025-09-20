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

- .Net Core Web Api projesi oluşturup MediatR kütüphanesini ve bağımlılıklarını yükleme:

```csharp
dotnet add package MediatR --version 9.0.0
dotnet add package MediatR.Extensions.Microsoft.DependencyInjection --version 9.0.0
```
- Startup sınıfında ConfigureServices metodunda MediatR’ı ekleme:

```csharp
services.AddMediatR(typeof(Startup));
```




### Sonuç
Event üzerinden işlemlerin yürütüldüğü sistemlerde transactional bağımlılık olmadığı için okuma ve yazma eylemleri birbirlerini beklemezler. Bu sebeple de CQRS altyapısı performansın önemli olduğu yerlerde kullanılmaktadır.
CQRS ile yazılım geliştirme maliyetli bir yöntemdir. Doğru yerde kullanılması halinde, geliştirilen sistemin bakımının yapılması ve sürdürülebilir şekilde olması daha kolay olacaktır. Bu sebeple, her yazılım geliştirme deseninde olduğu gibi gerektiği yerde kullanılması gerekmektedir.




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
