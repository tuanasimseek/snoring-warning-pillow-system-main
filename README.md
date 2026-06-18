# Horlama Algılamalı Robot Kol Sistemi

Bu proje, horlama sesini yapay zekâ modeliyle algılayan ve horlama tespit edildiğinde motorlarla oluşturulan robot kol mekanizmasını hareket ettiren bir uyarı sistemidir.

## Projenin Amacı

Uyku sırasında meydana gelen horlamayı otomatik olarak algılamak ve robot kolu hareket ettirerek kullanıcıya fiziksel bir uyarı vermek amaçlanmıştır.

## Nasıl Çalışır?

1. Mikrofon ortam sesini kaydeder.
2. Ses, 16 kHz örnekleme hızında işlenir.
3. Ses verisinden Mel-spektrogram özellikleri çıkarılır.
4. Eğitilmiş CNN modeli sesin horlama olup olmadığını belirler.
5. Horlama algılandığında kontrol kartına komut gönderilir.
6. Motorlar çalıştırılarak robot kol hareket ettirilir.

## Sistem Akışı

```text
Mikrofon
   ↓
Ses Kaydı
   ↓
Mel-Spektrogram Dönüşümü
   ↓
CNN Modeli
   ↓
Horlama Tespiti
   ↓
Mikrodenetleyici
   ↓
Motorlar ve Robot Kol
```

## Kullanılan Teknolojiler

- Python
- TensorFlow ve Keras
- Librosa
- NumPy
- Scikit-learn
- SoundDevice
- Arduino veya uyumlu mikrodenetleyici
- Servo/DC motorlar

## Veri Seti

Model eğitiminde toplam 1.000 adet, bir saniye uzunluğunda ses kaydı kullanılmıştır.

- 500 horlama sesi
- 500 horlama dışı ortam sesi

Horlama dışı sesler; konuşma, yağmur, televizyon, saat, siren, bebek ağlaması ve motor titreşimi gibi farklı ortam seslerini içermektedir.

## Modelin Eğitilmesi

Ses kayıtları Mel-spektrogramlara dönüştürülerek iki boyutlu bir CNN modeline verilmiştir. Verilerin %80'i eğitim, %20'si doğrulama için kullanılmıştır.

Modeli eğitmek için:

```bash
python train.py
```

Eğitim tamamlandığında model aşağıdaki dosyaya kaydedilir:

```text
snoring_model.h5
```

## Gerçek Zamanlı Test

Gerekli kütüphaneleri yükleyin:

```bash
pip install tensorflow librosa numpy scikit-learn sounddevice
```

Mikrofondan gerçek zamanlı horlama tespiti yapmak için:

```bash
python test.py
```

Program beş saniyelik ses kaydı alır, kaydı birer saniyelik parçalara böler ve tahminlerin ortalamasını hesaplar.

Programı durdurmak için `Ctrl+C` tuşlarına basabilirsiniz.

## Dosya Yapısı

```text
Snoring Dataset/
├── train.py              # CNN modelinin eğitim kodu
├── test.py               # Mikrofonla gerçek zamanlı test
├── snoring_model.h5      # Eğitilmiş model
└── Snoring_dataset.txt   # Veri seti açıklaması
```

## Donanım

- Mikrofon
- Arduino veya uyumlu kontrol kartı
- Robot kol mekanizması
- Servo veya DC motorlar
- Motor sürücü devresi
- Harici güç kaynağı
- Bağlantı kabloları

Motorlar kontrol kartından doğrudan beslenmemelidir. Uygun motor sürücüsü ve harici güç kaynağı kullanılmalıdır.

