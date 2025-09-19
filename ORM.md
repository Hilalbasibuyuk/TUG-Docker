# ORM
ORM(Object to Relational Mapping), Nesne ile İlişkisel Eşleme olarak açabiliriz. .NET geniş bir geliştirme yelpazede geliştirme araçları sunar ve veri tabanı işlemleri için ORM bu araçlardan biridir. İlişkisel veri tabanı ile uygulama içerisinde kullandığımız modelleri/nesneleri birbirine bağlama tekniğidir. Db objelerinin kod tarafında bir replikası bir yansıması var gibi düşünebilirsiniz. ORM bu mapleme tekniğinin adıdır. ORM'i uygulamak için kullandığımız yazılımlara da ORM Araçları diyoruz. ORM tekniği çoğu nesne yönelimli programlama dillerinde kullanılabilir.

- Özetle, ORM, bir veritabanı tablosunu, programlama dilindeki nesnelerle ilişkilendirir. Böylece geliştiriciler, veritabanına veri eklemek, silmek veya güncellemek gibi işlemleri nesne tabanlı bir yaklaşımla gerçekleştirir.


**NOT!!** Önceden geliştirilen projelerde veri tabanına bağlanmak istenildiğinde eskiden genellikle ADO.NET denilen, veri tabanı işlemlerini SQL sorgusu ile yaptığımız ve veri tabanına uygulama içerisinden bağlanılan bir yöntem kullanılırdı. Nesne tabanlı programlama dillerinin gelişmesi ve yaygınlaşması ile  ADO.NET' in karmaşıklığını basite indiren ve daha okunaklı kod yazılabilmesi için  ORM (Object Relational Mapping) ortaya çıktı.

### ORM’nin Temel Prensipleri
**Nesne ve Tablo İlişkisi: ** ORM, veritabanı tablolarını, yazılımın nesne modeline dönüştürür. Örneğin, bir kullanıcı tablosu (user) veritabanında bir User sınıfına karşılık gelir. Her tablodaki satır, bir nesnenin örneği olur ve her sütun, nesnenin özellikleri (properties) ile eşleşir.

**SQL’den Soyutlama:** ORM, geliştiricinin SQL komutlarını doğrudan yazmasına gerek bırakmadan veritabanı işlemleri yapmasını sağlar. Veritabanına erişim için SQL sorgularını manuel yazmak yerine, ORM araçları otomatik olarak sorguları oluşturur.

**Veri Erişimi ve Yönetimi:** ORM, veritabanı ile etkileşim için sınıflar ve nesneler üzerinden işlem yapılmasını sağlar. Veritabanına veri eklemek, güncellemek, silmek ve sorgulamak gibi işlemler, nesnelerle yapılır ve ORM, bu işlemleri veritabanı diline çevirir.


<img width="781" height="414" alt="image" src="https://github.com/user-attachments/assets/8bb889f5-b266-4aad-b2c5-2ea6665be159" />

Resim kaynakçası -> https://medium.com/kodluyoruz/orm-nedir-orm-ara%C3%A7lar%C4%B1-ve-yakla%C5%9F%C4%B1mlar%C4%B1-nelerdir-37af94ee873c

---

**Dillere göre ORM Araçları**
**C#(.NET)** : Entity Framework(EF), Dapper, NHibernate
**Java** : Hibernate, JPA, MyBatis, JOOQ (Java Object-Oriented Querying)
**Phyton** : Django ORM, Storm, Web2py, SQL Alchemy
**PHP** : PdoMap, CakePHP, Eloquent ORM (Laravel), RedBeanPHP, Doctrine ORM
**Nodejs** : Sequelize, Mongoose
**Ruby**: Active Record


**En çok kullanılan ORM araçları**
- Entity Framework
- Entity Framework Core
- Dapper
- nHibernate


**NOT!! -> Framework, başka kişiler tarafından önceden belli bir amaç için yazılmış, başkalarının kullanımına açılmış kodlara denir.**



**ORM Araçlarının Avantajları:**
- Database teknolojisine olan bağımlılığını ortadan kaldırır. Uygulama sadece ORM'i bilir. Database hakkında fikri yoktur.
- SQL/TSQL/PLSQL bilmeden çok kısa bir zamanda db işlemlerini çok daha az kod yazarak yapabilirsiniz.
- Nesne yönelimli kod yazmayı destekler.
- ORM Araçlarının çoğu açık kaynak kodludur.
- Kod daha temiz ve anlaşılır olur: SQL sorguları yazmak yerine nesnelerle çalışıldığı için kod okunabilirliği artar ve bakım yapmak kolaylaşır.
- Veri Tipi Dönüşümleri ve Hata Azaltma: ORM, veritabanı tiplerini otomatik olarak programlama dili tiplerine çevirir, böylece tip hataları ve manuel dönüşüm ihtiyacı en aza iner.
- İlişkili Verilerle Çalışma Kolaylığı: Tablolar arasındaki ilişkiler nesneler üzerinden yönetildiği için join işlemleri gibi karmaşık sorgular daha basit ve anlaşılır hale gelir.


**ORM Araçlarının Dezavantajları:**
- Performans sorunları yaratabilir. DB'ye bağlanıp sql çalıştırmak her zaman için daha performanslıdır.
- Orm araçlarının oluşturduğu sql lere müdahale edemezsiniz. Kontrolü developer'dan alır.
- Orm aracını öğrenmek için de zamana ihtiyacınız vardır.


### Orm ve veritabanı ilişkileri
ORM, veritabanındaki tablolarla yazılım dilindeki nesneler arasındaki ilişkileri yönetir. Bu ilişkiler genellikle şu şekildedir:

- Bir-bir (One-to-One): Bir nesnenin bir başka nesneyle ilişkili olduğu durumdur. Örneğin, her kullanıcı yalnızca bir profil resmine sahip olabilir.
- Bir-çok (One-to-Many): Bir nesnenin birden fazla nesneyle ilişkili olduğu durumdur. Örneğin, bir kullanıcı birden fazla gönderi (post) yapabilir.
- Çok-çok (Many-to-Many): Bir nesnenin birçok başka nesneyle ilişkili olduğu durumdur. Örneğin, bir öğrenci birçok derse kayıt olabilir ve bir ders birçok öğrenciye sahip olabilir.

---

Şimdi SQL ve ORM arasındaki farkı anlamak için bir SQL kodu ve ORM tabanlı bir framework kodunu karşılaştıralım, Bu kod, SQL kullanarak id’si bilinen bir kullanıcının bilgilerini sorgulamaya yarar.
```sql
"SELECT id, name, email, phone_number FROM users WHERE id = 5"
```

Bu kod da aynı işleve sahipken çok daha kısadır ve nesne tabanlı olmasından dolayı users nesnesinin GetById() fonksiyonu ile bütün bilgilerini görebilir:
```sql
users.GetById(5)
```


**ORM modelleme yaklaşımları 3'e ayrılır:**
- DB First Yaklaşım (Database öncelikli paylaşım)
- Code First Yaklaşım (Kod öncelikli paylaşım)
- Model First Yaklaşım (Model öncelikli paylaşım)


### DB First Yaklaşım
Bu yaklaşımda, var olan bir veri tabanı şeması ele alınır ve bu şema nesne modellerine dönüştürülür. Veri tabanında değişiklikler yapmak istendiğinde SQL de el ile yani manuel olarak değişiklikler yapıldıktan sonra modele aktarılır.

### Code First Yaklaşım
Bu yaklaşımda öncelikle entityler için sınıflar oluşturulur ve daha sonra bu sınıflar arasında veri tabanı için ilişkiler oluşturulur. Sınıfların içindeki propertyler kolon olarak, sınıflar tablo alarak veri tabanına aktarılır.

### Model First Yaklaşım
Bu yaklaşımda, model, grafiksel bir ara yüz veya XML tabanlı bir dosya olarak tanımlanabilir. Önce yeni bir model oluşturmaya sonra o modelden bir veri tabanı şeması oluşturmaya izin verir. Bu yöntemde daha çok design ile çalışılır.

---

## N+1 Problemi Nedir
Eğer ORM fonksiyonunu yanlış şekilde kullanırsak aslında 1(bir) SQL sorgusu ile yapabileceğimiz bir sorguyu, sorgumuzdan kaç adet satır döndüyse (yani N adet) o kadar fazla SQL sorgusu ile yapıyoruz.Yani, ORM ile ilişkili veriler çekilirken fazladan sorguların oluşmasıdır.

- **1 sorgu**: Ana tabloyu çekmek için atılır.
- **N sorgu**: Her bir satırın ilişkili verisini almak için ayrı ayrı atılır.

Bu da toplamda **N+1 sorgu** çalışmasına neden olur.

---

## Örnek Senaryo
Bir kullanıcının birden fazla gönderisi (Post) olduğunu varsayalım.

### Entity Tanımları
```csharp
public class User
{
    public int Id { get; set; }
    public string Name { get; set; }
    public ICollection<Post> Posts { get; set; }
}

public class Post
{
    public int Id { get; set; }
    public string Title { get; set; }
    public int UserId { get; set; }
    public User User { get; set; }
}
```

### N+1 Probleminin Oluştuğu Kod
```csharp
using (var context = new AppDbContext())
{
    var users = context.Users.ToList(); // 1. sorgu (Users tablosu)

    foreach (var user in users)
    {
        var posts = user.Posts.ToList(); // Her kullanıcı için 1 sorgu (N sorgu)
        Console.WriteLine($"{user.Name} - {posts.Count} post");
    }
}
```

- İlk satırda `Users` tablosu için **1 sorgu** atılır.
- Döngüde her `user.Posts` erişiminde **ayrı bir SQL sorgusu** atılır.
- 100 kullanıcı varsa toplamda **101 sorgu** oluşur.

---

## Çözüm: Eager Loading (`Include`)

Entity Framework ile ilişkili verileri tek seferde çekmek için `Include` kullanılır.

```csharp
using Microsoft.EntityFrameworkCore;

using (var context = new AppDbContext())
{
    var users = context.Users
                       .Include(u => u.Posts)
                       .ToList(); // Tek sorgu ile Users + Posts alınır

    foreach (var user in users)
    {
        Console.WriteLine($"{user.Name} - {user.Posts.Count} post");
    }
}
```

Bu şekilde hem kullanıcılar hem de gönderileri **tek bir SQL sorgusu** ile çekilir. N+1 problemi ortadan kalkar.

---

## Sonuç
- ORM'ler işimizi kolaylaştırır fakat farkında olmadan **N+1 problemi** yaratabiliriz.
- Çözüm için:
  - **Eager Loading (`Include`)**
  - **Explicit Loading**
  - **Projection (`Select`)**
  gibi yöntemler kullanılmalıdır.


# KAYNAKÇA
- https://academy.patika.dev/courses/net-core/2-orm-ve-ef-core
- https://medium.com/kodluyoruz/orm-nedir-orm-ara%C3%A7lar%C4%B1-ve-yakla%C5%9F%C4%B1mlar%C4%B1-nelerdir-37af94ee873c
- https://medium.com/@orkunkayman/orm-object-relational-mapping-nedir-e8acc7e11491
- https://www.fatihbaytar.com.tr/post/object-relational-mapping-orm-nedir
- https://www.ozzacademy.com/orm-object-relational-mapping-nedir/
- https://www.freecodecamp.org/news/what-is-an-orm-the-meaning-of-object-relational-mapping-database-tools/
- https://www.tutorialspoint.com/entity_framework/entity_code_first_approach.htm - Kod öncelikli yaklaşım
- https://www.tutorialspoint.com/entity_framework/entity_database_first_approach.htm - Veritabanı öncelikli yaklaşım
- https://www.tutorialspoint.com/entity_framework/entity_model_first_approach.htm - Model öncelikli yaklaşım
- https://www.soltrabilisim.com.tr/entity-framework-code-first-avantajlar/
- https://medium.com/@utkucanbykl/orm-ve-n-1-problemi-79ec4135290b

