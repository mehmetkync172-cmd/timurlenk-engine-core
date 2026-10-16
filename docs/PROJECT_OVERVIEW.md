# TİMURLENK Engine Core — Proje Özeti

**Belge durumu:** Kamuya açık proje özeti  
**Son gözden geçirme:** 16 Ekim 2026

## Tek cümlede

TİMURLENK, tarihî Timur Satrancı olarak modellenen geniş tahtalı bir varyantı modern C++ motor mühendisliği, arama/değerlendirme teknikleri ve tekrarlanabilir araştırma araçlarıyla inceleyen bir satranç motoru projesidir.

## Bu depo ne işe yarar?

`timurlenk-engine-core`, projenin dışarıya dönük tanıtım ve dokümantasyon yüzeyidir. Projenin ne olduğunu, mimari sınırlarını, doğrulama yaklaşımını ve gelecekteki araştırma yönünü anlatır. Bu deponun aktif motor kaynak kodu deposu olduğu düşünülmemelidir.

- **Özel motor deposu:** [timurlenk-engine-private](https://github.com/mehmetkync172-cmd/timurlenk-engine-private) — C++ kaynak, testler, modeller, deney araçları ve aktif değişiklikler.
- **Bu vitrin deposu:** proje özeti, kamuya uygun mimari açıklamalar, yol haritası ve kontrollü yayın.
- **Persona araştırması:** ayrı yönetilen Persona depolarında geliştiriliyor. Timurlenk entegrasyonu, Persona çalışmaları yeterli olgunluğa ulaştıktan sonra ele alınacak.
- **Tarih Oyunları:** prototipler/katalog olarak ayrı tutulur; arayüz veya prototip varlığı ortak C++ motorunun bağlandığını kanıtlamaz.

## Teknik kapsam

Motor tarafındaki belgelenmiş kapsam şunları içerir:

- 11 sütun × 10 satırlık tahta ve varyanta özel taş/oyun kuralları;
- C++20 tabanlı çekirdek, yasal hamle üretimi, arama ve zaman yönetimi;
- APEX araması, HCE ve bilişsel NNUE değerlendirmesi;
- UCI çalışma zamanı ve isteğe bağlı JSONL deney kaydı;
- self-play ve karşılaştırma araçları;
- sürümlenmiş veri şemaları, model/konfigürasyon hash'leri ve regresyon testleri.

Bunların varlığı, bütün araştırma sorularının çözüldüğü, tarihsel kural yorumlarının nihai olduğu veya motorun belirli bir ELO düzeyine ulaştığı anlamına gelmez. Kesin durum ve kanıt sınırlamaları [PROJECT_STATUS.md](PROJECT_STATUS.md) içinde tutulur.

## Araştırma ilkeleri

1. Kural doğruluğu, derleme, performans, pozisyon kalitesi ve oyun gücü farklı kanıt sınıflarıdır.
2. Deneyler motor commit'i, model kimliği, yapılandırma, açılış/konum ve sonuç bilgileriyle tekrar üretilebilir olmalıdır.
3. Veri sözleşmesi, çalışan entegrasyon değildir; entegrasyon ancak gerçek veri değişimi ve uçtan uca testten sonra etkin sayılır.
4. Motor, Persona araştırma deposu olmadan da derlenebilir ve oynanabilir kalmalıdır.
5. Tarihsel oyun kuralları kaynaklara, sürümlenmiş spesifikasyona ve regresyon testlerine göre açıkça belgelenmelidir.

## Hedef kitle

Motor geliştiricileri, tarihî oyunlar üzerinde çalışan araştırmacılar, yapay zekâ/arama algoritmalarıyla ilgilenenler ve projenin teknik yönünü hızlıca anlamak isteyen katkı sağlayıcılar.
