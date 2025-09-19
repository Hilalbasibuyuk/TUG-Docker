# TUG-Docker
## ORM 
ORM(Object to Relational Mapping), Nesne ile İlişkisel Eşleme olarak açabiliriz. İlişkisel veri tabanı ile uygulama içerisinde kullandığımız modelleri/nesneleri birbirine bağlama tekniğidir. Db objelerinin kod tarafında bir replikası bir yansıması var gibi düşünebilirsiniz. ORM bu mapleme tekniğinin adıdır. ORM'i uygulamak için kullandığımız yazılımlara da ORM Araçları diyoruz. ORM araçları ilişkisel veritabanları ve uygulama arasındaki köprüdür.

 ORM tekniği çoğu nesne yönelimli programlama dillerinde kullanılabilir.

<img width="781" height="414" alt="image" src="https://github.com/user-attachments/assets/8bb889f5-b266-4aad-b2c5-2ea6665be159" />

**Dillere göre ORM Araçları**
**C#** : Entity Framework, Dapper
**Java** : Hibernate, JPA, MyBatis
**Phyton** : Django, Storm
**PHP** : PdoMap, CakePHP
**Nodejs** : Sequelize, Mongoose


**En çok kullanılan ORM araçları**
- Entity Framework
- Entity Framework Core
- Dapper
- nHibernate


**ORM Araçlarının Avantajları:**
- Database teknolojisine olan bağımlılığını ortadan kaldırır. Uygulama sadece ORM'i bilir. Database hakkında fikri yoktur.
- SQL/TSQL/PLSQL bilmeden çok kısa bir zamanda db işlemlerini çok daha az kod yazarak yapabilirsiniz.
- Nesne yönelimli kod yazmayı destekler.
- ORM Araçlarının çoğu açık kaynak kodludur.


**ORM Araçlarının Dezavantajları:**
- Performans sorunları yaratabilir. DB'ye bağlanıp sql çalıştırmak her zaman için daha performanslıdır.
- Orm araçlarının oluşturduğu sql lere müdahale edemezsiniz. Kontrolü developer'dan alır.
- Orm aracını öğrenmek için de zamana ihtiyacınız vardır.


**ORM modelleme yaklaşımları 3'e ayrılır:**
- DB First Yaklaşım
- Code First Yaklaşım
- Model First Yaklaşım




# KAYNAKÇA
- https://academy.patika.dev/courses/net-core/2-orm-ve-ef-core
- https://medium.com/kodluyoruz/orm-nedir-orm-ara%C3%A7lar%C4%B1-ve-yakla%C5%9F%C4%B1mlar%C4%B1-nelerdir-37af94ee873c
- https://medium.com/@orkunkayman/orm-object-relational-mapping-nedir-e8acc7e11491
- https://www.fatihbaytar.com.tr/post/object-relational-mapping-orm-nedir
- https://www.ozzacademy.com/orm-object-relational-mapping-nedir/
- https://www.freecodecamp.org/news/what-is-an-orm-the-meaning-of-object-relational-mapping-database-tools/
- https://www.tutorialspoint.com/entity_framework/index.htm

