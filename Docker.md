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

### Terminale yazdığımız bu komut ile Ubuntu image'ini yükleriz

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

- it (i = interactive, t = tty) -> i - STDIN’i açık tutar, yani container’a komut girebilirsin., t - Bir terminal (pseudo-TTY) sağlar.
- Sonuç, Ubuntu image’inden açılan container’ın içine interaktif bir bash shell ile düşersin. **root@<container_id>:/#** Böyle bir terminal başlangıcı görünür.
 
```bash
docker run -it ubuntu
```

### exit komutu ile çıkabiliriz

```bash
exit
```



# KAYNAKÇA
- https://medium.com/batech/docker-nedir-docker-kavramlar%C4%B1-avantajlar%C4%B1-901b37742ee0
- https://academy.patika.dev/courses/deployment/what-is-docker
- https://medium.com/devopsturkiye/docker-nedir-avantajlar%C4%B1-cab6d72e1fcf
- https://www.ihsteknoloji.com/blog/docker-nedir/
- https://bulutistan.com/blog/docker-nedir/
- https://www.docker.com/  -> Docker indirme linki
- https://hub.docker.com/  -> Docker Hub
