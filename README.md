# Asset Maker — Oyun Asset Üretim Aracı

Tasarım tanımından arka plan, eşya, karakter, parçacık ve obje görselleri üreten, internetsiz çalışan bir Windows masaüstü uygulaması. Model bir kez kurulduktan sonra her şey yerel ekran kartında çalışır.

> 🔒 Kaynak kod şimdilik kapalı. Bu depo projeyi tanıtmak için var.

![C#](https://img.shields.io/badge/C%23-239120?logo=csharp&logoColor=white)
![Avalonia](https://img.shields.io/badge/Avalonia%20UI-8B44AC)
![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![CUDA](https://img.shields.io/badge/CUDA-76B900?logo=nvidia&logoColor=white)

## Özellikler

- **Kategoriye göre üretim:** arka plan, eşya, karakter, parçacık ve obje. Stil serbest, isteğe bağlı 2D çizim ya da pixel art.
- **Otomatik şeffaf PNG:** eşya türü çıktılar kontrollü düz bir zeminde üretilip şeffaf PNG'ye çevrilir, arka planlar tam kare kalır.
- **Üretim sonrası doğrulama:** birden fazla parça, yetersiz kenar payı, karakterin ya da eşyanın kopyalanması ve gerekiyorsa simetri kontrolü. Başarısız sonuç kayıtlı yeni bir seed ile bir kez yeniden denenir.
- **İş kuyruğu:** tek istekte 1–10 sonuç. İşler GPU belleği için yarışmasın diye sırayla işlenir. İlerleme, süre, seed ve dosya adı canlı görünür.
- **Kaldığı yerden devam:** bekleyen ve çalışan işler kaydedilir, uygulama yeniden açılınca geri yüklenir.
- **Seed kütüphanesi:** beğenilen tasarım adıyla kaydedilir, aynı sonuç tekrar üretilebilir.
- **Türkçe istek desteği** ve tam ekran önizleme.

## Mimari

| Katman | Teknoloji | Görevi |
|---|---|---|
| Masaüstü uygulaması | C# · Avalonia UI · .NET | Arayüz, kuyruk, seed kütüphanesi |
| Üretim motoru | Python · SDXL · CUDA | Görsel üretimi, kompozisyon, şeffaflık |
| İşçi süreci | Kalıcı Python worker | Modeli bellekte tutar, işleri sırayla işler |

- Uygulama ve GPU işçisi aynı anda tek örnek çalışacak şekilde korunur, böylece yarım kalan ya da çakışan GPU işi oluşmaz.
- Her istek yapılandırılmış bir `AssetSpec` taşır: tek konu, kategoriye göre şeffaflık, güvenli kenar payı, simetri kuralı.
- Model yüklemeden çalışan birim testleri ve sabit seed'li regresyon tarifleri
- .NET kurulumu gerektirmeyen tek dosyalık EXE olarak paketlenir

## Gereksinim

Windows 10/11 ve CUDA destekli bir NVIDIA ekran kartı.

---

Geliştiren: [Halit Bulut](https://github.com/HalittBulut)
