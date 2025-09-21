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



# KAYNAKÇA
- https://medium.com/batech/docker-nedir-docker-kavramlar%C4%B1-avantajlar%C4%B1-901b37742ee0
- https://academy.patika.dev/courses/deployment/what-is-docker
- https://medium.com/devopsturkiye/docker-nedir-avantajlar%C4%B1-cab6d72e1fcf
- https://www.ihsteknoloji.com/blog/docker-nedir/
- https://bulutistan.com/blog/docker-nedir/
