# Log Reader

Bu proje, **çift bağlı liste** veri yapısını kullanarak **Linux syslog** dosyasını okur ve ileri/geri yönde logları ekrana yazdırır.

## Özellikler
- **Çift bağlı liste veri yapısı** kullanılarak log verileri bellekte saklanır.
- **Dinamik bellek yönetimi** ile belleğin etkin kullanımı sağlanır.
- **İleri ve geri yönde okuma** özelliği ile logların ters sıralı analizi mümkündür.
- **Dosya okuma işlemi** ile `/var/log/syslog` dosyasından satır satır log verisi çekilir.
- **Bellek temizleme mekanizması** sayesinde dinamik olarak tahsis edilen bellek serbest bırakılır.

## Derleme ve Çalıştırma
```sh
gcc log_reader.c -o log_reader
sudo ./log_reader
```

**Not:** `/var/log/syslog` dosyasına erişmek için root yetkisi gerekebilir.

## Kod Açıklaması
- **`addLog()`**: Yeni bir log düğümü oluşturur ve bağlı listeye ekler.
- **`printLogsForward()`**: Logları eklenme sırasına göre ekrana yazdırır.
- **`printLogsBackward()`**: Logları ters sırayla ekrana yazdırır.
- **`freeList()`**: Bellekte tahsis edilen düğümleri serbest bırakır.
- **`main()`**:
  - `/var/log/syslog` dosyasını açar ve satır satır okur.
  - Okunan her satırı çift bağlı listeye ekler.
  - Logları hem ileri hem de geri yönde yazdırır.
  - Belleği temizleyerek işlemi tamamlar.

## Gereksinimler
- **Linux işletim sistemi** (Çünkü `/var/log/syslog` dosyası Linux'a özeldir.)
- **GCC Derleyici** (`sudo apt install gcc` ile yüklenebilir.)

## Örnek Kullanım
```sh
sudo ./log_reader
```
Çıktı:
```
İleri yönde loglar:
Feb 22 10:00:00 kernel: [ 0.000000] Linux version 5.15.0...
...

Geri yönde loglar:
...
Feb 22 10:00:00 kernel: [ 0.000000] Linux version 5.15.0...
```

## Katkıda Bulunma
Pull request'ler memnuniyetle karşılanır. Büyük değişiklikler için lütfen önce bir tartışma başlatın.

## Lisans
Bu proje **MIT Lisansı** ile lisanslanmıştır.

