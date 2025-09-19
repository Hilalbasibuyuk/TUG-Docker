# Zaman Temsilleri: Unix Time, Windows Time, Windows File Time, Julian Date Time

Bu belgede farklı sistemlerde kullanılan zaman temsil biçimleri açıklanmaktadır.

---

## 1. Unix Time
- **Tanım**: Unix/Linux sistemlerinde kullanılan zaman standardı.
- **Epoch (başlangıç noktası)**: `01 Ocak 1970 00:00:00 UTC`
- **Birim**: Saniye (bazı sistemlerde milisaniye veya mikrosaniye de olabilir).
- **Özellik**: 32-bit signed integer ile tutulduğunda **2038 yılı problemi** yaşanır.

👉 Örnek:  
- `0` → `1970-01-01 00:00:00 UTC`  
- `1633046400` → `2021-10-01 00:00:00 UTC`

---

## 2. Windows Time
- **Tanım**: Windows işletim sistemlerinde kullanılan zaman ölçüm sistemi.
- **Epoch (başlangıç noktası)**: `01 Ocak 1601 00:00:00 UTC`
- **Birim**: 100-nanosecond (tick) = 10⁻⁷ saniye.
- **Özellik**: 1601 yılından 30828 yılına kadar tarih aralığını destekler.

👉 Örnek:  
- `0` → `1601-01-01 00:00:00 UTC`  
- `132744384000000000` → `2022-01-26 00:00:00 UTC`

---

## 3. Windows File Time
- **Tanım**: Windows işletim sisteminde dosya oluşturulma, değiştirilme ve erişim zamanlarını temsil eden format.
- **Teknik olarak**: Windows File Time = Windows Time formatıdır. Yani `1601-01-01 UTC` bazlıdır ve 100-ns tick cinsinden tutulur.
- **Kullanım Alanı**: NTFS dosya sistemi metadata’sı.

👉 C yapısında gösterimi:
```c
typedef struct _FILETIME {
  DWORD dwLowDateTime;
  DWORD dwHighDateTime;
} FILETIME;
```

---

## 4. Julian Date Time
- **Tanım**: Astronomi ve bilimsel hesaplamalarda kullanılan sürekli zaman sayımı sistemidir.
- **Epoch (başlangıç noktası)**: `4713 BC, 1 Ocak, 12:00 TT (Terrestrial Time)`
- **Birim**: Gün.
- **Özellik**: Tarihleri kesintisiz bir sayı doğrusu üzerinde gün cinsinden ifade eder. Yarım gün = 0.5 eklenerek saat hesaplanır.

👉 Örnek:  
- `JD 2451545.0` → `2000-01-01 12:00 TT` (J2000 epoch)

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

