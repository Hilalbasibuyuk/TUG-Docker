# DOCKER
Docker en net tanımlamayla open source bir ‘container’ teknolojisidir. Docker, aynı işletim sistemi üzerinde, yüzlerce hatta binlerce birbirinden izole ve bağımsız containerlar sayesinde sanallaştırma sağlayan bir teknolojidir.  Docker, yazılımları kitaplıklar, sistem araçları, kod ve çalışma zamanı dâhil olmak üzere yazılımların çalışması için gerekli her şeyi içeren container adlı standartlaştırılmış birimler hâlinde paketler. Web uygulamalarımızın kolayca kurulumunu, testini, çalışmasını ve deploymentını sağlar. Bunun yanında sunucu maliyetlerini önemli ölçüde azaltır.

### Neden ihtiyacımız var?

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/6218b830-bc88-4de1-9eac-fd05ad37005e" />


### Neye ihtiyacımız var?

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/6f24bec1-b99a-4097-b8eb-f91c4b2e40cc" />

### Docker’dan önce işler nasıldı?

Docker dan önce yüksek performanslı bir sunucu üzerine birden fazla sanal makine kurulurdu ve her birine ayrı ayrı işletim sistemi kurulurdu. Docker ile misafir işletim sistemleri (sanal makinelere kurulan işletim sistemleri) artık kurulmuyor. Bunu docker yönetiyor. Böylece her bir uygulama için yeni bir sanal makine ve işletim sistemi kurmaktan kurtuluyoruz.


### Container Teknolojisi nedir?

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5b0d10d9-3e7f-4196-9d8c-ba8b71d18795" />


### Container Türleri
- LXC
- LXD
- LXCFS
**Docker LXC container yöntemini kullanmaktadır.**

Container yönetimi oldukça zor ve low level bir iştir. Docker bu işi kolaylaştırmak için bize high levek birçok araç sunuyor.

### LİNUX CONTAINER
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/ef8af17b-b79c-44f9-a31a-7602af24f004" />



Bir sanal makinenin sunucu donanımını sanallaştırmasına (doğrudan yönetme gereksinimini ortadan kaldırma) benzer şekilde container'lar da bir sunucunun işletim sistemini sanallaştırır. Docker her sunucuya yüklenir ve container'ları oluşturmak, başlatmak veya durdurmak için kullanabileceğiniz basit komutlar sağlar.

### Container VS VM
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/1ccdf05e-e05d-4303-a6b9-fcb70f93f08d" />

---

### Docker Image Nedir?
- İçerisinde birçok farklı yapıyı barındıran yapılardır.(OS, application vb.). Template, plan, packages gibi de düşünülebilir. Docker Hub(Docker'ın public veya private olarak bize sunduğu resmi repository hesabı) içerisindedir. Burada container'ı image'i çalıştırdığımızda elde ettiğimiz process olarak düşünebiliriz. Container çalışmıyorsa uygulama da çalışmaz.

### Docker Hub (Registry)

Sol tarafta yer alan komutlarla, her bir container'ı Docker Host'a taşıyoruz.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/7a05e014-a780-46f3-817b-d7395aae02fc" />


Sol taraftaki uygulamalar (Docker Hub üzerinden çekiyoruz bunları) bir image olarak sağdaki çalışan kısmı ise bir container olarak düşünebiliriz.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/07b875c1-6901-4d70-aa6c-41191dc19093" />

### Image/Container

**docker run ubuntu** diyerek ubuntunun bir container'ını çalıştırmış oluruz ve tekrar bu komutu çalıştırırsak başka bir ubuntu container'ını çalıştırmış oluruz. Diğer image'ler de aynı şekilde çalışır.

- **!!NOT:** "docker run ..." komutunu çalıştırdığımızda eğer Docker Host'ta bulamazsa kendiliğinde Docker Hub'tan pull etme işlevini de otomatik olarak yapar.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/df08493e-8db3-4674-9565-9e8aa40af76e" />


### Aşağıda geliştirme, test, üretim aşamalarında nerede olursa olsun aynı şekilde çalışabilen bir sistem görüyoruz

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/85781982-5e3c-44ff-8719-c7fdb85c3893" />


### Geliştirici DockerFile olmadan DevOps'a gönderirse, DevOps'un hata yapma olasılığı çok yüksek. DockerFile ile bu hata sıfıra iner.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/63597a00-57da-40a9-bf8d-7f4550c07bf0" />

### Kaynakça kısmındaki Docker Hub linki ile containerları indirebilirsiniz(pull edebilirsiniz) 

---

## Command Line Editor (CLI)

### Terminale yazdığımız bu komut ile Ubuntu image'ini Docker Hub'tan çekeriz.(yükleriz)

```bash
docker pull ubuntu
```

### Örneğin mongo image'ini indirmek için bir diğer komut

```bash
docker pull mongo
```

İndirme işlemini pull ile yapıyoruz. Çalıştırma kısmı ise konteynırda olacak. (run komutu ile)

### Örneğin bizde yüklü olmayan konteynırı çalıştırmak istersek run komutu ile, eğer image yoksa kendiliğinden otomatik olarak pull ederek yükler ve çalıştırır.

```bash
docker run redis
```

### Mevcut image'leri görmek için

```bash
docker images
```

Ubuntu bir işletim sistemidir. Biz "docker run ubuntu" komutunu çalıştırırsak görev vermediğimiz için çalışmaz. 

### Mesela 5 saniye çalış sonra kapan komutu:(Çok da işe yarar değildir)

```bash
docker run ubuntu sleep 5
```

### Bir görev vererek ubuntu'nun içine girme örneği(root). 

- it (i = interactive, t = tty) -> i - STDIN’i açık tutar, yani container’a komut girebilirsin., t - Bir terminal (pseudo-TTY) sağlar. (interactive terminal)
- Sonuç, Ubuntu image’inden açılan container’ın içine interaktif bir bash shell ile düşersin. **root@<container_id>:/#** Böyle bir terminal başlangıcı görünür.
 
```bash
docker run -it ubuntu
```

### exit komutu ile çıkabiliriz

```bash
exit
```

### Şu an ayakta olan containerları görmek için: (Container ID, Command, Time, Container Names gibi özellikleri gösterir) (ps - process) (İki komut da aynı sonucu verir)

```bash
docker ps
docker containner ls
```

### Daha önce de açılan containerları görüntülemek için kullanılan komutlar: (Aşağıdaki komutların hepsi aynı sonucu verir)

```bash
docker ps -all
docker ps -a
docker container ls -a
```

### Containerı çalıştırırken containera isim verme komutu: (Burada bash_ubuntu ismini verdik) (Yoksa kafasına göre veriyor isim)

```bash
docker run -it --name bash_ubuntu ubuntu
```

### Docker başlatma verdiğimiz isim ile(arka planda başlar)

```bash
docker start bash_ubuntu
```

### Docker durdurma 

```bash
docker stop bash_ubuntu
```

### Diyelim ki id'nin ilk birkaç karakterini hatırlıyoruz. Eğer aynı id ile başlayan başka bir container yoksa "docker stop b4" gibi bir komutla b4 ile başlayan id'li container'ı durdurabiliriz.

### Bir containerı silmek için(name dışında id ile de silebiliriz) (id'nin ilk birkaç karakteri olsa da siler)

```bash
docker rm bash_ubuntu
```

### Birden çok container silme örneği(id'ler ile)

```bash
docker rm b4 km 2b 55
```


### Bütün containerları silme

```bash
docker container rm $(docker container ls -aq)
```


### TAG - Aşağıdaki komut ile redis'in 5 sürümünü çalıştırmış oluruz. Burada da :'dan sonrası TAG'dir.

```bash
docker run redis:5
```

### Terminalde çalışması bizim terminalde işlem yapmamızı engelliyor. Bu komut ile bize id döndürüyor ve terminalde değil arka planda çalışıyor. Mesela Redis'in arka planda çalışması için komut: (detached mode)

```bash
docker run -d redis
```

### Çalışan container'ın loglarını anlık olarak terminalde görmek için: (Sondaki id)

```bash
docker attach 56cc
```

### Bizim görmediğimiz logları gösteren komut:

```bash
docker container logs 56cc
```


### PORT MAPPING

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f0871dee-ba65-4654-9f99-75050f0ad301" />





**!!! NOT**: Docker Hub'a kendi containerlarımızı da yükleyebiliriz.



### Volume Mapping

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/6a5e2703-4a4a-47e6-8651-58c32dcfd04f" />

Kalıcı olarak verileri kaydetmeyi sağlar.(-v  -> volume)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/51ae70de-66fc-47ee-a0cc-855741674595" />

Docker Desktop üzerinde Docker tarafından belirli olan yollara kayıt edebiliriz. Kafamıza göre vermek istiyorsak Docker'a eklemeliyiz. (Resouces/File Sharing kısmında görebiliriz)


Örnek dosya yolu mongo için:

```bash
docker run -v /opt/data:/data/db -p 27017:27017 mongo
```


!! NOT : Docker Hub'ı containerların dökümantasyonunu okumak için kullanabiliriz. Orada bulabiliriz, o containerı nasıl başlatabiliriz gibi birçok bilgiyi.

### Container hakkında detaylı bir bilgi almak için çalıştırmamız gereken komut(Sona container id veya container name gelir)

```bash
docker inspect 56cc
```

- docker run phpmyadmin/phpmyadmin  -> Bu komutta konteynır verified olmadığı için ilk phpmyadmin kullanıcı adı gibi oluyor. Bu şekilde indiriyoruz.
- docker run -e MYSQL_ROOT_PASSWORD=test123 -d mysql  -> (-e -> env variable) (Bu şekilde çalışacağını Docker Hub dökümantasyonundan öğrendik.)

### İki containerı birbirine bağlama

Bunu iki farklı örnek ile açıklayalım. Bir MySQL ayağa kaldırdığımız bir container'ımız var. Aynı şekilde MySQL'e erişebilecek bir arayüz olan phpMyAdmin olsun. Bu iki container arasında bağlantı kurmamız gerekiyor ki phpMyAdmin MySQL'e bağlanabilsin. Bunu "--link" ile yaparız. 

Burada bağlanılacak containerı ayağa kaldırıyoruz.
```bash
docker run --name mysql-server -p 3306:3306 -e MYSQL_ROOT_PASSWORD=test123 -d mysql
```

Aşağıdaki komutun açıklaması: 
- (--name pmyadmin → Container’a pmyadmin adını verir)
- (--link mysql-server:db → Bu phpMyAdmin container’ını mysql-server adlı başka bir container’a bağlar. İçeride bu bağlantı db host adıyla tanımlanır.)
- (phpmyadmin/phpmyadmin → Çalıştırılacak imajın adı)


```bash
docker run --name pmyadmin -p 8000:80 --link mysql-server:db -d phpmyadmin/phpmyadmin
```

---

## Docker Network Türleri

3 tane network türü vardır. Bridge, None ve Host

- Bridge network türü varsayılandır. (docker run mongo)
- None network türünde containera dışarıdan erişilemez ve container dışarıya erişemez.(docker run mongo --network=none)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5cd604d0-3295-46cd-8f32-ba19dc77a426" />


### Kullanıcı tanımlı network

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/38618e5c-0f1a-4ac7-acf7-0c30eba17418" />

### Bir image'i silmek için

```bash
docker rmi my-ubuntu
```

### Networkleri listelemek için(İkisi de aynı)

```bash
docker network list
docker network ls
```

### Network silmek için

```bash
docker network rm my-network 
```

### Docker içinde özel bir bridge network oluşturma kodu.
Açıklamaları:
- docker network create → Yeni bir ağ (network) oluşturur.
- --driver bridge → Ağ tipini bridge olarak belirler. (Varsayılan ağ türü, container’lar arasında iletişim için kullanılır.)
- --subnet 182.18.0.1/24 → Ağın IP aralığını tanımlar. Burada /24 demek: 182.18.0.0 ile 182.18.0.255 arasındaki adresleri kapsar (toplam 256 adres)
- --gateway 182.18.0.1 → Container’ların bu ağa bağlanırken kullanacağı varsayılan ağ geçidi.
- custom-network → Bu yeni network’e verilen isim.
- 
**Kodda kullanacağımız için name vermek önemli**

  
```bash
docker network create --driver bridge --subnet 182.18.0.1/24 --gateway 182.18.0.1 custom-network
 ```

### Oluşturduğumuz ağ üzerinden çalışmasını sağlama komutu. Db container'ı.

```bash
docker run --name mongo-server --net custom-network -d mongo
```

### Uygulamayı dış dünyaya açıyoruz, yani host makineden http://localhost:3000 ile erişebiliyoruz.(-p 3000:3000 ile)

```bash
docker run --net custom-network -p 3000:3000 gkandemir/todo-app
```

- Bu sayede db ve uygulamayı birbirine link kullanmadan bağlamış olduk.


### GitHub'ımdaki klasördek app-node kısmını kendi klasörümüze kopyalayıp o klasöre geçelim. Aşağıdaki kod bulunduğumuz klasördeki docker'ı build etmekte

```bash
docker build .
```

### Docker'ı build ederken isim vermek istiyorsak: (docker images komutu ile de ismini görebiliriz)

```bash
docker build . -t simple-node-app
```

**NOT** Dockerfile'daki her bir satır layer 1, layer 2... katmanları olarak devam eder. Dockerfile dosyasını kendimiz de oluşturabiliriz ama Docker Hub'da kendiliğinden Dockerfile dosyası  var.

- **.dockerignore dosyası**, Docker imajı build edilirken hangi dosya ve klasörlerin Docker context’e kopyalanmamasını istediğini belirtir.

### Prune -> Çalışmayan (stopped) tüm container’ları topluca silmek için kullanılır.

```bash
docker container prune
```


## Docker Compose

### .yaml dosyası ile işlem yaparız. 
Docker Compose YAML dosyası, birden fazla container’dan oluşan uygulamaları tek bir dosya ile tanımlayıp çalıştırmana yarar. Dosya adı genelde docker-compose.yml veya docker-compose.yaml olur. Her şey YAML formatında yazılır.

- İçinde services, networks, volumes gibi bölümler bulunur.
- services → Çalıştırılacak container’ları tanımlar (örn. web, db).
- networks → Container’ların haberleşeceği ağları tanımlar.
- volumes → Kalıcı veri saklama (örn. MySQL veritabanı) tanımlar.


Build eder(yükler)
```bash
docker-compose build
```

Çalıştırır. Build edilmemişse de build ederek çalıştırır

```bash
docker-compose up
```






# KAYNAKÇA
- https://medium.com/batech/docker-nedir-docker-kavramlar%C4%B1-avantajlar%C4%B1-901b37742ee0
- https://academy.patika.dev/courses/deployment/what-is-docker
- https://medium.com/devopsturkiye/docker-nedir-avantajlar%C4%B1-cab6d72e1fcf
- https://www.ihsteknoloji.com/blog/docker-nedir/
- https://bulutistan.com/blog/docker-nedir/
- https://www.docker.com/  -> Docker indirme linki
- https://hub.docker.com/  -> Docker Hub
