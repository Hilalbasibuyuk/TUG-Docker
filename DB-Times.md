# Zaman Temsilleri: Unix Time, Windows Time, Windows File Time, Julian Date Time

Bu belgede farklı sistemlerde kullanılan zaman temsil biçimleri açıklanmaktadır.

---

## 1. Unix Time = Unix Timestamp
- **Tanım**: Unix/Linux sistemlerinde kullanılan zaman standardı. Bu tarihe "Unix Epoch" veya "POSIX time" da denir.
- **Epoch (başlangıç noktası)**: `01 Ocak 1970 00:00:00 UTC` (Greenwich Ortalama Saati)
- **Neden bu tarih?**: Unix işletim sisteminin ilk versiyonlarının geliştirildiği zamanlar yaklaşık olarak 1970'tir. Bu tarih, birçok erken dönem bilgisayar sistemi için uygun bir referans noktası olarak seçilmiştir.
- **Birim**: Saniye (bazı sistemlerde milisaniye veya mikrosaniye de olabilir).
- **Özellik**: 32-bit signed integer(Tam sayı) ile tutulduğunda **2038 yılı problemi**(Zaman Sonu) yaşanır.

**2038 yılı problemi:** İşaretli 32-bit integer'ın maksimum değeri 2,147,483,647'dir. Bu sayı, 19 Ocak 2038 tarihinde saat 03:14:07 UTC'ye denk gelir. Bu saniyeden sonra, sayı taşacak ve negatif olarak yorumlanarak sistemler 13 Aralık 1901'i göstermeye başlayacaktır.
- **Çözüm:** Modern sistemlerin çoğu, bu sorunu aşmak için zaman damgasını 64-bit integer olarak saklamaya başlamıştır. 64-bit bir sistemde zamanın taşması için 292 milyar yıl gerekir, bu da pratikte sorunsuz olduğu anlamına gelir.

**Zaman Dilimi (Timezone) Bağımsızlığı:** Unix Time her zaman UTC (Coordinated Universal Time) baz alınarak hesaplanır. Bu, dünyanın neresinde olursanız olun aynı an için aynı zaman damgasının üretilmesi anlamına gelir. Yerel saate çevirme işlemi, zaman damgasına sahip olduktan sonra yapılır. Örneğin, Türkiye'de (UTC+3) yaz saati uygulaması varsa, zaman damgasına 10.800 saniye (3 saat) eklenerek yerel saat bulunur.

### Neden Bu Kadar Popüler?
- Basitlik: Zamanı tek bir sayıyla ifade etmek, karmaşık tarih ve saat formatlarından çok daha kolaydır.
- Hesap Kolaylığı: Zaman farklarını hesaplamak inanılmaz derecede basittir. İki olay arasında geçen süreyi bulmak için sadece iki zaman damgasını birbirinden çıkarırsınız.
- Evrensellik: Tüm dünyada aynı şekilde çalışır. Zaman dilimi karmaşası yoktur.
- Programlama Dostu: Hemen hemen tüm programlama dilleri ve veritabanı sistemleri Unix Time'ı işlemek için yerleşik fonksiyonlara sahiptir.
- Sıralama ve Karşılaştırma: İki tarihin hangisinin daha eski veya daha yeni olduğunu anlamak için sayısal karşılaştırma yapmak yeterlidir.


### Örnek:  
- `0` → `1970-01-01 00:00:00 UTC`  
- `1633046400` → `2021-10-01 00:00:00 UTC`
- Javascript'te, Math.floor(Date.now() / 1000)
- Python'da, time.time()
- PHP'de, time()
- Linux Terminalinde: date +%s
### Başka bir dönüşüm örneği:

UTC: 20 Eylül 2024, 12:33:20
UTC+3 (Türkiye Yaz Saati): 20 Eylül 2024, 15:33:20


### Sınırlamaları
- İnsan Tarafından Okunamaz: 1726850000 sayısına bakıp hangi tarih olduğunu anlamak imkansızdır. Her zaman bir dönüşüm gerektirir.

- 2038 Sorunu: Halen birçok gömülü sistemde 32-bit kullanıldığı için bu bir tehdit olmaya devam etmektedir.

- Sıçrama Saniyeleri (Leap Seconds): UTC'ye bazen astronomik zamanı senkronize tutmak için "sıçrama saniyeleri" eklenir. Unix Time genellikle bu saniyeleri görmezden gelerek her günü tam olarak 86.400 saniye kabul eder. Bu, yüksek hassasiyet gerektiren bilimsel uygulamalarda küçük sapmalara neden olabilir.

---

## 2. Windows Time Servisi(w32time)
- **Tanım**: Windows Time Servisi, ağ üzerindeki zaman senkronizasyonunu sağlayan sistem servisidir.
- **Görevi**: Bilgisayarın sistem saatini otomatik olarak doğru tutmak. Bunu, ağdaki diğer cihazlarla ya da internet üzerindeki zaman sunucularıyla (NTP – Network Time Protocol) senkronize ederek yapar.
- **Servis Adı**: w32time. Çalıştığı process: **svchost.exe**. Servis olarak başlatılır: **net start w32time**.
- **Epoch (başlangıç noktası)**: `01 Ocak 1601 00:00:00 UTC`
- **Birim**: 100-nanosecond (tick) = 10⁻⁷ saniye.
- **Özellik**: 1601 yılından 30828 yılına kadar tarih aralığını destekler.
- Ağ güvenliği, log analizi ve sistem uyumu için kritik öneme sahiptir.


### Çalışma Mimarisi
- Domain Ortamı: İnternet NTP Sunucuları → PDC Emulator → Diğer DC'ler → Client Makineler
- Workgroup Ortamı: İnternet NTP Sunucuları → Lokal Windows Makinesi

### Önemli Komutlar
- Zaman durumunu sorgulama: w32tm /query /status, w32tm /query /configuration
- Manuel senkronizasyon: w32tm /resync, w32tm /resync /rediscover
- Zaman kaynağını değiştirme: w32tm /config /syncfromflags:manual /manualpeerlist:"time.windows.com", w32tm /config /update

### Temel komutlar

### Servisi yeniden başlat

```bash
net stop w32time
net start w32time
```

### Hemen zaman senkronizasyonu yap

```bash
w32tm /resync
```

### Zaman kaynağını görmek için

```bash
w32tm /query /status
w32tm /query /source
```


👉 Örnek:  
- `0` → `1601-01-01 00:00:00 UTC`  
- `132744384000000000` → `2022-01-26 00:00:00 UTC`

---

## 3. Windows File Time
- **Tanım**: Windows işletim sisteminde dosya oluşturulma, değiştirilme ve erişim zamanlarını temsil eden format.
- **Teknik olarak**: Windows File Time = Windows Time formatıdır. Yani `1601-01-01 UTC` bazlıdır.
- **Neden bu tarih?** Bu garip görünen tarihin nedeni tarihseldir. Windows NT'nin tasarlandığı dönemde, 400 yıllık Gregoryen takvim döngüsünü temsil edebilecek bir başlangıç noktası aranıyordu. 1601 yılı, 400 yıllık döngünün başlangıcıdır. Bu, takvim hesaplamalarını büyük ölçüde basitleştirir.
- **Kullanım Alanı**: NTFS dosya sistemi metadata’sı.Event Log kayıtlarının zaman damgaları. Registry (kayıt defteri) değişiklik zamanları. Process oluşturma zamanları. Thread execution timing bilgileri.
- **Veri Tipi**: İşaretsiz 64-bit integer (uint64). Bu, değerin hiçbir zaman negatif olamayacağı anlamına gelir.
- **Zaman Birimi**: 100-ns tick cinsinden tutulur(100 nanosaniye). 1 saniye = 10.000.000 (10 milyon) File Time birimi, 1 milisaniye = 10.000 File Time birimi, 1 mikrosaniye = 10 File Time birimi.
- **Max Değer**: 0xFFFFFFFFFFFFFFFF (18,446,744,073,709,551,615). Bu değer yaklaşık 28.554 yılına kadar gider. Pratikte bir sınırlama oluşturmaz


### C# ile FileTime örnekleri:
```csharp
// Şu anki zamanı File Time'a çevirme
long fileTime = DateTime.UtcNow.ToFileTimeUtc();

// File Time'dan DateTime'a çevirme
DateTime dateTime = DateTime.FromFileTimeUtc(133776303209301291);

// Dosya zaman bilgilerini okuma
DateTime creationTime = File.GetCreationTimeUtc("dosya.txt");
DateTime lastWriteTime = File.GetLastWriteTimeUtc("dosya.txt");
```

### Powershell ile Zaman İşlemleri:
```powershell
# File Time'dan okunabilir zamana dönüşüm
[DateTime]::FromFileTime(133776303209301291)

# Dosya zaman bilgilerini görüntüleme
Get-Item "dosya.txt" | Select-Object CreationTime, LastWriteTime, LastAccessTime

# Zaman servisi durumunu kontrol
Get-Service w32time
w32tm /query /status
```

---

## 4. Julian Date Time (Jülyen Takvimi)
- **Tanım**: Astronomi, havacılık ve tarihsel hesaplamalarda kullanılan çok önemli bir zaman sistemidir. Julian Date (JD), astronomide ve diğer bilimsel disiplinlerde zamanı ölçmek için kullanılan sürekli bir zaman sistemidir. Julian Day Number (JDN) ise gün değişimlerini saymak için kullanılır.
- **Neden bu tarih?** Üç önemli döngünün kesiştiği nokta: 28 yıllık Güneş döngüsü, 19 yıllık Ay döngüsü (Metonic cycle), 15 yıllık Indiction cycle (Roma vergi döngüsü)
- **Temel Format**: Gerçek sayı (floating point). **Tam kısım**: Gün sayısını (JDN) temsil eder. **Kesirli kısım**: Gün içindeki zamanı temsil eder
- **Epoch (başlangıç noktası)**: `4713 BC, 1 Ocak, 12:00 TT (Terrestrial Time)`
- **Birim**: Gün.
- **Özellik**: Tarihleri kesintisiz bir sayı doğrusu üzerinde gün cinsinden ifade eder. Yarım gün = 0.5 eklenerek saat hesaplanır.

### Tam Julian Date (JD) Hesaplama:
- JD = JDN + (saat - 12)/24 + dakika/1440 + saniye/86400

### Modern Varyasyonlar:
- Modified Julian Date (MJD)
- Reduced Julian Date (RJD)
- Truncated Julian Date (TJD)


### Kullanım Alanları ve Uygulamalar
- **Astronomi**: Gök cisimlerinin konum hesaplamaları, Yıldız katalogları ve ephemeris hesaplamaları, Telescope scheduling ve observation planning
- **Havacılık ve Uzay**: Uydu yörünge hesaplamaları, Spacecraft navigation, Missile tracking systems
- **Tarihsel Araştırmalar**: Eski takvim dönüşümleri, Tarihsel olayların kronolojisi, Arkeolojik dating methods
- **Bilgisayar Sistemleri**: Yüksek hassasiyetli zaman kaydı, Scientific data recording, Financial market analysis

### Avantajlar ve Dezavantajlar
**Avantajlar**: 
- Süreklilik: Kesintisiz zaman ölçeği
- Kesinlik: Milisaniye hassasiyetinde hesaplama
- Evrensellik: Tüm kültür ve takvimlerden bağımsız
- Basit aritmetik: Zaman farkı hesaplamaları kolay

**Dezavantajlar**:
- İnsan tarafından okunması zor
- Büyük sayı değerleri
- Günlük kullanım için pratik değil


C# Kod Örneği:  

```csharp

using System;

public class JulianDateConverter
{
    // Julian Date başlangıç referansı: 1 Ocak 2000, 12:00:00 UTC = JD 2451545.0
    private static readonly DateTime JulianEpoch = new DateTime(2000, 1, 1, 12, 0, 0, DateTimeKind.Utc);
    private static readonly double JulianEpochJD = 2451545.0;

    /// <summary>
    /// DateTime'ı Julian Date'e dönüştürür
    /// </summary>
    public static double DateTimeToJulianDate(DateTime dateTime)
    {
        // UTC zamanına çevir
        DateTime utcDateTime = dateTime.ToUniversalTime();
        
        // JDN (Julian Day Number) hesapla
        int year = utcDateTime.Year;
        int month = utcDateTime.Month;
        int day = utcDateTime.Day;
        
        double jdn = CalculateJDN(year, month, day);
        
        // Gün içi zamanı ekle (saniye cinsinden)
        double timeFraction = (utcDateTime.Hour * 3600 + 
                             utcDateTime.Minute * 60 + 
                             utcDateTime.Second + 
                             utcDateTime.Millisecond / 1000.0) / 86400.0;
        
        return jdn + timeFraction;
    }

    /// <summary>
    /// Julian Date'i DateTime'a dönüştürür
    /// </summary>
    public static DateTime JulianDateToDateTime(double julianDate)
    {
        // JDN ve zaman fraksiyonunu ayır
        double jdn = Math.Floor(julianDate + 0.5);
        double timeFraction = julianDate + 0.5 - jdn;
        
        // JDN'den tarih hesapla
        var (year, month, day) = CalculateGregorianDate(jdn);
        
        // Zaman bileşenlerini hesapla
        double totalSeconds = timeFraction * 86400.0;
        int hours = (int)(totalSeconds / 3600);
        int minutes = (int)((totalSeconds % 3600) / 60);
        int seconds = (int)(totalSeconds % 60);
        int milliseconds = (int)((totalSeconds - Math.Floor(totalSeconds)) * 1000);
        
        return new DateTime(year, month, day, hours, minutes, seconds, milliseconds, DateTimeKind.Utc);
    }

    private static double CalculateJDN(int year, int month, int day)
    {
        if (month <= 2)
        {
            year--;
            month += 12;
        }
        
        int a = year / 100;
        int b = 2 - a + (a / 4);
        
        return Math.Floor(365.25 * (year + 4716)) + 
               Math.Floor(30.6001 * (month + 1)) + 
               day + b - 1524.5;
    }

    private static (int year, int month, int day) CalculateGregorianDate(double jd)
    {
        double z = Math.Floor(jd + 0.5);
        double w = Math.Floor((z - 1867216.25) / 36524.25);
        double x = Math.Floor(w / 4);
        double a = z + 1 + w - x;
        double b = a + 1524;
        double c = Math.Floor((b - 122.1) / 365.25);
        double d = Math.Floor(365.25 * c);
        double e = Math.Floor((b - d) / 30.6001);
        
        int day = (int)(b - d - Math.Floor(30.6001 * e));
        int month = (int)(e - (e < 13.5 ? 1 : 13));
        int year = (int)(c - (month > 2.5 ? 4716 : 4715));
        
        return (year, month, day);
    }
}
```
---

## 5. Dönüşümler

### Unix → Windows Time
```text
WindowsTime = (UnixTime * 10,000,000) + 116444736000000000
```

### Windows Time → Unix
```text
UnixTime = (WindowsTime - 116444736000000000) / 10,000,000
```

### Julian Date Hesabı (yaklaşık)
```text
JD = UnixTime / 86400 + 2440587.5
```

---

## Özet Karşılaştırma

| Özellik               | Unix Time                        | Windows Time                     | Windows File Time               | Julian Date Time                      |
|------------------------|----------------------------------|----------------------------------|---------------------------------|---------------------------------------|
| Epoch                  | 1970-01-01 00:00:00 UTC         | 1601-01-01 00:00:00 UTC          | 1601-01-01 00:00:00 UTC         | 4713 BC 01-01 12:00 TT                |
| Birim                  | Saniye                          | 100-ns tick                      | 100-ns tick                     | Gün                                    |
| Kullanım               | Unix/Linux, POSIX               | Windows API, .NET                | NTFS dosya zaman damgaları      | Astronomi, bilimsel hesaplamalar       |
| Tarih Aralığı          | 1901 – 2038 (32-bit signed)     | 1601 – 30828                     | 1601 – 30828                    | Binlerce yıl geriye ve ileriye doğru   |

